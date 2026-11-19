---
description: "Rà danh sách này trước khi chạy lưu lượng thật."
---

# Checklist trước khi lên production

## Key và quyền truy cập

* API key lưu trong secret manager hoặc biến môi trường, không bao giờ đưa xuống trình duyệt hay app mobile.
* Chỉ bật những model bạn dùng.
* Bạn biết cách xoá và thay key khi bị lộ.

## Độ tin cậy

* Response 429 và 5xx được retry với exponential backoff, tuân theo `Retry-After`. Xem [Lỗi](../api-reference/errors.md).
* Response 400, 401, 403 và 404 không được retry.
* Timeout HTTP ít nhất 10 phút, hoặc request dùng streaming.
* Stream bị đứt được retry lại từ đầu.
* Có model dự phòng cho các luồng quan trọng.

## Giới hạn và chi phí

* Lưu lượng cao điểm dự kiến nằm trong rate limit, hoặc đã được cấp mức cao hơn. Xem [Rate limit](../portal/rate-limits.md).
* `reasoning_effort` và `max_tokens` được đặt rõ ràng trong mọi request.
* Tài khoản trả trước có đủ quota và có quy trình nạp thêm; toàn bộ model bị tắt khi quota về 0. Xem [Billing & giá](../cach-tinh-phi.md).
* `usage` của mỗi response được ghi lại.

## Giám sát và hỗ trợ

* `x-kong-request-id` được ghi log cho mọi request.
* Tỉ lệ lỗi, tỉ lệ 429 và độ trễ có trên dashboard kèm cảnh báo.
* Team biết cách liên hệ [Hỗ trợ](../help/support.md).
