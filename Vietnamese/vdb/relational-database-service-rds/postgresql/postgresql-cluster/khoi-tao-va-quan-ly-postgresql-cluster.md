# Khởi tạo và Quản lý PostgreSQL Cluster

PostgreSQL Cluster cho phép triển khai database với kiến trúc **1 Writer + N Readers**, đảm bảo **High Availability** và khả năng **scale read** cho ứng dụng của bạn. Khi Writer gặp sự cố, hệ thống tự động failover sang một Reader mà không cần can thiệp thủ công.

Để tìm hiểu thêm về khái niệm, kiến trúc và so sánh giữa Single Node và Cluster, vui lòng tham khảo tại [PostgreSQL Cluster](README.md).

***

## Khởi tạo PostgreSQL Cluster

### Truy cập vDB Portal

Bạn truy cập đến giao diện dịch vụ vDB qua 2 cách:

* **Cách 1**: Truy cập trang chủ GreenNode tại đường dẫn: [https://dashboard.console.greennode.ai/](https://dashboard.console.greennode.ai/). Tại giao diện chính, bạn tìm đến dịch vụ **vServer** và chọn dịch vụ **vDB Relational** trong danh sách sản phẩm/dịch vụ vServer.
* **Cách 2**: Truy cập trực tiếp đến trang chủ vDB Relational tại đường dẫn: [https://vdb.console.greennode.ai/relational/database](https://vdb.console.greennode.ai/relational/database)

### Tạo PostgreSQL Cluster

Tại giao diện quản lý Database, bạn click chọn **Create Database**. Quá trình khởi tạo sẽ trải qua các bước sau:

#### Bước 1: Cấu hình cơ bản (Basic Configuration)

* **Cluster Name**: Nhập tên cho cluster (6-20 ký tự, bắt đầu bằng chữ cái).
* **Database Engine**: Chọn **PostgreSQL**.
* **Deployment Type**: Chọn **Cluster** (tùy chọn này chỉ hiển thị khi Engine là PostgreSQL).
* **Availability & Durability**: Chọn **Single-AZ** hoặc **Multi-AZ**. Với Multi-AZ, xem hướng dẫn riêng tại [Khởi tạo PostgreSQL Cluster Multi-AZ](khoi-tao-postgresql-cluster-multi-az.md).

{% hint style="info" %}
Khi chọn Deployment Type là **Cluster**, label sẽ đổi từ "Database Instance Name" thành "Cluster Name".
{% endhint %}

**Khôi phục từ Backup (tùy chọn):**

Khi chọn Deployment Type là **Cluster**, hệ thống hiển thị thêm section **Backup Image** cho phép bạn khôi phục cluster từ backup có sẵn:

* Expand một backup item để xem các **restore points**.
* Chọn một restore point nếu muốn tạo cluster với dữ liệu từ backup đó.
* Nếu không chọn restore point nào, cluster sẽ được tạo mới với database trống.

{% hint style="warning" %}
**Lưu ý:** Khi khôi phục từ backup, **Storage Size** của cluster mới phải lớn hơn hoặc bằng **Backup Size** của bản backup đã chọn.
{% endhint %}

#### Bước 2: Thông số kỹ thuật (Specifications)

* **Engine Version**: Chọn phiên bản PostgreSQL (ví dụ: 15, 14, 13...).
* **Flavor**: Chọn cấu hình instance (vCPU, RAM). Cấu hình này áp dụng cho **tất cả các node** trong cluster.
* **Storage Type**: Chọn loại ổ cứng lưu trữ.
* **Storage Size**: Chọn dung lượng ổ cứng (bao gồm data và log).
* **Number of Nodes**: Chọn số lượng node cho cluster (từ 2 đến 10). Hệ thống sẽ hiển thị **Role Distribution** tương ứng:

| Số lượng Node | Phân bổ vai trò |
| --- | --- |
| 2 | 1 Writer + 1 Reader |
| 3 | 1 Writer + 2 Readers |
| 5 | 1 Writer + 4 Readers |
| 10 | 1 Writer + 9 Readers |

#### Bước 3: Cài đặt phiên bản DB (DB Settings)

* **Master Username**: Username để quản trị database cluster.

{% hint style="warning" %}
**Reserved Usernames:** Bạn không được sử dụng các username sau: `postgres`, `admin`, `cron_admin`, `robot_zmon`, `vngpooler`, `vngpam`, `vngrep`, `vngsuperrole`.
{% endhint %}

* **Master Password**: Password của master user. Password cần thỏa các yêu cầu:
  * Độ dài từ 8-32 ký tự.
  * Cho phép: A-Z, a-z, 0-9 và các ký tự đặc biệt ($, ^, \_, <, >).
  * Phải bắt đầu bằng ký tự chữ cái (A-Z hoặc a-z).
  * Không được bắt đầu hay kết thúc bằng ký tự đặc biệt.

#### Bước 4: Mạng và bảo mật (Network & Security)

* **Cloud Network (VPC & Subnet)**: Chọn VPC và Subnet cho cluster. Nếu chưa có, bạn có thể tạo mới theo hướng dẫn [tại đây](../../../../vserver/compute-hcm03-1a/network/virtual-private-cloud-vpc/README.md).
* **Public Accessibility**: Bật nếu muốn cluster có IP Public và truy cập từ Internet; tắt nếu chỉ muốn truy cập qua IP Private.
* **Multi-AZ**: nếu ở Bước 1 bạn chọn **Multi-AZ**, mục này yêu cầu VPC đã bật DNS và hiển thị bảng **Subnets** để chọn zone thay cho một Subnet đơn — xem [Khởi tạo PostgreSQL Cluster Multi-AZ](khoi-tao-postgresql-cluster-multi-az.md).

{% hint style="warning" %}
**Lưu ý:** Thiết lập Public Accessibility chỉ được chọn **một lần duy nhất** tại thời điểm khởi tạo và không thể thay đổi sau đó.
{% endhint %}

#### Bước 5: Tùy chọn DB (DB Options)

* **Database Name**: Tên database sẽ được khởi tạo tự động.
* **DB Configuration Group** (tùy chọn): Chọn Configuration Group áp dụng cho cluster.

#### Bước 6: Cài đặt Backup (Backup Settings)

{% hint style="info" %}
Backup Settings là **bắt buộc** khi tạo PostgreSQL Cluster. Bạn phải chọn cả Backup Policy và Backup Location.
{% endhint %}

* **Backup Policy**: Chọn policy quy định lịch backup và thời gian lưu trữ (retention) từ Backup Center.
* **Backup Location**: Chọn location lưu trữ backup từ Backup Center. Dropdown chỉ hiển thị các location có **status = Available** và **Product = vDB**, sắp xếp theo thứ tự **mới nhất lên đầu**.

{% hint style="warning" %}
**Trường hợp không có Backup Location khả dụng:**

Nếu tài khoản của bạn chưa có Backup Location nào ở trạng thái Available, dropdown Backup Location sẽ hiển thị viền màu đỏ kèm thông báo lỗi. Bạn cần click vào link trong thông báo để mở Backup Center và tạo mới location trước khi tiếp tục tạo cluster.
{% endhint %}

Nếu chưa có Backup Policy, bạn có thể click vào link để mở Backup Center và tạo mới.

{% hint style="info" %}
**Lưu ý:** Backup Location **không thể thay đổi** sau khi cluster đã được tạo. Mỗi cluster được gắn cố định với một Backup Location duy nhất, vì vậy hãy chọn location phù hợp ngay từ đầu.
{% endhint %}

#### Hoàn tất

Tại mục **Summary** bên phải, rà soát lại các thông tin cấu hình. Khi mọi thông tin đã chính xác, nhấn **Create Database** để hoàn tất. Trong quá trình khởi tạo, cluster sẽ có trạng thái **Building**. Khi khởi tạo thành công, cluster sẽ chuyển sang trạng thái **Active**.

***

## Quản lý PostgreSQL Cluster

### Xem danh sách Database

Tại trang Database List, bạn có thể lọc nhanh database theo loại deployment:

| Tab | Mô tả |
| --- | --- |
| **All Databases** | Hiển thị tất cả database |
| **Single Node** | Chỉ hiển thị các database Single Node |
| **Clusters** | Chỉ hiển thị các database Cluster |

### Xem chi tiết Cluster

Khi click vào một cluster trong danh sách, trang chi tiết hiển thị các thông tin:

**General Information:**

| Thông tin | Mô tả | Ví dụ |
| --- | --- | --- |
| ID | ID định danh của cluster | pg-1dfa6aaf-20c9-44a1-... |
| Zone | Availability Zone | HCM03-1A |
| Role | Vai trò của instance | Primary Writer / Replica Reader |
| Replica Source | Nguồn replica (nếu có) | N/A |
| Instance Type | Cấu hình instance | db-postgre.s-general-2x4-n10 (2 Core, 4 GB) |
| Engine | Engine và deployment type | PostgreSQL 15 (Cluster, 3 Node) |
| Storage | Dung lượng và loại storage | 20 GB (GEN2-NVME-IOPS5000) |
| Free GB | Dung lượng backup miễn phí đi kèm package | 20 GB |
| Configuration Group | Configuration group đang áp dụng | default-group |
| Network | VPC network | vpc-10-10-0-0 |

**Các tab chi tiết:**

| Tab | Nội dung |
| --- | --- |
| **Configuration** | Thông tin flavor (vCPU, RAM) và storage (type, size, disk usage) |
| **Connectivity & Security** | Connection endpoints và cài đặt bảo mật |
| **Backup** | Lịch sử backup, tạo manual backup, xem backup information |
| **History** | Activity logs |
| **Monitor** | Metrics và biểu đồ giám sát, xem mục **Giám sát cluster (Monitoring)** bên dưới |

***

### Tạo Backup ngay lập tức (Back up now)

Nút **Back up now** hiển thị trực tiếp trên thanh action của trang chi tiết cluster (ngang hàng với Reboot, Edit Number of Nodes, Resize IOPS, Resize Storage Size), không nằm trong menu More Actions (⋮).

1. Tại trang chi tiết cluster, click **Back up now** trên thanh action.
2. Hệ thống hiển thị dialog xác nhận.
3. Click **Confirm** để bắt đầu tạo backup.

Sau khi xác nhận, hệ thống trigger tạo Full Snapshot và hiển thị toast thông báo. Bản backup mới xuất hiện trong tab **Backup** với trạng thái **In Progress** và chuyển sang **Completed** khi hoàn tất.

{% hint style="warning" %}
**Lưu ý:**

* Nút **Back up now** sẽ bị **disabled** khi đang có một backup job (Auto hoặc Manual) đang chạy. Hover vào nút sẽ hiển thị tooltip thông báo.
* Nếu tài khoản hết quota hoặc bị khóa, hệ thống trả lỗi và không tự động retry.
{% endhint %}

### Thay đổi số lượng Node (Edit Number of Nodes)

Bạn có thể thay đổi số lượng node trong cluster (từ 2 đến 10):

1. Tại trang chi tiết cluster, click **Edit Number of Nodes** trên thanh action.
2. Nhập số lượng node mong muốn.
3. Xác nhận thay đổi.

Hệ thống sẽ tự động thêm hoặc bớt Reader nodes. Writer node không bị ảnh hưởng.

### Thay đổi IOPS (Resize IOPS)

1. Tại trang chi tiết cluster, click **Resize IOPS** trên thanh action.
2. Chọn thông số IOPS mới.
3. Xác nhận thay đổi.

### Thay đổi dung lượng Storage (Resize Storage Size)

1. Tại trang chi tiết cluster, click **Resize Storage Size** trên thanh action.
2. Nhập dung lượng storage mới (chỉ hỗ trợ tăng, không hỗ trợ giảm).
3. Xác nhận thay đổi.

### Chỉnh sửa Configuration Group

1. Tại trang chi tiết cluster, click **More Actions (⋮)** > **Edit Configuration Group**.
2. Chọn Configuration Group mới.
3. Xác nhận thay đổi.

### Khởi động lại Cluster (Reboot)

1. Tại trang chi tiết cluster, click **Reboot** trên thanh action.
2. Xác nhận khởi động lại.

### Giám sát cluster (Monitoring)

Khi bạn tạo PostgreSQL Cluster, hệ thống tự động thu thập metric của cluster qua vMonitor Platform và hiển thị ở tab **Monitor** trong trang chi tiết. Một số metric được bật sẵn, bạn không cần cấu hình thêm.

Để xem metric:

1. Truy cập trang chi tiết PostgreSQL Cluster.
2. Chọn tab **Monitor**.
3. Chọn **Cluster metric** để xem metric của cả cluster, hoặc **Node metric** để xem metric của từng node.
4. Chọn khoảng thời gian cần xem ở góc phải, từ 15 phút đến 1 ngày.

Các biểu đồ chính có sẵn ở tab Monitor:

| Chế độ xem | Nhóm | Biểu đồ |
| --- | --- | --- |
| Cluster metric | Kết nối | Max Connections, Connection Usage Per Node |
| Cluster metric | Bộ nhớ và cache | Shared Buffers, Cache Hit Rate |
| Cluster metric | Replication | Replication Lag |
| Node metric | Trạng thái node | Online Nodes |
| Node metric | Tài nguyên | CPU Usage, Mem Usage (Percent), Volume Usage (Percent) |

Để xem thêm metric ngoài tập bật sẵn, tự vẽ dashboard hoặc tạo cảnh báo (alarm), chọn **Monitored by vMonitor Platform** để chuyển sang vMonitor Platform và bật Detailed Monitoring. Tham khảo:

* [Giám sát hoạt động vDB bằng vMonitor Platform](../../working-with-rds/giam-sat-hoat-dong-vdb-bang-vmonitor-platform.md)
* [Danh sách metrics của vDB](../../../../vmonitor-platform/cach-tinh-nang-cua-vmonitor-platform/metrics/danh-sach-metrics-ho-tro/danh-sach-metrics-cua-vdb.md)

***

## Quản lý Backup

### Xem thông tin Backup

Tại trang chi tiết cluster, chọn tab **Backup** để xem:

* **Backup Information**: Thông tin tổng quan bao gồm Description, Created Date, Latest Record, Backup Size, Backup Policy, Backup Location.
* **Backup List**: Danh sách các bản backup với thông tin Backup DB Point ID, Min.Restore Size (GB), Backup Type, Schedule Type, Backup Location, Backup Point, Status, Action (Restore / Delete).

Tại đầu tab Backup có link **"View full backup details →"** dẫn thẳng đến trang backup chi tiết của cluster đang xem trong Backup Center (mở trong tab mới).

### Tạo Manual Backup

Có 2 cách tạo Manual Backup:

* **Cách 1 (khuyến nghị):** Click nút **Back up now** trực tiếp trên thanh action của trang chi tiết cluster (xem hướng dẫn tại [Tạo Backup ngay lập tức](#tạo-backup-ngay-lập-tức-back-up-now)).
* **Cách 2:** Tại tab **Backup**, click **Create Manual Backup**, sau đó xác nhận.

Hệ thống sẽ tạo một **Full Snapshot** của database. Bản backup mới xuất hiện trong danh sách với trạng thái **In Progress** và chuyển sang **Completed** khi hoàn tất.

{% hint style="warning" %}
**Lưu ý:**

* Manual Backup chỉ hỗ trợ tạo **Full Snapshot**.
* Chỉ cho phép **1 job** backup/restore chạy tại 1 thời điểm. Nếu Auto Backup đang chạy, Manual Backup sẽ bị từ chối.
* Nếu tài khoản hết quota hoặc bị khóa, hệ thống sẽ trả lỗi và không tự động retry.
{% endhint %}

### Khôi phục từ Backup (Restore)

Việc khôi phục từ backup sẽ **tạo một cluster mới** (không restore đè lên cluster hiện tại):

1. Tại tab **Backup**, click **Restore** trên bản backup muốn khôi phục.
2. Hoặc khi tạo cluster mới, chọn restore point tại section **Backup Image** trong Bước 1.
3. Cấu hình các thông số cho cluster mới (Storage Size phải >= Backup Size).
4. Hoàn tất tạo cluster.

### Trang Backup vDB

Truy cập **Menu: Relational > Backup** để xem tổng quan các bản backup:

* Khi chưa có backup: Hiển thị thông báo và nút **Create a Backup** để chuyển đến Backup Center.
* Khi đã có backup: Hiển thị danh sách backup và nút **Go to Backup Center** để quản lý đầy đủ (Download, Restore, Delete, Policy).

{% hint style="info" %}
Trang Backup vDB chỉ cho phép **xem** danh sách backup. Để thực hiện các thao tác quản lý đầy đủ (Download, Restore, Delete), vui lòng truy cập **Backup Center**.
{% endhint %}

***

## Xóa PostgreSQL Cluster

1. Tại trang chi tiết cluster, click **More Actions (⋮)** > **Delete**.
2. Hệ thống hiển thị dialog xác nhận với các thành phần:
   * **Checkbox "Create final backup?"** (tùy chọn): Chọn nếu muốn tạo một bản backup cuối trước khi xóa.
   * **Ô nhập xác nhận:** Nhập chữ **`delete`** để kích hoạt nút Delete.
3. Click **Delete** (màu đỏ) để hoàn tất.

{% hint style="info" %}
**Trường hợp cluster không còn Backup Database trong Backup Center:**

* Checkbox "Create final backup?" sẽ bị **disabled** và không thể chọn.
* Hệ thống hiển thị thông báo kèm theo.
* Vẫn cần nhập chữ **`delete`** để xác nhận.
{% endhint %}

{% hint style="warning" %}
**Lưu ý khi xóa Cluster:**

* **Auto Backup** sẽ được tự động xóa cùng cluster.
* **Manual Backup** sẽ được giữ lại. Bạn cần tự xóa tại Backup Center nếu không còn cần thiết.
* Hành động xóa **không thể hoàn tác**. Hãy đảm bảo bạn đã sao lưu dữ liệu cần thiết trước khi xóa.
{% endhint %}
