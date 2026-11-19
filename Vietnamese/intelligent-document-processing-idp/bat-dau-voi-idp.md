# Bắt đầu với IDP



### Đăng nhập

GreenNode IDP dùng tài khoản GreenNode không cần tạo tài khoản riêng.

1\.   Truy cập: [https://idp.console.greennode.ai/](https://idp.console.greennode.ai/)

2\.   Hệ thống chuyển sang trang đăng nhập GreenNode.

3\.   Chọn Sign in with Root User Account (chủ tài khoản) hoặc Sign in with IAM User Account (tài khoản con), nhập thông tin và hoàn tất xác thực.

4\.   Đăng nhập thành công, bạn được đưa về Bảng điều khiển.

***

### Các bước để xử lý tài liệu đầu tiên



**Bước 1 — Bật mô hình AI**

1\.   Đầu trang hiển thị Gói hiện tại, Mô hình đã kích hoạt (đã dùng / giới hạn) và Trạng thái.

2\.   Tìm mô hình theo tên/mã, hoặc lọc theo nhóm, category (Có cấu trúc, Bán cấu trúc, Phức tạp), trạng thái.

3\.   Gạt công tắc ở cột Kích hoạt để bật mô hình.

**Bước 2 — Tạo Loại tài liệu**

Trong Tài liệu & Mô hình → Loại tài liệu → tab Đang sử dụng. Trong Tab Đang sử dụng liệt kê các loại tài liệu tenant đang dùng (Tên, Mã, Trạng thái, Thời gian tạo).

<figure><img src="../.gitbook/assets/greennode-idp.png (1).jpg" alt=""><figcaption><p align="center"><em>Loại tài liệu — Đang sử dụng</em></p></figcaption></figure>

1\.   Bấm Tạo mới. Cửa sổ Chọn từ danh sách các mô hình đã được hỗ trợ sẵn mở ra.

2\.   Lọc theo Tags (Banking, Business, ID, Insurance, Popular) hoặc tìm theo từ khoá.

3\.   Bấm vào thẻ mô hình phù hợp → điền Tên và Mã cho loại tài liệu → Gửi.

<figure><img src="../.gitbook/assets/greennode-idp.png (2).jpg" alt=""><figcaption><p align="center"><em>Chọn mô hình để tạo loại tài liệu</em></p></figcaption></figure>

{% hint style="info" %}
Mẹo: Nút + Mẫu tài liệu mới ở góc phải cửa sổ dùng để tạo [Mẫu tự định nghĩa](huong-dan-su-dung-trich-xuat-thong-tin/tu-dinh-nghia-bieu-mau-moi.md)
{% endhint %}

**Bước 3 — Tạo API Key**

Chọn tab Quản lý → tab API Keys

API Key là bắt buộc: mọi chức năng trong Bộ trích xuất và mọi lời gọi API từ hệ thống của bạn đều yêu cầu chọn/gửi API Key.

1\.   Bấm Tạo mới.

2\.   Điền:

◦     Tên và Mô tả (bắt buộc).

◦     Webhook (tuỳ chọn): địa chỉ nhận kết quả, chọn từ danh sách webhook đã khai báo.

◦     Trạng thái: CÓ HIỆU LỰC / KHÔNG CÓ HIỆU LỰC.

◦     Hết hạn lúc (tuỳ chọn): phải là thời điểm trong tương lai. Để trống nếu không muốn hết hạn.

◦     Phạm vi quyền (tuỳ chọn).

3\.   Bấm Gửi.

<figure><img src="../.gitbook/assets/greennode-idp.png (3).jpg" alt=""><figcaption><p align="center"><em>Tạo API Key</em></p></figcaption></figure>

Danh sách API Key hiển thị khoá ở dạng che một phần, có nút sao chép, và công tắc bật/tắt nhanh.

<figure><img src="../.gitbook/assets/greennode-idp.png (4).jpg" alt=""><figcaption><p align="center"><em>Danh sách API Keys</em></p></figcaption></figure>

{% hint style="info" %}
Bảo mật API Key: không gửi khoá qua email/chat, không đưa vào mã nguồn công khai. Nếu nghi lộ khoá: tắt khoá cũ và tạo khoá mới. Khi gọi API, gửi khoá qua header API-KEY.
{% endhint %}

**Bước 5 — Xử lý tài liệu đầu tiên**

Trong tab Xử lý tài liệu → Bộ trích xuất → Tài liệu đơn

1\.   Chọn API KEY vừa tạo.

2\.   Chọn Loại tài liệu đơn vừa tạo ở Bước 3/4.

3\.   Chọn Image hoặc PDF, rồi kéo thả tệp vào ô tải lên (hoặc bấm Chọn tập tin).

4\.   Bấm Gửi. Hệ thống mở trang kết quả của hồ sơ.

{% hint style="info" %}
Chi tiết tại [trich-xuat-tai-lieu-don.md](huong-dan-su-dung-trich-xuat-thong-tin/trich-xuat-tai-lieu-don.md "mention") hoặc [trich-xuat-bo-tai-lieu.md](huong-dan-su-dung-trich-xuat-thong-tin/trich-xuat-bo-tai-lieu.md "mention")
{% endhint %}

