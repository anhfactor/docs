# Whitelist

### **Tổng quan**

Tính năng Whitelist IP trên chế độ Private Node Group của VKS cho phép bạn chỉ cho phép các địa chỉ IP cụ thể kết nối đến Cluster của bạn. Điều này giúp tăng cường bảo mật cho các ứng dụng và dữ liệu nhạy cảm bằng cách hạn chế truy cập từ các nguồn không xác định.

**Lợi ích**

* **Tăng cường bảo mật:** Whitelist IP giúp bảo vệ dữ liệu và ứng dụng của bạn khỏi các mối đe dọa tiềm ẩn trên mạng công cộng, chẳng hạn như tấn công mạng và vi phạm dữ liệu.
* **Giảm thiểu rủi ro:** Bằng cách hạn chế truy cập vào các node nhạy cảm, Whitelist IP giúp giảm thiểu rủi ro lây lan vi phạm dữ liệu sang các phần khác của mạng của bạn.
* **Kiểm soát tốt hơn:** Whitelist IP cho phép bạn kiểm soát chặt chẽ quyền truy cập vào các node của mình, đảm bảo chỉ những người dùng và ứng dụng được ủy quyền mới có thể truy cập.

{% hint style="info" %}
**Khuyến nghị về Sử dụng Whitelist trong Các Mô Hình Cluster:**

**1. Public Cluster Chỉ Bao Gồm Public Node Group**

* **Khuyến nghị**: Không khuyến khích sử dụng whitelist.
* Trên **Region HCM:** Nếu bạn có nhu cầu sử dụng Whitelist IP vì security, vui lòng allow danh sách IP Range Public của vServer theo danh sách sau:

```
49.213.64.0/23
49.213.71.0/24
49.213.83.0/24
49.213.86.0/23
49.213.89.0/24
61.28.224.0/20
61.28.250.0/24
103.245.248.0/22
58.84.0.0/22
116.118.88.0/21
180.93.180.0/22
120.138.75.0/24
120.138.79.0/24
122.201.13.0/24
122.201.15.0/24
103.196.238.0/23
103.245.254.0/23
210.245.38.93/32
```

* Trên **Region HAN**: Nếu bạn có nhu cầu sử dụng Whitelist IP vì security, vui lòng allow danh sách IP Range Public của vServer theo danh sách sau:

```
42.1.126.0/23
157.20.201.0/24
157.20.200.96/27
157.20.200.128/25
```

**2. Public Cluster Bao Gồm Private Node Group Đi Qua NAT Gateway (Pfsense, PaloAlto)**

* **Khuyến nghị**: Có thể sử dụng tính năng whitelist.
* Cần thực hiện Whitelist thêm IP của NAT Gateway.

**3. Private Cluster Bao Gồm Public Node Group hoặc Private Node Group**

* **Khuyến nghị:** Có thể sử dụng tính năng whitelist.
{% endhint %}

***

### Chỉnh sửa Whitelist

Để sử dụng tính năng Whitelist IP trên chế độ Private Node Group, bạn cần thực hiện các bước sau:

**Bước 1:** Truy cập vào [https://vks.console.greennode.ai/overview](https://vks.console-dev.vngcloud.tech/overview)

**Bước 2:** Tại màn hình **Overview**, chọn menu **Kubernetes Cluster.**

**Bước 3:** Chọn biểu tượng **Action** và chọn **Edit Whitelist** hoặc chọn biểu tượng **Edit** khi xem chi tiết một Cluster để thực hiện thêm Whitelist cho Cluster của bạn.

**Bước 4:** Lúc này, màn hình **Edit Whitelist** hiển thị, bạn có thể nhập địa chỉ IP mà bạn muốn cho phép truy cập vào Cluster sau đó chọn **Add**.

**Bước 5:** Lặp lại bước 4 nếu bạn muốn thêm nhiều **Whitelist IP** cho Cluster của bạn. Bạn cũng có thể chọn **Delete** để xóa Whitelist IP mà bạn đã thêm trước đó.

**Bước 6:** Chọn **Save** để lưu thông tin hoặc **Cancel** để hủy bỏ việc lưu các thông số này.
