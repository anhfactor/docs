---
description: "Tài khoản có thể được cấu hình guardrail an toàn nội dung: phát hiện nội dung độc hại, bảo vệ PII và chính sách từ khoá. Request được kiểm tra trước khi tới model."
---

# An toàn nội dung

## Khi request bị chặn

Request được trả **400** kèm `x-ai-error-code: request_denied`. Body không phải object `error` thông thường mà nêu nội dung bị phát hiện:

{% code title="400 · x-ai-error-code: request_denied" %}
```json
{
  "status": "Prompt has been rejected by AI Guard",
  "reason": "Content violates the following categories: ...",
  "violations": [ ... ]
}
```
{% endcode %}

{% code title="400 · keyword policy" %}
```json
{
  "status": "Request blocked due to detected keyword",
  "reason": "..."
}
```
{% endcode %}

* Nhận biết bị chặn qua status 400 cùng trường `status` trong body. Không retry cùng nội dung; hãy diễn đạt lại hoặc bỏ phần bị gắn cờ.
* Request bị chặn không tới model và không sinh token.
* Nếu dịch vụ an toàn tạm thời không khả dụng, bạn nhận 503. Lỗi này retry được.

## Thay đổi thiết lập guardrail

Guardrail tắt trừ khi đã được cấu hình cho tài khoản của bạn. Thiết lập do GreenNode quản lý; [liên hệ hỗ trợ](../help/support.md) để bật hoặc điều chỉnh guardrail.

{% hint style="info" %}
**Nguồn**

Cấu trúc response lấy từ mã nguồn gateway; chưa được kích hoạt trên production trong đợt kiểm tra ngày 2026-11-14.
{% endhint %}
