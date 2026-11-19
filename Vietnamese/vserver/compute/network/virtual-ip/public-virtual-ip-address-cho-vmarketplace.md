# Public Virtual IP Address cho vMarketplace

## I. Mục đích

Virtual IP được sử dụng chủ yếu để:

**1. Đảm bảo High Availability (HA)**

* Khi server chính gặp sự cố, VIP tự động chuyển sang server dự phòng
* Dịch vụ vẫn hoạt động liên tục, người dùng không bị gián đoạn

**2. Load Balancing**

* Phân phối traffic đến nhiều server backend
* Tối ưu hiệu suất và tránh quá tải

**3. Đơn giản hóa quản lý**

* Người dùng chỉ cần truy cập một IP duy nhất
* Admin có thể thay đổi server backend mà không ảnh hưởng đến client

## II. Mục tiêu tài liệu

Tài liệu này nhằm hướng dẫn khách hàng:

· Hiểu và sử dụng tính năng Virtual IP Address(es) trên vMarketplace.

· Sử dụng pfSense như một Internet Gateway.

## III. Các bước thực hiện:

**1.Standalone Mode (Single Firewall)**

Đặc điểm Standalone Mode:

**Ưu điểm:**

* Cấu hình đơn giản, dễ triển khai
* Chi phí thấp (chỉ cần 1 firewall VM)
* Phù hợp cho môi trường dev/test hoặc ứng dụng nhỏ

**Nhược điểm:**

* Không có failover - nếu firewall VM die thì mất kết nối
* Single Point of Failure (SPOF)
* Downtime khi bảo trì hoặc restart firewall

**Luồng traffic:** Internet → VIP (157.20.200.185) → Firewall VM (NAT + Filter) → Server 1 (192.168.2.7), Server 2 (192.168.2.5)

**Bước 1: Tiến hành khởi tạo Virtual IP Address trên portal GreenNode**

