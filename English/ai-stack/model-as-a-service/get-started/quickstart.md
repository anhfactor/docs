---
description: "Three steps to your first completion."
---

# Quickstart

{% stepper %}
{% step %}
### Get an API key

Create a key in the GreenNode MaaS portal and enable the models you need. Store it in an environment variable:

{% code title="shell" %}
```bash
export GREENNODE_API_KEY="vn-..."
```
{% endcode %}
{% endstep %}
{% step %}
### Point your client at GreenNode

OpenAI SDKs use `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1`. Anthropic SDKs use `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` (no `/v1` — the SDK adds it).
{% endstep %}
{% step %}
### Send a request

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

Response (trimmed):

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
**Notice the reasoning tokens**

Many models think before answering. Above, 248 of 255 output tokens were reasoning. For simple tasks set `"reasoning_effort": "minimal"` or `"low"` — faster and cheaper. See [Reasoning](../features/reasoning.md).
{% endhint %}

## Next steps

* [Stream tokens as they are generated](../api-reference/streaming.md)
* [Let the model call your functions](../features/tool-calling.md)
* [Handle errors and retries](../api-reference/errors.md)
