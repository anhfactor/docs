---
description: >-
  AI Platform cung cấp dịch vụ Mô hình dưới dạng Dịch vụ (MaaS), cho phép các
  nhà phát triển và doanh nghiệp dễ dàng tích hợp các mô hình AI mạnh mẽ vào ứng
  dụng của họ.
---

# Model as a Service

Truy cập vào phần [Models ](https://aiplatform.console.greennode.ai/models)trong AI Platform:

* Để sử dụng và enable bất kỳ mô hình nào, bạn cần có API key. [xem thêm](../ai-platform/bat-dau-voi-ai-platform.md#id-6.-quan-ly-api-keys)

Bạn có thể lọc các mô hình bằng các tùy chọn ở thanh bên trái:

* Nhà cung cấp (Provider): Google, Anthropic, OpenAI, GreenNode, ...
* Loại mô hình (Model Type):
  * Chat: Được thiết kế cho các cuộc hội thoại tương tác. Gọi qua Chat Completions, Messages (Anthropic) hoặc Responses tuỳ model.
  * Embedding: chuyển đổi dữ liệu (văn bản, hình ảnh, âm thanh,…) thành vector nhiều chiều, giúp máy tính hiểu và so sánh ngữ nghĩa để phục vụ tìm kiếm, phân loại hoặc gợi ý nội dung.
  * Rerank: Sắp xếp lại danh sách tài liệu theo mức độ liên quan với câu truy vấn.
  * OCR: Trích xuất văn bản và dữ liệu từ ảnh, tài liệu.
* Trường hợp sử dụng (Use-case):
  * Vietnamese: Tối ưu cho các tác vụ tiếng Việt.
  * General Tasks: Phù hợp cho nhiều tác vụ chung.
  * Translation: Chuyên về dịch thuật.
  * Research: Hỗ trợ các tác vụ nghiên cứu.
  * Finance: Chuyên về lĩnh vực tài chính.
  * Marketing: Tối ưu cho tiếp thị.
  * Technology: Phục vụ các tác vụ liên quan đến công nghệ.

### Bật / Tắt mô hình

1. Nhấp vào nút "Bật/Tắt model" (Toggle models). User cần activate billing để enable model, đối với user Prepaid cần nạp quota để enable model còn user Postpaid có thể enable model và sử dụng được ngay. Tham khảo [cách tính phí](cach-tinh-phi.md)<br>

<figure><img src="../../.gitbook/assets/image (779).png" alt=""><figcaption></figcaption></figure>

2. Lựa chọn mô hình: Một cửa sổ popup sẽ hiện ra. Tại đây, bạn có thể tìm kiếm và lọc mô hình theo Nhà cung cấp (Provider), Trạng thái (Status) hoặc Loại mô hình (Type).
3. Bật/tắt riêng lẻ hoặc hàng loạt mô hình.
4. Lưu (Save) các thay đổi.

<figure><img src="../../.gitbook/assets/image (16) (1) (2).png" alt=""><figcaption></figcaption></figure>

Để bắt đầu thử nghiệm và so sánh các mô hình trước khi tích hợp, bạn có thể sử dụng [Playground](playground.md)

<figure><img src="../../.gitbook/assets/image (1120).png" alt=""><figcaption></figcaption></figure>

### **Thử nghiệm với AI Platform Playground**

Trước khi tích hợp vào ứng dụng của bạn, hãy khám phá các khả năng của mô hình trong Playground:

* So sánh các mô hình khác nhau dựa trên độ trễ, độ chính xác và khả năng hỗ trợ.
* Gửi các yêu cầu thử nghiệm một cách tương tác và đánh giá kết quả đầu ra.
* Tinh chỉnh các tham số để tìm ra mô hình hoạt động tốt nhất cho trường hợp sử dụng cụ thể.

[**Xây dựng với API của AI Platform MaaS**](maas-api.md)

Sau khi thử nghiệm trong Playground, bạn có thể truy cập các mô hình thông qua AI Platform MaaS:

* Hỗ trợ cả yêu cầu đồng bộ và truyền phát (streaming) cho các ứng dụng thời gian thực.

### Bảo mật và quyền riêng tư dữ liệu

* Dữ liệu được mã hóa trên kênh truyền bằng **TLS 1.2 trở lên**.
