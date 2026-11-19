---
description: "Ba bước để có kết quả đầu tiên."
---

# Bắt đầu nhanh

{% stepper %}
{% step %}
### Lấy API key

Tạo key trong GreenNode MaaS portal và bật các model cần dùng. Lưu key vào biến môi trường:

{% code title="shell" %}
```bash
export GREENNODE_API_KEY="vn-..."
```
{% endcode %}
{% endstep %}
{% step %}
### Trỏ client về GreenNode

OpenAI SDK dùng `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`. Anthropic SDK dùng `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` (không có `/v1` — SDK tự thêm).
{% endstep %}
{% step %}
### Gửi request

{% endstep %}
{% endstepper %}

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "messages": [{"role": "user", "content": "Say hello in one short sentence."}]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
# pip install openai
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key=os.environ["GREENNODE_API_KEY"],
)

completion = client.chat.completions.create(
    model="qwen/qwen3.6-flash",
    messages=[{"role": "user", "content": "Say hello in one short sentence."}],
)
print(completion.choices[0].message.content)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
// npm install openai
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
  apiKey: process.env.GREENNODE_API_KEY,
});

const completion = await client.chat.completions.create({
  model: "qwen/qwen3.6-flash",
  messages: [{ role: "user", content: "Say hello in one short sentence." }],
});
console.log(completion.choices[0].message.content);
```
{% endtab %}
{% tab title="Anthropic SDK" %}
```python
# pip install anthropic
import os
import anthropic

client = anthropic.Anthropic(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn",
    api_key=os.environ["GREENNODE_API_KEY"],
)

message = client.messages.create(
    model="qwen/qwen3.6-flash",
    max_tokens=1024,
    messages=[{"role": "user", "content": "Say hello in one short sentence."}],
)
print(message.content[-1].text)
```
{% endtab %}
{% endtabs %}

Kết quả (rút gọn):

{% code title="200 OK" %}
```json
{
  "id": "chatcmpl-d508d9f7-8f49-9727-806a-1bfe9a81dc95",
  "object": "chat.completion",
  "model": "qwen3.6-flash",
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "reasoning_content": "Thinking Process: ...",
      "content": "Hello!"
    },
    "finish_reason": "stop"
  }],
  "usage": {
    "prompt_tokens": 17,
    "completion_tokens": 255,
    "total_tokens": 272,
    "completion_tokens_details": { "reasoning_tokens": 248 }
  }
}
```
{% endcode %}

{% hint style="success" %}
**Chú ý token suy luận**

Nhiều model "suy nghĩ" trước khi trả lời. Ở ví dụ trên, 248/255 token đầu ra là reasoning. Với tác vụ đơn giản, đặt `"reasoning_effort": "minimal"` hoặc `"low"` — nhanh và rẻ hơn. Xem [Reasoning](../features/reasoning.md).
{% endhint %}

## Tiếp theo

* [Stream token theo thời gian thực](../api-reference/streaming.md)
* [Cho model gọi hàm của bạn](../features/tool-calling.md)
* [Xử lý lỗi và retry](../api-reference/errors.md)
