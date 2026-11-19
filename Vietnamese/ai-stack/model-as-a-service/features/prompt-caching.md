---
description: "Phần đầu prompt lặp lại được cache tự động. Trúng cache giúp phản hồi nhanh hơn và được báo trong cached_tokens. Không cần sửa code — nhưng cách bạn xây dựng prompt quyết định tỉ lệ trúng cache."
---

# Prompt caching

## Xem tỉ lệ trúng cache

| Endpoint | Trường |
| --- | --- |
| Chat | `usage.prompt_tokens_details.cached_tokens` |
| Responses | `usage.input_tokens_details.cached_tokens` |
| Messages | `usage.cache_read_input_tokens` (khi có) |

## Tăng tỉ lệ trúng cache

* **Phần đầu ổn định:** đặt system prompt và định nghĩa tool lên đầu, giữ nguyên từng byte giữa các lần gọi (cùng nội dung, cùng thứ tự tool).
* **Lịch sử chỉ nối thêm:** thêm lượt mới ở cuối; không sửa, đảo thứ tự hay tóm tắt các lượt trước giữa chừng. Mọi thay đổi ở lượt _n_ làm mất cache từ lượt _n_ trở đi.
* **Nội dung thay đổi để cuối:** thời gian, user ID, tài liệu truy xuất đặt sau phần ổn định.
