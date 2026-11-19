# Virtual IP

Virtual IP (VIP) giúp người dùng xây dựng các kiến trúc **High Availability (HA)** và **Load Balancing** bằng cách trừu tượng hóa địa chỉ IP khỏi máy chủ vật lý cụ thể. Người dùng có thể lựa chọn cấu hình VIP theo nhu cầu hệ thống.

## **Tổng quát về Virtual IP** <a href="#virtualip-tongquatvevirtualip" id="virtualip-tongquatvevirtualip"></a>

Một Virtual IP được dùng chung bởi nhiều máy chủ ảo. Một máy chủ ảo có thể có cả IP private và Virtual IP, bạn có thể truy cập đến máy chủ ảo bằng cả 2 IP trên. Virtual IP có đầy đủ chức năng tương tự IP private của máy chủ.

Bạn có thể gán Virtual IP cho các máy chủ ảo trong cùng hệ thống của mô hình active/standby. Virtual IP thường được dùng kết hợp với Keepalived để đảm bảo tính sẵn sàng cao. Nếu máy chủ chính gặp lỗi, máy chủ dự phòng sẽ tự động chạy tiếp dịch vụ. Virtual IP thường dùng để cấu hình HA hoặc cân bằng tải cho hệ thống.

## Sử dụng VIP

### Bước 1: Chọn Loại VIP – Private hoặc Public

**✅ Private VIP**

* **Sử dụng trong nội bộ hệ thống**, không truy cập được từ Internet.
* **Yêu cầu**: Người dùng cần chỉ định địa chỉ IP mong muốn thuộc dải **subnet nội bộ (private subnet)**.
* **Ví dụ**: `192.168.10.100`, nếu subnet là `192.168.10.0/24`.

**✅ Public VIP**

* **Cho phép truy cập từ Internet**, thích hợp cho dịch vụ công khai (web, API...).
* **Người dùng chọn:**
  1. **Zone** mà địa chỉ IP sẽ được sử dụng (ví dụ: `HAN-1A`, `HCM-1A`).
  2. **Chế độ IP:**
     * **Auto**: Hệ thống tự động tạo mới một Floating IP trong Zone đã chọn.
     * **Chọn từ Floating IP Available**: Người dùng chọn một địa chỉ Floating IP có sẵn chưa sử dụng.

### Bước 2. Chọn Chế Độ Hoạt Động của VIP

VIP hỗ trợ hai chế độ hoạt động: **Active/Active** và **Active/Passive**. Tham khảo chi tiết các mode [tại đây](vip-mode.md).

**Active/Active Mode**

* **Tất cả các node đều hoạt động đồng thời**, chia sẻ lưu lượng hoặc tác vụ.
* **Tính năng nổi bật:**
  * Load balancing: giảm tải cho từng node.
  * Không có thời gian chết (zero downtime).
  * Tăng hiệu suất và độ tin cậy.
* **Phù hợp với:**
  * Web server phân tải qua Load Balancer (Nginx, HAProxy, ELB).
  * Cơ sở dữ liệu phân tán (Cassandra, MongoDB).
  * Dịch vụ CDN hoặc microservices trong môi trường đa vùng.

**Active/Passive Mode**

* **Chỉ một node chính xử lý tác vụ**, các node còn lại ở chế độ chờ (standby).
* **Tính năng nổi bật:**
  * Khi node chính gặp lỗi, một node phụ sẽ kích hoạt VIP và tiếp quản.
  * Có thể gây ra một khoảng gián đoạn ngắn trong quá trình chuyển đổi.
* **Phù hợp với:**
  * Hệ thống nhỏ, tiết kiệm chi phí.
  * Ứng dụng ERP hoặc hệ thống nội bộ doanh nghiệp.
  * Cụm cơ sở dữ liệu đơn giản cần failover (MySQL, SQL Server).

### Bước 3: Gán/ Xóa Virtual IP cho Instance <a href="#virtualip-gan-xoavirtualipchoinstance" id="virtualip-gan-xoavirtualipchoinstance"></a>

**Gán IP cho Instance**

Sau khi tạo Virtual IP, bạn cần gán nó vào máy chủ ảo để sử dụng:

1. Vào GreenNode portal console, đến trang Virtual IP
2. Xem chi tiết của Virtual IP và chuyển qua mục **Address Pair Interface,** chọn **Add Address Pair Interface/Remove Address Pair Interface** và chọn máy chủ ảo mà bạn muốn gán hay xóa
3. Bạn sẽ cần cấu hình network trong máy chủ ảo để có thể sử dụng đc Virtual IP

**Xóa Virtual IP**

1. Vào GreenNode portal console, đến trang Virtual IP
2. Chọn Virtual IP cần xóa và nhấn **Delete** ở phía bên phải

## Trường hợp sử dụng

**Ví dụ minh họa**

* **Trường Hợp 1 – VIP Private cho Cụm Web Server:**
  * **Mục tiêu**: HA nội bộ không public IP.
  * **VIP Mode**: Active/Active.
  * **Cấu hình**: Chọn **VIP Private**.
    * Nhập IP mong muốn: `192.168.100.200`.
    * Gán VIP cho 2 Web Server trong cùng subnet, kết hợp Load Balancer nội bộ.
* **Trường Hợp 2 – VIP Public với Auto Floating IP:**
  * **Mục tiêu**: Dịch vụ Web công khai có dự phòng.
  * **VIP Mode**: Active/Passive.
  * **Cấu hình**:
    * Chọn **VIP Public**.
      * Zone: `HCM-1A`.
      * Floating IP: **Auto**.
      * Gán VIP cho cặp máy chủ master/standby với giải pháp như Keepalived.

**Tóm tắt**

<table><thead><tr><th width="194">Thành phần</th><th>Mô tả</th></tr></thead><tbody><tr><td><strong>VIP Private</strong></td><td>Dùng trong mạng nội bộ (không public).</td></tr><tr><td><strong>VIP Public</strong></td><td>Truy cập từ Internet thông qua Floating IP.</td></tr><tr><td><strong>Auto Floating IP</strong></td><td>Tạo IP mới tự động trong Zone.</td></tr><tr><td><strong>Active/Active</strong></td><td>Tăng hiệu năng, không downtime, yêu cầu load balancer.</td></tr><tr><td><strong>Active/Passive</strong></td><td>Failover đơn giản, downtime ngắn, phù hợp hệ thống tiết kiệm chi phí.</td></tr></tbody></table>
