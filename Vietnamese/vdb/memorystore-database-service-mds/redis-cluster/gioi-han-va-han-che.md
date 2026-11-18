# Giới hạn và hạn chế

Trang này liệt kê các giới hạn và hạn chế hiện hành của **Redis Cluster (Non-sharding)** trên vDB — bao gồm topology và scaling, kết nối và bảo mật.

***

## 1. Topology & Scaling

| Hạng mục                | Giới hạn                                                                                                              |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------- |
| Kiến trúc               | Non-sharding — 1 shard duy nhất, 1 Master + 2–9 Replica (tổng 3–10 nodes)                                             |
| Write scaling           | Không hỗ trợ — toàn bộ ghi đi qua 1 Master (single writer)                                                            |
| Scale Replica           | Mỗi lần thay đổi ±1 node (tăng hoặc giảm đúng 1); không thể nhảy nhiều bước. Cluster luôn giữ 3–10 nodes              |
| Scale-down              | Nếu Master nằm trong nhóm bị xóa, hệ thống tự động failover sang Replica → gián đoạn ghi ngắn trong lúc chuyển Master |
| Scale dọc (nâng flavor) | Yêu cầu tạo lại node theo từng bước → kết nối tới node đang chuyển bị ngắt và tự kết nối lại; dữ liệu không bị mất    |

***

## 2. Kết nối & Client

| Hạng mục             | Giới hạn / Hành vi                                                                                                                              |
| -------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| Endpoint ghi         | Port `6379` — luôn trỏ tới Master                                                                                                               |
| Endpoint đọc         | Port `6380` — round-robin qua các Replica                                                                                                       |
| Độ nhất quán khi đọc | Replica đồng bộ bất đồng bộ → dữ liệu đọc từ endpoint `6380` có thể trễ hơn bản ghi mới nhất. Cần read-your-writes thì dùng endpoint ghi `6379` |
| Idle connection      | Kết nối nhàn rỗi quá 3.600 giây (1 giờ) bị LoadBalancer ngắt — ứng dụng nên có cơ chế auto-reconnect                                            |

{% hint style="info" %}
Cách cấu hình keepalive và health check cho kết nối dài, xem mục **E. Long-time query** tại [Lưu ý & hạn chế](../../announcements/luu-y-and-han-che.md).
{% endhint %}

***

## 3. Bảo mật

* Nếu tự đặt password (app-password): 9–32 ký tự, chỉ gồm `a-z A-Z 0-9 $ ^ _ < > % #`, bắt đầu bằng chữ cái, kết thúc bằng chữ hoặc số, và phải đủ 4 nhóm (in hoa, thường, số, ký tự đặc biệt).
* Truy cập chỉ qua LoadBalancer endpoint; giới hạn nguồn truy cập bằng whitelist (security group) cấu hình khi tạo/chỉnh sửa cluster. Xem [Kết nối Redis Cluster](ket-noi-redis-cluster.md).
