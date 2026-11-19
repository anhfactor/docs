# Trình khám phá chi phí



**Trình khám phá chi phí / Cost explorer** tại vConsole cung cấp thống kê, phân tích và dự đoán chi phí sử dụng dịch vụ trên GreenNode theo **nhiều chiều dữ liệu** (theo sản phẩm, theo loại tài nguyên và theo từng resource), với nhiều mức tổng hợp thời gian và khả năng lọc dữ liệu linh hoạt.

Truy cập đến trang **Trình khám phá chi phí / Cost explorer** [**tại đây**](https://dashboard.console.greennode.ai/cost-explorer)**.**

**Cost explorer chỉ hỗ trợ dự đoán chi phí dịch vụ của các sản phẩm / dịch vụ sau:**

| Sản phẩm     | Loại tài nguyên tiêu biểu                | Hỗ trợ thống kê / dự đoán phí tại Cost Explorer |
| ------------ | ---------------------------------------- | ----------------------------------------------- |
| **vServer**  | `instance`, `volume`, `load balancer`, … | Có                                              |
| **vStorage** | `object-storage`, `backup-location`, …   | Có                                              |
| **vMonitor** | `monitor-platform-log`, …                | Có                                              |
| **AI Base**  | <p><code>ai-runtime</code>, …<br></p>    | Có                                              |

{% hint style="info" %}
Bảng trên chỉ nêu **một số loại tài nguyên tiêu biểu** của mỗi sản phẩm; danh sách đầy đủ có thể mở rộng theo từng sản phẩm. Người dùng xem toàn bộ loại tài nguyên đang phát sinh chi phí qua bộ lọc **Loại tài nguyên** trên giao diện. Loại tài nguyên có chi phí bằng 0 trong kỳ vẫn được liệt kê để theo dõi đầy đủ.


{% endhint %}

### **1.** Bộ lọc và phạm vi dữ liệu <a href="#trinhkhamphachiphi-costexplorer-1.currentmonthcost-phisudungtrongthang" id="trinhkhamphachiphi-costexplorer-1.currentmonthcost-phisudungtrongthang"></a>

***

Thanh bộ lọc ở đầu trang cho phép người dùng tùy chỉnh dữ liệu hiển thị. Các tùy chọn sẽ thay đổi tương ứng theo **chế độ xem (Xem theo)** đang chọn.

| Bộ lọc                           | Mô tả                                                                                                                                                                                                                        |
| -------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Xem theo**                     | Chế độ phân tích dữ liệu, gồm 3 lựa chọn: **Sản phẩm**, **Loại tài nguyên**, **Resource ID**. Đây là bộ lọc quyết định cách tổng hợp và hiển thị toàn trang.                                                                 |
| **Sản phẩm**                     | Lọc theo một sản phẩm cụ thể hoặc **Tất cả sản phẩm**.                                                                                                                                                                       |
| **Loại tài nguyên**              | Lọc theo một loại tài nguyên cụ thể hoặc **Tất cả loại**. _(Hiển thị ở chế độ xem theo Loại tài nguyên và Resource ID.)_                                                                                                     |
| **Tên resource**                 | Tìm kiếm theo tên resource.                                                                                                                                                                                                  |
| **ID resource**                  | Tìm kiếm theo ID resource. _(Ở chế độ Resource ID, ô tìm kiếm gộp chung "Tìm theo tên hoặc ID resource".)_                                                                                                                   |
| **Mức tổng hợp**                 | Mức độ gom nhóm dữ liệu theo thời gian, gồm 4 lựa chọn: **Hourly** (theo giờ), **Daily** (theo ngày), **Weekly** (theo tuần), **Monthly** (theo tháng). Trục thời gian của biểu đồ và các cột trong bảng thay đổi tương ứng. |
| **Ngày bắt đầu / Ngày kết thúc** | Khoảng thời gian thống kê, **cố định theo tháng hiện tại** (từ đầu tháng đến thời điểm truy cập). Trường này hiển thị để tham chiếu, người dùng không tự chọn khoảng thời gian khác.                                         |
| **Áp dụng**                      | Áp dụng toàn bộ điều kiện lọc để cập nhật biểu đồ, bảng biểu và các chỉ số tổng quan.                                                                                                                                        |

{% hint style="info" %}
**Mức tổng hợp linh hoạt:** Người dùng có thể đổi mức gom nhóm dữ liệu giữa **Hourly / Daily / Weekly / Monthly** để xem chi phí ở các độ phân giải thời gian khác nhau trong tháng hiện tại.<br>
{% endhint %}

### **2.** Các chỉ số tổng quan <a href="#trinhkhamphachiphi-costexplorer-2.forecastmonthcost-dudoanphisudung" id="trinhkhamphachiphi-costexplorer-2.forecastmonthcost-dudoanphisudung"></a>

***

Khu vực bên trái hiển thị các thẻ chỉ số tổng quan. Nội dung thẻ thay đổi theo chế độ xem.

#### Phí sử dụng trong tháng

* Tổng chi phí sử dụng dịch vụ (chỉ tính các sản phẩm được Cost Explorer hỗ trợ) trong khoảng thời gian đã chọn.
* Hiển thị tỉ lệ **chênh lệch so với kỳ trước** (tăng / giảm bao nhiêu %) — so sánh với kỳ liền trước có cùng độ dài.
* Quy ước:
  * Tỉ lệ % ≥ 0: **Tăng** so với kỳ trước.
  * Ngược lại: **Giảm** so với kỳ trước.

#### Dự đoán phí sử dụng

* Dự đoán tổng chi phí đến cuối tháng hiện tại, dựa trên xu hướng sử dụng dịch vụ từ đầu tháng đến thời điểm truy cập.
* _(Hiển thị ở chế độ xem theo Sản phẩm.)_

#### Loại tài nguyên cao nhất

* Loại tài nguyên có chi phí cao nhất trong kỳ, kèm giá trị và **tỉ trọng (%)** trên tổng chi phí.
* _(Hiển thị ở chế độ xem theo Loại tài nguyên.)_

#### Phân bổ theo sản phẩm / theo loại

* Bảng xếp hạng tỉ trọng chi phí của từng sản phẩm (chế độ Sản phẩm) hoặc từng loại tài nguyên (chế độ Loại tài nguyên), kèm thanh tỉ lệ trực quan và giá trị chi phí tương ứng.

#### Các thẻ tổng quan ở chế độ Resource ID

| Thẻ                           | Ý nghĩa                                                     |
| ----------------------------- | ----------------------------------------------------------- |
| **Tổng chi phí resources**    | Tổng chi phí của toàn bộ resource trong kỳ.                 |
| **Số resources trong kỳ**     | Số lượng resource phát sinh chi phí trong khoảng thời gian. |
| **Phí trung bình / resource** | Chi phí trung bình của mỗi resource trong kỳ.               |

### 3. Chế độ xem theo Sản phẩm

***

Tổng hợp chi phí theo từng **sản phẩm** (vserver, vstorage, ai base, vmonitor…).

* **Chỉ số tổng quan:** Phí sử dụng trong tháng, Dự đoán phí sử dụng, Phân bổ theo sản phẩm.
* **Biểu đồ "Chi tiết chi phí — theo Sản phẩm":** mỗi màu tương ứng với một sản phẩm.
* **Bảng "Chi tiết chi phí — theo Sản phẩm":**
  * Cột: **Sản phẩm**, **Tổng (VND)** và chi phí từng ngày trong khoảng đã chọn.
  * Dòng đầu **Tổng chi phí** cộng dồn tất cả sản phẩm; mỗi dòng tiếp theo là một sản phẩm.

### 4. Chế độ xem theo Loại tài nguyên

***

Tổng hợp chi phí theo từng **loại tài nguyên** (instance, volume, object-storage, ai-runtime, backup-location, monitor-platform-log, snapshot,...).

* **Chỉ số tổng quan:** Phí sử dụng trong tháng, Loại tài nguyên cao nhất, Phân bổ theo loại.
* **Biểu đồ "Chi tiết chi phí — theo Loại tài nguyên":** mỗi màu tương ứng với một loại tài nguyên.
* **Bảng "Chi tiết chi phí — theo Loại tài nguyên":**
  * Cột: **Loại tài nguyên**, **Tổng (VND)**, **% tổng** (tỉ trọng trên tổng chi phí) và chi phí từng ngày.
  * Dòng đầu **Tổng chi phí**; mỗi dòng tiếp theo là một loại tài nguyên.

### 5. Chế độ xem theo Resource ID

***

Liệt kê chi tiết chi phí đến từng **resource** riêng lẻ — mức xem chi tiết nhất.

* **Chỉ số tổng quan:** Tổng chi phí resources, Số resources trong kỳ, Phí trung bình / resource.
* **Bảng "Danh sách resources trong kỳ":**

| Cột                 | Mô tả                                                            |
| ------------------- | ---------------------------------------------------------------- |
| **Resource ID**     | Mã định danh duy nhất của resource (có thể bấm để xem chi tiết). |
| **Tên resource**    | Tên hiển thị của resource.                                       |
| **Sản phẩm**        | Sản phẩm mà resource thuộc về.                                   |
| **Loại tài nguyên** | Loại tài nguyên của resource.                                    |
| **Tổng (VND)**      | Tổng chi phí của resource trong kỳ.                              |
| **TB hằng ngày**    | Chi phí trung bình mỗi ngày của resource.                        |
| **Ngày bắt đầu**    | Ngày resource bắt đầu phát sinh chi phí trong kỳ.                |

* **Bấm vào một dòng** để xem chi tiết của resource đó.
* Hỗ trợ tùy chọn số dòng hiển thị (**Show**) và phân trang.

### &#x20;6. Biểu đồ và bảng biểu thống kê

***

* **Các loại biểu đồ được hỗ trợ:**
  * **Cột:** so sánh chi phí theo từng mốc thời gian.
  * **Đường:** thể hiện xu hướng chi phí theo thời gian. _(Bổ sung mới)_
  * **Xếp chồng:** so sánh tỉ trọng đóng góp của từng thành phần trên cùng một cột.
* Trục thời gian của biểu đồ và các cột trong bảng được xác định theo **Mức tổng hợp** đã chọn (Hourly / Daily / Weekly / Monthly), trong phạm vi tháng hiện tại.
* Dữ liệu của biểu đồ và bảng luôn đồng bộ với các chỉ số tổng quan và bộ lọc đang áp dụng.

### Một số lưu ý (\*)

* Số liệu tại Cost Explorer là con số **dự đoán / ước lượng**, không chính xác 100%, do:
  * Dữ liệu tại vConsole không phải dữ liệu thời gian thực, có độ trễ cập nhật.
  * Dữ liệu chỉ tính trên các sản phẩm / loại tài nguyên được Cost Explorer hỗ trợ ghi nhận (xem bảng đầu trang).
* Đơn giá dùng để tính là **bảng giá hiện hành**, do đó số liệu phản ánh **gần đúng nhất với người dùng trả sau**. Với **người dùng trả trước**, có thể có sai lệch khi bảng giá thay đổi giữa thời điểm thanh toán và thời điểm truy cập Cost Explorer.
* Chỉ số **Dự đoán phí sử dụng** dựa trên xu hướng sử dụng từ đầu tháng đến hiện tại nên chỉ mang tính tham khảo.

\
\
\
<br>



