# Hạn mức tài nguyên

Sản phẩm vDB OpenSearch thiết lập hạn mức tài nguyên để đảm bảo rằng chúng tôi có thể cung cấp dịch vụ nhanh chóng và linh hoạt cho tất cả khách hàng. Hạn mức tài nguyên này là mức tối đa mà chúng tôi đề xuất và một số hạn mức tài nguyên có thể được tùy chỉnh theo nhu cầu lưu trữ của bạn. Để gửi yêu cầu điều chỉnh tăng hạn mức, vui lòng truy cập Trung tâm hỗ trợ GreenNode và tạo yêu cầu [tại đây](https://helpdesk.greennode.ai/portal/en/newticket).

## Bảng hạn mức

Các hạn mức dưới đây áp dụng như nhau cho mọi phiên bản OpenSearch đang hỗ trợ: **2.8, 2.12, 2.15 và 2.17**.

| Hạn mức | Giá trị | Điều chỉnh được | Ghi chú |
| --- | --- | --- | --- |
| Số OpenSearch Cluster / tài khoản (SSO account email) | 10 | Có, gửi yêu cầu tới Trung tâm hỗ trợ GreenNode | Tính theo tài khoản, chung cho mọi phiên bản |
| Số node tối đa / cluster | 9 | Trên 9 node, vui lòng liên hệ GreenNode | Chỉ tăng được số node, không giảm được |
| Dung lượng ổ đĩa tối thiểu / node | 20 GB | Có | Chỉ tăng được, không giảm được |
| Dung lượng ổ đĩa tối đa / node | 5 TB | — | Chỉ tăng được, không giảm được |
| IOPS tối đa / node | 60.000 | Có | Tăng và giảm IOPS đều được |
| JVM heap | 50% memory của node | Có | Tối đa 32 GB |
| Số shard tối đa / cluster | 1.000 × số data node | Có, qua Configuration Group (khoảng 1 – 10.000 shard / node) | Mặc định 1.000 shard / node. Ví dụ: cluster 3 node có tối đa 3.000 shard; cluster 9 node có tối đa 9.000 shard |
| Region có thể triển khai | HCM | — | Chưa hỗ trợ region HAN |
| Multi-AZ | Không hỗ trợ | — | Chưa hỗ trợ Multi-AZ |

## Ghi chú

### Số shard tối đa

* Giới hạn tính trên toàn cluster, bằng `cluster.max_shards_per_node` × số data node, gồm cả primary lẫn replica của các index đang mở. Node của vDB OpenSearch vừa là master vừa là data, nên số data node bằng số node của cluster.
* Khi vượt giới hạn, request tạo index hoặc tăng replica sẽ bị từ chối với lỗi `this action would add [...] total shards, but this cluster currently has [...]/[...] maximum shards open`.
* Nếu có đặt `cluster.max_shards_per_cluster` (khác -1), `cluster.max_shards_per_node` không được lớn hơn giá trị đó.

### JVM heap

Dịch vụ OpenSearch giới hạn bộ nhớ của các tiến trình Java ở mức 50% tổng bộ nhớ khả dụng của node (tối đa 32 GiB).
