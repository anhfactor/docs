# Cách tính phí

## Tổng quan

Hiện tại chúng tôi hỗ trợ **2 loại người dùng**: trả trước (prepaid) và trả sau (postpaid), với **2 hình thức tính phí**: Pay monthly và Pay as you go.

* **Pay monthly (Mua gói):** Bạn mua trước một lượng dung lượng cố định và thanh toán một khoản phí cố định, bất kể mức sử dụng thực tế. Ưu điểm là chi phí ổn định, dễ lập ngân sách, phù hợp với khối lượng công việc ổn định và có thể dự đoán trước. Đơn giá trên mỗi GB thường rẻ hơn nếu bạn sử dụng gần hết quota. Tuy nhiên, có thể gây lãng phí nếu bạn không dùng hết quota đã mua.
* **Pay as you go (PAYG):** Đo lường chính xác mức sử dụng của bạn trên các tier lưu trữ khác nhau — bạn chỉ trả tiền cho phần thực tế sử dụng. Ưu điểm là tối ưu chi phí, đặc biệt với nhu cầu sử dụng biến động, không cần dự báo trước. Phù hợp với startup hoặc khối lượng công việc không ổn định. Tuy nhiên, chi phí khó dự đoán và bạn cần theo dõi liên tục để tránh tăng đột biến.

Khi bạn tạo project mới, hệ thống hỗ trợ thay đổi quota của gói lưu trữ tới một giá trị nhất định.

Ban đầu, khi bạn đăng ký tài khoản GreenNode thành công, mặc định chúng tôi xếp bạn vào loại **người dùng trả trước**. Tức là bạn cần thanh toán gói lưu trữ trước khi có thể sử dụng dịch vụ, và gói sẽ có thời hạn tùy theo chu kỳ bạn chọn.

Nếu có nhu cầu và đáp ứng một số điều kiện về chỉ số chi tiêu, chúng tôi có thể hỗ trợ **chuyển đổi hình thức người dùng từ trả trước sang trả sau**, hoặc bạn có thể cân nhắc sử dụng hình thức thanh toán theo dung lượng sử dụng. Khi đó bạn không cần trả tiền lúc mua gói lưu trữ — giá trị hóa đơn mỗi tháng sẽ được tính dựa trên dung lượng, số lượng request... thực tế bạn sử dụng.

Bạn có thể lựa chọn hình thức phù hợp để tối ưu chi phí lưu trữ của bạn hay đơn vị của bạn. Chi tiết tham khảo thêm tại [Quản lý hóa đơn, chi phí & tài nguyên trên GreenNode](../../quan-ly-hoa-don-chi-phi-and-tai-nguyen/).

***

## Bảng giá

Bảng giá dưới đây áp dụng cho toàn bộ các region Object Storage (HCM03, HAN02, HCM04).

|                                 | Gold         | Gold (PAYG)        | Gold High Perf | Gold High Perf (PAYG) | Instant Archive | Instant Archive (PAYG) |
| ------------------------------- | ------------ | ------------------ | -------------- | --------------------- | --------------- | ---------------------- |
| **Giá lưu trữ** (VND/GB/tháng)  | 1.000        | 1.400              | 3.400          | 4.760                 | 530             | 742                    |
| **Request**                     | Unlimited    | Unlimited          | Unlimited      | Unlimited             | Unlimited       | Unlimited              |
| **Traffic download (free)**     | Free x10     | Free x10           | Free x10       | Free x10              | Free 3TB        | Free 3TB               |
| **Traffic upload**              | Free         | Free               | Free           | Free                  | Free            | Free                   |
| **Thời gian retrieval dữ liệu** | Ngay lập tức | Ngay lập tức       | Ngay lập tức   | Ngay lập tức          | Ngay lập tức    | Ngay lập tức           |
| **Hình thức tính phí**          | Mua package  | Dung lượng sử dụng | Mua package    | Dung lượng sử dụng    | Mua package     | Dung lượng sử dụng     |
| **Đơn vị tính phí**             | GB           | GB                 | GB/30 ngày     | GB                    | GB              | GB                     |
| **Minimum package size**        | 30 GB        | 1 GB               | 30 GB          | 1 GB                  | 30 GB           | 1 GB                   |

***

## Phí phát sinh (Extra)

|                                             | Gold & Gold PAYG | Gold High Perf & Gold High Perf PAYG | Instant Archive | Instant Archive (PAYG) |
| ------------------------------------------- | ---------------- | ------------------------------------ | --------------- | ---------------------- |
| **Domestic download traffic** (VND/GB)      | 280              | 280                                  | 280             | 280                    |
| **International download traffic** (VND/GB) | 330–580          | 330–580                              | 330–580         | 330–580                |

> **Lưu ý về Traffic download free:**
>
> * **Gold:** Hạn mức download miễn phí bằng 10 lần dung lượng lưu trữ (VD: lưu 30 GB → miễn phí 300 GB/tháng).
> * **Instant Archive:** Hạn mức cố định 3 TB/tháng.
> * Khi vượt hạn mức free, traffic sẽ tính phí theo giá **Domestic / International download** ở bảng Phí phát sinh.
