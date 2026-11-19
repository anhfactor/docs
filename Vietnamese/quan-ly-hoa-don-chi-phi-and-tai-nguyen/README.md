# Quản lý hóa đơn, chi phí & tài nguyên trên GreenNode

**Billing & Payment** giúp bạn thanh toán, nhận hóa đơn và theo dõi chi phí của mọi dịch vụ GreenNode như vServer, vStorage, vMonitor, vCDN ở cùng một nơi, mà không cần đối soát riêng từng sản phẩm.

***

## Cách Billing & Payment hoạt động

Mỗi khi bạn khởi tạo, thay đổi cấu hình, gia hạn hay xóa tài nguyên trên trang sản phẩm, Billing & Payment ghi nhận hành động đó, xử lý thanh toán và phát sinh hóa đơn cho đúng tài nguyên. Hóa đơn, lịch sử thanh toán và biến động Credit của mọi sản phẩm được gom về **vConsole** tại [dashboard.console.greennode.ai](https://dashboard.console.greennode.ai/).

Với người dùng trả trước, luồng khởi tạo tài nguyên gồm 3 bước:

1. **Cấu hình tài nguyên**: chọn tài nguyên và cấu hình tại trang sản phẩm, xác nhận để chuyển sang trang thanh toán.
2. **Thanh toán**: chọn số lượng và thời gian sử dụng, nhập coupon nếu có, rồi thanh toán bằng số dư Credit, **Top up & Pay** hoặc tài khoản liên kết.
3. **Kiểm tra kết quả**: tài nguyên hiện ở trang sản phẩm, hóa đơn và lịch sử thanh toán hiện trên vConsole.

***

## Người dùng trả trước và trả sau

Mỗi tài khoản GreenNode thuộc một trong hai loại người dùng. Loại người dùng quyết định khi nào bạn trả tiền, khi nào hóa đơn phát sinh và bạn làm được những hành động nào trên tài nguyên.

| Tiêu chí                  | Trả trước                                                              | Trả sau                                                         |
| ------------------------- | ---------------------------------------------------------------------- | --------------------------------------------------------------- |
| Thời điểm trả tiền        | Trước khi dùng, theo cấu hình và thời gian sử dụng bạn chọn            | Sau khi dùng, theo chi phí sử dụng thực tế, chốt mỗi cuối tháng |
| Cấp tài nguyên            | Sau khi thanh toán thành công. Cấp lỗi thì tiền được hoàn về ví Credit | Ngay khi bạn xác nhận, không qua bước thanh toán                |
| Hóa đơn                   | Phát sinh khi cấp tài nguyên xong, ở trạng thái đã thanh toán          | Phát sinh mỗi cuối tháng, ở trạng thái chưa thanh toán          |
| Cách thanh toán hóa đơn   | Không cần, hóa đơn đã thanh toán khi phát sinh                         | Thanh toán hóa đơn tự động                                      |
| Hành động trên tài nguyên | Khởi tạo, thay đổi cấu hình, gia hạn, tự động gia hạn, khôi phục, xóa  | Khởi tạo, thay đổi cấu hình, xóa                                |

{% hint style="info" %}
Tài khoản mới đăng ký mặc định là người dùng trả trước. Để chuyển sang trả sau, hoặc từ trả sau quay về trả trước, bạn liên hệ bộ phận Sale / Support.
{% endhint %}

***

## Các nhóm chức năng chính

### Thanh toán

Billing & Payment hỗ trợ nhiều phương thức: thanh toán trực tuyến, thanh toán tài nguyên POC, tạm giữ Credit và thanh toán hóa đơn tự động. Bạn có thể thanh toán nhiều tài nguyên trong một lần. Khi đó lịch sử thanh toán ghi một khoản tiền chung, còn mỗi tài nguyên có hóa đơn riêng.

### Quản lý hóa đơn

Mỗi hành động trên tài nguyên như tạo mới, thay đổi cấu hình, gia hạn đều phát sinh hóa đơn cho đúng tài nguyên đó, nên bạn đối soát được chi phí tới từng tài nguyên.

### Quản lý vòng đời tài nguyên

Hệ thống theo dõi trạng thái tài nguyên từ lúc khởi tạo tới lúc xóa và gửi email nhắc trước khi tài nguyên trả trước hết hạn. Nếu sản phẩm hỗ trợ tự động gia hạn và bạn đã bật tính năng này cho tài nguyên, hệ thống sẽ tự gia hạn để việc sử dụng không bị gián đoạn. Tài nguyên trả trước hết hạn mà không được gia hạn sẽ bị tạm ngưng, sau đó bị xóa vĩnh viễn.

### Theo dõi chi phí trên vConsole

| Trang                                                                                                                                             | Dùng để                                                                             |
| ------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [Lịch sử hóa đơn](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/lich-su-hoa-don.md) (**Billing history**)             | Xem hóa đơn và tình trạng thanh toán của mọi sản phẩm                               |
| [Lịch sử thanh toán](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/lich-su-thanh-toan.md) (**Payment history**)       | Xem số tiền, hình thức và ngày của từng lần thanh toán                              |
| [Lịch sử tín dụng](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/lich-su-tin-dung.md) (**Credit history**)            | Xem biến động số dư ví Credit: nạp Credit, thanh toán, hoàn tiền                    |
| [Thống kê sử dụng](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/thong-ke-su-dung.md) (**Usage report**)              | Xem thời gian sử dụng và các lần thay đổi cấu hình của từng tài nguyên, kèm chi phí |
| [Trình khám phá chi phí](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/trinh-kham-pha-chi-phi.md) (**Cost explorer**) | Phân tích và dự đoán chi phí theo sản phẩm, loại tài nguyên và từng tài nguyên      |
| [Cài đặt thông báo](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/cai-dat-thong-bao.md)                               | Nhận email về hóa đơn, bảo trì hệ thống và cảnh báo dịch vụ                         |

***

## Bắt đầu với Billing & Payment

| Tôi muốn...                                      | Đi đến                                                                                                                                                                 |
| ------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nạp Credit vào ví                                | [Mua Credit](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/cac-tinh-nang-khac/mua-credit.md)                                               |
| Hiểu rõ khác biệt giữa trả trước và trả sau      | [Người dùng trả trước & trả sau](trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/nguoi-dung-tra-truoc-and-tra-sau.md)                                   |
| Dùng coupon khi thanh toán                       | [Áp dụng coupon khi thanh toán](trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/thanh-toan/ap-dung-coupon-khi-thanh-toan.md)                            |
| Thanh toán hóa đơn trả sau                       | [Thanh toán hóa đơn tự động](trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/thanh-toan/thanh-toan-hoa-don-tu-dong.md)                                  |
| Gia hạn tài nguyên                               | [Gia hạn tài nguyên](trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/quan-ly-vong-doi-tai-nguyen/gia-han-tai-nguyen.md)                                 |
| Khôi phục tài nguyên đã hết hạn                  | [Khôi phục tài nguyên](trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/quan-ly-vong-doi-tai-nguyen/khoi-phuc-tai-nguyen.md)                             |
| Phân quyền cho thành viên khác truy cập vConsole | [Phân quyền truy cập thông qua IAM](vconsole-kenh-quan-ly-chung-ve-hoa-don-va-tai-nguyen/trai-nghiem-vconsole/cac-tinh-nang-khac/phan-quyen-truy-cap-thong-qua-iam.md) |
