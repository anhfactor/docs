---
description: "Base URL, xác thực và các quy ước chung cho mọi endpoint."
---

# Tổng quan API

## Base URL

{% code title="Base URL" %}
```
https://maas-llm-aiplatform-hcm.api.vngcloud.vn
```
{% endcode %}

| Endpoint | Định dạng | Streaming |
| --- | --- | --- |
| [`POST /v1/chat/completions`](chat-completions.md) | OpenAI Chat Completions | ✓ |
| [`POST /v1/messages`](messages.md) | Anthropic Messages | ✓ |
| [`POST /v1/responses`](responses.md) | OpenAI Responses | ✓ |
| [`POST /v1/embeddings`](embeddings.md) | OpenAI Embeddings | — |
| [`POST /v1/rerank`](rerank.md) | Rerank (`query` + `documents`) | — |
| [`GET /v1/models`](../models/README.md) | Danh mục model | — |

## Xác thực

Gửi API key qua một trong các header sau; dùng header mà SDK của bạn gửi mặc định. Nếu request có nhiều header, gateway đọc `Authorization` trước, rồi `apikey`, rồi `x-api-key`.

| Header | Client thường dùng |
| --- | --- |
| `Authorization: Bearer <key>` | OpenAI SDKs, curl, most tools |
| `x-api-key: <key>` | Anthropic SDKs |
| `apikey: <key>` | Tích hợp cũ |

`GET /v1/models` không nhận header `apikey` (trả 401); với endpoint này hãy dùng `Authorization: Bearer` hoặc `x-api-key`.

Thiếu key hoặc key không hợp lệ → **401** `request_denied`. Model chưa được bật cho key → **403** `request_denied`.

## Chọn model

Đặt model ID trong body (`"model": "z-ai/glm-5.3"`). Ngoài ra, một số công cụ cần base URL riêng cho từng model; mọi endpoint cũng truy cập được qua đường dẫn riêng của model, khi đó `model` trong body phải trùng khớp:

{% code title="per-model URL" %}
```
https://maas-llm-aiplatform-hcm.api.vngcloud.vn/{vendor}/{model}/v1/chat/completions
# e.g.
https://maas-llm-aiplatform-hcm.api.vngcloud.vn/qwen/qwen3.6-flash/v1/chat/completions
```
{% endcode %}

## Quy ước

* Request dạng JSON: `Content-Type: application/json`, UTF-8. Kích thước body tối đa: **50 MB** (gồm cả ảnh base64).
* Các yêu cầu sinh dài có thể mất vài phút. Đặt timeout HTTP client tối thiểu **10 phút**, hoặc dùng [streaming](streaming.md).
* Mọi response đều có `x-kong-request-id` — hãy ghi log phía bạn.
* Lỗi trả về theo định dạng của endpoint bạn gọi (kiểu OpenAI hoặc Anthropic). Xem [Lỗi](errors.md).
