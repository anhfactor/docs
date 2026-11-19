# Xóa tài nguyên

Sử dụng tài liệu này như là một hướng dẫn xóa tài nguyên. Tài liệu sẽ mô tả chi tiết các bước xử lý liên quan đến việc **quản lý tài nguyên và chi phí phát sinh** khi xóa tài nguyên. Các bước khác sẽ giản lược bớt và chỉ đề cập đến như một phần của quy trình.

#### Tính năng xóa tài nguyên áp dụng đối với: <a href="#xoatainguyen-tinhnangxoatainguyenapdungdoivoi" id="xoatainguyen-tinhnangxoatainguyenapdungdoivoi"></a>

* **Đối tượng:** Người dùng trả trước và trả sau
* **Nguồn tiền:** Ví GreenNode (trong trường hợp có hoàn trả phí sử dụng)
* **Tài nguyên:** Tất cả tài nguyên thuộc các sản phẩm GreenNode

#### **Người dùng trả trước xóa tài nguyên** <a href="#xoatainguyen-nguoidungtratruocxoatainguyen" id="xoatainguyen-nguoidungtratruocxoatainguyen"></a>

***

#### **Quy trình xóa tài nguyên** <a href="#xoatainguyen-quytrinhxoatainguyen" id="xoatainguyen-quytrinhxoatainguyen"></a>

* **Bước 1: Chọn tài nguyên cần xóa**
  * 1.1 Truy cập vào trang sản phẩm **vServer, vStorage, vMonitor**
  * 1.2 Chọn tài nguyên cần xóa tại trang sản phẩm
  * 1.3 Xác nhận xóa tài nguyên.
* **Bước 2: Hệ thống thực hiện xóa tài nguyên**
  * Tài nguyên được chọn sẽ bị xóa vĩnh viễn và không thể khôi phục.
  * Tiến hành hoàn trả chi phí tài nguyên chưa sử dụng đối với các tài nguyên có áp dụng hoàn trả phí.
* **Bước 3: Kiểm tra thông tin**
  * Người dùng kiểm tra thông tin hoàn trả phí tại user portal, trang [Lịch sử tín dụng](https://dashboard.console.greennode.ai/credit-history).

#### **Hướng dẫn tính giá tài nguyên được hoàn trả** <a href="#xoatainguyen-huongdantinhgiatainguyenduochoantra" id="xoatainguyen-huongdantinhgiatainguyenduochoantra"></a>

Dưới đây là hướng dẫn tính giá tiền được hoàn trả khi xóa tài nguyên Server, người dùng có thể áp dụng công thức để tính tương tự cho các tài nguyên khác trong hệ thống GreenNode Service.

Ví dụ: tài nguyên Server được khởi tạo ngày 06-03-2023 với thời hạn sử dụng đến 06-05-2023, và bị xóa ngày 16-04-2023. Để dễ theo dõi, ví dụ quy ước mỗi tháng có 30 ngày.

| Hành động          | Cấu hình      | Thời điểm thực hiện | Đơn giá tại thời điểm khởi tạo (VND / 30 ngày) | Số ngày còn lại đến hết hạn | Giá trị tài nguyên chưa sử dụng (VND) | Giá trị được hoàn trả (VND) |
| ------------------ | ------------- | ------------------- | ---------------------------------------------- | --------------------------- | ------------------------------------- | --------------------------- |
| **Khởi tạo**       | s-general-1x1 | 06-03-2023          | 181,000                                        | 60                          |                                       |                             |
| **Xóa tài nguyên** | s-general-1x1 | 16-04-2023          | 181,000                                        | 20                          | 181,000 / 30 × 20 = 120,667           | 120,667                     |

Từ ví dụ trên, người dùng được hoàn 120,667 VND vào ví Credit khi xóa tài nguyên Server vào ngày 16-04-2023.

#### (\*) Lưu ý <a href="#xoatainguyen-luuy" id="xoatainguyen-luuy"></a>

* Giá trị tài nguyên chưa sử dụng được tính chính xác đến đơn vị phút
* Sẽ có dịch vụ không áp dụng hoàn phí tùy vào điều khoản sử dụng của từng sản phẩm (vServer, vStorage, vMonitor)

#### **Người dùng trả sau xóa tài nguyên** <a href="#xoatainguyen-nguoidungtrasauxoatainguyen" id="xoatainguyen-nguoidungtrasauxoatainguyen"></a>

***

#### **Quy trình xóa tài nguyên** <a href="#xoatainguyen-quytrinhxoatainguyen.1" id="xoatainguyen-quytrinhxoatainguyen.1"></a>

* **Bước 1: Chọn tài nguyên cần xóa**
  * 1.1 Truy cập vào trang sản phẩm **vServer, vStorage, vMonitor**
  * 1.2 Chọn tài nguyên cần xóa tại trang sản phẩm
  * 1.3 Xác nhận xóa tài nguyên.
* **Bước 2: Hệ thống thực hiện xóa tài nguyên**
  * Tài nguyên được chọn sẽ bị xóa vĩnh viễn và không thể khôi phục.
  * Ghi nhận thời điểm người dùng ngừng sử dụng tài nguyên dùng cho việc phát sinh hóa đơn sử dụng tài nguyên thực tế vào mỗi cuối tháng.
