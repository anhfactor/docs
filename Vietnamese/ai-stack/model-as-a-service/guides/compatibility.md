---
description: "MaaS hỗ trợ ba chuẩn API trên cùng các model. Trang này liệt kê phần nào dùng nguyên được và phần nào khác so với API gốc."
---

# Tương thích OpenAI & Anthropic

## Endpoint

| API gốc | Endpoint MaaS | Base URL cho SDK |
| --- | --- | --- |
| OpenAI Chat Completions | `POST /v1/chat/completions` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| OpenAI Responses | `POST /v1/responses` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| OpenAI Embeddings | `POST /v1/embeddings` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Rerank | `POST /v1/rerank` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| OpenAI Models | `GET /v1/models` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Anthropic Messages | `POST /v1/messages` | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` (không có `/v1` — SDK tự thêm) |

## Mức hỗ trợ tính năng

| Tính năng | Chat | Messages | Responses | Ghi chú |
| --- | --- | --- | --- | --- |
| Sinh văn bản, system prompt | ✓ | ✓ | ✓ |   |
| Streaming (SSE) | ✓ | ✓ | ✓ | Mỗi endpoint stream theo định dạng event gốc. |
| Function tool | ✓ | ✓ | ✓ |   |
| Server tool tìm kiếm web | ✓ | ✓ | ✓ | Chỉ có trên `google/gemma-4-31b-it`. Gửi tool `web_search` cho model khác: Chat trả 400, Responses bỏ qua. |
| Reasoning effort | ✓ | ✓ | ✓ | Một thang chung, được chuyển sang thiết lập gốc của từng model. |
| JSON / output có cấu trúc | ✓ | ✗ | ✓ | JSON Schema chặt chỉ với model có `structured_outputs`. Model chỉ có `response_format` xử lý như `json_object`: prompt phải có chữ "json", nếu không trả 400. Messages: `output_format` bị bỏ qua. |
| Ảnh đầu vào | ✓ | ✓ | ✓ | Model có `image` trong loại đầu vào. |
| PDF / file đầu vào | ✗ | một phần | ✗ | Messages chỉ nhận block `document` với nguồn dạng text; block PDF trả 400. |
| Prompt caching | ✓ | ✓ | ✓ | Tự động; Chat `prompt_tokens_details.cached_tokens`, Messages `cache_read_input_tokens`, Responses `input_tokens_details.cached_tokens`. |
| Lưu hội thoại (`previous_response_id`) | — | — | ✗ | Gateway không lưu trạng thái: gửi `previous_response_id` trả `400 invalid_request`. Gửi toàn bộ hội thoại mỗi lượt. |
| Tool dựng sẵn: `file_search`, `code_interpreter`, `custom` | ✗ | — | ✗ | Không hỗ trợ: trả `400 invalid_request` trên cả Chat và Responses. Dùng tool loại `function`. |
| Server tool `web_fetch` | ✗ | ✗ | ✗ | Chưa có. |

## Điểm khác cần lưu ý

* Model ID có dạng `vendor/model`, ví dụ `z-ai/glm-5.3` — không phải tên model của OpenAI hay Anthropic.
* Trường `model` trong response là tên phía backend (ví dụ `qwen3.6-flash`), có thể khác ID bạn gửi.
* Nhiều model mặc định có reasoning, và token reasoning tính vào `max_tokens`. Hãy đặt effort rõ ràng.
* Lỗi có mã ổn định trong header `x-ai-error-code` ngoài phần body.
* Tham số mà model không liệt kê trong `supported_parameters` bị bỏ qua (không báo lỗi).
