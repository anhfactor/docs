# KIến trúc và luồng xử lí

Mỗi tài liệu đi qua 8 bước. Nắm được 8 bước này là điều kiện bắt buộc để Support khoanh vùng sự cố, vì màn hình Request Detail hiển thị đúng trạng thái của từng bước kèm mốc thời gian.

| Bước         | Nội dung xử lý                             | Ý nghĩa khi chuẩn đoán sự cố                             |
| ------------ | ------------------------------------------ | -------------------------------------------------------- |
| Ingested     | Nhận tài liệu vào hệ thống                 | Không có → kiểm tra Data Source / API key                |
| Queued       | Chờ worker xử lý                           | Đứng lâu → hàng đợi đầy, kiểm tra tải hệ thống           |
| Classify     | Phân loại tài liệu                         | Sai loại → xem confidence, cân nhắc thêm custom template |
| Extract      | Trích xuất dữ liệu                         | Thiếu field → xem confidence từng field                  |
| Normalize    | Chuẩn hoá dữ liệu                          | Sai định dạng → xem cấu hình Normalization               |
| Validate     | Áp rule nghiệp vụ, tính Risk Score         | Failed → xem rule nào FAILED ở Score Breakdown           |
| Human Review | Người kiểm tra Approve / Reject / Escalate | Waiting review → xử lý tại To Do                         |
| Decision     | Chốt kết quả cuối                          | Not run → chưa qua Human Review                          |
