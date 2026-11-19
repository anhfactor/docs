---
description: "Gateway làm gì khi backend của model lỗi, và phần nào thuộc về client của bạn."
---

# Độ tin cậy

## Gateway xử lý

* **Chuyển sang nhà cung cấp dự phòng.** Model có nhà cung cấp dự phòng sẽ chuyển sang đó khi nhà cung cấp chính trả 429, 502, 503 hoặc 504. Với request không streaming, việc này diễn ra ngay trong request nên bạn chỉ thấy câu trả lời thành công.
* **Thời gian nghỉ.** Backend lỗi bị bỏ qua khoảng 60 giây rồi được thử lại.
* **Không phải model nào cũng có dự phòng.** Model chỉ có một backend sẽ trả lỗi của backend (`upstream_error`) về cho bạn.
* **Bảo vệ công suất.** Khi mọi backend của model không khả dụng hoặc đã đầy, gateway trả `pool_exhausted` (503 hoặc 529) thay vì xếp hàng vô hạn.

## Phần của client

* Retry 429 và 5xx với exponential backoff kèm jitter, tuân theo `Retry-After`. Xem [Lỗi](../api-reference/errors.md).
* Request streaming bị lỗi không được gateway retry, và stream đã bắt đầu rồi đứt thì không nối lại được. Hãy retry toàn bộ request.
* Với luồng quan trọng, chuẩn bị model thứ hai (ví dụ biến thể `-thirdparty`, hoặc dòng model khác) và chuyển sang khi gặp `pool_exhausted` hoặc `upstream_error` lặp lại.
* Tự bảo đảm tính idempotent phía bạn: request retry là một lần sinh mới và bị tính phí lần nữa nếu lần đầu đã sinh nội dung.

## Timeout

| Thiết lập | Khuyến nghị | Lý do |
| --- | --- | --- |
| Connect timeout | 10 giây | Kết nối không mở nhanh thì sẽ không tự hồi phục; nên lỗi sớm rồi retry. |
| Read timeout, không streaming | 10 phút | Gateway chờ model tối đa 10 phút trên `/v1/…`. Timeout phía client ngắn hơn sẽ bỏ dở câu trả lời đang được sinh. |
| Read timeout, streaming | vài phút giữa các chunk | Model reasoning có thể im lặng trong lúc suy luận trước token đầu tiên. |
| Số lần retry | 3–5, kèm backoff | Đủ để vượt qua một đợt nghỉ mà không làm sự cố nặng thêm. |
