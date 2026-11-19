# VIP mode

Trong các hệ thống yêu cầu tính sẵn sàng cao (High Availability - HA), **Virtual IP (VIP)** đóng vai trò là một địa chỉ IP trừu tượng được chuyển đổi linh hoạt giữa nhiều node/máy chủ nhằm đảm bảo tính liên tục của dịch vụ. Một trong những lựa chọn quan trọng khi cấu hình VIP là chế độ hoạt động: **Active/Active** hoặc **Active/Passive**.

Hiểu rõ sự khác biệt giữa hai chế độ này giúp bạn đưa ra quyết định đúng đắn về kiến trúc hệ thống, hiệu năng và chi phí vận hành.

## 1. Active/Active Mode

#### Định nghĩa

Trong chế độ **Active/Active**, **tất cả các node** tham gia đều hoạt động đồng thời và cùng xử lý yêu cầu từ người dùng hoặc các hệ thống khác. Mỗi node đều có khả năng nhận và xử lý lưu lượng, đồng thời phối hợp để đảm bảo tính toàn vẹn dữ liệu và hiệu năng tối ưu.

#### Đặc điểm nổi bật

* **Phân tải công việc**: Nhiều node xử lý đồng thời nhờ load balancer, giảm thiểu tải từng máy.
* **Tăng hiệu suất và mở rộng dễ dàng**: Khi cần mở rộng, có thể bổ sung thêm node mà không làm gián đoạn dịch vụ.
* **Tính sẵn sàng cao tuyệt đối**: Nếu một node bị lỗi, các node còn lại vẫn tiếp tục xử lý công việc.
* **Cấu hình phức tạp hơn**: Yêu cầu cơ chế đồng bộ dữ liệu và cân bằng tải tinh vi.

#### Ứng dụng thực tế

* **Web server clusters**: Amazon, Google hay Facebook triển khai các cụm máy chủ web Active/Active kết hợp với Load Balancer như NGINX hoặc AWS ELB để xử lý hàng triệu request mỗi giây.
* **Distributed databases**: Hệ quản trị cơ sở dữ liệu như **MongoDB**, **Cassandra**, hoặc **CockroachDB** cho phép tất cả node cùng tham gia đọc/ghi.
* **Content Delivery Network (CDN)**: Hệ thống như **Cloudflare** hoặc **Akamai** sử dụng hàng nghìn edge server hoạt động đồng thời để phân phối nội dung đến người dùng gần nhất.

## 2. Active/Passive Mode

#### Định nghĩa

Trong chế độ **Active/Passive**, **chỉ có một node hoạt động (Active)** tại một thời điểm, còn node còn lại (Passive) ở trạng thái **chờ dự phòng**. Khi node Active gặp sự cố, VIP sẽ được chuyển sang node Passive, giúp hệ thống tiếp tục hoạt động sau thời gian failover ngắn.

#### Đặc điểm nổi bật

* **Hoạt động đơn giản**: Chỉ một node xử lý nên ít xung đột và dễ theo dõi.
* **Dự phòng an toàn**: Passive node luôn sẵn sàng tiếp quản khi node chính gặp sự cố.
* **Chi phí thấp hơn**: Không cần chia tải, chỉ cần 1 node xử lý và 1 node standby.
* **Downtime ngắn khi failover**: Có thể gián đoạn vài giây đến phút tùy hệ thống.

#### Ứng dụng thực tế

* **Database failover clusters**: Cụm SQL Server hoặc MySQL master-slave, chỉ master hoạt động, slave tiếp quản khi cần.
* **High Availability firewall**: Trong các mạng doanh nghiệp, một firewall chính bảo vệ hệ thống, firewall dự phòng chỉ hoạt động khi cần.
* **Ứng dụng nội bộ doanh nghiệp**: Các hệ thống ERP như SAP, CRM hoặc ứng dụng kế toán hoạt động ổn định với mô hình Active/Passive.

## 3. So sánh tổng thể

<table data-header-hidden><thead><tr><th width="184"></th><th width="273"></th><th></th></tr></thead><tbody><tr><td><strong>Tiêu chí</strong></td><td><strong>Active/Active</strong></td><td><strong>Active/Passive</strong></td></tr><tr><td><strong>Hiệu suất</strong></td><td>Cao, phân tải giữa các node</td><td>Thấp hơn, chỉ một node xử lý tại một thời điểm</td></tr><tr><td><strong>Tính sẵn sàng</strong></td><td>Không gián đoạn (zero downtime)</td><td>Có gián đoạn ngắn khi failover</td></tr><tr><td><strong>Chi phí</strong></td><td>Cao hơn (nhiều node hoạt động đồng thời)</td><td>Thấp hơn (1 node xử lý, 1 node standby)</td></tr><tr><td><strong>Độ phức tạp</strong></td><td>Phức tạp hơn (đồng bộ hóa, load balancing)</td><td>Đơn giản hơn (cần cấu hình failover)</td></tr><tr><td><strong>Ứng dụng phù hợp</strong></td><td>Hệ thống web lớn, cơ sở dữ liệu phân tán</td><td>Ứng dụng nội bộ, hệ thống tiết kiệm chi phí</td></tr></tbody></table>

## 4. Khuyến nghị mô hình hợp lý

* **Active/Active** lý tưởng cho các hệ thống **mission-critical**, web traffic lớn, hoặc nền tảng phân tán nhiều vùng.
* **Active/Passive** phù hợp với các ứng dụng **nội bộ**, **dữ liệu không thay đổi liên tục**, hoặc hệ thống backup đảm bảo sẵn sàng.

#### Khuyến nghị theo dòng firewall

* **pfSense**: khuyến nghị dùng **Active/Active**
* **Palo Alto**: khuyến nghị dùng **Active/Passive**

<table><thead><tr><th width="469">Nhu cầu của hệ thống bạn</th><th>Nên chọn chế độ</th></tr></thead><tbody><tr><td><strong>Không chấp nhận downtime</strong></td><td>Active/Active</td></tr><tr><td><strong>Cần hiệu suất xử lý cao</strong></td><td>Active/Active</td></tr><tr><td><strong>Hệ thống nhỏ, ưu tiên chi phí</strong></td><td>Active/Passive</td></tr><tr><td><strong>Ứng dụng có thể chấp nhận downtime ngắn</strong></td><td>Active/Passive</td></tr></tbody></table>
