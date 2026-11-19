# Flavor

Flavor là một cấu hình tài nguyên phần cứng dành cho Server cụ thể hoá các chỉ số hiệu năng về Cpu, Ram, Gpu, Disk và mục đích đặc biệt. Tùy thuộc vào nhu cầu của ứng dụng mà người dùng có thể chọn cấu hình Flavor tương ứng.

GreenNode cung cấp các Flavor phù hợp với đa dạng nhu cầu để người dùng có thể lựa chọn. Phần đầu tiên trong tên gọi của Flavor quy định loại hạ tầng cho Server, ví dụ s1 là hạ tầng CPU Intel Scalable, a1 là hạ tầng CPU AMD EPYC. Phần thứ 2 là mô tả tỷ lệ tài nguyên như Standard, HighCPU, HighMem. Phần cuối cùng là kích thước của Server, thể hiện số lượng vCPU, RAM (đơn vị GB) sẽ được cấp cho Server.

<figure><img src="../../../.gitbook/assets/image (914).png" alt=""><figcaption></figcaption></figure>

<figure><img src="https://docs.vngcloud.vn/download/attachments/49647880/download.png?version=1&#x26;modificationDate=1668406683000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

GreenNode cung cấp nhiều loại cấu hình Flavor được tinh chỉnh cho nhiều mục đích khác nhau. Để xác định tốt nhất các nhu cầu tài nguyên này, người dùng có thể xem thêm ở {trang chi tiết Flavor}.

* **Các dòng máy Server**: tập hợp các cấu hình tài nguyên được định nghĩa sẵn cho các nhu cầu sử dụng khác nhau như mục đích chung, mục đích tối ưu tính toán, mục đích tối ưu bộ nhớ hay mục đích tối ưu card GPU.
  * Mục đích chung: nhóm cấu hình cân bằng giữa chi phí và hiệu năng cho đa dạng mục đích.
  * Tối ưu tính toán: nhóm cấu hình được tinh chỉnh tối ưu cho việc xử lý của CPU mang lại hiệu năng cao nhất trên mỗi tài nguyên CPU được cấp.
  * Tối ưu bộ nhớ: nhóm cấu hình được tinh chỉnh tối ưu cho việc sử dụng bộ nhớ và được cấp phát tỷ lệ bộ nhớ nhiều hơn cho mỗi đơn vị CPU.
  * Tối ưu GPU: cung cấp cấu hình có card GPU cho các Server đối với các mục đích dùng trong trí tuệ nhân tạo, xử lý dữ liệu lớn. Các flavor GPU H100 hỗ trợ **Multi-Instance GPU (MIG)** — cho phép phân chia một GPU vật lý thành nhiều instance độc lập. Xem hướng dẫn tại [Sử dụng Multi-Instance GPU (MIG)](su-dung-multi-instance-gpu-mig.md).
* **Hạ tầng CPU**: Các dòng Server được phân loại rõ thêm bằng việc phân loại các dòng CPU. Ví dụ các Flavor S và S1 trong nhóm mục đích chung sẽ sử dụng CPU Intel Scalable Gen2 và 3. Tương tự, A và A1 sẽ dùng CPU AMD EPYC Zen2 và Zen3. Các chữ số phía sau chữ cái đầu tiên để chỉ thế hệ CPU.
* **Loại cấu hình**: Mô tả tỷ lệ cấu hình, xác định số lượng tài nguyên CPU, RAM… được cấp phát cho Server.
* Ngoài ra, còn có 1 loại flavor đặc biệt chứa Emperal Disk như: g5-standard-16x120x300NVMe-1H100.
  * Ephemeral Disk cung cấp bộ nhớ tạm thời dạng block-level cho Server của bạn trên nền tảng GreenNode Cloud. Loại lưu trữ này được cung cấp bởi các đĩa vật lý gắn trực tiếp vào máy chủ (host computer) nơi server của bạn đang chạy
  * Dữ liệu trên Ephemeral Disk sẽ bị mất vĩnh viễn khi server bị delete, migrate hoặc khi phần cứng gặp sự cố. Hãy đảm bảo bạn không lưu dữ liệu quan trọng trên loại lưu trữ này.
  * Ephemeral Storage có thể backup với Veeam [https://docs.vngcloud.vn/vng-cloud-document/vn/backup-center/backup-voi-veeam](https://docs.vngcloud.vn/vng-cloud-document/vn/backup-center/backup-voi-veeam).

<br>
