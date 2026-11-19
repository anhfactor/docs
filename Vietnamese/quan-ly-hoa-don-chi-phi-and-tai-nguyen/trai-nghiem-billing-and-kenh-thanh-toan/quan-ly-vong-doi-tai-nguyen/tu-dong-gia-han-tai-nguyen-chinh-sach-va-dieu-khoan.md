# Tự động gia hạn tài nguyên - Chính sách và điều khoản

Sử dụng tài liệu này để hiểu thêm về tính năng tự động gia hạn tài nguyên. Tài liệu sẽ mô tả chi tiết các bước xử lý liên quan đến việc **tự động gia hạn tài nguyên và chi phí phát sinh** khi tự động gia hạn tài nguyên. Các bước khác sẽ giản lược bớt và chỉ đề cập đến như một phần của quy trình.

#### 1. Chính sách tự động gia hạn tài nguyên chỉ áp dụng đối với: <a href="#tudonggiahantainguyen-chinhsachvadieukhoan-1.chinhsachtudonggiahantainguyenchiapdungdoivoi" id="tudonggiahantainguyen-chinhsachvadieukhoan-1.chinhsachtudonggiahantainguyenchiapdungdoivoi"></a>

* **Đối tượng:** Người dùng trả trước
* **Tài nguyên**: Tất cả các tài nguyên cho phép tự động gia hạn và đang trong thời gian sử dụng.
* **Nguồn tiền**: GreenNode Credit

#### **2. Hướng dẫn bật/tắt tính năng "Tự động gia hạn"** <a href="#tudonggiahantainguyen-chinhsachvadieukhoan-2.huongdanbat-tattinhnang-tudonggiahan" id="tudonggiahantainguyen-chinhsachvadieukhoan-2.huongdanbat-tattinhnang-tudonggiahan"></a>

