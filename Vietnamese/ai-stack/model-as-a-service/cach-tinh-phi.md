---
description: >-
  Tài liệu này mô tả cách tính phí sử dụng MaaS, bao gồm nguyên tắc chung cho
  từng loại model và nguyên tắc riêng cho tài khoản Prepaid và Postpaid.
---

# Cách tính phí

### 1. Tổng quan cách tính phí

MaaS hỗ trợ nhiều loại model khác nhau, và **cách tính phí phụ thuộc vào loại model được sử dụng**.

Đơn giá chi tiết của từng model được hiển thị trực tiếp trên [Portal AI Platform](https://aiplatform.console.greennode.ai/models).

#### Phân loại model theo billing

Hiện tại có **2 nhóm model chính**:

* **Model tính theo tokens**
* **Model tính theo hình ảnh (Image-based models)**

***

### 2. Nguyên tắc chung

#### 2.1. Model tính theo Tokens

Áp dụng cho các model dạng:

* Chat
* Completion
* Embedding
* Rerank
* Speech-to-text / Text-to-speech _(nếu quy đổi sang tokens)_

**Cách tính phí**

* Tokens được chia thành 3 loại:
  * **Input tokens**
  * **Cache tokens** _(nếu có)_
  * **Output tokens**
* Mỗi loại tokens có **đơn giá riêng**

<figure><img src="../../.gitbook/assets/image (756).png" alt=""><figcaption></figcaption></figure>

* Phí được tính theo **đơn vị 1.000.000 tokens**

**Công thức tính phí**

```
Total Cost =
((Input tokens − Cache tokens) / 1,000,000) × Input price
+ (Cache tokens / 1,000,000 × Cache price)
+ (Output tokens / 1,000,000 × Output price)
```

Cache token chỉ được trừ khỏi input token với các model tính phí cache token riêng; với model khác, toàn bộ input token tính theo giá Input.

***

#### 2.2. Model Gen-Image (Tạo hình ảnh)

Áp dụng cho các model tạo ảnh như:

* Text-to-image
* Image-to-image

**Cách tính phí**

Phí được tính dựa trên:

* **Số lượng hình ảnh được tạo**
* **Cấu hình của mỗi hình ảnh**, ví dụ:
  * Resolution (kích thước)
  * Quality
  * Style / Model version

⇒ Mỗi cấu hình hình ảnh sẽ có **đơn giá khác nhau**.

<figure><img src="../../.gitbook/assets/image (760).png" alt=""><figcaption></figcaption></figure>

***

### 3. **Quy Định Chi Tiết Theo Loại Tài Khoản**

#### 3.1. Tài khoản Prepaid

**3.1.1. Nguyên tắc sử dụng**

* Người dùng cần **mua trước user-credit** để sử dụng dịch vụ bằng tính năng Top up credits

<figure><img src="../../.gitbook/assets/image (811).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (820).png" alt=""><figcaption></figcaption></figure>

* Với mỗi lần sử dụng model:
  * Tokens và/hoặc images phát sinh sẽ được:
    * Tính theo **đơn giá tương ứng**
    * **Trừ trực tiếp vào quota user-credit hiện tại**
* Khi **quota = 0**:
  * Tất cả models sẽ bị **disable**
  * Người dùng cần **mua thêm quota** để tiếp tục sử dụng

***

**3.1.2. Thời hạn user-credit**

* **user-credit** có **thời hạn 1 năm**
* Thời hạn được tính theo **ngày mua quota gần nhất**

**Khi user-credit hết hạn**

* Tất cả models sẽ bị **disable**
* Người dùng có thể:
  * **Recover user-credits** tại trang Billing

Sau khi recover:

* Quota user-credits cũ sẽ **bị mất**
* Hệ thống chỉ tính theo **quota user-credits mới**

**Quá hạn recover**

* Nếu **quá 7 ngày** kể từ khi **user-credit** expire:
  * Người dùng cần:
    * Activate billing lại
    * Buy-more user-credits nếu có nhu cầu tiếp tục sử dụng

> Khuyến nghị người dùng **ước lượng trước nhu cầu sử dụng và chủ động buy-more** để tránh gián đoạn dịch vụ khi hết quota hoặc hết hạn credits.\
> &#xNAN;_(Chức năng Quota Alarm đang được phát triển và sẽ cập nhật trong thời gian tới)_

***

#### 3.2. Tài khoản Postpaid

**3.2.1. Nguyên tắc sử dụng**

* **user-credit** có **thời hạn sử dụng vĩnh viễn**
* Người dùng có thể sử dụng model **không cần mua trước quota**
* Usage sẽ được:
  * Ghi nhận theo **thời gian thực**
  * **Tổng hợp và thanh toán vào cuối mỗi tháng**
  *

      <figure><img src="../../.gitbook/assets/image (771).png" alt=""><figcaption></figcaption></figure>

***

### 4. Theo dõi usage

Để xem chi tiết lượng usage đã sử dụng:

* Truy cập trang [**Model Usage**](https://aiplatform.console.greennode.ai/model-usage)
* Cho phép:
  * Chọn **khoảng thời gian cụ thể**
  * Xem chi tiết:
    * Tokens input / output / cache
    * Số lượng hình ảnh đã tạo
    * Chi phí tương ứng
