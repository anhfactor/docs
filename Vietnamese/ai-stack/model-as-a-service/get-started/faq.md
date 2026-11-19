---
description: "Các câu hỏi thường gặp từ lập trình viên và BA."
---

# FAQ

### Response có `content` rỗng và `finish_reason: "length"`. Tại sao?

Model đã dùng hết ngân sách `max_tokens` cho phần suy luận trước khi kịp viết câu trả lời. Giảm effort (`"reasoning_effort": "low"`) và/hoặc tăng `max_tokens`. Kiểm tra `usage.completion_tokens_details.reasoning_tokens` để xác nhận.

### Nên dùng endpoint nào — Chat, Messages hay Responses?

Dùng chuẩn mà SDK/công cụ của bạn hỗ trợ — cả ba đều dùng chung các model. Chat Completions được hỗ trợ rộng rãi nhất. Messages phù hợp Anthropic SDK và Claude Code. Responses phù hợp Codex CLI và code OpenAI SDK mới.

### 429 khác 503 thế nào?

**429**: hoặc bạn vượt rate limit của chính mình (mã `request_denied`; message cho biết giới hạn nào và khi nào reset), hoặc nhà cung cấp model đang giới hạn lưu lượng (mã `rate_limited`). Hãy giảm tốc và retry kèm backoff. **503/529 `pool_exhausted`**: mọi backend của model tạm thời không khả dụng — retry sau thời gian trong header `Retry-After`, hoặc chuyển sang model khác.

### Token được tính thế nào?

Token đầu vào = toàn bộ nội dung bạn gửi (system prompt, lịch sử hội thoại, định nghĩa tool, ảnh). Token đầu ra = toàn bộ nội dung model sinh ra, **bao gồm cả reasoning**. Token đầu vào trúng cache được báo riêng trong `cached_tokens`. Xem [Thống kê usage](../features/usage-accounting.md).

### Nếu client ngắt kết nối giữa chừng khi stream, usage có được ghi nhận không?

Có. Số token đã sinh ra đến lúc ngắt vẫn được ghi nhận; nếu nhà cung cấp không trả usage cuối cùng, gateway sẽ ước lượng.

### Cùng một prompt có cho cùng một câu trả lời không?

Không đảm bảo. Dùng `temperature: 0` và `seed` (nếu model hỗ trợ) để giảm sai khác, và [structured outputs](../features/structured-outputs.md) khi cần định dạng cố định.

### Dữ liệu của tôi có bị dùng để huấn luyện hay ghi log không?

Vui lòng tham khảo hợp đồng dịch vụ GreenNode MaaS về chính sách xử lý và lưu trữ dữ liệu.

### Báo lỗi thế nào?

Gửi cho bộ phận hỗ trợ GreenNode: header `x-kong-request-id` của response, thời điểm gọi (kèm múi giờ), model ID, endpoint, và HTTP status / `x-ai-error-code`. Không bao giờ gửi API key.
