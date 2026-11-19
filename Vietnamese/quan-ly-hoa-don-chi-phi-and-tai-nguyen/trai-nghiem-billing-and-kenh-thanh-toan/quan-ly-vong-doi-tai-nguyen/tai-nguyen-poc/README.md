# Tài nguyên POC

Tài nguyên POC sinh ra nhằm mục đích hỗ trợ người dùng có thể trải nghiệm dịch vụ tại GreenNode một cách tốt nhất.

Điều kiện sử dụng tài nguyên POC:

* **Đối tượng**: Người dùng trả trước được cấp ví POC
* **Nguồn tiền:** [**Ví POC**](../../thanh-toan/thanh-toan-tai-nguyen-poc.md)
* **Tài nguyên:** Tất cả các tài nguyên được áp dụng POC
* **Thời gian sử dụng:** Tùy thuộc vào thời hạn ví POC được cấp.

## Khởi tạo tài nguyên POC <a href="#tainguyenpoc-khoitaotainguyenpoc" id="tainguyenpoc-khoitaotainguyenpoc"></a>

***

* **Bước 1: Cấu hình tài nguyên**
  * 1.1 Truy cập vào trang sản phẩm **vServer, vStorage, vMonitor**
  * 1.2 Chọn tài nguyên và cấu hình cần sử dụng tại trang sản phẩm
  * 1.3 Nhấn chọn sử dụng tài nguyên POC
  * 1.3 Xác nhận sử dụng tài nguyên để chuyển đến bước thanh toán: Tại đây, hệ thống sẽ điều hướng người dùng đến trang thanh toán tài nguyên
* **Bước 2: Thanh toán tài nguyên bằng ví POC**
  * Xem hướng dẫn chi tiết [**tại đây**](../../thanh-toan/thanh-toan-tai-nguyen-poc.md)
* **Bước 3: Hệ thống thực hiện**
  * Cung cấp tài nguyên
  * Email thông báo thông tin tài nguyên vừa khởi tạo

**Một số lưu ý khi khởi tạo tài nguyên POC**

* Thời gian sử dụng tài nguyên POC mặc định trùng với thời gian kết thúc ví POC
* Chỉ được dùng ví POC để thanh toán tài nguyên POC
* Đối với tài nguyên POC, hệ thống sẽ không phát sinh hóa đơn tài nguyên tương ứng
* Cách tính giá sử dụng tài nguyên POC tương tự như tài nguyên thường. Tham khảo chi tiết [tại đây](../khoi-tao-tai-nguyen.md)

## Thay đổi cấu hình tài nguyên POC <a href="#tainguyenpoc-thaydoicauhinhtainguyenpoc" id="tainguyenpoc-thaydoicauhinhtainguyenpoc"></a>

***

Quy trình và phương thức tính giá tương tự như khi thay đổi cấu hình khi sử dụng tài nguyên thường. Tham khảo chi tiết [tại đây](../thay-doi-cau-hinh-tai-nguyen.md)

#### Gia hạn tài nguyên POC <a href="#tainguyenpoc-giahantainguyenpoc" id="tainguyenpoc-giahantainguyenpoc"></a>

***

Trong trường hợp thời hạn sử dụng ví POC của người dùng được gia hạn thêm sau khi đã khởi tạo tài nguyên POC, người dùng có thể tiến hành gia hạn tài nguyên POC tương ứng với thời gian kết thúc mới của ví POC.

Quy trình và phương thức tính giá tương tự như khi gia hạn tài nguyên thường. Tham khảo chi tiết [tại đây](../gia-han-tai-nguyen.md)

## Dừng POC đối với tài nguyên POC <a href="#tainguyenpoc-dungpocdoivoitainguyenpoc" id="tainguyenpoc-dungpocdoivoitainguyenpoc"></a>

***

Người dùng có thể dừng POC đối với tài nguyên POC bất kỳ lúc nào trong thời hạn hiệu lực của ví POC. **Dừng POC đồng nghĩa với việc chuyển đổi tài nguyên từ POC sang dịch vụ trả phí**: tài nguyên được giữ nguyên cấu hình và tiếp tục sử dụng như một tài nguyên thường.

Khi người dùng dừng POC, hệ thống sẽ:

* Hoàn phí sử dụng tài nguyên POC còn lại (nếu có) vào ví POC.
* Chuyển người dùng đến trang thanh toán. Người dùng phải thanh toán phí sử dụng tài nguyên thông qua các hình thức khác ngoài ví POC, như GreenNode Credit hoặc cổng thanh toán.

Sau khi thanh toán thành công, tài nguyên được tính là tài nguyên thường.

## Hết thời gian sử dụng ví POC <a href="#tainguyenpoc-hetthoigiansudungvipoc" id="tainguyenpoc-hetthoigiansudungvipoc"></a>

***

Tại thời điểm hết hạn sử dụng ví POC, hệ thống sẽ:

* Kết thúc POC đối với tất cả tài nguyên POC đang sử dụng. Tài nguyên **không** được tự động chuyển sang dịch vụ trả phí:
  * Đối với các tài nguyên áp dụng **tạm giữ credit**, hệ thống sẽ dừng cung cấp dịch vụ và xóa luôn tài nguyên POC đó. Do đó, nếu muốn tiếp tục sử dụng, quý khách hàng cần chủ động dừng POC (chuyển sang dịch vụ trả phí) trước khi ví POC hết hạn. Xem danh sách dịch vụ áp dụng tạm giữ credit.
  * Đối với các tài nguyên áp dụng hình thức trả trước từ ví POC, tài nguyên sẽ bị tạm ngưng trong vòng 7 ngày trước khi xóa vĩnh viễn. Trong thời gian này, quý khách có thể gia hạn tài nguyên nếu có nhu cầu sử dụng tiếp.
* Tắt ví POC: Người dùng sẽ không được phép sử dụng tài nguyên dưới hình thức POC cho đến khi ví POC được bật trở lại.
