# Kết nối Redis Cluster

Hướng dẫn này mô tả các bước kết nối tới Redis Cluster trên vDB bằng redis-cli, thông qua IP hoặc Domain, sử dụng ACL user để xác thực.

---

## Điều kiện tiên quyết

* Đã tạo Redis Cluster trên vDB. Xem [Khởi tạo Redis Cluster](khoi-tao-redis-cluster.md).
* Đã cài **redis-cli** trên máy dùng để kết nối (hoặc một redis client tương đương).
* Máy kết nối nằm chung Network với Instance, hoặc thuộc Network có mở ACL tới Endpoint Private của Instance.

---

## Cài đặt redis-cli

Nếu chưa có redis-cli, trên Linux bạn tải source và build như sau:

```bash
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make distclean  # Ubuntu systems only
make
sudo make install
```

---

## Bước 1 - Xác định thông tin Endpoint & xác thực

1. Mở giao diện quản lý Database, chọn Redis Cluster cần kết nối.
2. Chọn tab **Connectivity & Security**, xem mục **Endpoint & Port**.
3. Ghi lại **IP** hoặc **Domain** của Instance và **Port**:
   * `6379` — endpoint ghi, luôn trỏ tới Master.
   * `6380` — endpoint đọc, round-robin qua các Replica. Dữ liệu đọc từ endpoint này có thể trễ hơn bản ghi mới nhất; cần read-your-writes thì dùng `6379`.
4. Lấy thông tin xác thực: ACL user (mặc định `master-user`) và password.

![](../../../.gitbook/assets/Redis-cluster/ket-noi-redis-cluster-endpoint.png)

{% hint style="info" %}
Redis Cluster cho phép kết nối qua **IP** hoặc **Domain** — dùng giá trị nào cũng được.
{% endhint %}

## Bước 2 - Tùy chỉnh Security Group Rules (tùy chọn)

1. Mở tab **Connectivity & Security**, tại mục **Security Group Rules**, chọn **EDIT**.
2. Điền **Remote IP** tin cậy theo chuẩn CIDR, hoặc nhấn **ADD RULE** để thêm rule mới.
3. Nhấn **Save** và chờ thay đổi được lưu lại.

![](../../../.gitbook/assets/Redis-cluster/ket-noi-redis-cluster-security-group.png)

{% hint style="warning" %}
Mặc định Instance cho phép truy cập từ mọi nơi (`0.0.0.0/0`). GreenNode khuyến nghị giới hạn chỉ những Remote IP tin cậy được truy cập vào Instance.
{% endhint %}

## Bước 3 - Kết nối bằng redis-cli

Khi tạo Redis Cluster, hệ thống tự tạo ACL user mặc định tên `master-user`. Bạn kết nối bằng `master-user` cùng password đã đặt lúc khởi tạo.

Kết nối qua **IP**:

```bash
redis-cli -h 10.0.0.10 -p 6379 --user master-user --pass '<PASSWORD>'
```

Kết nối qua **Domain**:

```bash
redis-cli -h my-redis-cluster.vdb-redis.vngcloud.vn -p 6379 --user master-user --pass '<PASSWORD>'
```

Thay `10.0.0.10` hoặc `my-redis-cluster.vdb-redis.vngcloud.vn` bằng IP/Domain của Instance, và `<PASSWORD>` bằng password đã đặt lúc khởi tạo.

{% hint style="info" %}
Đối với long-time query, cấu hình **tcp_keepalive** hoặc **healthcheck_interval** để tránh gián đoạn kết nối. Xem thêm [Lưu ý & hạn chế](../../announcements/luu-y-and-han-che.md#e.-long-time-query).
{% endhint %}

---

## Kết quả

Sau khi kết nối thành công, bạn nhận được prompt của redis-cli:

```bash
<IP>:6379>
```

Bạn đã có thể chạy các lệnh Redis lên Redis Cluster.
