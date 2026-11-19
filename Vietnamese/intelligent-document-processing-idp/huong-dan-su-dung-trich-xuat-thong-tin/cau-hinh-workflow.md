# Cấu hình workflow

Trong tab **Xử lý tài liệu** → Chọn **Quy trình**

Quy trình định nghĩa cách xử lý một bộ hồ sơ từ đầu đến cuối.

### 1.Danh sách quy trình

<figure><img src="../../.gitbook/assets/greennode-idp.png (5).jpg" alt=""><figcaption><p align="center"><em>Danh sách quy trình</em></p></figcaption></figure>

**Mỗi dòng gồm:**

◦     Tên quy trình, kèm mã (WF…) và ID.

◦     Nhãn phiên bản đang chạy.

◦     Phiên bản mới nhất, Trạng thái, Thời điểm cập nhật/tạo.

◦     Số tài liệu đã xử lý.

Bấm › ở đầu dòng để xem các phiên bản cũ.

Tìm theo tên hoặc mã; lọc theo trạng thái.

**Menu ⋮** ở cột Hành động:

◦     Thông tin quy trình

◦     Quản lý yêu cầu

◦     Chỉnh sửa

◦     Kích hoạt / Lưu trữ (tuỳ trạng thái)

<figure><img src="../../.gitbook/assets/greennode-idp.png (6).jpg" alt=""><figcaption><p><em>Menu thao tác quy trình</em></p></figcaption></figure>

Thông tin quy trình mở bảng bên phải gồm:

•     Tên, phiên bản, trạng thái, lần cập nhật cuối, số tài liệu đã xử lý.

•     Chỉ số xử lý: tỷ lệ tự động / thủ công; số hồ sơ tự duyệt, duyệt tay, tự từ chối, từ chối tay.

•     Thời gian xử lý.

•     Integration Incident: tình trạng kết nối gửi kết quả. Khi kết nối bị ngắt do lỗi liên tiếp, bấm Send Integration Again để gửi lại.

<figure><img src="../../.gitbook/assets/greennode-idp.png (7).jpg" alt=""><figcaption><p align="center"><em>Thông tin quy trình</em></p></figcaption></figure>

{% hint style="info" %}
•     Muốn sửa một quy trình đang chạy: bấm Phiên bản mới để tạo bản nháp, sửa, rồi Kích hoạt. Phiên bản cũ tự chuyển sang DEPRECATED.

•     Một quy trình phải có phiên bản CÓ HIỆU LỰC thì mới nhận được hồ sơ.
{% endhint %}



***

### 2. Vòng đời phiên bản

| **Trạng thái**        | **Ý nghĩa**                                       | **Chuyển được sang**   |
| --------------------- | ------------------------------------------------- | ---------------------- |
| BẢN NHÁP (DRAFT)      | Đang soạn, chỉnh sửa và Lưu được                  | Kích hoạt, Lưu trữ     |
| CÓ HIỆU LỰC (ACTIVE)  | Đang nhận hồ sơ                                   | Tạm dừng, Lưu trữ      |
| TẠM DỪNG (SUSPENDED)  | Ngừng nhận hồ sơ                                  | Kích hoạt lại, Lưu trữ |
| DEPRECATED            | Phiên bản cũ, đã được thay bằng phiên bản mới hơn | —                      |
| ĐÃ LƯU TRỮ (ARCHIVED) | Ngừng sử dụng                                     | —                      |

***

### 3.Tạo mới quy trình

1\.   Bấm Tạo quy trình mới.

2\.   Nhập Tên (bắt buộc) và Mô tả (tối đa 500 ký tự).

3\.   Bấm Gửi. Hệ thống mở trang cấu hình ở trạng thái BẢN NHÁP.

<figure><img src="../../.gitbook/assets/greennode-idp.png (8).jpg" alt=""><figcaption><p align="center"><em>Tạo quy trình mới</em></p></figcaption></figure>



***

### 4.Cấu hình quy trình 9 chặng

Trang cấu hình có thanh chặng ở trên và các nút ở góc phải:

•     Kích hoạt, Lưu trữ, Phiên bản mới, Lưu.

•     Làm mới: chỉ xuất hiện khi có thay đổi chưa lưu, dùng để bỏ thay đổi.

