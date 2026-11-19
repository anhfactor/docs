---
description: "Mô tả các hàm của bạn; model tự quyết định khi nào gọi và với tham số nào. Bạn thực thi hàm và gửi kết quả lại cho model."
---

# Tool calling

## Vòng lặp

1. Gửi `messages` + `tools`.
2. Response có `finish_reason: "tool_calls"` và `message.tool_calls`.
3. Thực thi từng lời gọi; thêm message assistant và một message `role: "tool"` cho mỗi lời gọi (khớp `tool_call_id`).
4. Gọi lại — lặp đến khi `finish_reason` là `stop`.

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

* `"auto"` — model tự quyết (mặc định).
* `"none"` — không gọi tool.
* `"required"` — bắt buộc gọi ít nhất một tool.
* `{"type":"function","function":{"name":"get_weather"}}` — buộc gọi một tool cụ thể.

Lưu ý: một số model (ví dụ `qwen/qwen3.8-flash`) có thể không tuân theo `"required"` hoặc tool được chỉ định và vẫn trả lời bằng văn bản (`finish_reason: stop`). Hãy kiểm tra `tool_calls` trong response.

{% hint style="info" %}
Chỉ hỗ trợ tool loại `function` (và server tool [web search](web-search.md)). Các loại tool tích hợp khác của OpenAI như `file_search`, `code_interpreter` hay `custom` không dùng được: trên `/v1/responses` request trả `400`, trên `/v1/chat/completions` model sẽ từ chối. Hãy dùng tool loại `function`.
{% endhint %}

Với Messages dùng định dạng Anthropic (`tools[].input_schema`, block `tool_use` / `tool_result`); với Responses dùng item `function_call` / `function_call_output`. Xem [Tham số](../api-reference/parameters.md).