Truy cập vào [vServer Portal - Create-virtual-ip-address](https://hcm-3.console.greennode.ai/vserver/network/virtual-ip-address), chọn Virtual IP Address type là Public Market Place sau đó điền các thông tin theo yêu cầu

<figure><img src="../../../../.gitbook/assets/image (466).png" alt=""><figcaption></figcaption></figure>

**Bước 2: Tiến hành allow address pair cho VIP với External IP Marketplace**

Sau khi tạo xong VIP dạng public marketplace khách hàng tiến hành thực hiện allow address pair bằng cách chọn Add Address Pair Interface để hiển thị pop-up và chọn External IP Marketplace của pfSense

<figure><img src="../../../../.gitbook/assets/image (1) (6).png" alt=""><figcaption></figcaption></figure>

Kiểm tra đã allow address thành công hay chưa

\*Lưu ý: Lưu VIP lại để cấu hình VIP bên trong pfSense ở các bước sau

<figure><img src="../../../../.gitbook/assets/image (476).png" alt=""><figcaption></figcaption></figure>

**Bước 3: Tiến hành khởi tạo VIP trong pfsense**

Truy cập vào pfSense vào Firewall -> Virtual IPs sau đó nhấn vào nút Add

Tại giao diện cấu hình Virtual IP tiến hành điền các thông tin theo yêu cầu

\*Tại mục Address(es) khách hàng cần điền địa chỉ của VIP đã khởi tạo trên portal GreenNode tại Bước 2

<figure><img src="../../../../.gitbook/assets/image (480).png" alt=""><figcaption></figcaption></figure>

Kiểm tra VIP trong pfSense

<figure><img src="../../../../.gitbook/assets/image (483).png" alt=""><figcaption></figcaption></figure>

**Bước 4: Tạo rule NAT cho IP/Subnet ra internet theo IP chỉ định**

1. Chuyển Mode Manual Outbound NAT

<figure><img src="../../../../.gitbook/assets/image (485).png" alt=""><figcaption></figcaption></figure>

2. Tạo rule NAT

<figure><img src="../../../../.gitbook/assets/image (491).png" alt=""><figcaption></figcaption></figure>

3. Cấu hình rule NAT

Tạo rule theo yêu cầu:

Server 1 (192.168.2.7), Server 2 (192.168.2.5) đứng sau pfSense: Rule đi internet với Virtual IP Address 157.20.200.185

<figure><img src="../../../../.gitbook/assets/image (494).png" alt=""><figcaption></figcaption></figure>

4. **Tạo Route table**

Chọn VPC ID là VPC đang chứa firewall pfSense và servers nội bộ

Thêm route rule với Destination: 0.0.0.0/0 (internet), Targer: 192.168.2.4 (IP internal interface của pfSense)

<figure><img src="../../../../.gitbook/assets/image (711).png" alt=""><figcaption></figcaption></figure>

**Bước 5: Kiểm tra**

Truy cập vào 2 server (192.168.2.7, 192.168.2.5) và sử dụng curl ifconfig.me để kiểm tra kết quả

<figure><img src="../../../../.gitbook/assets/image (543).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (544).png" alt=""><figcaption></figcaption></figure>

Lúc này server (192.168.2.7, 192.168.2.5) đã ra được internet với Virtual IP Address, traffic cũng đi qua pfSense, ngoài ra có thể vào webGUI của pfSense bằng Virtual IP address này.

<figure><img src="../../../../.gitbook/assets/image (542).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (541).png" alt=""><figcaption></figcaption></figure>

**2.High Availability (HA) Mode (2+ Firewall VM)**

**a. Đặc điểm:**

* VIP được chia sẻ giữa **2 hoặc nhiều firewall**
* Có cơ chế failover tự động

**b. Khi nào dùng:**

* Production environment
* Dịch vụ mission-critical (không được phép downtime)
* Yêu cầu SLA cao (99.9% uptime trở lên)

**Ưu điểm:**

* Firewall chính die → VIP tự động chuyển sang Firewall backup
* Zero downtime hoặc downtime tối thiểu (vài giây)

**Cấu hình phổ biến:**

* **Active-Passive**: 1 server chính xử lý, 1 server dự phòng chờ sẵn
* **Active-Active**: Cả 2 servers cùng xử lý (kết hợp load balancing)

Hiện tại Virtual IP Address cho vMarketplace đang hỗ trợ cấu hình **Active-Passive**

**Luồng traffic:** Internet → VIP (157.20.200.185) → Firewall VM 1 (NAT + Filter), Firewall VM 2 (NAT + Filter) → Server 1 (192.168.2.7), Server 2 (192.168.2.5)

**Các bước thực hiện:**

**Bước 1: Chuẩn bị Virtual IP Address và 2 Firewall pfSense, thực hiện pair và add Virtual IP Address, thêm rule để server nội bộ ra internet như Bước 1, Bước 2, Bước 3, Bước 4 ở hướng dẫn mode standalone**

Lưu ý: Virtual IP Address phải Add Address pair với cả 2 external interface của 2 firewall pfSense

<figure><img src="../../../../.gitbook/assets/image (545).png" alt=""><figcaption></figcaption></figure>

**Bước 2: Trên portal vServer, vào Firewall VM detail và Add thêm 1 internal interface vào cả 2 firewall pfSense để làm interface HA**

<figure><img src="../../../../.gitbook/assets/image (546).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (585).png" alt=""><figcaption></figcaption></figure>

**Bước 3: Config chân interface HA cho 2 firewall pfsense**

Vào webGUI pfsense, assignment interface vừa add từ vServer portal, và config như sau

IPv4 Address là IP của interface HA, lấy từ portal vServer

<figure><img src="../../../../.gitbook/assets/image (592).png" alt=""><figcaption></figcaption></figure>

Thực hiện tương tự với firewall pfsense còn lại.

**Bước 4: Thêm rule cho interface HA để allow synchronize configuration giữa 2 firewall pfSense**

Trên webGUI pfSense, vào Firewall -> Rules -> SYNC (hoặc tên interface HA) -> Add

<figure><img src="../../../../.gitbook/assets/image (594).png" alt=""><figcaption></figcaption></figure>

Tiến hành config rule như sau

<figure><img src="../../../../.gitbook/assets/image (600).png" alt=""><figcaption></figcaption></figure>

Thực hiện tương tự với backup firewall còn lại.

**Bước 5: Config HA (chỉ trên Master firewall)**

Trên webGUI pfSense, vào System -> High Availability

Config như hình bên dưới:

Lưu ý:

* pfsync Synchronize Peer IP, Synchronize Config to IP: nhập địa chỉ IP interface HA của backup pfSense.
* Remote System Username, Remote System Password: nhập username/password của backup pfSense (bắt buộc là account admin)
* Select options to sync: chọn các option mà khách hàng muốn synchronize qua backup pfSense

<figure><img src="../../../../.gitbook/assets/image (654).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../../../.gitbook/assets/image (660).png" alt=""><figcaption></figcaption></figure>

**Bước 6: Kiểm tra**

Trên webGUI pfSense, vào Status -> CARP (failover)

* Trên Master firewall pfSense

<figure><img src="../../../../.gitbook/assets/image (696).png" alt=""><figcaption></figcaption></figure>

* Trên Backup firewall pfSense

<figure><img src="../../../../.gitbook/assets/image (710).png" alt=""><figcaption></figcaption></figure>

Việc cấu hình CARP Virtual IP trong pfSense HA nhằm mục đích tạo ra một địa chỉ IP ảo có thể được chia sẻ giữa các thiết bị trong cụm HA.\
Khi một thiết bị hoặc tường lửa chính (Master) gặp sự cố, CARP cho phép địa chỉ IP ảo tự động chuyển từ thiết bị gặp sự cố sang thiết bị dự phòng (Backup).
