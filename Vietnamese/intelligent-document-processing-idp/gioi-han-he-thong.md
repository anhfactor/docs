# Giới hạn hệ thống

| Hạng mục                         | Giới hạn mặc định                              |
| -------------------------------- | ---------------------------------------------- |
| Định dạng ảnh                    | .jpg, .jpeg, .png, .bmp, .tif, .tiff           |
| Ảnh                              | 2KB – 10MB mỗi ảnh                             |
| PDF                              | 2KB – 100MB                                    |
| ZIP                              | 1 tệp, tối đa 50MB                             |
| Tổng dung lượng mỗi hồ sơ        | 100MB                                          |
| Chuyển qua Word/PDF              | Tối đa 50 trang; từ 20 trang xử lý bất đồng bộ |
| Kiểm thử quy trình               | Tối đa 50 bộ tài liệu                          |
| Chạy lại OCR                     | 3 lần mỗi hồ sơ, chỉ khi đang chờ duyệt        |
| Xuất Excel hàng loạt             | 1.000 hồ sơ mỗi lần                            |
| Xem lịch sử sử dụng              | Tối đa 31 ngày mỗi lần lọc                     |
| Tự thử lại bước lỗi              | 3 lần (cấu hình được)                          |
| Chờ duyệt / chờ thao tác sau lỗi | 3 ngày (cấu hình được)                         |
| Lưu trữ dữ liệu / tệp            | 90 ngày (mặc định)                             |
| Gọi API tạo hồ sơ                | 100 request/phút cho mỗi API Key               |
| Gọi API lấy/sửa kết quả          | 200 request/phút cho mỗi API Key               |
| Giao diện web                    | 1.000 request/phút cho mỗi địa chỉ IP          |

Vượt giới hạn tần suất, hệ thống trả lỗi 429 — chờ một lúc rồi thử lại, giãn dần khoảng cách giữa các lần thử.
