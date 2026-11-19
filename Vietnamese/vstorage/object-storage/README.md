# Object storage

**Object Storage** là một mô hình lưu trữ dữ liệu mà trong đó dữ liệu được lưu dưới dạng **"object"** thay vì file hoặc block. Mỗi object bao gồm:

1. **Dữ liệu**: Nội dung thực tế (ví dụ: hình ảnh, video, file văn bản,...).
2. **Metadata**: Thông tin mô tả đối tượng (ví dụ: tên, thời gian tạo, định dạng,...).
3. **Object ID**: Một định danh duy nhất (ví dụ: hash, UUID) giúp truy cập object đó.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

Trên GreenNode, chúng tôi đang cung cấp cho bạn đa dạng sự lựa chọn **Farm** để khởi tạo project và thực hiện lưu trữ object, cụ thể:

<table><thead><tr><th width="113.54547119140625">Farm</th><th>Endpoint</th><th>Mô tả và Mục đích sử dụng</th></tr></thead><tbody><tr><td>HCM03</td><td>https://hcm03.vstorage.vngcloud.vn</td><td><strong>Đã ngừng nhận khách hàng mới.</strong> Farm HCM03 tiếp tục phục vụ khách hàng hiện tại. Khách hàng mới vui lòng sử dụng farm HCM04 hoặc HAN02.</td></tr><tr><td>HAN02</td><td>https://han02.vstorage.vngcloud.vn</td><td>Region HAN02 được xây dựng để đáp ứng các yêu cầu lưu trữ object với Hiệu suất cao, đa dạng các cơ chế mã hóa (SSE-S3, SSE-C), cung cấp gói cước mới - Instant Archive với chi phí thấp hơn, giúp khách hàng tiết kiệm chi phí lưu trữ dữ liệu dài hạn mà không phát sinh chi phí ẩn và vẫn đáp ứng đầy đủ tiêu chí cho việc lưu trữ backup.</td></tr><tr><td>HCM04</td><td>https://hcm04.vstorage.vngcloud.vn</td><td>Region HCM04 được xây dựng để đáp ứng các yêu cầu lưu trữ object với Hiệu suất cao, đa dạng các cơ chế mã hóa (SSE-S3, SSE-C), cung cấp gói cước mới - Instant Archive với chi phí thấp hơn, giúp khách hàng tiết kiệm chi phí lưu trữ dữ liệu dài hạn mà không phát sinh chi phí ẩn và vẫn đáp ứng đầy đủ tiêu chí cho việc lưu trữ backup.</td></tr></tbody></table>
