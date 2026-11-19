---
description: "MaaS speaks three API dialects on the same models. This page lists what works unchanged and what differs from the original APIs."
---

# OpenAI & Anthropic compatibility

## Endpoints

| Original API | MaaS endpoint | SDK base URL |
| --- | --- | --- |
| OpenAI Chat Completions | `POST /v1/chat/completions` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| OpenAI Responses | `POST /v1/responses` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| OpenAI Embeddings | `POST /v1/embeddings` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Rerank | `POST /v1/rerank` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| OpenAI Models | `GET /v1/models` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Anthropic Messages | `POST /v1/messages` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` (no `/v1` — the SDK adds it) |

## Feature support

| Feature | Chat | Messages | Responses | Notes |
| --- | --- | --- | --- | --- |
| Text generation, system prompt | ✓ | ✓ | ✓ |   |
| Streaming (SSE) | ✓ | ✓ | ✓ | Each endpoint streams in its native event format. |
| Function tools | ✓ | ✓ | ✓ |   |
| Web search server tool | ✓ | ✓ | ✓ | Only on `google/gemma-4-31b-it`. Sending a `web_search` tool to other models: 400 on Chat, ignored on Responses. |
| Reasoning effort | ✓ | ✓ | ✓ | One scale, mapped to each model's native setting. |
| JSON / structured output | ✓ | ✗ | ✓ | Strict JSON Schema only on models listing `structured_outputs`. Models with only `response_format` treat it as `json_object`: the prompt must contain the word "json" or the request returns 400. Messages: `output_format` is ignored. |
| Image input | ✓ | ✓ | ✓ | Models whose input modalities include `image`. |
| PDF / file input | ✗ | partial | ✗ | Messages accepts `document` blocks with a text source only; PDF blocks return 400. |
| Prompt caching | ✓ | ✓ | ✓ | Automatic; Chat `prompt_tokens_details.cached_tokens`, Messages `cache_read_input_tokens`, Responses `input_tokens_details.cached_tokens`. |
| Stored conversations (`previous_response_id`) | — | — | ✗ | The gateway is stateless: sending `previous_response_id` returns `400 invalid_request`. Send the full conversation each turn. |
| Built-in tools: `file_search`, `code_interpreter`, `custom` | ✗ | — | ✗ | Not supported: returns `400 invalid_request` on both Chat and Responses. Use `function` tools. |
| `web_fetch` server tool | ✗ | ✗ | ✗ | Not available yet. |

## Differences to keep in mind

* Model IDs are `vendor/model`, for example `z-ai/glm-5.3` — not OpenAI or Anthropic model names.
* The `model` field in a response is the backend's own name (for example `qwen3.6-flash`), which can differ from the ID you sent.
* Many models reason by default, and reasoning tokens count toward `max_tokens`. Set the effort explicitly.
* Errors carry a stable code in the `x-ai-error-code` header in addition to the body.
* A parameter the model does not list in `supported_parameters` is ignored (no error).
