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

Send your API key in one of these headers; use the one your SDK sends by default. If a request carries several, the gateway reads `Authorization` first, then `apikey`, then `x-api-key`.

| Header | Typical client |
| --- | --- |
| `Authorization: Bearer <key>` | OpenAI SDKs, curl, most tools |
| `x-api-key: <key>` | Anthropic SDKs |
| `apikey: <key>` | Legacy integrations |

`GET /v1/models` does not accept the `apikey` header (returns 401); use `Authorization: Bearer` or `x-api-key` for that endpoint.

Missing or unknown key → **401** `request_denied`. Model not enabled for the key → **403** `request_denied`.

## Selecting the model

Put the model ID in the request body (`"model": "z-ai/glm-5.3"`). Alternatively, some tools need a model-specific base URL; every endpoint is also reachable under the model's own path, and the body `model` must then match it:

{% code title="per-model URL" %}
```
https://maas-llm-aiplatform-hcm.api.vngcloud.vn/{vendor}/{model}/v1/chat/completions
# e.g.
https://maas-llm-aiplatform-hcm.api.vngcloud.vn/qwen/qwen3.6-flash/v1/chat/completions
```
{% endcode %}

## Conventions

* Requests are JSON: `Content-Type: application/json`, UTF-8. Maximum request body: **50 MB** (including base64 images).
* Long generations can take minutes. Set your HTTP client timeout to at least **10 minutes**, or use [streaming](streaming.md).
* Every response carries `x-kong-request-id` — log it on your side.
* Errors follow the format of the endpoint you called (OpenAI-style or Anthropic-style). See [Errors](errors.md).
