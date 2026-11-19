---
description: "Ask the model to return JSON — either any valid JSON object, or JSON that matches your schema."
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

`"response_format": {"type": "json_object"}` guarantees valid JSON but no particular shape. Some models require the word "JSON" to appear in your messages when using this mode.

{% hint style="info" %}
Supported on models that list `response_format` (and `structured_outputs` for strict schema) in `supported_parameters`.
{% endhint %}
