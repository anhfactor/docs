---
description: "Hầu hết model chat suy luận từng bước trước khi trả lời. Bạn điều chỉnh mức độ bằng một thiết lập — gateway tự chuyển sang định dạng gốc của từng model."
---

# Reasoning

## Trạng thái reasoning của model

Cột **Reasoning** trong [Danh sách model](../models/README.md) có ba giá trị:

| Trạng thái | Ý nghĩa | Trường trong `GET /v1/models` |
| --- | --- | --- |
| **Luôn bật** | Model luôn suy luận. Bạn có thể hạ mức effort nhưng không tắt được. | `reasoning.mandatory: true` |
| **Mặc định bật** | Model suy luận nếu bạn không chỉ định gì; có thể tắt hoặc hạ effort. | `mandatory: false`, `default_enabled: true` |
| **Tùy chọn** | Model chỉ suy luận khi bạn bật (đặt `reasoning_effort`). | `mandatory: false`, `default_enabled: false` |

## Đặt mức effort

| Endpoint | Trường | Ví dụ |
| --- | --- | --- |
| Chat Completions | `reasoning_effort` | `"reasoning_effort": "low"` |
| Messages | `output_config.effort` | `"output_config": {"effort": "low"}` |
| Responses | `reasoning.effort` | `"reasoning": {"effort": "low"}` |

Giá trị hợp lệ: `none` · `minimal` · `low` · `medium` · `high` · `xhigh` · `max`. Giá trị khác → 400.

* Mỗi model hỗ trợ một tập con (xem `reasoning.supported_efforts` ở trang [Danh sách model](../models/README.md)). Giá trị model không hỗ trợ trực tiếp sẽ được ánh xạ sang mức gần nhất.
* Nếu không đặt effort, mức `default_effort` của model được dùng — với nhiều model đó là `max`, chậm và tốn token.
* Model có `reasoning.mandatory: true` luôn suy luận; `none` chỉ hạ effort xuống mức thấp nhất chứ không tắt hẳn.

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3-flash",
    "reasoning_effort": "low",
    "max_tokens": 2000,
    "messages": [{"role": "user", "content": "What is 17*23? Answer with the number only."}]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
completion = client.chat.completions.create(
    model="z-ai/glm-5.3-flash",
    reasoning_effort="low",
    max_tokens=2000,
    messages=[{"role": "user", "content": "What is 17*23? Answer with the number only."}],
)
msg = completion.choices[0].message
print(msg.content)                                   # "391"
print(getattr(msg, "reasoning_content", None))       # reasoning text, if any
```
{% endtab %}
{% endtabs %}

## Đọc nội dung suy luận

| Endpoint | Nội dung suy luận | Số token suy luận |
| --- | --- | --- |
| Chat | `message.reasoning_content` (stream: `delta.reasoning_content`) | `usage.completion_tokens_details.reasoning_tokens` (một số model, ví dụ GLM: `usage.reasoning_tokens`) |
| Messages | `content[type="thinking"].thinking` | `usage.output_tokens_details.reasoning_tokens` |
| Responses | `output[type="reasoning"].summary[].text` | `usage.output_tokens_details.reasoning_tokens` |

## Tính ngân sách token

{% hint style="warning" %}
**Reasoning dùng chung ngân sách đầu ra**

`max_tokens` bao gồm cả reasoning **và** câu trả lời. Nếu reasoning dùng hết, bạn nhận `content` rỗng với `finish_reason: "length"`.
{% endhint %}

* Trích xuất, phân loại, trả lời ngắn → `minimal` / `low`.
* Lập trình, phân tích, agent nhiều bước → `medium` / `high`.
* Toán khó, bài toán dạng thi đấu → `xhigh` / `max`, kèm `max_tokens` rộng rãi.
* Chừa dư: `max_tokens` ≥ 4 lần độ dài câu trả lời mong đợi.
