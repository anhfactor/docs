# Giám sát dịch vụ

Khi bạn tạo Kafka Cluster, hệ thống tự động thu thập metric của cluster qua vMonitor Platform và hiển thị ở tab **Monitor** trong trang chi tiết. Một số metric được bật sẵn, bạn không cần cấu hình thêm.

Để xem metric:

1. Truy cập trang chi tiết Kafka Cluster.
2. Chọn tab **Monitor**.
3. Chọn **Cluster metric** để xem metric của cả cluster, có thể lọc theo topic, hoặc **Node metric** để xem metric của từng broker.
4. Chọn khoảng thời gian cần xem ở góc phải, từ 15 phút đến 1 ngày.

Các biểu đồ chính có sẵn ở tab Monitor:

| Chế độ xem | Nhóm | Biểu đồ |
| --- | --- | --- |
| Cluster metric | Topic và partition | Topics, Partitions, Replicas, In Sync Replicas, Under Replicated Partitions |
| Cluster metric | Message và consumer group | Messages in per second, Messages consumed per second, Consumer Group Lag, Latest Offsets, Oldest Offsets |
| Node metric | Trạng thái broker | Brokers Online, Active Controllers, Offline Partitions Count, Unclean Leader Election |
| Node metric | Tài nguyên | CPU Usage, Memory Usage, Available Disk Space, Log Size |
| Node metric | JVM | JVM Memory Used, JVM GC Time, JVM GC Count, JVM Thread Count |
| Node metric | Lưu lượng và request | Byte Rate, Messages In Per Second, Produce Request Rate, Fetch Request Rate |

Để xem thêm metric ngoài tập bật sẵn, tự vẽ dashboard hoặc tạo cảnh báo (alarm), chọn **Monitored by vMonitor Platform** để chuyển sang vMonitor Platform và bật Detailed Monitoring. Tham khảo:

* [Giám sát hoạt động vDB bằng vMonitor Platform](../relational-database-service-rds/working-with-rds/giam-sat-hoat-dong-vdb-bang-vmonitor-platform.md)
* [Danh sách metrics của vDB](../../vmonitor-platform/cach-tinh-nang-cua-vmonitor-platform/metrics/danh-sach-metrics-ho-tro/danh-sach-metrics-cua-vdb.md)
