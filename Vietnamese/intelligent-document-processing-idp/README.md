---
description: >-
  GreenNode IDP là nền tảng xử lý tài liệu thông minh: tự động tiếp nhận, phân
  loại, trích xuất, chuẩn hoá, kiểm tra nghiệp vụ và đẩy dữ liệu sang hệ thống
  của khách hàng.
---

# Intelligent Document Processing (IDP)

**Tổng quan**

GreenNode IDP là nền tảng xử lý tài liệu thông minh, chuyển thông tin nằm trong ảnh chụp, bản scan và tệp PDF thành dữ liệu có cấu trúc — đã được chuẩn hoá, đối chiếu theo quy tắc nghiệp vụ và sẵn sàng đưa thẳng vào hệ thống của tổ chức.

Phần lớn thông tin mà một tổ chức phải xử lý hằng ngày không nằm trong cơ sở dữ liệu mà nằm trong giấy tờ: hợp đồng, hoá đơn, chứng từ giao dịch, hồ sơ bồi thường. Để đưa được thông tin đó vào hệ thống, người ta vẫn phải đọc và nhập lại thủ công — tốn nhân lực, kéo dài thời gian xử lý, và tỷ lệ sai sót tăng theo khối lượng.

GreenNode IDP khác với công cụ nhận dạng ký tự thông thường ở chỗ không dừng lại ở việc đọc ra chữ. Nền tảng xác định loại tài liệu, hiểu ngữ cảnh để lấy đúng trường thông tin cần thiết, chuẩn hoá về định dạng mà hệ thống đích yêu cầu, đối chiếu với quy tắc nghiệp vụ do tổ chức tự định nghĩa, chấm điểm rủi ro cho từng bộ hồ sơ, và chỉ chuyển sang người kiểm tra những hồ sơ thực sự cần can thiệp.

**Bốn nhóm năng lực**

* **Xác thực tài liệu**. Phân loại tài liệu và kiểm tra tính đầy đủ của bộ hồ sơ, xác thực chữ ký và con dấu, so khớp với mẫu gốc, phát hiện tài liệu đã bị chỉnh sửa hoặc giả mạo.
* **Số hoá tài liệu**. Chuyển ảnh và PDF scan thành văn bản giữ nguyên ngữ nghĩa và thứ tự đọc, hoặc xuất ra tệp Word tái tạo được bảng biểu và bố cục của bản gốc.
* **Bóc tách thông tin**. Trích xuất trường thông tin, bảng biểu, ô đánh dấu và logo bằng mô hình tổng quát áp dụng cho mọi định dạng, hoặc bằng mô hình chuyên biệt đã tinh chỉnh riêng cho từng loại giấy tờ.
* **Giải pháp nghiệp vụ.** Chuẩn hoá và xác thực dữ liệu sau khi bóc tách, phân tích logic nghiệp vụ theo từng lĩnh vực như đọc báo cáo tài chính hoặc xử lý hồ sơ bồi thường bảo hiểm.

Như vậy, với giải pháp IDP của GreenNode, người dùng có thể xử lý một bộ hồ sơ nhiều trang chỉ trong vài phút thay vì hàng giờ nhập liệu thủ công, hạn chế sai sót nhờ dữ liệu được chuẩn hoá và kiểm tra bằng quy tắc nghiệp vụ trước khi vào hệ thống, nắm được rủi ro của từng hồ sơ qua điểm rủi ro chỉ rõ quy tắc không đạt, để hồ sơ đủ điều kiện tự duyệt và nhân sự chỉ xem xét số ít trường hợp cần thiết, đồng thời kiểm soát chi phí theo số trang thực dùng với lịch sử sử dụng và cảnh báo ngân sách.

**Lợi ích khi sử dụng**

* **Độ chính xác cao trên tài liệu tiếng Việt.** Mô hình được huấn luyện trên dữ liệu tiếng Việt, đạt 99% độ chính xác ở cấp trường thông tin với biểu mẫu chữ in và 94% với biểu mẫu viết tay. Điểm mạnh rõ nhất nằm ở hai nhóm trường mà mô hình quốc tế thường xử lý kém: chữ tiếng Việt có dấu và địa chỉ hành chính. Nền tảng còn tra cứu và chuẩn hoá địa chỉ về đúng tỉnh và phường theo danh mục hành chính Việt Nam, nên dữ liệu đầu ra dùng được ngay mà không cần đối chiếu lại.
* **Sẵn sàng vận hành ngay, không cần huấn luyện mô hình.** Hệ thống cung cấp sẵn 46 loại tài liệu đọc được ngay: giấy tờ định danh (căn cước, chứng minh nhân dân, hộ chiếu, giấy khai sinh, bằng lái xe), giấy tờ phương tiện, hồ sơ doanh nghiệp và ngân hàng (giấy phép kinh doanh, đăng ký thuế, hợp đồng, báo cáo tài chính, hoá đơn VAT, hoá đơn quốc tế, phiếu thu), giấy tờ bất động sản và nhóm bảo hiểm sức khoẻ.&#x20;
* **Tự tạo loại tài liệu mới trong vài phút, không cần huấn luyện lại.**&#x54;ừ mô hình phải train theo từng mẫu tài liệu sang mô hình generic​, người dùng có thể  tự khai báo biểu mẫu mới trên phần mềm, không cần train lại​. Qua đó, việc Onboarding mẫu mới tính theo phút.
* **Cấu hình toàn bộ bằng giao diện, không cần cài đặt hay lập trình lại.** Quá trình xử lý được thiết kế qua 8 bước trên giao diện, từ tiếp nhận tài liệu đến trả kết quả. Khi quy tắc nghiệp vụ thay đổi, người dùng chỉnh sửa cấu hình và kích hoạt phiên bản mới — không phải sửa mã nguồn hay phát triển lại hệ thống.
* **Hệ thống chấm điểm rủi ro cho từng bộ hồ sơ.** Người dùng có thể cài đặt tự động duyệt hồ sơ đạt ngưỡng và chỉ chuyển sang người kiểm tra những hồ sơ vượt ngưỡng.&#x20;
