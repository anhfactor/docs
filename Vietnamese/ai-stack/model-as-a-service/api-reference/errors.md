---
description: "Lỗi do gateway sinh ra có mã máy đọc được trong header x-ai-error-code và trong error.code. Hãy xử lý dựa trên HTTP status và mã lỗi, không dựa vào nội dung message."
---

# Lỗi

## Mã lỗi

| Code | HTTP | Ý nghĩa | Retry? |
| --- | --- | --- | --- |
| `invalid_request` | 400 | Thiếu prompt (`messages` thiếu hoặc rỗng — message "request body doesn't contain valid prompts"), tham số hoặc giá trị không hỗ trợ, `max_tokens` quá lớn, loại nội dung không hỗ trợ, hoặc `model` trong body khác model trên URL riêng của model. | Không — sửa request |
| `request_denied` | 401 | Thiếu API key, key không tồn tại, bị vô hiệu hoặc hết hạn. | Không |
| `request_denied` | 403 | Model chưa được bật cho tài khoản (“model not allowed for this key”). | Không — bật model |
| `request_denied` | 400 | Guardrail an toàn nội dung đã chặn request. Xem [An toàn nội dung](../features/content-safety.md). | Không |
| `request_denied` | 429 | Vượt rate limit của bạn. Message cho biết giới hạn nào và số giây đến lúc reset. Xem [Giới hạn & rate limit](limits.md). | Có, sau khi reset |
| `model_not_found` | 404 | Model ID không tồn tại. ID có dạng `vendor/model`. | Không |
| `rate_limited` | 429 | Nhà cung cấp phía sau model đang giới hạn lưu lượng. | Có, kèm backoff |
| `upstream_error` | 500–504 | Backend của model lỗi. Status là status backend trả về. | Có, kèm backoff |
| `pool_exhausted` | 503 hoặc 529 | Mọi backend của model tạm thời không khả dụng hoặc đã hết công suất. | Có, sau `Retry-After` |
| `guard_unavailable` | 503 | Không truy cập được dịch vụ xác thực key. | Có, kèm backoff |
| `internal_error` | 500 hoặc 503 | Lỗi bất ngờ của gateway, hoặc dịch vụ an toàn nội dung không khả dụng. | Có, vài lần |

{% hint style="warning" %}
**429 có hai mã**

Khi vượt giới hạn **của bạn**, mã là `request_denied`; `rate_limited` nghĩa là nhà cung cấp model đang giới hạn. Hãy retry theo status 429, không theo mã.
{% endhint %}

## Cấu trúc lỗi

Lỗi xác thực, quyền dùng model và rate limit dùng cấu trúc này trên mọi endpoint, kể cả `/v1/messages`:

{% code title="401 / 403 · x-ai-error-code: request_denied" %}
```json
{"error": {"message": "missing api key", "code": "request_denied", "type": "request_denied"}}
{"error": {"message": "unknown api key", "code": "request_denied", "type": "request_denied"}}
{"error": {"message": "model not allowed for this key", "code": "request_denied", "type": "request_denied"}}
```
{% endcode %}

{% code title="404 · x-ai-error-code: model_not_found" %}
```json
{"error": {"message": "The requested model is not found", "type": "not_found_error", "code": "model_not_found"}}
```
{% endcode %}

Lỗi về chính request hoặc từ model theo định dạng của endpoint. `/v1/chat/completions`, `/v1/responses`, `/v1/embeddings`, `/v1/rerank` — định dạng OpenAI:

{% code title="400 · x-ai-error-code: invalid_request" %}
```json
{
  "error": {
    "message": "invalid reasoning_effort value 'banana'; must be one of: minimal, low, medium, high, xhigh, max, none",
    "type": "invalid_request_error",
    "code": "invalid_request"
  }
}
```
{% endcode %}

`/v1/messages` — định dạng Anthropic:

{% code title="400 · x-ai-error-code: invalid_request" %}
```json
{
  "type": "error",
  "error": {
    "type": "invalid_request_error",
    "message": "max_completion_tokens is too large: 10000000.This model supports at most 1048576 completion tokens.",
    "code": "invalid_request"
  }
}
```
{% endcode %}

## Lỗi không có mã

Một số response do tầng proxy trả trước khi request tới model. Chúng không có header `x-ai-error-code` và có body khác, vì vậy hãy xử lý lỗi theo cả HTTP status.

| HTTP | Body | Nguyên nhân và cách xử lý |
| --- | --- | --- |
| 404 | `{"message":"no Route matched with those values", …}` | Sai đường dẫn hoặc HTTP method, hoặc model không tồn tại trong URL riêng của model. Kiểm tra lại URL. |
| 405 | `{"error":{"code":"method_not_allowed", …}}` | `/v1/models` chỉ nhận `GET`. |
| 502 | `{"message":"An invalid response was received from the upstream server", …}` | Trên các endpoint `/v1/…`: gateway không đọc được trường `model` trong body (body không phải JSON hợp lệ, body rỗng, hoặc thiếu `model`) nên không định tuyến được. Gửi body JSON hợp lệ có `model`. Lỗi này không retry được. |
| 504 | `{"message":"The upstream server is timing out", …}` | Model không trả lời trong giới hạn thời gian của request. Dùng streaming hoặc giảm `max_tokens`. Xem [giới hạn](limits.md). |

{% hint style="info" %}
**Đã đối chiếu production**

Các response 401, 404 `model_not_found`, 404 không có route, 405 và 502 ở trên đã được ghi nhận trên gateway production ngày 2026-11-14 và kiểm tra lại ngày 2026-11-18.
{% endhint %}

## Chính sách retry khuyến nghị

Retry 429 và 5xx với exponential backoff kèm jitter, và chờ theo `Retry-After` khi có. Không retry 400, 401, 403, 404 hay 502 do thiếu `model`.

{% tabs %}
{% tab title="Python" %}
```python
import random, time
from openai import OpenAI, APIStatusError

RETRYABLE_STATUS = {429, 500, 502, 503, 504, 529}

def call_with_retry(fn, attempts=4):
    for i in range(attempts):
        try:
            return fn()
        except APIStatusError as e:
            if e.status_code not in RETRYABLE_STATUS or i == attempts - 1:
                raise
            wait = e.response.headers.get("retry-after")
            time.sleep(float(wait) if wait else (2 ** i) + random.random())

# The OpenAI/Anthropic SDKs also retry 429/5xx automatically (max_retries=2 by default).
client = OpenAI(base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1", api_key="...")
completion = call_with_retry(lambda: client.chat.completions.create(
    model="qwen/qwen3.8-flash",
    messages=[{"role": "user", "content": "hi"}],
))
```
{% endtab %}
{% tab title="JavaScript" %}
```typescript
const RETRYABLE_STATUS = new Set([429, 500, 502, 503, 504, 529]);

async function callWithRetry(fn, attempts = 4) {
  for (let i = 0; ; i++) {
    try {
      return await fn();
    } catch (e) {
      if (!RETRYABLE_STATUS.has(e?.status) || i === attempts - 1) throw e;
      const ra = Number(e?.headers?.get?.("retry-after"));
      await new Promise((r) => setTimeout(r, (ra || 2 ** i + Math.random()) * 1000));
    }
  }
}
```
{% endtab %}
{% endtabs %}