{% hint style="info" %}
Lưu ý: Thay đổi chỉ có hiệu lực sau khi bấm Lưu. Trình duyệt tạm nhớ bản nháp chưa lưu; nếu không muốn giữ, bấm Làm mới.
{% endhint %}

**Chặng 1 — Thông tin chung**

•     Tên và Mô tả quy trình.

•     Cấu hình nâng cao (biểu tượng ⚙):

| **Tham số**              | **Ý nghĩa**                                  | **Mặc định** |
| ------------------------ | -------------------------------------------- | ------------ |
| Số lần thử lại tối đa    | Số lần hệ thống tự thử lại một bước bị lỗi   | 3            |
| Số ngày tối đa           | Số ngày chờ người xử lý sau khi một bước lỗi | 3            |
| Số ngày tối đa chờ duyệt | Số ngày chờ người duyệt                      | 3            |

<figure><img src="../../.gitbook/assets/greennode-idp.png (9).jpg" alt=""><figcaption><p><em>Chặng Thông tin chung</em></p></figcaption></figure>

**Chặng 2 — Nguồn dữ liệu**

•     Cấu hình để hệ thống tự lấy tệp về xử lý, thay vì tải tay.

•     Bấm Thêm nguồn dữ liệu để chọn loại nguồn (vd. S3: bucket, region, endpoint, access/secret key, thư mục…).

•     Có thể đặt lịch chạy.

•     Bảng nguồn dữ liệu gồm: Loại, Chi tiết, Loại tệp, Loại lịch trình, Giá trị lịch trình, Có hiệu lực.

<figure><img src="../../.gitbook/assets/greennode-idp.png (10).jpg" alt=""><figcaption><p><em>Chặng Nguồn dữ liệu</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (11).jpg" alt=""><figcaption><p align="center"><em>Chọn loại nguồn dữ liệu</em></p></figcaption></figure>

**Chặng 3 — Mô hình**

1\.   Bấm Thêm mô hình để chọn các loại tài liệu mà bộ hồ sơ có thể chứa. Có 2 tab: Mô hình đã được huấn luyện sẵn và Mô hình tuỳ chỉnh (mẫu tự định nghĩa).

2\.   Bấm Thêm trên từng mô hình, xong bấm Xong.

3\.   Bật/tắt tuỳ chọn cho từng mô hình (hoặc Sửa tất cả):

◦     Trích xuất thông tin

◦     Phát hiện bảng

◦     Phát hiện chữ ký

◦     Phát hiện con dấu

◦     Tự động sửa chính tả

◦     Kiểm tra trùng lặp

<figure><img src="../../.gitbook/assets/greennode-idp.png (12).jpg" alt=""><figcaption><p align="center"><em>Chặng Mô hình</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (13).jpg" alt=""><figcaption><p align="center"><em>Thêm mô hình vào quy trình</em></p></figcaption></figure>

**Chặng 4 — Chuẩn hoá**

•     Chọn từng mô hình ở cột trái, rồi xây chuỗi bước chuẩn hoá cho các trường của mô hình đó.

•     Bấm Thêm bước mới để chọn bước, ví dụ:

◦     Chuyển định dạng ngày

◦     Xoá ký tự

◦     Tìm và thay thế

◦     Chuyển sang số nguyên / số thập phân

◦     Đổi viết hoa / thường

◦     Cắt khoảng trắng

◦     Tra cứu Dataset

◦     Code

•     Dùng Mẫu đầu vào để chạy thử bước trên dữ liệu mẫu.

<figure><img src="../../.gitbook/assets/greennode-idp.png (14).jpg" alt=""><figcaption><p align="center"><em>Chặng Chuẩn hoá</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (15).jpg" alt=""><figcaption><p align="center"><em>Thêm bước chuẩn hoá</em></p></figcaption></figure>

**Chặng 5 — Xác thực & Xét duyệt**

Chặng này chấm điểm rủi ro và quyết định hồ sơ nào cần người duyệt.

•     Danh mục: nhóm quy tắc, mỗi nhóm có trọng số. Bấm Thêm danh mục để tạo nhóm.

•     Danh sách quy tắc: mỗi quy tắc gồm mã, tên, điểm cơ bản (vd. HIGH 80, MEDIUM 40) và công tắc bật/tắt.

