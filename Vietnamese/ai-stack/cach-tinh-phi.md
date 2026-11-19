# Cách tính phí

Trong hành trình xây dựng các ứng dụng AI hiện đại, việc hiểu rõ chi phí vận hành là yếu tố quan trọng để tối ưu ngân sách và đảm bảo hiệu suất đầu tư. Với AI Stack tại **GreenNode**, chúng tôi cung cấp một hệ sinh thái mạnh mẽ cho các nhà phát triển, AI Engineer, Data Scientist và doanh nghiệp — từ **Notebook để phát triển**, **Inference để triển khai mô hình**, đến **Network Volume để lưu trữ dữ liệu linh hoạt**.

Bài viết này sẽ giúp bạn nắm rõ cách thức tính phí của từng tài nguyên trong AI Stack và các hình thức thanh toán tương ứng, giúp bạn kiểm soát chi phí hiệu quả ngay từ đầu.

## 1. Notebook Instance

* **Cách tính phí**:
  * Tính theo **loại compute (flavor)**: số CPU, RAM, GPU.
  * Tính theo dung lượng **Local Block Storage** được gắn vào notebook.
* **Hình thức thanh toán**:
  * **Trả trước (User Prepaid)**: Hệ thống sẽ trừ chi phí ngay khi tạo notebook. Khi notebook bị xóa sớm, phần chi phí còn lại sẽ được **tự động hoàn lại**.
  * **Trả sau (User Postpaid)**: Sử dụng trước, trả tiền sau tại cuối mỗi kì đối soát, thường là cuối tháng

## 2. Inference Endpoint

* **Cách tính phí**:
  * Tính theo **loại compute (flavor)**: số CPU, RAM, GPU để chạy model.
  * Trong trường hợp bật **auto-scaling**, phí được nhân với số lượng instance đang chạy thực tế.
* **Hình thức thanh toán**:
  * **Trả trước (User Prepaid)**: Trừ phí khi khởi tạo endpoint. Phần thời gian chưa dùng đến sẽ được **refund nếu endpoint bị xóa**.
  * **Trả sau (User Postpaid)**: Sử dụng trước, trả tiền sau tại cuối mỗi kì đối soát, thường là cuối tháng

## 3. Network Volume

* **Cách tính phí**:
  * Dựa trên **dung lượng sử dụng thực tế (GB)** — giúp tiết kiệm tối đa chi phí nếu bạn chỉ sử dụng một phần dữ liệu.
* **Hình thức thanh toán**:
  * **Hold Credit**: Hệ thống giữ một phần credit và trừ dần dựa theo mức sử dụng.

## 4. Các Hình Thức Thanh Toán trên GreenNode

GreenNode hỗ trợ 3 cơ chế thanh toán linh hoạt:

* **Trả trước (Prepaid)** – Thanh toán trước, hoàn tiền khi không sử dụng hết.
* **Trả sau (Postpaid)** – Thanh toán sau theo mức sử dụng thực tế.
* **Hold Credit** – Hệ thống giữ một khoản tạm thời, trừ dần theo usage.

Tham khảo chi tiết: [Giới thiệu các hình thức thanh toán tại GreenNode](../quan-ly-hoa-don-chi-phi-and-tai-nguyen/trai-nghiem-billing-and-kenh-thanh-toan/ve-billing-and-payment/)
