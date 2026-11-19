# Người dùng trả trước & trả sau

Sử dụng tài liệu này để hiểu rõ hơn về các hình thức sử dụng tài nguyên theo loại người dùng. Ở cấp độ GreenNode Service, chúng tôi hỗ trợ 2 loại người dùng chính:

* **Người dùng trả trước:** Là người dùng phải thanh toán chi phí sử dụng tài nguyên trước khi được phép sử dụng. Thanh toán chi phí sử dụng tài nguyên theo cấu hình và thời gian muốn sử dụng (Cần xác định thời điểm ngừng sử dụng tài nguyên).
* **Người dùng trả sau:** Là người dùng được phép sử dụng tài nguyên trước và trả tiền sau, dựa trên chi phí sử dụng tài nguyên thực tế. Số tiền phải chi trả sẽ được chốt định kỳ mỗi cuối tháng cho đến khi người dùng không sử dụng tài nguyên nữa.

Cùng điểm qua một số khác biệt về khái niệm cũng như quyền hạn và chức năng giữa 2 loại người dùng này đối với các dịch vụ GreenNode như:

* **Quy trình thao tác trên tài nguyên:** Khởi tạo, thay đổi cấu hình, gia hạn, khôi phục, xóa tài nguyên
* **Quy trình cung cấp tài nguyên**
* **Quản lý tài nguyên**
* **Quản lý hóa đơn**
* **Quản lý thanh toán**

#### **So sánh người dùng trả trước và trả sau** <a href="#nguoidungtratruoc-and-trasau-sosanhnguoidungtratruocvatrasau" id="nguoidungtratruoc-and-trasau-sosanhnguoidungtratruocvatrasau"></a>

***

#### 1. Quy trình thao tác trên tài nguyên <a href="#nguoidungtratruoc-and-trasau-1.quytrinhactiontrentainguyen" id="nguoidungtratruoc-and-trasau-1.quytrinhactiontrentainguyen"></a>

* **Người dùng trả trước**

<figure><img src="https://docs.vngcloud.vn/download/attachments/49649325/Daily_Job_HC%20(3)-Page-5.drawio.png?version=1&#x26;modificationDate=1678094370000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

* **Người dùng trả sau**

<figure><img src="https://docs.vngcloud.vn/download/attachments/49649325/Daily_Job_HC%20(3)-Page-6.drawio.png?version=1&#x26;modificationDate=1678094411000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

#### 2. Quy trình cung cấp tài nguyên <a href="#nguoidungtratruoc-and-trasau-2.quytrinhcungcaptainguyen" id="nguoidungtratruoc-and-trasau-2.quytrinhcungcaptainguyen"></a>

* **Người dùng trả trước**
  * Sau khi xác nhận thanh toán thành công, phía Product sẽ tiến hành cung cấp tài nguyên theo cấu hình mà người dùng yêu cầu
  * Trong quá trình cung cấp tài nguyên, nếu có xảy ra lỗi quá trình, hệ thống sẽ tiến hành hoàn trả tiền dịch vụ đã thanh toán của người dùng ở bước trước đó. Tiền được hoàn trả sẽ quy về Credit và chuyển vào ví GreenNode
* **Người dùng trả sau**
  * Ngay tại bước "Xác nhận", Product sẽ tiến hành cung cấp tài nguyên theo cấu hình người dùng yêu cầu, và hệ thống sẽ ghi nhận lại thời gian bắt đầu sử dụng tài nguyên.

_→ Ghi chú: Vì là người dùng trả sau nên không cần thực hiện bước thanh toán tại quy trình thao tác trên tài nguyên._

#### 3. Quản lý tài nguyên <a href="#nguoidungtratruoc-and-trasau-3.quanlytainguyen" id="nguoidungtratruoc-and-trasau-3.quanlytainguyen"></a>

Về cơ bản, các tính năng mà người dùng có thể thực hiện trên tài nguyên như:

* **Đối với người dùng trả trước**:
  * Khởi tạo mới
  * Thay đổi cấu hình
  * Gia hạn
  * Khôi phục tài nguyên
  * Tự động gia hạn
  * Xóa tài nguyên
* **Đối với người dùng trả sau:**
  * Khởi tạo mới
  * Thay đổi cấu hình
  * Xóa tài nguyên

Tham khảo chi tiết hơn tại mục: [**Quản lý tài nguyên**](https://dashboard.console.greennode.ai/resource)

#### 4. Quản lý hóa đơn <a href="#nguoidungtratruoc-and-trasau-4.quanlyhoadon" id="nguoidungtratruoc-and-trasau-4.quanlyhoadon"></a>

* **Người dùng trả trước**
  * Tại bước thanh toán thành công, sau khi cung cấp tài nguyên thành công, hệ thống sẽ phát sinh **hóa đơn được tính là đã thanh toán** tương ứng với tài nguyên của người dùng.
* **Người dùng trả sau**
  * Hóa đơn theo tài nguyên được phát sinh mỗi cuối tháng, dựa trên mức sử dụng thực tế trong tháng đó, với trạng thái **chưa thanh toán**.
  * Hóa đơn được thanh toán tự động bằng số dư Credit trong ví GreenNode. Người dùng chỉ cần nạp Credit vào ví, hệ thống sẽ tự động thanh toán các hóa đơn chưa thanh toán mỗi ngày.
  * Tìm hiểu thêm tại Mua Credit và Thanh toán hóa đơn tự động.

#### 5. Quản lý thanh toán <a href="#nguoidungtratruoc-and-trasau-5.quanlythanhtoan" id="nguoidungtratruoc-and-trasau-5.quanlythanhtoan"></a>

* **Người dùng trả trước**
  * Lịch sử thanh toán sẽ xuất hiện ngay tại User Portal, mục [Payment history](https://dashboard.console.greennode.ai/payment-history) ngay sau khi người dùng thực hiện thanh toán tài nguyên
* **Người dùng trả sau**
  * Lịch sử thanh toán được ghi nhận mỗi khi hệ thống tự động thanh toán hóa đơn bằng số dư Credit, và hiển thị tại User Portal, mục [Payment history](https://dashboard.console.greennode.ai/payment-history).



#### **Làm sao để thay đổi từ trả trước sang trả sau và ngược lại?** <a href="#nguoidungtratruoc-and-trasau-lamsaodethaydoitutratruocsangtrasauvanguoclai" id="nguoidungtratruoc-and-trasau-lamsaodethaydoitutratruocsangtrasauvanguoclai"></a>

***

* Khi người dùng đăng ký mới tài khoản tại GreenNode, hệ thống sẽ mặc định đây là **người dùng trả trước.**
* Để **chuyển sang loại người dùng trả sau**, người dùng chủ động liên hệ bộ phận Sale / Support để được hỗ trợ theo yêu cầu.
* Trường hợp người dùng là loại trả sau và muốn **quay về loại trả trước**, cũng chủ động liên hệ bộ phận Sale / Support để được hỗ trợ theo yêu cầu.
