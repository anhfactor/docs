# Các Model được cung cấp

MaaS API cung cấp quyền truy cập vào các họ mô hình như Qwen, DeepSeek, GLM, Kimi, MiniMax, Gemma… Danh sách đầy đủ ở bên dưới.

{% hint style="info" %}
Danh mục model bên dưới gồm model do GreenNode self-host và model third-party đã ký hợp đồng chính thức. Xem các lần thay đổi danh mục tại [Release Notes](../release-notes.md) và nguyên tắc tính phí tại [Cách tính phí](cach-tinh-phi.md).
{% endhint %}

### Rate limit

Mặc định áp dụng cho **mọi tài khoản mới** dùng MaaS API, tính **riêng cho từng model**:

| Giới hạn | Giá trị mặc định (mỗi model) |
| --- | --- |
| Request | **10 RPM** — 10 request/phút |
| Token | **1.000.000 TPM** — 1 triệu token/phút |

Mỗi model có bộ đếm riêng: gọi model A không làm giảm hạn mức của model B. Xem chi tiết tại [Rate limit](portal/rate-limits.md).

{% hint style="info" %}
Cần mức cao hơn? Hãy [liên hệ GreenNode](https://helpdesk.greennode.ai/portal/vi/newticket) để được xem xét đưa vào **whitelist**. Whitelist được xét theo từng trường hợp cụ thể.
{% endhint %}

***

### Danh sách mô hình

Danh sách model đầy đủ (Model ID, độ dài ngữ cảnh, đầu vào, endpoints, reasoning) được cập nhật tự động theo hệ thống tại **[Danh sách model](models/README.md)**.

Model được cung cấp theo một trong hai hình thức:

* **GreenNode self-host** — model chạy trên hạ tầng của GreenNode.
* **Third-party** — request được chuyển tiếp đến nhà cung cấp model theo hợp đồng chính thức.

Theo [Cam kết SLA](cam-ket-sla.md), cam kết về Tỷ Lệ Uptime Hàng Tháng áp dụng đối với tính sẵn sàng của Dịch Vụ đối với các Mô Hình GreenNode; GreenNode không cam kết SLA đối với Mô Hình Bên Thứ Ba. Danh sách các mô hình được cung cấp và phân loại mô hình được GreenNode công bố và cập nhật trên [Console của Dịch Vụ](https://aiplatform.console.greennode.ai/models).

MaaS hỗ trợ các loại model: **Chat**, **Embedding**, **Rerank** và **OCR**.
