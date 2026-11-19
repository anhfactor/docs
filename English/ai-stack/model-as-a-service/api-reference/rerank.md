---
description: "Score documents by relevance to a query — typically the second stage of a RAG pipeline, after vector search."
---

# Rerank

**POST** `/v1/rerank`

## Headers

| Header | Required | Value | Description |
| --- | --- | --- | --- |
| `Authorization` | **Required** | `Bearer <API_KEY>` | Your API key. `Authorization: Bearer`, `x-api-key` and `apikey` are equivalent. Missing → 401 `missing api key`; wrong → 401 `unknown api key`. |
| `Content-Type` | **Required** | `application/json` | The body is JSON, UTF-8. |

## Body parameters

| Parameter | Type | Required | Accepted values | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Required** | baai/bge-reranker-v2-m3 · qwen/qwen3-reranker-8b | — | A rerank model enabled for your account. |
| `query` | string | **Required** | — | — | The search query. |
| `documents` | array | **Required** | array of strings | — | The candidate passages to score. |
| `top_n` | integer | Optional | ≥ 1 | all documents | Return only the N best documents. |

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/rerank \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-reranker-v2-m3",
    "query": "What is the capital of Vietnam?",
    "documents": [
      "Hanoi is the capital of Vietnam.",
      "Ho Chi Minh City is the largest city.",
      "Paris is in France."
    ],
    "top_n": 2
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
import os, requests

r = requests.post(
    "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/rerank",
    headers={"Authorization": f"Bearer {os.environ['GREENNODE_API_KEY']}"},
    json={
        "model": "baai/bge-reranker-v2-m3",
        "query": "What is the capital of Vietnam?",
        "documents": ["Hanoi is the capital of Vietnam.",
                      "Ho Chi Minh City is the largest city.",
                      "Paris is in France."],
        "top_n": 2,
    },
    timeout=60,
)
for item in r.json()["results"]:
    print(item["index"], round(item["relevance_score"], 3))
```
{% endtab %}
{% endtabs %}

{% code title="200 OK" %}
```json
{
  "model": "bge-reranker-v2-m3",
  "results": [
    { "index": 0, "relevance_score": 0.99984, "document": { "text": "Hanoi is the capital of Vietnam." } },
    { "index": 1, "relevance_score": 0.54622, "document": { "text": "Ho Chi Minh City is the largest city." } }
  ],
  "usage": { "prompt_tokens": 55, "total_tokens": 55 }
}
```
{% endcode %}

`index` refers to the position in your `documents` array. Results are sorted by `relevance_score`, highest first.
