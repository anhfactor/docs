---
description: "Endpoint chat tương thích OpenAI. Dùng được với mọi model chat."
---

# Chat Completions

**POST** `/v1/chat/completions`

## Header

| Header | Bắt buộc | Giá trị | Mô tả |
| --- | --- | --- | --- |
| `Authorization` | **Bắt buộc** | `Bearer <API_KEY>` | API key của bạn. `Authorization: Bearer`, `x-api-key` và `apikey` tương đương nhau. Thiếu → 401 `missing api key`; sai → 401 `unknown api key`. |
| `Content-Type` | **Bắt buộc** | `application/json` | Body là JSON, UTF-8. |

## Tham số body

| Tham số | Kiểu | Bắt buộc | Giá trị nhận | Mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Bắt buộc** | một model ID | — | Ví dụ `qwen/qwen3.6-flash`. Phải được bật cho tài khoản, nếu không sẽ lỗi 403. |
| `messages` | array | **Bắt buộc** | `role`: system · user · assistant · tool | — | Hội thoại tính đến hiện tại. `content` là chuỗi, hoặc mảng các phần (`text`, `image_url`) với model nhận ảnh. |
| `max_tokens`<br>`max_completion_tokens` | integer | Tuỳ chọn | 1 … output tối đa của model | theo model | Giới hạn output, **gồm cả reasoning**. Lớn hơn output tối đa của model → 400. |
| `stream` | boolean | Tuỳ chọn | true · false | false | Trả kết quả dạng server-sent events. Xem [Streaming](streaming.md). |
| `stream_options` | object | Tuỳ chọn | `{"include_usage": true}` | — | Thêm chunk cuối chứa `usage`. |
| `reasoning_effort` | string | Tuỳ chọn | none · minimal · low · medium · high · xhigh · max | `default_effort` của model; model không khai báo thì theo mặc định của nhà cung cấp | Mức suy luận trước khi trả lời. Giá trị khác → 400. Xem [Reasoning](../features/reasoning.md). |
| `temperature` | number | Tuỳ chọn | 0 – 2 | theo model | Càng cao càng ngẫu nhiên. Chỉnh tham số này hoặc `top_p`, không chỉnh cả hai. |
| `top_p` | number | Tuỳ chọn | 0 – 1 | theo model | Nucleus sampling. |
| `stop` | string \| array | Tuỳ chọn | một hoặc nhiều chuỗi | — | Dừng sinh khi gặp một trong các chuỗi này. |
| `tools` | array | Tuỳ chọn | `type: "function"`, hoặc `{"type":"web_search"}` | — | Các hàm model được phép gọi. Loại tool dựng sẵn khác → 400. Xem [Tool calling](../features/tool-calling.md). |
| `tool_choice` | string \| object | Tuỳ chọn | auto · none · required · một hàm cụ thể | auto | Bắt buộc hoặc cấm gọi tool. |
| `parallel_tool_calls` | boolean | Tuỳ chọn | true · false | theo model | Cho phép nhiều lần gọi tool trong một lượt. |
| `response_format` | object | Tuỳ chọn | json_object · json_schema | — | Output có cấu trúc. Xem [Structured outputs](../features/structured-outputs.md). |
| `seed` | integer | Tuỳ chọn | số nguyên bất kỳ | — | Giúp kết quả lặp lại ổn định hơn (không đảm bảo tuyệt đối). |
| `presence_penalty`<br>`frequency_penalty` | number | Tuỳ chọn | -2 – 2 | 0 | Giảm lặp từ / khuyến khích chủ đề mới. |
| `logprobs`<br>`top_logprobs` | boolean \| integer | Tuỳ chọn | — | — | Log-probability của token, với model có hỗ trợ. |
| `top_k`<br>`min_p`<br>`repetition_penalty` | number | Tuỳ chọn | — | — | Chỉ có tác dụng ở model có liệt kê trong `supported_parameters`; model khác bỏ qua (không báo lỗi). |

## Ví dụ

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

## Các trường response

| Trường | Mô tả |
| --- | --- |
| `choices[].message.content` | Câu trả lời. |
| `choices[].message.reasoning_content` | Nội dung suy luận của model (nếu có). |
| `choices[].message.tool_calls` | Các lời gọi hàm model yêu cầu. |
| `choices[].finish_reason` | `stop` · `length` · `tool_calls` · `content_filter` |
| `usage` | [Usage accounting](../features/usage-accounting.md) |
