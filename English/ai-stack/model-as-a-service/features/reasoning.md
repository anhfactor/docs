---
description: "Most chat models think step by step before answering. You control how much with one setting — the gateway translates it to each model's native format."
---

# Reasoning

## Reasoning modes

The **Reasoning** column of the [Model list](../models/README.md) has three values:

| Mode | Meaning | Field in `GET /v1/models` |
| --- | --- | --- |
| **Always on** | The model always reasons. You can lower the effort but cannot turn it off. | `reasoning.mandatory: true` |
| **On by default** | The model reasons unless you say otherwise; you can disable it or lower the effort. | `mandatory: false`, `default_enabled: true` |
| **Optional** | The model reasons only when you enable it (set `reasoning_effort`). | `mandatory: false`, `default_enabled: false` |

## Setting the effort

| Endpoint | Field | Example |
| --- | --- | --- |
| Chat Completions | `reasoning_effort` | `"reasoning_effort": "low"` |
| Messages | `output_config.effort` | `"output_config": {"effort": "low"}` |
| Responses | `reasoning.effort` | `"reasoning": {"effort": "low"}` |

Accepted values: `none` · `minimal` · `low` · `medium` · `high` · `xhigh` · `max`. Any other value → 400.

* Each model supports a subset (see `reasoning.supported_efforts` on the [Models](../models/README.md) page). A value the model doesn't support natively is mapped to the closest level it does.
* If you don't set an effort, the model's `default_effort` applies — for several models that is `max`, which is slow and token-hungry.
* Models with `reasoning.mandatory: true` always reason; `none` lowers effort to the minimum rather than disabling it.

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

## Reading the reasoning

| Endpoint | Reasoning text | Reasoning token count |
| --- | --- | --- |
| Chat | `message.reasoning_content` (stream: `delta.reasoning_content`) | `usage.completion_tokens_details.reasoning_tokens` (some models, e.g. GLM: `usage.reasoning_tokens`) |
| Messages | `content[type="thinking"].thinking` | `usage.output_tokens_details.reasoning_tokens` |
| Responses | `output[type="reasoning"].summary[].text` | `usage.output_tokens_details.reasoning_tokens` |

## Budgeting tokens

{% hint style="warning" %}
**Reasoning shares the output budget**

`max_tokens` covers reasoning **and** the answer. If reasoning uses it all, you get empty `content` with `finish_reason: "length"`.
{% endhint %}

* Simple extraction, classification, short answers → `minimal` / `low`.
* Coding, analysis, multi-step agents → `medium` / `high`.
* Hard math, competition-style problems → `xhigh` / `max`, with a generous `max_tokens`.
* Leave headroom: `max_tokens` ≥ 4× the answer length you expect.
