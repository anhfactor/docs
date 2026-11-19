---
description: "Anthropic-compatible Messages API, available on every chat model. Use it with Anthropic SDKs and Claude Code."
---

# Messages

**POST** `/v1/messages`

## Headers

| Header | Required | Value | Description |
| --- | --- | --- | --- |
| `x-api-key` | **Required** | `<API_KEY>` | Your API key. `Authorization: Bearer`, `x-api-key` and `apikey` are equivalent. Missing → 401 `missing api key`; wrong → 401 `unknown api key`. |
| `Content-Type` | **Required** | `application/json` | The body is JSON, UTF-8. |

## Body parameters

| Parameter | Type | Required | Accepted values | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Required** | a model ID | — | Must be enabled for your account. |
| `max_tokens` | integer | **Required** | 1 … the model's max output | — | Output cap, reasoning included. |
| `messages` | array | **Required** | `role`: user · assistant | — | Alternating turns. `content` is a string or blocks: `text`, `image`, `tool_use`, `tool_result`, `document` with a text source. |
| `system` | string \| array | Optional | — | — | System prompt, as a string or text blocks. |
| `output_config.effort` | string | Optional | low … max | the model's `default_effort`; if the model declares none, the provider's own default | Reasoning effort. See [Reasoning](../features/reasoning.md). |
| `thinking` | object | Optional | `{"type":"enabled","budget_tokens":N}` · `{"type":"disabled"}` | per model | Anthropic-style thinking control. Some models (for example `qwen/qwen3.8-flash`) still think when `disabled`. |
| `stream` | boolean | Optional | true · false | false | Stream as Anthropic events. |
| `stop_sequences` | array | Optional | strings | — | Stop sequences. |
| `temperature`<br>`top_p` | number | Optional | 0 – 1 | per model | Sampling, as in Anthropic's API. |
| `tools` | array | Optional | `{name, description, input_schema}`, or the server tool `web_search_20250305` | — | See [Tool calling](../features/tool-calling.md) and [Web search](../features/web-search.md). |
| `tool_choice` | object | Optional | auto · any · tool · none | auto | Anthropic tool-choice format. |

{% hint style="info" %}
**About ranges and defaults**

Ranges follow the API specification the endpoint is compatible with. Whether a given model accepts a parameter is listed in its `supported_parameters` (`GET /v1/models`); a parameter not on that list is ignored (no error). See [Parameters](parameters.md) for how many models support each one.
{% endhint %}

## Example

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
Reasoning appears as a `thinking` block before the `text` block. Read the last `text` block for the answer.
{% endhint %}

{% hint style="warning" %}
**PDF documents:** `document` blocks with `application/pdf` are accepted only by models that list `file` among their input types (see [Models](../models/README.md)); other models reject them (400). For those, extract the text first and send it as a `document` with `source.type: "text"`.
{% endhint %}