•     Thêm quy tắc mới mở trình tạo quy tắc:

◦     UI: ghép điều kiện VÀ/HOẶC.

◦     Script: viết điều kiện bằng mã.

◦     Chọn Kích hoạt quy tắc khi và Gán điểm.

◦     Dùng Kiểm tra rule (Tạo mẫu tự động → Chạy) để thử trước khi lưu.

•     Tóm tắt tác động quy tắc: số quy tắc đang bật theo mức rủi ro, điểm và mức đóng góp dự kiến.

<figure><img src="../../.gitbook/assets/greennode-idp.png (16).jpg" alt=""><figcaption><p align="center"><em>Chặng Xác thực &#x26; Xét duyệt</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (17).jpg" alt=""><figcaption><p><em>Thêm danh mục quy tắc</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (18).jpg" alt=""><figcaption><p align="center"><em>Thêm quy tắc mới</em></p></figcaption></figure>

Xét duyệt (khung dưới cùng bên trái → Cấu hình) gán hành động cho từng mức rủi ro, theo điểm cuối cùng từ 0 đến 100:

| **Mức rủi ro (ví dụ)** | **Khoảng điểm** | **Hành động có thể chọn**                                   |
| ---------------------- | --------------- | ----------------------------------------------------------- |
| Thấp                   | 0 – 24          | Tự động phê duyệt / Cần duyệt / Tự động từ chối / Gửi email |
| Trung bình             | 25 – 39         | như trên                                                    |
| Cao                    | 40 – 79         | như trên                                                    |
| Nghiêm trọng           | 80 – 100        | như trên                                                    |

•     Với hành động Cần duyệt, chọn người được giao (Assign To).

•     Bấm Thêm hành động để thêm hành động cho một mức.

<figure><img src="../../.gitbook/assets/greennode-idp.png (19).jpg" alt=""><figcaption><p><em>Cấu hình xét duyệt theo mức rủi ro</em></p></figcaption></figure>

{% hint style="info" %}
Lưu ý: Hồ sơ chờ duyệt quá Số ngày tối đa chờ duyệt (mặc định 3 ngày) sẽ tự động bị từ chối (BỊ TỪ CHỐI).
{% endhint %}

**Chặng 6 — Phân tích nghiệp vụ (tuỳ chọn, AI)**

Dành cho nghiệp vụ chuyên sâu, ví dụ Claim Bảo hiểm sức khoẻ:

•     Loại nghiệp vụ: quyết định các tính năng AI áp dụng và cách phân loại tài liệu.

•     Tính năng AI áp dụng (BETA):

◦     Tóm tắt hồ sơ bảo hiểm: thêm mục _Thông tin claim bảo hiểm_ vào kết quả.

◦     Phân tích nghiệp vụ: đối chiếu hồ sơ với tài liệu chính sách, đưa ra khuyến nghị kèm trích dẫn điều khoản.

•     API tra cứu dữ liệu nghiệp vụ: gọi hệ thống lõi để lấy hạn mức, thông tin người được bảo hiểm.

•     Tài liệu chính sách: tải hợp đồng/quy tắc bảo hiểm làm căn cứ phân tích (Tải tài liệu). Tài liệu phải ở trạng thái INDEXED mới được dùng.

<figure><img src="../../.gitbook/assets/greennode-idp.png (20).jpg" alt=""><figcaption><p><em>Chặng Phân tích nghiệp vụ</em></p></figcaption></figure>

**Chặng 7 — Chuyển đổi**

Định nghĩa định dạng kết quả gửi sang hệ thống của bạn:

•     Định dạng Payload: JSON hoặc XML.

•     Script tổng hợp (Global Transform Script): chạy một lần sau khi đã chuyển đổi xong từng tài liệu.

•     Quy tắc chuyển đổi theo từng loại tài liệu: ánh xạ Trường nguồn → Trường đích, có công tắc bật/tắt.

<figure><img src="../../.gitbook/assets/greennode-idp.png (21).jpg" alt=""><figcaption><p align="center"><em>Chặng Chuyển đổi</em></p></figcaption></figure>

**Chặng 8 — Tích hợp**

Cấu hình nơi nhận kết quả. Bấm Thêm kết nối, chọn Loại tích hợp: REST API, Webhook, S3 hoặc Email.

