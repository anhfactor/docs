---
description: "Mọi response thành công đều báo lượng token đã dùng. Hãy lưu lại để theo dõi chi phí và phát hiện reasoning vượt kiểm soát."
---

# Thống kê usage

|   | Chat | Messages | Responses |
| --- | --- | --- | --- |
| Đầu vào | `prompt_tokens` | `input_tokens` | `input_tokens` |
| Đầu ra (gồm reasoning) | `completion_tokens` | `output_tokens` | `output_tokens` |
| trong đó reasoning | `completion_tokens_details.reasoning_tokens` (một số model, ví dụ GLM: `reasoning_tokens` ở cấp `usage`) | `output_tokens_details.reasoning_tokens` | `output_tokens_details.reasoning_tokens` |
| Đầu vào trúng cache | `prompt_tokens_details.cached_tokens` | `cache_read_input_tokens` | `input_tokens_details.cached_tokens` |
| Web search | — | `server_tool_use.web_search_requests` | `server_tool_use.web_search_requests` |

* **Streaming:** trên Chat, chunk cuối trước `[DONE]` mang `usage`; bạn cũng có thể đặt `stream_options.include_usage: true` tường minh. Messages báo trong `message_delta`; Responses trong `response.completed`.
* **Stream bị ngắt:** nếu kết nối bị ngắt, usage cho phần token đã sinh vẫn được ghi nhận (ước lượng nếu nhà cung cấp không báo).
* **Request lỗi** (4xx/5xx trước khi sinh nội dung) không tiêu tốn token.
