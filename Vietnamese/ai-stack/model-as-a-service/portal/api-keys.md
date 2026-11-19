---
description: "API key định danh tài khoản của bạn trong mọi request MaaS. Bạn cần có key trước khi bật hoặc gọi bất kỳ model nào."
---

# API key

## Tạo API key

1. Đăng nhập [AI Platform](https://aiplatform.console.greennode.ai) và mở mục **API Keys**.
2. Bấm **Create an API key**.
3. Nhập **API Key Name**: không bắt đầu hoặc kết thúc bằng dấu gạch ngang (`-`) và không trùng tên key đã có. Có thể chọn **Set as default** để đặt làm key mặc định.
4. Bấm **Create API key**. Key xuất hiện trong danh sách.

{% hint style="info" %}
**Giới hạn**

Mặc định mỗi tài khoản có tối đa 50 API key. Tạo thêm sẽ báo “API key limit exceeded”. Cần nhiều hơn, hãy [liên hệ hỗ trợ](../help/support.md). Mọi key của một tài khoản dùng chung danh sách model đã bật và chung bộ đếm rate limit.
{% endhint %}

## Xem hoặc xoá key

| Thao tác | Cách làm |
| --- | --- |
| Xem / sao chép | Bấm ︙ ở cột **Actions** → **View API Key**. |
| Xoá | Bấm ︙ → **Delete API Key** và xác nhận. Request dùng key đó sẽ lỗi 401. |

## Gửi key trong request

| Header | Client thường dùng |
| --- | --- |
| `Authorization: Bearer <API_KEY>` | OpenAI SDK, curl |
| `x-api-key: <API_KEY>` | Anthropic SDK, Claude Code |

{% code title="shell" %}
```bash
export GREENNODE_API_KEY="<your API key>"

curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer $GREENNODE_API_KEY"
```
{% endcode %}

## Lỗi liên quan đến key

Tất cả response dưới đây đều kèm header `x-ai-error-code: request_denied`.

| HTTP | Nội dung | Nguyên nhân và cách xử lý |
| --- | --- | --- |
| 401 | `{"error":{"message":"missing api key","code":"request_denied","type":"request_denied"}}` | Không gửi header chứa key. Thêm một trong các header ở trên. |
| 401 | `{"error":{"message":"unknown api key","code":"request_denied","type":"request_denied"}}` | Key sai hoặc đã bị xoá. Sao chép lại từ portal hoặc tạo key mới. |
| 403 | `{"error":{"message":"model not allowed for this key","code":"request_denied","type":"request_denied"}}` | Model chưa được bật cho tài khoản. Xem [Bật / tắt model](enable-models.md). |

## Xoay vòng key không gián đoạn

1. Tạo key mới. Đặt tên có ngày, ví dụ `backend-2026-11`, để dễ phân biệt.
2. Triển khai key mới cho ứng dụng và xác nhận request chạy được với key này.
3. Xoá key cũ. Request còn dùng key cũ sẽ lỗi `401` “unknown api key”.

Dùng mỗi ứng dụng hoặc môi trường một key, để khi xoay vòng hay thu hồi một key thì các key khác không bị ảnh hưởng. Các key cùng tài khoản dùng chung model đã bật, bộ đếm rate limit và billing.

## Khi key bị lộ

1. Xoá key trên portal ngay. Đây là cách duy nhất để thu hồi key.
2. Tạo key thay thế và triển khai.
3. Mở **Model Usage** và kiểm tra mức dùng lạ trong khoảng thời gian key bị lộ.
4. Gỡ key khỏi nơi bị lộ (lịch sử repository, log, chat) và liên hệ hỗ trợ nếu thấy khoản phí bất thường.

## Giữ key an toàn

* Không đặt key trong code chạy trên trình duyệt hay mobile. Gọi MaaS từ backend.
* Lưu key trong biến môi trường hoặc secret manager, không lưu trong mã nguồn.
* Nếu key bị lộ, xoá key trên portal và tạo key mới.
* Không gửi key cho bộ phận hỗ trợ. Hãy gửi request ID.
