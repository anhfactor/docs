# Volume Types

Volume Type thể hiện thông tin hiệu năng của volume. GreenNode sử dụng Volume Type để cung cấp tính năng QoS cho Volume. QoS giúp kiểm soát băng thông và IOPS cho từng Volume, bạn cần chọn mức QoS phù hợp với ứng dụng để ứng dụng hoạt động tốt nhất.

### **Volume QoS** <a href="#volumetypes-volumeqos" id="volumetypes-volumeqos"></a>

IOPS là chỉ số thể hiện số read/write có thể thực hiện trên volume trong mỗi giây. IOPS cao sẽ cần thiết cho các ứng dụng nhạy cảm về giao tiếp đọc ghi data ví dụ như các ứng dụng database.

Bảng sau mô tả thông tin IOPS chi tiết cho từng loại Volume Type:



## NVME

#### Hỗ trợ ở Region HCM (Zone 1a, 1b), HAN (Zone 1a, 1b)

| IOPS  | Minimum Size (GB) | Throughput |
| ----- | ----------------- | ---------- |
| 3000  | 1                 | 200 MB/s   |
| 5000  | 1                 | 400 MB/s   |
| 10000 | 1                 | 600 MB/s   |
| 20000 | 1                 | 600 MB/s   |
| 40000 | 1                 | 600 MB/s   |
| 60000 | 1                 | 800 MB/s   |



## SSD

#### Hỗ trợ ở Region HCM (Zone 1c)

| IOPS  | Minimum Size (GB) | Throughput |
| ----- | ----------------- | ---------- |
| 3000  | 1                 | 200 MB/s   |
| 3200  | 1                 | 200 MB/s   |
| 6400  | 1                 | 400 MB/s   |
| 10000 | 1                 | 400 MB/s   |



Bạn có thể thay đổi Volume Type bất cứ lúc nào.

Đối với multi-attach volume, không hỗ trợ attach loại volume này vào các server nằm trên các Zone khác nhau.
