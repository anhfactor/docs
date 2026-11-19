---
description: "Cách giới hạn được báo trên mỗi response, lỗi rate limit trông ra sao, và giới hạn kích thước, thời gian của một request."
---

# Giới hạn & rate limit

{% hint style="info" %}
**Giới hạn mặc định**

Mỗi tài khoản khởi đầu với 10 request và 1.000.000 token mỗi phút trên từng model (đếm riêng từng model); mọi API key của tài khoản dùng chung bộ đếm. Xem [Rate limit](../portal/rate-limits.md) để biết mặc định và cách đề nghị tăng.
{% endhint %}

## Header rate limit

Mỗi giới hạn áp dụng cho request được báo bằng ba header, đặt tên theo dạng `x-ratelimit-{limit|remaining|reset}-{scope}-{dimension}-{window}`:

{% code title="response headers" %}
```
x-ratelimit-limit-model-rpm-minute: 10
x-ratelimit-remaining-model-rpm-minute: 7
x-ratelimit-reset-model-rpm-minute: 41
```
{% endcode %}

| Thành phần | Giá trị | Ý nghĩa |
| --- | --- | --- |
| `scope` | `model` · `tenant` · `key` · `key_model` · `group` · `group_model` | Đối tượng tính giới hạn: `model` là tài khoản của bạn trên model này, `tenant` là cả tài khoản, `key` là một API key. |
| `dimension` | `rpm` · `tpm` | `rpm` đếm request, `tpm` đếm token — trong cửa sổ đi kèm. Giới hạn request theo ngày là `rpm-day`. |
| `window` | `second` · `minute` · `hour` · `day` · `month` | Độ dài cửa sổ. Cửa sổ ngày và tháng reset lúc 00:00 (UTC+7). |
| `reset` | giây | Số giây đến khi cửa sổ reset. |

## Khi vượt giới hạn

{% code title="429 · x-ai-error-code: request_denied" %}
```json
{"error": {"message": "model rpm limit exceeded (10/10), resets in 41s", "type": "request_denied", "code": "request_denied"}}
```
{% endcode %}

* Message cho biết scope và dimension bị vượt cùng số giây đến lúc reset.
* `Retry-After` được gửi khi một cửa sổ đã hết. Nếu không có, hãy chờ theo giá trị `x-ratelimit-reset-*` nhỏ nhất.
* 429 với mã `rate_limited` đến từ nhà cung cấp model, không phải giới hạn của bạn. Retry kèm backoff.

## Giới hạn request

| Giới hạn | Giá trị | Khi vượt |
| --- | --- | --- |
| Kích thước body | 50 MB | `400 invalid_request`, `413` hoặc `502` tuỳ endpoint |
| Token vào + ra | `context_length` của model | `400 invalid_request` |
| Token đầu ra | `max_completion_tokens` của model | `400 invalid_request` |
| Thời lượng request trên `/v1/…` | 10 phút không có dữ liệu từ model | `504` không có mã |

Với các lần sinh dài hãy dùng [streaming](streaming.md): giới hạn thời gian tính cho khoảng chờ giữa các chunk, không tính cho toàn bộ response.

## Response header

| Header | Mô tả |
| --- | --- |
| `x-kong-request-id` | ID duy nhất của request, có trên mọi response. Hãy ghi log và cung cấp khi liên hệ hỗ trợ. |
| `x-ai-error-code` | Mã lỗi, có trên lỗi do gateway sinh ra. Xem [Lỗi](errors.md). |
| `Retry-After` | Số giây cần chờ trước khi retry; có trên một số response 429 và 503. |
| `x-ratelimit-*` | Các giới hạn áp dụng cho request (ở trên). |
| `x-kong-upstream-latency` | Thời gian (ms) chờ model xử lý. Có trên response đã tới model. |
| `x-kong-proxy-latency` | Thời gian (ms) gateway xử lý. Có trên response đã tới model. |
| `x-kong-response-latency` | Thời gian (ms) tạo response do chính gateway sinh ra (ví dụ 401). |
