---
description: "Mọi client tương thích OpenAI hoặc Anthropic đều dùng được. Chỉ cần đặt base URL và API key."
---

# SDK & framework

| Client | Base URL |
| --- | --- |
| Tương thích OpenAI | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1` |
| Tương thích Anthropic | `https://maas-llm-aiplatform-hcm.api.vngcloud.vn` |

## OpenAI SDK

{% tabs %}
{% tab title="Python" %}
```python
import os
from openai import OpenAI
client = OpenAI(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key=os.environ["GREENNODE_API_KEY"],
    timeout=600,
)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
import OpenAI from "openai";
const client = new OpenAI({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
  apiKey: process.env.GREENNODE_API_KEY,
  timeout: 600_000,
});
```
{% endtab %}
{% endtabs %}

## Anthropic SDK

{% tabs %}
{% tab title="Python" %}
```python
import os
import anthropic
client = anthropic.Anthropic(
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn",
    api_key=os.environ["GREENNODE_API_KEY"],
)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
import Anthropic from "@anthropic-ai/sdk";
const client = new Anthropic({
  baseURL: "https://maas-llm-aiplatform-hcm.api.vngcloud.vn",
  apiKey: process.env.GREENNODE_API_KEY,
});
```
{% endtab %}
{% endtabs %}

## LangChain

```python
# pip install langchain-openai
import os
from langchain_openai import ChatOpenAI

llm = ChatOpenAI(
    model="z-ai/glm-5.3",
    base_url="https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
    api_key=os.environ["GREENNODE_API_KEY"],
    reasoning_effort="low",
)
print(llm.invoke("Xin chào!").content)
```
