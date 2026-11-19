---
description: "Cách liên hệ GreenNode, cần gửi gì khi báo lỗi, và các thuật ngữ dùng trong tài liệu."
---

# Hỗ trợ & thuật ngữ

## Liên hệ

| Kênh | Chi tiết |
| --- | --- |
| Help Center | [helpdesk.greennode.ai](https://helpdesk.greennode.ai/portal/vi/home) |
| Email | [support@greennode.ai](mailto:support@greennode.ai) |
| Hotline | 19001549 |

## Cần gửi gì

* Header `x-kong-request-id` trong response.
* Thời điểm gọi, kèm múi giờ.
* Model ID và endpoint.
* HTTP status và `x-ai-error-code`.
* **Không bao giờ** gửi API key.

## Thuật ngữ

| Thuật ngữ | Ý nghĩa |
| --- | --- |
| MaaS | Model as a Service: model được cung cấp qua API, không cần vận hành hạ tầng. |
| Token | Đơn vị model đọc và viết, cũng là đơn vị tính phí. Xấp xỉ một mảnh từ. |
| Context length | Số token input cộng output tối đa trong một request. |
| Token reasoning | Token model dùng để suy luận trước khi trả lời. Tính phí như output. |
| Cached token | Token input lấy từ prompt cache, tính theo giá cache. |
| RPM / TPM | Số request mỗi phút / số token mỗi phút. |
| Self-host / Third-party | Mô Hình GreenNode (GreenNode trực tiếp vận hành trên hạ tầng GreenNode) hoặc Mô Hình Bên Thứ Ba (nhà cung cấp bên thứ ba vận hành). Cam kết SLA chỉ áp dụng cho Mô Hình GreenNode, xem [Cam kết SLA](../cam-ket-sla.md). |
| SSE | Server-sent events, định dạng dùng cho streaming. |
| RAG | Retrieval-augmented generation: trả lời dựa trên tài liệu truy xuất được. |
| Trả trước / Trả sau | Trả từ credit mua trước, hoặc nhận hoá đơn hằng tháng. |
