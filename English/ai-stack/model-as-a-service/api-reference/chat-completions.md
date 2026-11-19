---
description: "OpenAI-compatible chat endpoint. Works with every chat model."
---

# Chat Completions

**POST** `/v1/chat/completions`

## Headers

| Header | Required | Value | Description |
| --- | --- | --- | --- |
| `Authorization` | **Required** | `Bearer <API_KEY>` | Your API key. `Authorization: Bearer`, `x-api-key` and `apikey` are equivalent. Missing → 401 `missing api key`; wrong → 401 `unknown api key`. |
| `Content-Type` | **Required** | `application/json` | The body is JSON, UTF-8. |

## Body parameters

| Parameter | Type | Required | Accepted values | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Required** | a model ID | — | For example `qwen/qwen3.6-flash`. Must be enabled for your account, otherwise 403. |
| `messages` | array | **Required** | `role`: system · user · assistant · tool | — | The conversation so far. `content` is a string, or an array of parts (`text`, `image_url`) for models that accept images. |
| `max_tokens`<br>`max_completion_tokens` | integer | Optional | 1 … the model's max output | per model | Output cap, **reasoning included**. Larger than the model's max output → 400. |
| `stream` | boolean | Optional | true · false | false | Stream the reply as server-sent events. See [Streaming](streaming.md). |
| `stream_options` | object | Optional | `{"include_usage": true}` | — | Adds a final chunk carrying `usage`. |
| `reasoning_effort` | string | Optional | none · minimal · low · medium · high · xhigh · max | the model's `default_effort`; if the model declares none, the provider's own default | How much the model reasons before answering. Any other value → 400. See [Reasoning](../features/reasoning.md). |
| `temperature` | number | Optional | 0 – 2 | per model | Higher is more random. Tune this or `top_p`, not both. |
| `top_p` | number | Optional | 0 – 1 | per model | Nucleus sampling. |
| `stop` | string \| array | Optional | one or more strings | — | Generation stops when one of these strings appears. |
| `tools` | array | Optional | `type: "function"`, or `{"type":"web_search"}` | — | Functions the model may call. Other built-in tool types → 400. See [Tool calling](../features/tool-calling.md). |
| `tool_choice` | string \| object | Optional | auto · none · required · a named function | auto | Forces or forbids tool calls. |
| `parallel_tool_calls` | boolean | Optional | true · false | per model | Allow several tool calls in one turn. |
| `response_format` | object | Optional | json_object · json_schema | — | Structured output. See [Structured outputs](../features/structured-outputs.md). |
| `seed` | integer | Optional | any integer | — | Makes results more repeatable (best effort). |
| `presence_penalty`<br>`frequency_penalty` | number | Optional | -2 – 2 | 0 | Reduce repetition / encourage new topics. |
| `logprobs`<br>`top_logprobs` | boolean \| integer | Optional | — | — | Token log-probabilities, where the model supports them. |
| `top_k`<br>`min_p`<br>`repetition_penalty` | number | Optional | — | — | Only take effect on models that list them in `supported_parameters`; other models ignore them (no error). |

## Example

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "reasoning_effort": "minimal",
    "max_tokens": 1024,
    "messages": [
      {"role": "system", "content": "You are a concise assistant."},
      {"role": "user", "content": "hi"}
    ]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
completion = client.chat.completions.create(
    model="qwen/qwen3.6-flash",
    reasoning_effort="minimal",
    max_tokens=1024,
    messages=[
        {"role": "system", "content": "You are a concise assistant."},
        {"role": "user", "content": "hi"},
    ],
)
print(completion.choices[0].message.content)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
const completion = await client.chat.completions.create({
  model: "qwen/qwen3.6-flash",
  reasoning_effort: "minimal",
  max_tokens: 1024,
  messages: [
    { role: "system", content: "You are a concise assistant." },
    { role: "user", content: "hi" },
  ],
});
console.log(completion.choices[0].message.content);
```
{% endtab %}
{% endtabs %}

{% code title="200 OK" %}
```json
{
  "id": "chatcmpl-c07d7b62-b812-93d6-8336-53b49bf2cd02",
  "object": "chat.completion",
  "created": 1794492772,
  "model": "qwen3.6-flash",
  "choices": [{
    "index": 0,
    "message": { "role": "assistant", "content": "Hello! How can I help you today?" },
    "finish_reason": "stop",
    "logprobs": null
  }],
  "usage": { "prompt_tokens": 13, "completion_tokens": 9, "total_tokens": 22 }
}
```
{% endcode %}

## Response fields

| Field | Description |
| --- | --- |
| `choices[].message.content` | The answer. |
| `choices[].message.reasoning_content` | The model's reasoning text, when it reasons. |
| `choices[].message.tool_calls` | Function calls requested by the model. |
| `choices[].finish_reason` | `stop` · `length` · `tool_calls` · `content_filter` |
| `usage` | [Usage accounting](../features/usage-accounting.md) |
