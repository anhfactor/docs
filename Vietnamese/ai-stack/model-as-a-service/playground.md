---
description: >-
  Playground là một giao diện trực quan trên nền tảng, cho phép bạn thử nghiệm
  và so sánh các mô hình AI một cách nhanh chóng mà không cần viết code. Đây là
  môi trường lý tưởng để khám phá các khả năng
---

# Playground

### Truy cập [Playground](https://aiplatform.console.greennode.ai/playground)

### Hướng dẫn thử nghiệm mô hình

1. Chọn loại mô hình tùy thuộc vào tác vụ của bạn: Chat, Embedding, Rerank, OCR
2. Chọn loại mô hình: Ở bảng điều khiển bên phải, chọn một mô hình từ danh sách
3. Thiết lập prompt
   * Trong phần System prompt, hãy định nghĩa các hướng dẫn hoặc ngữ cảnh cho mô hình. Bạn cũng có thể thêm các ví dụ để định hướng hành vi của nó.
4.  [Tinh chỉnh các tham số:](playground.md#huong-dan-tinh-chinh-tham-so-mo-hinh)

    <figure><img src="../../.gitbook/assets/image (442).png" alt=""><figcaption></figcaption></figure>
5. Bắt đầu thử nghiệm:

* Nhập câu lệnh của bạn và quan sát cách các mô hình khác nhau phản hồi.

6. Lưu cấu hình:

* Sao chép dưới dạng code: Nhấp vào biểu tượng `<> API`
* Chọn ngôn ngữ lập trình:
  * Curl: Mã lệnh này được sử dụng trong Terminal hoặc Command Prompt, giúp bạn dễ dàng kiểm tra API trực tiếp mà không cần viết code.
  * Python: Cung cấp đoạn mã Python sẵn sàng để bạn sao chép và sử dụng trong các dự án Python của mình.
  * TypeScript: Cung cấp đoạn mã TypeScript/Node.js, phù hợp cho các dự án web và ứng dụng server-side.

<figure><img src="../../.gitbook/assets/image (1124).png" alt=""><figcaption></figcaption></figure>

### Hướng dẫn tinh chỉnh tham số mô hình

Khi sử dụng Playground, bạn có thể điều chỉnh các thông số sau để kiểm soát kết quả đầu ra của mô hình. Các thông số này có thể khác nhau tùy thuộc vào loại mô hình bạn chọn.

**Mô hình Chat**

* Past messages included: Số lượng tin nhắn gần nhất mà mô hình sẽ ghi nhớ.
  * Phạm vi: 1 - 20 (Mặc định: 10).
* Maximum token output: Số token tối đa mà mô hình có thể tạo ra.
  * Phạm vi và mặc định tùy model (ví dụ 1 - 8.192, mặc định 2.000; hoặc 1 - 32.768, mặc định 4.096; một số model tới 131.072).
* Temperature: Kiểm soát độ ngẫu nhiên của câu trả lời.
  * 0: Kết quả nhất quán, mang tính xác định cao.
  * < 1: Kết quả tập trung, chính xác, lý tưởng cho tóm tắt hoặc hỏi đáp.
  * ≈ 1: Khuyến khích sự sáng tạo và đa dạng trong câu trả lời.
  * Phạm vi: 0 - 2 (Mặc định: 1).
* Top P: Ngưỡng xác suất để mô hình chọn từ vựng. Giúp cân bằng giữa sự tự nhiên và đa dạng của câu trả lời.
  * Phạm vi: 0 - 1 (Mặc định: 0.7 hoặc 0.95 tùy model).
* Presence Penalty (chỉ một số model): Mức phạt cho các từ đã xuất hiện trong cuộc trò chuyện, khuyến khích mô hình tạo ra các chủ đề mới và giảm lặp từ.
  * Phạm vi: -2 đến 2 (Mặc định: 0).

**Mô hình Embedding**

* Encoding format: Định dạng vector trả về.
  * BGE-M3: Dense, Sparse, Sparse dense (Mặc định: Dense).
  * Qwen3 Embedding 8B: Float.

**Mô hình Rerank**

* Top N: Số kết quả giữ lại sau khi xếp hạng lại (tối thiểu 1).

**Mô hình OCR (GreenNode IDP)**

* Loại tài liệu: 15 loại (Mặc định: Căn cước công dân).
* Loại tệp: Ảnh (jpg, png, bmp, tif; tối đa 10 MB) hoặc PDF (tối đa 50 MB).

Để xem thêm các thông số chi tiết, bạn có thể tham khảo tài liệu của [vLLM](https://docs.vllm.ai) và [OpenAI](https://platform.openai.com/docs/api-reference/introduction).

### So sánh mô hình

Tính năng này cho phép bạn chạy và so sánh kết quả đầu ra của hai mô hình cùng lúc.

* Nhấp vào nút So sánh (Compare) để mở hai cửa sổ trò chuyện song song.
* Bạn có thể nhập câu lệnh và gửi tới cả hai mô hình cùng một lúc để xem phản hồi và đánh giá hiệu quả.

<figure><img src="../../.gitbook/assets/image (1125).png" alt="" width="164"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (1127).png" alt="" width="563"><figcaption></figcaption></figure>
