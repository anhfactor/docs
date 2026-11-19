---
description: >-
  Cam kết chất lượng dịch vụ (SLA) của GreenNode AI MaaS, phiên bản 2026.1: tỷ
  lệ uptime cam kết, phạm vi áp dụng, mức bù dịch vụ, bảo trì, thời gian phản
  hồi và quy trình khiếu nại.
---

# Cam kết SLA

{% hint style="info" %}
Trang này tóm tắt **Cam Kết Chất Lượng Dịch Vụ AI MaaS (Model as a Service), phiên bản 2026.1, hiệu lực từ ngày 9/11/2026**. Văn bản có giá trị pháp lý là bản tại [Điều khoản dịch vụ GreenNode — SLA](https://greennode.ai/vi/terms-of-service/vietnam/service-level-agreement). Nếu có khác biệt, văn bản đó được ưu tiên áp dụng.
{% endhint %}

## Cam kết tỷ lệ uptime hàng tháng

| Dịch Vụ | Tỷ Lệ Uptime Hàng Tháng Cam Kết | Đơn Vị Tính | Tương Đương Thời Gian Downtime |
| --- | --- | --- | --- |
| AI MaaS | **99,90%** | Model | Tương đương 43 phút 28 giây |

**Phạm vi cam kết:** cam kết áp dụng đối với tính sẵn sàng của Dịch Vụ đối với các **Mô Hình GreenNode**. GreenNode không cam kết SLA đối với:

* Mô Hình Bên Thứ Ba;
* Các chỉ số hiệu năng của Dịch Vụ, bao gồm nhưng không giới hạn ở số token mỗi phút (TPM), số request mỗi phút (RPM), tốc độ phản hồi (response speed) và các chỉ số tương tự.

## Khái niệm và định nghĩa

| Thuật ngữ | Định nghĩa |
| --- | --- |
| **Mô Hình GreenNode** | Các mô hình AI do GreenNode trực tiếp triển khai và vận hành trên hạ tầng của GreenNode. |
| **Mô Hình Bên Thứ Ba** (third-party model) | Các mô hình AI do nhà cung cấp bên thứ ba vận hành và được GreenNode cung cấp cho Khách hàng thông qua Dịch Vụ. Danh sách mô hình và phân loại được công bố, cập nhật trên Console của Dịch Vụ. |
| **Trạng Thái Không Sẵn Sàng** (Downtime) | Khoảng thời gian Dịch Vụ không khả dụng do lỗi của GreenNode, không bao gồm thời gian bảo trì, các trường hợp không được xem là ngưng trệ và các trường hợp khác được loại trừ theo SLA. |
| **Thời Gian Uptime Hàng Tháng** | Tổng số phút trong tháng trừ đi tổng số phút Dịch Vụ ở Trạng Thái Không Sẵn Sàng do lỗi của GreenNode, không bao gồm thời gian bảo trì, thời gian ngưng Dịch Vụ do Sự Kiện Bất Khả Kháng và các trường hợp khác được loại trừ. |
| **Tỷ Lệ Downtime Hàng Tháng** | Tổng thời gian Dịch Vụ ở Trạng Thái Không Sẵn Sàng trong tháng chia cho tổng thời gian trong tháng, nhân với 100. |
| **Tỷ Lệ Uptime Hàng Tháng** | 100% trừ đi Tỷ Lệ Downtime Hàng Tháng. |
| **Sự Kiện Bất Khả Kháng** | Sự kiện xảy ra khách quan, không thể lường trước và không thể khắc phục dù đã áp dụng mọi biện pháp cần thiết, bao gồm nhưng không giới hạn ở thiên tai, địch họa, thời tiết cực đoan, hành động phá hoại, biểu tình, đình công, lệnh cấm của Cơ quan Nhà nước. |
| **Credit** | Giá trị được ghi nhận trên tài khoản Dịch Vụ của Khách hàng, dùng để thanh toán cho việc sử dụng Dịch Vụ theo chính sách tính phí của GreenNode. |

### Khi nào tính là Trạng Thái Không Sẵn Sàng

Trạng Thái Không Sẵn Sàng được xác định khi xảy ra một hoặc nhiều trường hợp sau:

* a. Hệ thống Dịch Vụ dừng phản hồi các API request của Khách hàng;
* b. Máy chủ (server) vận hành Dịch Vụ ngừng hoạt động.

Thời gian ở Trạng Thái Không Sẵn Sàng được tính từ thời điểm sớm hơn giữa (i) thời điểm hệ thống giám sát của GreenNode ghi nhận sự cố và (ii) thời điểm Khách hàng thông báo sự cố cho GreenNode, với điều kiện GreenNode xác nhận sự cố thuộc phạm vi Dịch Vụ, cho đến thời điểm Dịch Vụ hoạt động trở lại.

## Công thức

| Dịch Vụ | Công Thức |
| --- | --- |
| AI MaaS | Uptime = 100% − Tỷ Lệ Downtime Hàng Tháng |

## Bù dịch vụ khi không đạt cam kết

Khi Dịch Vụ không đạt Tỷ Lệ Uptime Hàng Tháng cam kết, GreenNode cung cấp bù Dịch Vụ dưới hình thức **Credit cộng vào tài khoản Dịch Vụ** của Khách hàng:

| Tỷ Lệ Uptime Hàng Tháng | Tỷ lệ Dịch Vụ được bù |
| --- | --- |
| Từ 95% đến dưới 99,90% | 10% |
| Từ 90% đến dưới 95% | 30% |
| Dưới 90% | 100% |

Giá trị bù được tính như sau:

* **Gói token (token plan):** khi bất kỳ Mô Hình GreenNode nào thuộc gói không đạt cam kết, Tỷ Lệ Uptime Hàng Tháng được xác định cho toàn bộ gói và giá trị bù được tính trên giá trị của gói trong chu kỳ thanh toán của tháng đó.
* **Trả theo mức sử dụng (pay-as-you-go):** Tỷ Lệ Uptime Hàng Tháng được xác định riêng cho từng Mô Hình GreenNode bị sự cố và giá trị bù được tính trên tổng Credit Khách hàng đã sử dụng cho mô hình đó trong tháng xảy ra sự cố.

## Các trường hợp không được xem là ngưng trệ

* Dịch Vụ gián đoạn do GreenNode bảo trì hệ thống theo mục **Bảo trì hệ thống** bên dưới.
* Dịch Vụ không truy cập được do Sự Kiện Bất Khả Kháng.
* Dịch Vụ không khả dụng do gián đoạn, suy giảm hiệu năng, thay đổi hoặc ngừng cung cấp từ phía nhà cung cấp Mô Hình Bên Thứ Ba, nằm ngoài tầm kiểm soát của GreenNode.
* Dịch Vụ không khả dụng do nguyên nhân không xuất phát từ lỗi của GreenNode; Downtime chỉ được tính khi Trạng Thái Không Sẵn Sàng phát sinh do lỗi của GreenNode.
* Các trường hợp khác được loại trừ theo SLA, Điều khoản dịch vụ của GreenNode hoặc hợp đồng dịch vụ (nếu có).

## Bảo trì hệ thống

Bảo trì có thể được lên kế hoạch vào bất kỳ ngày nào trong tuần (kể cả cuối tuần) và bất kỳ thời điểm nào trong ngày; GreenNode nỗ lực chọn thời điểm ít ảnh hưởng nhất đến Khách hàng. Khi bảo trì phải tạm ngừng Dịch Vụ, GreenNode thông báo qua điện thoại, email hoặc trên trang chủ [greennode.ai](https://greennode.ai/):

| Trường hợp | Thời hạn thông báo |
| --- | --- |
| Bảo trì định kỳ | Trước ba (03) ngày làm việc |
| Bảo trì khẩn cấp | Trước ít nhất ba mươi (30) phút |
| Sự cố nằm ngoài tầm kiểm soát của GreenNode, bao gồm Sự Kiện Bất Khả Kháng | Trong vòng bốn (4) giờ làm việc kể từ khi xảy ra sự cố |

Tổng thời gian bảo trì có ảnh hưởng đến Dịch Vụ của Khách hàng trong một (1) tháng **không quá 120 phút**.

## Thời gian phản hồi và giải quyết sự cố

Liên hệ: tổng đài hỗ trợ 24/7 **1900 1549**, website [greennode.ai](https://greennode.ai/) hoặc email [support@greennode.ai](mailto:support@greennode.ai).

| Hạng mục | Thời gian |
| --- | --- |
| Phản hồi yêu cầu giải quyết sự cố | Trong vòng 15 phút kể từ khi nhận được yêu cầu |
| Đáp ứng và giải quyết sự cố | Từ 15 phút đến 48 giờ làm việc kể từ khi phản hồi yêu cầu |
| Sự cố nghiêm trọng | Có thể lâu hơn nhưng không quá 72 giờ làm việc kể từ khi phản hồi yêu cầu |

## Quy trình khiếu nại

Gửi bằng văn bản hoặc email đến [support@greennode.ai](mailto:support@greennode.ai), gồm:

* Tiêu đề email hoặc văn bản ghi rõ: **"Yêu cầu bồi thường theo cam kết SLA"**;
* Thông tin tài khoản bị ảnh hưởng;
* Ngày, giờ cụ thể và các thời điểm Dịch Vụ rơi vào Trạng Thái Không Sẵn Sàng;
* Logs ghi lỗi hoặc ảnh chụp màn hình tại thời điểm xảy ra lỗi (che thông tin bảo mật);
* Khiếu nại về mất dữ liệu chỉ được tiếp nhận khi có văn bản giám định chính thức của tổ chức giám định độc lập có chức năng hợp pháp; chi phí giám định do Khách hàng chịu;
* Thiệt hại và giá trị thiệt hại kèm chứng từ, hóa đơn liên quan;
* Mức bồi thường Khách hàng yêu cầu.

| Hạng mục | Thời hạn |
| --- | --- |
| Tiếp nhận khiếu nại | Trong vòng ba (3) tháng kể từ ngày xảy ra sự cố; quá hạn GreenNode không tiếp nhận |
| Phản hồi, giải quyết khiếu nại | Trong vòng 15 ngày làm việc kể từ ngày tiếp nhận |

Nếu không hài lòng với kết quả giải quyết, Khách hàng có thể gửi lại phản hồi; phản hồi đó được xử lý như một khiếu nại mới.
