---
description: "Yêu cầu model trả về JSON — JSON hợp lệ bất kỳ, hoặc JSON đúng theo schema của bạn."
---

# Structured outputs

## JSON schema

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3-flash",
    "reasoning_effort": "low",
    "messages": [{"role": "user", "content": "Give me the capital of Vietnam and its population estimate."}],
    "response_format": {
      "type": "json_schema",
      "json_schema": {
        "name": "city",
        "strict": true,
        "schema": {
          "type": "object",
          "properties": {"city": {"type": "string"}, "population": {"type": "integer"}},
          "required": ["city", "population"],
          "additionalProperties": false
        }
      }
    }
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
from pydantic import BaseModel

class City(BaseModel):
    city: str
    population: int

completion = client.chat.completions.parse(
    model="z-ai/glm-5.3-flash",
    reasoning_effort="low",
    messages=[{"role": "user", "content": "Give me the capital of Vietnam and its population estimate."}],
    response_format=City,
)
print(completion.choices[0].message.parsed)
```
{% endtab %}
{% endtabs %}

{% code title="choices[0].message.content" %}
```json
{
  "city": "Hanoi",
  "population": 8400000
}
```
{% endcode %}

## JSON object

`"response_format": {"type": "json_object"}` đảm bảo JSON hợp lệ nhưng không ràng buộc cấu trúc. Một số model yêu cầu trong messages phải có từ "JSON" khi dùng chế độ này.

{% hint style="info" %}
Hỗ trợ trên các model có `response_format` (và `structured_outputs` cho schema strict) trong `supported_parameters`.
{% endhint %}
