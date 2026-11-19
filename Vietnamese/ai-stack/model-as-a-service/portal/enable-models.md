---
description: "Model phải được bật cho tài khoản thì API key mới gọi được. Bạn quản lý việc này ở trang Models của AI Platform."
---

# Bật / tắt model

## Điều kiện để bật

| Điều kiện | Chi tiết |
| --- | --- |
| Có API key | Tạo ít nhất một key trước. Xem [API key](api-keys.md). |
| Đã kích hoạt billing | Tài khoản trả trước phải nạp thêm quota trước khi bật; tài khoản trả sau bật và dùng được ngay. Xem [Billing & giá](../cach-tinh-phi.md). |
| Model còn được cung cấp | Model đã ngừng cung cấp không bật được. |

## Cách bật / tắt

1. Mở [Models](https://aiplatform.console.greennode.ai/models) trong AI Platform.
2. Bấm **Toggle models**. Một popup liệt kê các model; có thể tìm kiếm hoặc lọc theo Provider, Status, Type.
3. Bật/tắt từng model hoặc nhiều model cùng lúc.
4. Lưu thay đổi.

## Tìm model

Trang Models có bộ lọc ở thanh bên trái:

| Bộ lọc | Giá trị |
| --- | --- |
| Provider | BAAI, DeepSeek, Google, GreenNode, Kimi, Minimax, Qwen, Z.ai |
| Model Type | Chat, Messages, Responses, Embedding, Rerank, OCR |
| Use case | Vietnamese, General Tasks, Translation, Research, Finance, Marketing, Technology |

## Trạng thái model

| Trạng thái | Ý nghĩa |
| --- | --- |
| ENABLED | Key của bạn gọi được model. |
| DISABLED | Request bị từ chối với `403 request_denied`. |
| UPDATING | Thay đổi đang được áp dụng trên gateway. |
| ERROR | Thay đổi thất bại. Có thể thử lại ngay; nếu vẫn lỗi hãy liên hệ hỗ trợ. |

## Quy tắc cần biết

* Bật model không bị chặn. Tắt một model vừa mới đổi trạng thái sẽ bị chặn trong 5 phút; portal trả 429 cho đến khi hết thời gian chờ.
* Nếu một model trong lần đổi hàng loạt còn trong thời gian chờ, toàn bộ thay đổi bị từ chối — không áp dụng một phần.
* Tài khoản có thể bị giới hạn số model được bật cùng lúc.
* Khi tài khoản trả trước hết quota hoặc credit hết hạn, toàn bộ model tự động bị tắt.

## Self-host và third-party

Model chạy trên hạ tầng GreenNode (**GreenNode self-host**) hoặc được chuyển tới nhà cung cấp model theo hợp đồng chính thức (**Third-party**). Một số dòng model có cả hai; biến thể qua đối tác có ID kết thúc bằng `-thirdparty` và công tắc bật/tắt riêng.

## Kiểm tra kết quả

`GET /v1/models` chỉ trả các model mà key dùng được nên là cách kiểm tra nhanh nhất sau khi đổi. Gọi model đã tắt sẽ trả `403 request_denied` — “model not allowed for this key”. Xem [Danh sách model](../models/README.md).
