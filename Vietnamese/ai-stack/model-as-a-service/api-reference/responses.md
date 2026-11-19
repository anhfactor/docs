---
description: "OpenAI Responses API, dùng được với mọi model chat. Được dùng bởi Codex CLI và client.responses của OpenAI SDK."
---

# Responses

**POST** `/v1/responses`

## Header

| Header | Bắt buộc | Giá trị | Mô tả |
| --- | --- | --- | --- |
| `Authorization` | **Bắt buộc** | `Bearer <API_KEY>` | API key của bạn. `Authorization: Bearer`, `x-api-key` và `apikey` tương đương nhau. Thiếu → 401 `missing api key`; sai → 401 `unknown api key`. |
| `Content-Type` | **Bắt buộc** | `application/json` | Body là JSON, UTF-8. |

## Tham số body

| Tham số | Kiểu | Bắt buộc | Giá trị nhận | Mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Bắt buộc** | một model ID | — | Phải được bật cho tài khoản. |
| `input` | string \| array | **Bắt buộc** | text, hoặc các item: `message`, `function_call`, `function_call_output` | — | Toàn bộ hội thoại cho lượt này. Ảnh đặt trong phần `input_image`. |
| `instructions` | string | Tuỳ chọn | — | — | Chỉ dẫn hệ thống. |
| `max_output_tokens` | integer | Tuỳ chọn | 1 … output tối đa của model | theo model | Giới hạn output, gồm cả reasoning. |
| `reasoning.effort` | string | Tuỳ chọn | none · minimal · low · medium · high · xhigh · max | `default_effort` của model; model không khai báo thì theo mặc định của nhà cung cấp | Xem [Reasoning](../features/reasoning.md). |
| `tools` | array | Tuỳ chọn | `{type:"function", name, parameters}`, hoặc `{"type":"web_search"}` | — | Function tool và server tool tìm kiếm web. |
| `tool_choice` | string \| object | Tuỳ chọn | auto · none · required · một hàm cụ thể | auto | Bắt buộc hoặc cấm gọi tool. |
| `stream` | boolean | Tuỳ chọn | true · false | false | Stream theo chuỗi event của Responses. |
| `temperature`<br>`top_p` | number | Tuỳ chọn | 0 – 2 · 0 – 1 | theo model | Sampling. |
| `text.format` | object | Tuỳ chọn | json_object · json_schema | — | Output có cấu trúc. |
| `previous_response_id` | string | Tuỳ chọn | — | — | **Không hỗ trợ.** Gateway không lưu trạng thái; hãy gửi toàn bộ hội thoại trong `input` ở mỗi lượt. |

{% hint style="info" %}
**Về khoảng giá trị và mặc định**

Khoảng giá trị theo đặc tả API mà endpoint tương thích. Model có nhận một tham số hay không được liệt kê trong `supported_parameters` (`GET /v1/models`); tham số không có trong danh sách đó bị bỏ qua (không báo lỗi). Xem [Tham số](parameters.md) để biết bao nhiêu model hỗ trợ từng tham số.
{% endhint %}

{% hint style="info" %}
Gateway không lưu trạng thái: gửi toàn bộ hội thoại trong `input` ở mỗi lượt. `previous_response_id` trả `400 invalid_request`. `store`, `background`, `truncation`, `metadata` và `conversation` bị bỏ qua chứ không bị từ chối — request dựa vào chúng sẽ chạy mà không có ngữ cảnh trước đó.
{% endhint %}

## Ví dụ

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

Khi model suy luận, một item `{"type":"reasoning","summary":[…]}` xuất hiện trước item message.
