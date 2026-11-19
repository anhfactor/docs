# Quản lý vòng đời tài nguyên

Sử dụng tài liệu này để hiểu hơn về tài nguyên mà bạn đang sử dụng.

Tại đây, chúng tôi cung cấp thông tin về **vòng đời tài nguyên** và **các hành động của người dùng** / **hệ thống** có thể ảnh hưởng đến **trạng thái tài nguyên** mà người dùng đang sử dụng.

Thông qua **mô hình vòng đời tài nguyên** dưới đây, bạn sẽ có cái nhìn tổng quan về sự **chuyển đổi trạng thái tài nguyên**, cũng như sự **liên kết giữa tài nguyên với hóa đơn**.

#### Mô hình vòng đời tài nguyên của người dùng trả trước

* **New → Active:** Khi người dùng khởi tạo tài nguyên thành công, tài nguyên có trạng thái Active và **phát sinh hóa đơn tương ứng**.
* **Active ⇄ Stopped:** Người dùng thực hiện Start, Reboot / Stop tài nguyên để chuyển qua lại giữa 2 trạng thái này.
* **Active / Stopped → Suspended:** Tài nguyên hết hạn mà không được gia hạn sẽ bị tạm ngưng. Dữ liệu của tài nguyên vẫn được giữ lại.
* **Suspended → Active:** Người dùng gia hạn tài nguyên trong thời gian tạm ngưng để tiếp tục sử dụng.
* **Active / Stopped → Deleted:** Người dùng thực hiện xóa tài nguyên.
* **Suspended → Deleted:** Hết thời gian tạm ngưng mà tài nguyên vẫn chưa được gia hạn, tài nguyên bị xóa vĩnh viễn và không thể khôi phục.
* **Phát sinh hóa đơn:** Hóa đơn được phát sinh mỗi khi người dùng khởi tạo, thay đổi cấu hình, gia hạn tài nguyên, hoặc khi hệ thống tự động gia hạn tài nguyên.

Mốc thời gian chi tiết sau khi tài nguyên hết hạn, xem tại Gia hạn tài nguyên đã hết hạn.

#### Mô hình vòng đời tài nguyên của người dùng trả sau

* **New → Active:** Khi người dùng khởi tạo tài nguyên thành công, tài nguyên có trạng thái Active.
* **Active ⇄ Stopped:** Người dùng thực hiện Start, Reboot / Stop tài nguyên để chuyển qua lại giữa 2 trạng thái này.
* **Active → Deleted:** Người dùng thực hiện xóa tài nguyên.
* **Phát sinh hóa đơn:**
  * Hóa đơn được phát sinh vào cuối tháng, ghi nhận thông tin sử dụng của tài nguyên trong tháng.
  * Khi người dùng xóa tài nguyên, hệ thống ghi nhận thời điểm ngừng sử dụng, và chi phí đến thời điểm đó được tính vào hóa đơn cuối tháng.
