---
description: "Base URL, authentication and conventions shared by every endpoint."
---

# API overview

## Base URL

{% code title="Base URL" %}
```
https://maas-llm-aiplatform-hcm.api.vngcloud.vn
```
{% endcode %}

| Endpoint | Format | Streaming |
| --- | --- | --- |
| [`POST /v1/chat/completions`](chat-completions.md) | OpenAI Chat Completions | ✓ |
| [`POST /v1/messages`](messages.md) | Anthropic Messages | ✓ |
| [`POST /v1/responses`](responses.md) | OpenAI Responses | ✓ |
| [`POST /v1/embeddings`](embeddings.md) | OpenAI Embeddings | — |
| [`POST /v1/rerank`](rerank.md) | Rerank (`query` + `documents`) | — |
| [`GET /v1/models`](../models/README.md) | Model catalog | — |

## Authentication

Send your API key in one of these two headers:

| Header | Typical client |
| --- | --- |
| `Authorization: Bearer <key>` | OpenAI SDK, curl |
| `x-api-key: <key>` | Anthropic SDK, Claude Code |

Missing or unknown key → **401** `request_denied`. Model not enabled for the key → **403** `request_denied`.

## Selecting the model

Put the model ID in the `model` field of the request body, in the form `vendor/model`:

{% code title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
{% endcode %}

* The endpoint path is the same for every model (for example `POST /v1/chat/completions`); only the `model` value changes.
* Get model IDs from the [Model list](../models/README.md) or with `GET /v1/models`.
* A request without `model` cannot be routed and returns `502`; an unknown model ID returns `404 model_not_found`. See [Errors](errors.md).

{% hint style="info" %}
**Exception: OCR.** The OCR model (`greennode/idp`) takes a file and returns the result later, so it has its own set of endpoints and does not take `model` in the body. See [OCR API](ocr.md).
{% endhint %}

## Conventions

* Requests are JSON: `Content-Type: application/json`, UTF-8. Maximum request body: **50 MB** (including base64 images).
* Long generations can take minutes. Set your HTTP client timeout to at least **10 minutes**, or use [streaming](streaming.md).
* Every response carries `x-kong-request-id` — log it on your side.
* Errors follow the format of the endpoint you called (OpenAI-style or Anthropic-style). See [Errors](errors.md).
