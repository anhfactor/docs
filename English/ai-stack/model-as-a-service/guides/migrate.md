---
description: "Existing OpenAI, OpenRouter or Anthropic code needs three changes: the base URL, the API key and the model ID."
---

# Migrate to GreenNode MaaS

## What to change

| Coming from | Base URL | Key header | Model ID |
| --- | --- | --- | --- |
| OpenAI SDK | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `Authorization: Bearer` | `vendor/model` from the Models page |
| OpenRouter | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` | `Authorization: Bearer` | Same `vendor/model` shape; check the exact ID. |
| Anthropic SDK | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` | `x-api-key` | `vendor/model` |

{% tabs %}
{% tab title="Python (OpenAI SDK)" %}
```python
import os
from openai import OpenAI

client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",   # was https://api.openai.com/v1
    api_key=os.environ["GREENNODE_API_KEY"],                        # was OPENAI_API_KEY
    timeout=600,
)
completion = client.chat.completions.create(
    model="z-ai/glm-5.3",                                           # was gpt-…
    reasoning_effort="low",
    messages=[{"role": "user", "content": "Hello"}],
)
```
{% endtab %}
{% tab title="Python (Anthropic SDK)" %}
```python
import os, anthropic

client = anthropic.Anthropic(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn",      # no /v1
    api_key=os.environ["GREENNODE_API_KEY"],
)
message = client.messages.create(
    model="z-ai/glm-5.3",
    max_tokens=2000,
    messages=[{"role": "user", "content": "Hello"}],
)
```
{% endtab %}
{% tab title="Node.js" %}
```
import OpenAI from "openai";

const client = new OpenAI({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
  apiKey: process.env.GREENNODE_API_KEY,
  timeout: 600_000,
});
```
{% endtab %}
{% endtabs %}

## Checklist after switching

1. Call `GET /v1/models` and confirm the models you need are listed. If not, [enable them](../portal/enable-models.md).
2. Set `reasoning_effort` explicitly and raise `max_tokens`; otherwise answers can come back empty with `finish_reason: "length"`.
3. Remove features that are not supported: stored responses, `file_search`, `code_interpreter`, PDF file parts. See [Compatibility](compatibility.md).
4. Switch error handling to the `x-ai-error-code` values. See [Errors](../api-reference/errors.md).
5. Check the default rate limit (10 RPM) against your traffic. See [Rate limits](../portal/rate-limits.md).
6. Raise HTTP client timeouts to at least 10 minutes, or stream.
