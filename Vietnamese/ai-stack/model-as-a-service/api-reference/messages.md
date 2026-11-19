---
description: "Messages API tương thích Anthropic, dùng được với mọi model chat. Phù hợp với Anthropic SDK và Claude Code."
---

# Messages

**POST** `/v1/messages`

## Header

| Header | Bắt buộc | Giá trị | Mô tả |
| --- | --- | --- | --- |
| `x-api-key` | **Bắt buộc** | `<API_KEY>` | API key của bạn. `Authorization: Bearer`, `x-api-key` và `apikey` tương đương nhau. Thiếu → 401 `missing api key`; sai → 401 `unknown api key`. |
| `Content-Type` | **Bắt buộc** | `application/json` | Body là JSON, UTF-8. |

## Tham số body

| Tham số | Kiểu | Bắt buộc | Giá trị nhận | Mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Bắt buộc** | một model ID | — | Phải được bật cho tài khoản. |
| `max_tokens` | integer | **Bắt buộc** | 1 … output tối đa của model | — | Giới hạn output, gồm cả reasoning. |
| `messages` | array | **Bắt buộc** | `role`: user · assistant | — | Các lượt xen kẽ. `content` là chuỗi hoặc các block: `text`, `image`, `tool_use`, `tool_result`, `document` với nguồn dạng text. |
| `system` | string \| array | Tuỳ chọn | — | — | System prompt, dạng chuỗi hoặc các block text. |
| `output_config.effort` | string | Tuỳ chọn | low … max | `default_effort` của model; model không khai báo thì theo mặc định của nhà cung cấp | Mức reasoning. Xem [Reasoning](../features/reasoning.md). |
| `thinking` | object | Tuỳ chọn | `{"type":"enabled","budget_tokens":N}` · `{"type":"disabled"}` | theo model | Điều khiển thinking theo kiểu Anthropic. Một số model (ví dụ `qwen/qwen3.8-flash`) vẫn suy luận khi `disabled`. |
| `stream` | boolean | Tuỳ chọn | true · false | false | Stream theo chuỗi event của Anthropic. |
| `stop_sequences` | array | Tuỳ chọn | các chuỗi | — | Chuỗi dừng. |
| `temperature`<br>`top_p` | number | Tuỳ chọn | 0 – 1 | theo model | Sampling, như API của Anthropic. |
| `tools` | array | Tuỳ chọn | `{name, description, input_schema}`, hoặc server tool `web_search_20250305` | — | Xem [Tool calling](../features/tool-calling.md) và [Tìm kiếm web](../features/web-search.md). |
| `tool_choice` | object | Tuỳ chọn | auto · any · tool · none | auto | Định dạng tool-choice của Anthropic. |

{% hint style="info" %}
**Về khoảng giá trị và mặc định**

Khoảng giá trị theo đặc tả API mà endpoint tương thích. Model có nhận một tham số hay không được liệt kê trong `supported_parameters` (`GET /v1/models`); tham số không có trong danh sách đó bị bỏ qua (không báo lỗi). Xem [Tham số](parameters.md) để biết bao nhiêu model hỗ trợ từng tham số.
{% endhint %}

## Ví dụ

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/messages \
  -H "x-api-key: $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3-flash",
    "max_tokens": 2000,
    "output_config": {"effort": "low"},
    "messages": [{"role": "user", "content": "17*23?"}]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
import os, anthropic

client = anthropic.Anthropic(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn",
    api_key=os.environ["GREENNODE_API_KEY"],
)
message = client.messages.create(
    model="z-ai/glm-5.3-flash",
    max_tokens=2000,
    messages=[{"role": "user", "content": "17*23?"}],
    extra_body={"output_config": {"effort": "low"}},
)
for block in message.content:
    if block.type == "text":
        print(block.text)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
import Anthropic from "@anthropic-ai/sdk";

const client = new Anthropic({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn",
  apiKey: process.env.GREENNODE_API_KEY,
});
const message = await client.messages.create({
  model: "z-ai/glm-5.3-flash",
  max_tokens: 2000,
  messages: [{ role: "user", content: "17*23?" }],
});
console.log(message.content);
```
{% endtab %}
{% endtabs %}

{% code title="200 OK (trimmed)" %}
```json
{
  "id": "874b2793a6034529a53d...",
  "type": "message",
  "role": "assistant",
  "model": "zai-org/GLM-5.3-Flash",
  "content": [
    { "type": "thinking", "thinking": "..." },
    { "type": "text", "text": "17 × 23 = 391" }
  ],
  "stop_reason": "end_turn",
  "usage": {
    "input_tokens": 16,
    "output_tokens": 39,
    "output_tokens_details": { "reasoning_tokens": 3 }
  }
}
```
{% endcode %}

{% hint style="info" %}
Phần suy luận xuất hiện dưới dạng block `thinking` trước block `text`. Đọc block `text` cuối cùng để lấy câu trả lời.
{% endhint %}

{% hint style="warning" %}
**Tài liệu PDF:** block `document` dạng `application/pdf` chỉ được nhận bởi model có `file` trong các loại đầu vào (xem [Danh sách model](../models/README.md)); model khác sẽ từ chối (400). Với các model đó, hãy trích xuất văn bản trước và gửi dưới dạng `document` với `source.type: "text"`.
{% endhint %}
