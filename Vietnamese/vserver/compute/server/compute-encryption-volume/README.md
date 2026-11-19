# Compute Encryption Volume

Compute Encryption Volume  là dịch vụ mã hóa các Volume  được tích hợp vào trong hệ thống vServer. Dịch vụ này dùng để tạo, lưu trữ và kiểm soát các khóa để mã hóa dữ liệu của mình&#x20;



Bạn có thể mã hóa cả Boot Volume và Data Volume của một Server. Khi bạn tạo một Volume được mã hóa và gắn nó vào một Server, các loại dữ liệu sau sẽ được mã hóa:

Dữ liệu tĩnh bên trong Volume\
Tất cả dữ liệu di chuyển giữa Volume và Server\
Tất cả các bản Snapshot, Backup của Volume trên.\
Tất cả các Volume được tạo từ Snapshot, Volume trên.

Các hoạt động mã hóa diễn ra trên các máy chủ (Compute) lưu trữ các Server, đảm bảo an toàn cho cả dữ liệu tĩnh và dữ liệu đang truyền giữa Server và Volume sẽ không bị ảnh hưởng đến IOPS, Throughput. Bạn có thể gắn đồng thời cả Volume mã hóa và không mã hóa vào một Server.

Khi bạn tạo một Server mới, bạn có thể mã hóa nó bằng cách bật mã hóa cho Volume cụ thể. Nếu bạn đã bật mã hóa theo mặc định, Volume sẽ tự động được mã hóa bằng khóa KMS mặc định của bạn. Volume được mã hóa ngay khi nó sẵn sàng sử dụng lần đầu, đảm bảo dữ liệu của bạn luôn được bảo mật.

Theo mặc định, khóa KMS mà bạn chọn khi tạo Volume sẽ mã hóa các Snapshot, Backup được tạo từ Volume đó và các Volume được khôi phục từ những Snapshot, Backup mã hóa đó. Bạn không thể tắt mã hóa một Volume hoặc Snapshot đã được mã hóa, điều này có nghĩa là một Volume được khôi phục từ Snapshot hoặc một bản Backup mã hóa sẽ luôn được mã hóa.

Bạn không thể thay đổi khóa KMS được liên kết với Snapshot, Backup hoặc Volume hiện có. Tuy nhiên, bạn có thể liên kết một khóa KMS khác trong quá trình Server Migration đến một Server mới.

Chi phí: Vì quá trình mã hóa nằm trên máy chủ (Compute) nằm ngoài Server của bạn nên khi bật chức năng mã hóa, GreenNode sẽ charge thêm 30% giá của flavor hiện tại.





<figure><img src="https://docs.vngcloud.vn/download/attachments/59803291/image2020-10-15_10-39-57.png?version=1&#x26;modificationDate=1686204792000&#x26;api=v2" alt=""><figcaption></figcaption></figure>