**2.1 Đối với các sản phẩm dịch vụ vStorage:** [**https://docs.greennode.ai/vn/vstorage/object-storage/cach-tinh-phi**](https://docs.greennode.ai/vn/vstorage/object-storage/cach-tinh-phi)

**2.2 Đối với các sản phẩm, dịch vụ vServer**

*   **Bật "Tự động gia hạn" khi khởi tạo**

    * Bước 1: Cấu hình thông tin dịch vụ tại trang sản phẩm → Nhấn "**Khởi tạo**" để chuyển đến trang thanh toán
    * Bước 2: Tại trang thanh toán, tick vào "**Auto-renew**" để bật tính năng tự động gia hạn

    <figure><img src="../../../.gitbook/assets/image (919).png" alt=""><figcaption></figcaption></figure>

    <figure><img src="https://docs.vngcloud.vn/download/attachments/49649295/image2023-12-12_10-49-53.png?version=1&#x26;modificationDate=1702352993000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
* **Bật/Tắt trong quá trình sử dụng dịch vụ**<br>
  * Bước 1: Điều hướng đến trang Resource Billing trong dịch vụ vServer: [https://dashboard.console.greennode.ai/resource](https://dashboard.console.greennode.ai/resource)
  * Bước 2: Nhấn vào biểu tượng ba chấm tại vị trí tài nguyên cần thực hiện thay đổi. Xem hình bên dưới
    * Chọn **"Tự động gia hạn"** để bật tính năng tự động gia hạn nếu chưa bật khi khởi tạo
    * Chọn **"Cập nhật tự động gia hạn"** để điều chỉnh thời gian sử dụng tài nguyên được áp dụng khi hệ thống thực hiện tự động gia hạn
    * Chọn **"Tắt tự động gia hạn"** để tắt tính năng tự động gia hạn nếu không có nhu cầu

<figure><img src="../../../.gitbook/assets/image (920).png" alt=""><figcaption></figcaption></figure>

**2.3 Đối với sản phẩm, dịch vụ vMonitor**

* **Bật "Tự động gia hạn" khi khởi tạo**
  * Bước 1: Cấu hình thông tin dịch vụ tại trang sản phẩm → Nhấn "Khởi tạo" để chuyển đến trang thanh toán
  * Bước 2: Tại trang thanh toán, tick vào "Auto-renew" để bật tính năng tự động gia hạn

<figure><img src="../../../.gitbook/assets/image (921).png" alt=""><figcaption></figcaption></figure>

_Lưu ý: Hiện tại các dịch vụ trong sản phẩm vMonitor chưa hỗ trợ tắt tự động gia hạn khi người dùng bật lúc khởi tạo. Để tắt tự động gia hạn khi không có nhu cầu, vui lòng liên hệ đội ngũ 247 để hỗ trợ thêm._

#### **3. Quy trình tự động gia hạn tài nguyên** <a href="#tudonggiahantainguyen-chinhsachvadieukhoan-3.quytrinhtudonggiahantainguyen" id="tudonggiahantainguyen-chinhsachvadieukhoan-3.quytrinhtudonggiahantainguyen"></a>

Tự động gia hạn tài nguyên là **tính năng của hệ thống**, giúp quá trình sử dụng tài nguyên của người dùng không bị gián đoạn tại thời điểm kết thúc tài nguyên (người dùng có nhu cầu tiếp tục sử dụng nhưng quên không thực hiện gia hạn trên hệ thống vì lý do nào đó).

**Điều khoản áp dụng dành cho tính năng "Tự động gia hạn" trên GreenNode như sau:**

* Từ **7 ngày trước ngày hết hạn**, hệ thống gửi email nhắc gia hạn để người dùng chuẩn bị đủ số dư Credit khả dụng. Nên nạp đủ Credit trước 8:30 sáng của ngày gia hạn.
* Tài nguyên được mặc định **gia hạn thêm 1 tháng**, kể từ thời điểm kết thúc.
* Vào mỗi mốc **7 ngày, 4 ngày, 1 ngày trước ngày hết hạn và ngay ngày hết hạn**, hệ thống bắt đầu chạy tự động gia hạn từ **8:30 sáng**. Các tài nguyên được xử lý lần lượt, nên thời điểm gia hạn hoàn tất có thể khác nhau giữa các tài nguyên. Nếu một lần gia hạn không thành công do thiếu Credit, hệ thống thử lại ở mốc tiếp theo.
  * Cách tính giá khi hệ thống tự động gia hạn không khác biệt so với việc người dùng chủ động gia hạn tài nguyên, tham khảo thêm tại Gia hạn tài nguyên.
  * Hệ thống gửi thông tin tài nguyên được gia hạn thành công / thất bại đến người dùng.
  * Hệ thống phát sinh hóa đơn tương ứng với khoảng thời gian được gia hạn thêm.
* **Lưu ý:** Tính năng tự động gia hạn chỉ áp dụng cho tài nguyên thuộc sản phẩm có hỗ trợ tự động gia hạn, đã được Khách hàng bật tự động gia hạn và đang ở trạng thái hoạt động (Active). Tài nguyên đã hết hạn hoặc bị xóa trước các mốc trên sẽ không được tự động gia hạn.
* **Lưu ý về thời điểm hết hạn:** Tại mỗi lần chạy tự động gia hạn, nếu thời điểm hết hạn của tài nguyên đã qua trước thời điểm hệ thống thực hiện gia hạn, tài nguyên sẽ không còn thỏa điều kiện tự động gia hạn. Ví dụ: tài nguyên hết hạn lúc 7:00 sáng ngày T, trong khi lần chạy của ngày T bắt đầu từ 8:30 sáng. Khi đó, bạn cần chủ động gia hạn tài nguyên trên giao diện.
* Nếu cả 4 lần gia hạn đều thất bại, tính năng tự động gia hạn dừng lại và tài nguyên sẽ hết hạn. Để tiếp tục sử dụng, người dùng cần chủ động gia hạn tài nguyên trước khi tài nguyên bị xóa vĩnh viễn. Tham khảo Gia hạn tài nguyên đã hết hạn.
