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

Gửi API key qua một trong hai header sau:

| Header | Client thường dùng |
| --- | --- |
| `Authorization: Bearer <key>` | OpenAI SDK, curl |
| `x-api-key: <key>` | Anthropic SDK, Claude Code |

Thiếu key hoặc key không hợp lệ → **401** `request_denied`. Model chưa được bật cho key → **403** `request_denied`.

## Chọn model

Đặt model ID trong trường `model` của body, theo dạng `vendor/model`:

{% code title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3",
    "messages": [{"role": "user", "content": "Xin chào"}]
  }'
```
{% endcode %}

* Đường dẫn endpoint giống nhau cho mọi model (ví dụ `POST /v1/chat/completions`); chỉ giá trị `model` thay đổi.
* Lấy model ID tại [Danh sách model](../models/README.md) hoặc bằng `GET /v1/models`.
* Request thiếu `model` không định tuyến được và trả `502`; model ID không tồn tại trả `404 model_not_found`. Xem [Lỗi](errors.md).

{% hint style="info" %}
**Ngoại lệ: OCR.** Model OCR (`greennode/idp`) nhận file và trả kết quả sau, nên dùng bộ endpoint riêng và không nhận `model` trong body. Xem [OCR API](ocr.md).
{% endhint %}

## Quy ước

* Request dạng JSON: `Content-Type: application/json`, UTF-8. Kích thước body tối đa: **50 MB** (gồm cả ảnh base64).
* Các yêu cầu sinh dài có thể mất vài phút. Đặt timeout HTTP client tối thiểu **10 phút**, hoặc dùng [streaming](streaming.md).
* Mọi response đều có `x-kong-request-id` — hãy ghi log phía bạn.
* Lỗi trả về theo định dạng của endpoint bạn gọi (kiểu OpenAI hoặc Anthropic). Xem [Lỗi](errors.md).
