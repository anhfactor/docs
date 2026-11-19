---
description: "Code đang dùng OpenAI, OpenRouter hoặc Anthropic chỉ cần đổi ba thứ: base URL, API key và model ID."
---

# Chuyển sang GreenNode MaaS

## Cần đổi gì

| Chuyển từ | Base URL | Header chứa key | Model ID |
| --- | --- | --- | --- |
| OpenAI SDK | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `Authorization: Bearer` | `vendor/model` lấy ở trang Danh sách model |
| OpenRouter | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `Authorization: Bearer` | Cùng dạng `vendor/model`; kiểm tra lại ID chính xác. |
| Anthropic SDK | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `x-api-key` | `vendor/model` |

{% tabs %}
{% tab title="Python (OpenAI SDK)" %}
```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",   # was https://api.openai.com/v1
    api_key=os.environ["GREENNODE_API_KEY"],                        # was OPENAI_API_KEY
    timeout=600,
)
completion = client.chat.completions.create(
    model="z-ai/glm-5.3",                                           # was gpt-…
    reasoning_effort="low",
    messages=[{"role": "user", "content": "Hello"}],
)
```
{% endtab %}
{% tab title="Python (Anthropic SDK)" %}
```python
import os, anthropic

client = anthropic.Anthropic(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn",      # no /v1
    api_key=os.environ["GREENNODE_API_KEY"],
)
message = client.messages.create(
    model="z-ai/glm-5.3",
    max_tokens=2000,
    messages=[{"role": "user", "content": "Hello"}],
)
```
{% endtab %}
{% tab title="Node.js" %}
```
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
  apiKey: process.env.GREENNODE_API_KEY,
  timeout: 600_000,
});
```
{% endtab %}
{% endtabs %}

## Kiểm tra sau khi chuyển

1. Gọi `GET /v1/models` và xác nhận có các model cần dùng. Nếu chưa có, hãy [bật model](../portal/enable-models.md).
2. Đặt `reasoning_effort` rõ ràng và tăng `max_tokens`; nếu không câu trả lời có thể rỗng với `finish_reason: "length"`.
3. Bỏ các tính năng chưa hỗ trợ: lưu response, `file_search`, `code_interpreter`, phần file PDF. Xem [Tương thích](compatibility.md).
4. Chuyển xử lý lỗi sang các giá trị `x-ai-error-code`. Xem [Lỗi](../api-reference/errors.md).
5. Đối chiếu rate limit mặc định (10 RPM) với lưu lượng của bạn. Xem [Rate limit](../portal/rate-limits.md).
6. Tăng timeout của HTTP client lên ít nhất 10 phút, hoặc dùng streaming.
