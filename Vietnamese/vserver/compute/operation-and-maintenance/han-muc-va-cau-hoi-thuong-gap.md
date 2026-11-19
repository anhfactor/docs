# Hạn mức và câu hỏi thường gặp

## Hạn mức sử dụng (Quota)

* Mỗi tài khoản có hạn mức số lượng Scheduled Task được phép tạo. Hạn mức mặc định hiện tại: **20 task / tài khoản**.
* Tạo mới hoặc nhân bản task sẽ trừ hạn mức; xoá task sẽ hoàn trả hạn mức.
* Bạn có thể tra cứu hạn mức hiện tại ngay trên giao diện O&M.

{% hint style="info" %}
**Chú ý:** Nếu nhận thông báo vượt hạn mức khi tạo task, hãy xoá các task không còn dùng hoặc liên hệ đội ngũ hỗ trợ VNG Cloud để nâng hạn mức.
{% endhint %}

## Câu hỏi thường gặp và xử lý sự cố

### Task không chạy vào giờ đã hẹn?

Kiểm tra lần lượt: (1) task còn ở trạng thái **ACTIVE** không (task đã CANCELED hoặc EXPIRED sẽ không chạy); (2) thời điểm hiện tại có nằm trong khoảng hiệu lực (effective from/until) không; (3) trạng thái kích hoạt dịch vụ có đang **ACTIVE** không. Nếu tất cả đều đúng mà task vẫn không chạy, liên hệ hỗ trợ kèm tên task và khung giờ.

### Trạng thái kích hoạt hiển thị SA\_BROKEN nghĩa là gì?

Service Account của bạn gặp sự cố (thường do bị xoá hoặc thay đổi quyền ngoài ý muốn). Chỉ cần nhấn **Re-activate** — hệ thống sẽ tự khôi phục. Các task hiện có không bị mất; lịch chạy tiếp tục sau khi kích hoạt lại thành công.

### Tôi đã xoá một VM trên vServer, task có bị lỗi không?

Không. Trước mỗi lần thực thi, hệ thống tự đối soát với vServer và loại VM đã xoá khỏi danh sách đối tượng. Task tiếp tục chạy bình thường trên các VM còn lại.

### Execution báo PARTIAL\_FAILED, tôi cần làm gì?

Mở chi tiết execution để xem từng VM: VM nào thất bại sẽ có thông báo lỗi cụ thể. Xử lý theo nguyên nhân (ví dụ VM đang ở trạng thái không cho phép thao tác) rồi có thể bấm **Chạy ngay** để thực hiện lại nếu cần.

### Chạy thủ công có làm lệch lịch tự động không?

Không. Lần chạy thủ công (**MANUAL**) độc lập với lịch; lần chạy tự động kế tiếp vẫn diễn ra đúng giờ đã hẹn.

### Tôi muốn tạm dừng task một thời gian?

Dùng **Huỷ (Cancel)** để dừng lịch — lịch sử vẫn được giữ. Khi cần chạy lại, tạo task mới hoặc dùng **Nhân bản (Duplicate)** từ task đã huỷ để khôi phục cấu hình nhanh.

### Một task áp dụng được cho VM ở nhiều region không?

Chưa. Trong bản Beta, mỗi task thuộc về một region. Nếu có VM ở cả **HCM-03** và **HAN-01**, hãy tạo task riêng cho từng region.

## Góp ý & hỗ trợ

Trong quá trình trải nghiệm bản Beta, nếu bạn gặp sự cố hoặc có đề xuất tính năng, vui lòng liên hệ đội ngũ hỗ trợ VNG Cloud qua kênh hỗ trợ hiện tại của bạn. Mọi phản hồi của bạn đều là đầu vào quan trọng giúp chúng tôi hoàn thiện sản phẩm trước khi phát hành chính thức.
