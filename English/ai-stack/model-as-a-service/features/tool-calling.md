---
description: "Describe your functions; the model decides when to call them and with which arguments. You run the function and send the result back."
---

# Tool calling

## The loop

1. Send `messages` + `tools`.
2. The response has `finish_reason: "tool_calls"` and `message.tool_calls`.
3. Run each call; append the assistant message and one `role: "tool"` message per call (matching `tool_call_id`).
4. Call again — repeat until `finish_reason` is `stop`.

{% tabs %}
{% tab title="Python" %}
```python
import json

tools = [{
    "type": "function",
    "function": {
        "name": "get_weather",
        "description": "Get current weather for a city",
        "parameters": {
            "type": "object",
            "properties": {"city": {"type": "string"}},
            "required": ["city"],
        },
    },
}]

def get_weather(city):
    return {"city": city, "temp_c": 31, "sky": "sunny"}

messages = [{"role": "user", "content": "What is the weather in Hanoi?"}]
while True:
    resp = client.chat.completions.create(
        model="qwen/qwen3.6-flash", messages=messages, tools=tools,
        tool_choice="auto", reasoning_effort="minimal",
    )
    msg = resp.choices[0].message
    if not msg.tool_calls:
        print(msg.content)
        break
    messages.append(msg)
    for call in msg.tool_calls:
        result = get_weather(**json.loads(call.function.arguments))
        messages.append({"role": "tool", "tool_call_id": call.id,
                         "content": json.dumps(result)})
```
{% endtab %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "reasoning_effort": "minimal",
    "messages": [{"role": "user", "content": "What is the weather in Hanoi?"}],
    "tools": [{
      "type": "function",
      "function": {
        "name": "get_weather",
        "description": "Get current weather for a city",
        "parameters": {"type": "object", "properties": {"city": {"type": "string"}}, "required": ["city"]}
      }
    }],
    "tool_choice": "auto"
  }'
```
{% endtab %}
{% endtabs %}

{% code title="200 OK — choices[0]" %}
```json
{
  "index": 0,
  "message": {
    "role": "assistant",
    "content": "",
    "tool_calls": [{
      "id": "call_529994e21bc148fd89b05252",
      "type": "function",
      "function": { "name": "get_weather", "arguments": "{\"city\": \"Hanoi\"}" }
    }]
  },
  "finish_reason": "tool_calls"
}
```
{% endcode %}

## `tool_choice`

* `"auto"` — the model decides (default).
* `"none"` — never call tools.
* `"required"` — must call at least one tool.
* `{"type":"function","function":{"name":"get_weather"}}` — force a specific tool.

Note: some models (for example `qwen/qwen3.8-flash`) may not honour `"required"` or a named tool and answer in text instead (`finish_reason: stop`). Always check `tool_calls` in the response.

{% hint style="info" %}
Only `function` tools (plus the [web search](web-search.md) server tool) are supported. Other OpenAI built-in tool types such as `file_search`, `code_interpreter` or `custom` do not work: on `/v1/responses` the request returns `400`, on `/v1/chat/completions` the model rejects them. Use `function` tools instead.
{% endhint %}

On Messages use Anthropic's format (`tools[].input_schema`, `tool_use` / `tool_result` blocks); on Responses use `function_call` / `function_call_output` items. See [Parameters](../api-reference/parameters.md).
