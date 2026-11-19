---
description: "Errors produced by the gateway carry a machine-readable code in the x-ai-error-code header and in error.code. Decide what to do from the HTTP status and the code, not from the message text."
---

# Errors

## Error codes

| Code | HTTP | Meaning | Retry? |
| --- | --- | --- | --- |
| `invalid_request` | 400 | No prompt (`messages` missing or empty — message "request body doesn't contain valid prompts"), unsupported parameter or value, `max_tokens` too large, unsupported content type, or the `model` in the body differs from the model in a per-model URL. | No — fix the request |
| `request_denied` | 401 | API key missing, unknown, inactive or expired. | No |
| `request_denied` | 403 | The model is not enabled for the account (“model not allowed for this key”). | No — enable the model |
| `request_denied` | 400 | A content-safety guardrail blocked the request. See [Content safety](../features/content-safety.md). | No |
| `request_denied` | 429 | Your rate limit is exceeded. The message names the limit and the seconds until it resets. See [Rate limits & limits](limits.md). | Yes, after the reset |
| `model_not_found` | 404 | The model ID does not exist. IDs have the form `vendor/model`. | No |
| `rate_limited` | 429 | The provider behind the model is throttling. | Yes, with backoff |
| `upstream_error` | 500–504 | The model backend failed. The status is the one the backend returned. | Yes, with backoff |
| `pool_exhausted` | 503 or 529 | Every backend of the model is temporarily unavailable or at capacity. | Yes, after `Retry-After` |
| `guard_unavailable` | 503 | The key-verification service could not be reached. | Yes, with backoff |
| `internal_error` | 500 or 503 | Unexpected gateway error, or a content-safety service is unavailable. | Yes, a few times |

{% hint style="warning" %}
**429 has two codes**

When **your** limit is exceeded the code is `request_denied`; `rate_limited` means the model provider is throttling. Retry on the 429 status, not on the code.
{% endhint %}

## Error shape

Authentication, model-access and rate-limit errors use this shape on every endpoint, including `/v1/messages`:

{% code title="401 / 403 · x-ai-error-code: request_denied" %}
```json
{"error": {"message": "missing api key", "code": "request_denied", "type": "request_denied"}}
{"error": {"message": "unknown api key", "code": "request_denied", "type": "request_denied"}}
{"error": {"message": "model not allowed for this key", "code": "request_denied", "type": "request_denied"}}
```
{% endcode %}

{% code title="404 · x-ai-error-code: model_not_found" %}
```json
{"error": {"message": "The requested model is not found", "type": "not_found_error", "code": "model_not_found"}}
```
{% endcode %}

Errors about the request itself or from the model follow the format of the endpoint. `/v1/chat/completions`, `/v1/responses`, `/v1/embeddings`, `/v1/rerank` — OpenAI format:

{% code title="400 · x-ai-error-code: invalid_request" %}
```json
{
  "error": {
    "message": "invalid reasoning_effort value 'banana'; must be one of: minimal, low, medium, high, xhigh, max, none",
    "type": "invalid_request_error",
    "code": "invalid_request"
  }
}
```
{% endcode %}

`/v1/messages` — Anthropic format:

{% code title="400 · x-ai-error-code: invalid_request" %}
```json
{
  "type": "error",
  "error": {
    "type": "invalid_request_error",
    "message": "max_completion_tokens is too large: 10000000.This model supports at most 1048576 completion tokens.",
    "code": "invalid_request"
  }
}
```
{% endcode %}

## Errors without a code

A few responses come from the proxy layer before the request reaches a model. They have no `x-ai-error-code` header and a different body, so also handle errors by HTTP status.

| HTTP | Body | Cause and fix |
| --- | --- | --- |
| 404 | `{"message":"no Route matched with those values", …}` | Wrong path or HTTP method, or an unknown model in a per-model URL. Check the URL. |
| 405 | `{"error":{"code":"method_not_allowed", …}}` | `/v1/models` only accepts `GET`. |
| 502 | `{"message":"An invalid response was received from the upstream server", …}` | On `/v1/…` endpoints: the gateway cannot read `model` from the body (the body is not valid JSON, is empty, or has no `model`), so the request cannot be routed. Send a valid JSON body with `model`. This is not retryable. |
| 504 | `{"message":"The upstream server is timing out", …}` | The model did not answer within the request time limit. Use streaming or lower `max_tokens`. See [limits](limits.md). |

{% hint style="info" %}
**Checked on production**

The 401, 404 `model_not_found`, 404 no-route, 405 and 502 responses above were observed on the production gateway on 2026-11-14 and re-checked on 2026-11-18.
{% endhint %}

## Recommended retry policy

Retry 429 and 5xx with exponential backoff and jitter, and wait for `Retry-After` when it is present. Do not retry 400, 401, 403, 404 or a 502 caused by a missing `model`.

{% tabs %}
{% tab title="Python" %}
```python
import random, time
from openai import OpenAI, APIStatusError

RETRYABLE_STATUS = {429, 500, 502, 503, 504, 529}

def call_with_retry(fn, attempts=4):
    for i in range(attempts):
        try:
            return fn()
        except APIStatusError as e:
            if e.status_code not in RETRYABLE_STATUS or i == attempts - 1:
                raise
            wait = e.response.headers.get("retry-after")
            time.sleep(float(wait) if wait else (2 ** i) + random.random())

# The OpenAI/Anthropic SDKs also retry 429/5xx automatically (max_retries=2 by default).
client = OpenAI(base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1", api_key="...")
completion = call_with_retry(lambda: client.chat.completions.create(
    model="qwen/qwen3.8-flash",
    messages=[{"role": "user", "content": "hi"}],
))
```
{% endtab %}
{% tab title="JavaScript" %}
```typescript
const RETRYABLE_STATUS = new Set([429, 500, 502, 503, 504, 529]);

async function callWithRetry(fn, attempts = 4) {
  for (let i = 0; ; i++) {
    try {
      return await fn();
    } catch (e) {
      if (!RETRYABLE_STATUS.has(e?.status) || i === attempts - 1) throw e;
      const ra = Number(e?.headers?.get?.("retry-after"));
      await new Promise((r) => setTimeout(r, (ra || 2 ** i + Math.random()) * 1000));
    }
  }
}
```
{% endtab %}
{% endtabs %}
