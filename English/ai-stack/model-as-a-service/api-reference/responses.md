---
description: "OpenAI Responses API, available on every chat model. Used by Codex CLI and the OpenAI SDK's client.responses."
---

# Responses

**POST** `/v1/responses`

## Headers

| Header | Required | Value | Description |
| --- | --- | --- | --- |
| `Authorization` | **Required** | `Bearer <API_KEY>` | Your API key. `Authorization: Bearer`, `x-api-key` and `apikey` are equivalent. Missing → 401 `missing api key`; wrong → 401 `unknown api key`. |
| `Content-Type` | **Required** | `application/json` | The body is JSON, UTF-8. |

## Body parameters

| Parameter | Type | Required | Accepted values | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Required** | a model ID | — | Must be enabled for your account. |
| `input` | string \| array | **Required** | text, or items: `message`, `function_call`, `function_call_output` | — | The full conversation for this turn. Images go in `input_image` parts. |
| `instructions` | string | Optional | — | — | System instructions. |
| `max_output_tokens` | integer | Optional | 1 … the model's max output | per model | Output cap, reasoning included. |
| `reasoning.effort` | string | Optional | none · minimal · low · medium · high · xhigh · max | the model's `default_effort`; if the model declares none, the provider's own default | See [Reasoning](../features/reasoning.md). |
| `tools` | array | Optional | `{type:"function", name, parameters}`, or `{"type":"web_search"}` | — | Function tools and the web search server tool. |
| `tool_choice` | string \| object | Optional | auto · none · required · a named function | auto | Forces or forbids tool calls. |
| `stream` | boolean | Optional | true · false | false | Stream as Responses events. |
| `temperature`<br>`top_p` | number | Optional | 0 – 2 · 0 – 1 | per model | Sampling. |
| `text.format` | object | Optional | json_object · json_schema | — | Structured output. |
| `previous_response_id` | string | Optional | — | — | **Not supported.** The gateway is stateless; send the full conversation in `input` every turn. |

{% hint style="info" %}
**About ranges and defaults**

Ranges follow the API specification the endpoint is compatible with. Whether a given model accepts a parameter is listed in its `supported_parameters` (`GET /v1/models`); a parameter not on that list is ignored (no error). See [Parameters](parameters.md) for how many models support each one.
{% endhint %}

{% hint style="info" %}
The gateway is stateless: send the full conversation in `input` each turn. `previous_response_id` returns `400 invalid_request`. `store`, `background`, `truncation`, `metadata` and `conversation` are ignored, not rejected — a request that relies on them will run without the earlier context.
{% endhint %}

## Example

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/responses \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "input": "Count 1 to 3.",
    "reasoning": {"effort": "low"},
    "max_output_tokens": 200
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
response = client.responses.create(
    model="qwen/qwen3.6-flash",
    input="Count 1 to 3.",
    reasoning={"effort": "low"},
    max_output_tokens=200,
)
print(response.output_text)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
const response = await client.responses.create({
  model: "qwen/qwen3.6-flash",
  input: "Count 1 to 3.",
  reasoning: { effort: "low" },
  max_output_tokens: 200,
});
console.log(response.output_text);
```
{% endtab %}
{% endtabs %}

{% code title="200 OK (trimmed)" %}
```json
{
  "id": "chatcmpl-0e3aa9e8-...",
  "object": "response",
  "status": "completed",
  "model": "qwen3.6-flash",
  "output": [{
    "type": "message",
    "role": "assistant",
    "status": "completed",
    "content": [{ "type": "output_text", "text": "1, 2, 3", "annotations": [] }]
  }],
  "output_text": "1, 2, 3",
  "usage": {
    "input_tokens": 19,
    "input_tokens_details": { "cached_tokens": 0 },
    "output_tokens": 7,
    "output_tokens_details": { "reasoning_tokens": 0 },
    "total_tokens": 26
  }
}
```
{% endcode %}

When the model reasons, a `{"type":"reasoning","summary":[…]}` item precedes the message item.
