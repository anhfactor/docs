# Auto associate floating IP

Trước đây, khi tạo **External Interface** hoặc **Public VIP**, người dùng **bắt buộc phải chọn một Floating IP có sẵn** từ danh sách "Available Floating IPs". Điều này yêu cầu người dùng phải quản lý, theo dõi và cấp phát Floating IP một cách thủ công trước khi cấu hình dịch vụ.

Để đơn giản hoá quy trình và nâng cao trải nghiệm người dùng, hệ thống đã bổ sung tính năng **Auto Associate Floating IP**.

## Tính năng Auto Associate Floating IP là gì?

**Auto Associate Floating IP** là tuỳ chọn cho phép người dùng:

* **Tự động khởi tạo một Floating IP mới** từ Zone đã chọn.
* **Gắn trực tiếp IP đó** vào **External Interface** hoặc **Public VIP**.

Tính năng này **giảm thiểu các bước cấu hình**, **tối ưu hóa luồng triển khai**, và giúp người dùng **tránh sai sót** khi chọn nhầm Floating IP đang được sử dụng.

## Hướng dẫn sử dụng

**Khi tạo External Interface:**&#x20;

* Chọn Zone cần sử dụng Floating IP và chọn option "Auto" tại phần Available Floating IPs để tạo mới

<figure><img src="../../../../.gitbook/assets/image (1081).png" alt=""><figcaption></figcaption></figure>

**Khi tạo Public VIP:**&#x20;

* Chọn mode Public VIP, tại phần Network Setting chọn Zone cần sử dụng Floating IP và chọn option "Auto" tại phần Available Floating IPs để tạo mới

<figure><img src="../../../../.gitbook/assets/image (1082).png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
**Ghi chú quan trọng**

* Floating IP được tạo thông qua **Auto Associate** sẽ thuộc vùng (Zone) đã chọn.
* IP này **được ghi nhận và hiển thị trong danh sách Floating IP như bình thường** sau khi tạo.
* Bạn có thể **giải phóng hoặc tái sử dụng** Floating IP này trong tương lai như các IP thông thường.
{% endhint %}