•     REST/Webhook cần khai báo:

◦     URL Endpoint và Phương thức HTTP.

◦     Xác thực: không / API Key / Bearer / Basic / OAuth2.

◦     Header tuỳ chỉnh.

◦     Mã thành công (mặc định 200, 201) và Timeout.

•     Gửi webhook khi: mặc định chỉ gửi khi hồ sơ kết thúc (HOÀN TẤT, BỊ TỪ CHỐI, ĐÃ HUỶ, THẤT BẠI). Có thể chọn thêm các bước trung gian.

•     Chính sách thử lại & ngắt mạch:

◦     Số lần thử lại tối đa, khoảng cách giữa các lần thử.

◦     Ngưỡng ngắt mạch (mặc định 5 lần lỗi liên tiếp). Khi bị ngắt, OWNER nhận email; dùng Send Integration Again (mục 7.1) để gửi lại.

•     Mục Hướng dẫn tích hợp Webhook / REST API mô tả cấu trúc payload, header và cách xác thực chữ ký.

<figure><img src="../../.gitbook/assets/greennode-idp.png (22).jpg" alt=""><figcaption><p align="center"><em>Chặng Tích hợp — chưa có kết nối</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (23).jpg" alt=""><figcaption><p align="center"><em>Form khai báo một kết nối REST API</em></p></figcaption></figure>

{% hint style="info" %}
Mẹo: Hệ thống của bạn nên chống xử lý trùng theo request\_id, vì một hồ sơ có thể được gửi nhiều lần (thử lại, gửi lại).
{% endhint %}

**Chặng 9 — Kiểm thử**

Chạy thử toàn bộ cấu hình trên tài liệu mẫu trước khi kích hoạt:

1\.   Bấm Thêm tài liệu → Tải lên từ thiết bị hoặc Lấy từ S3. Tối đa 50 bộ kiểm thử.

2\.   Chọn chế độ tích hợp:

◦     Dry-run: mô phỏng, không gửi dữ liệu ra ngoài.

◦     Live: gửi thật tới kết nối đã cấu hình.

3\.   Chạy từng tệp, hoặc chọn nhiều tệp và bấm Chạy hàng loạt.

4\.   Xem kết quả ở các tab: Kết quả OCR, Kết quả kiểm tra, Kết quả JSON, Lịch sử.

<figure><img src="../../.gitbook/assets/greennode-idp.png (24).jpg" alt=""><figcaption><p align="center"><em>Chặng Kiểm thử</em></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/greennode-idp.png (25).jpg" alt=""><figcaption><p align="center"><em>Thêm tài liệu kiểm thử</em></p></figcaption></figure>

Kiểm thử đạt thì bấm Kích hoạt để đưa quy trình vào vận hành.

***

#### 5 Quản lý yêu cầu của một quy trình

Tại menu ⋮ của quy trình → chọn **Quản lý yêu cầu**

•     Danh sách hồ sơ của riêng quy trình. Nhãn N Cần duyệt cho biết số hồ sơ đang chờ duyệt.

•     Lọc theo: mã hồ sơ / tên tệp, trạng thái, nguồn (API, S3, Email, Tải lên), Ẩn kiểm thử, khoảng ngày nhận.

•     Nút Xuất kết quả và Tải tập tin.

<figure><img src="../../.gitbook/assets/greennode-idp.png (26).jpg" alt=""><figcaption><p align="center"><em>Quản lý yêu cầu của quy trình</em></p></figcaption></figure>

Tải hồ sơ lên tay:

1\.   Bấm Tải tập tin.

2\.   Chọn API Keys.

3\.   Chọn loại tệp: Ảnh / PDF / PDF + Image / ZIP.

4\.   Kéo thả tệp. Với nhiều ảnh, hệ thống sắp xếp theo thứ tự tên tệp (alphabet).

5\.   (Tuỳ chọn) Nhập Metadata dạng JSON, ví dụ thông tin hợp đồng của người được bảo hiểm. Metadata được chuyển nguyên vẹn cho bước Phân tích nghiệp vụ.

6\.   Bấm Tải tập tin.

<figure><img src="../../.gitbook/assets/greennode-idp.png (27).jpg" alt=""><figcaption><p align="center"><em>Tải tập tin vào quy trình</em></p></figcaption></figure>
