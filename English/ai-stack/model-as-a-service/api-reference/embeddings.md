---
description: "Turn text into vectors for search, clustering and RAG. OpenAI-compatible."
---

# Embeddings

**POST** `/v1/embeddings`

## Headers

| Header | Required | Value | Description |
| --- | --- | --- | --- |
| `Authorization` | **Required** | `Bearer <API_KEY>` | Your API key. `Authorization: Bearer`, `x-api-key` and `apikey` are equivalent. Missing → 401 `missing api key`; wrong → 401 `unknown api key`. |
| `Content-Type` | **Required** | `application/json` | The body is JSON, UTF-8. |

## Body parameters

| Parameter | Type | Required | Accepted values | Default | Description |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Required** | baai/bge-m3 · qwen/qwen3-embedding-8b | — | An embedding model enabled for your account. |
| `input` | string \| array | **Required** | one string or an array of strings | — | Each item must fit the model's context: 8,192 tokens for `bge-m3`, 32,768 for `qwen3-embedding-8b`. |
| `encoding_format` | string | Optional | float · base64 | float | Format of the returned vectors. |

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/embeddings \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"model": "baai/bge-m3", "input": ["GreenNode MaaS", "Xin chào"]}'
```
{% endtab %}
{% tab title="Python" %}
```python
result = client.embeddings.create(
    model="baai/bge-m3",
    input=["GreenNode MaaS", "Xin chào"],
)
vectors = [d.embedding for d in result.data]
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
const result = await client.embeddings.create({
  model: "baai/bge-m3",
  input: ["GreenNode MaaS", "Xin chào"],
});
const vectors = result.data.map((d) => d.embedding);
```
{% endtab %}
{% endtabs %}

{% code title="200 OK (vectors trimmed)" %}
```json
{
  "object": "list",
  "model": "bge-m3",
  "data": [
    { "object": "embedding", "index": 0, "embedding": [-0.0391, -0.0097, -0.0426, ...] },
    { "object": "embedding", "index": 1, "embedding": [-0.0487, 0.0204, -0.0590, ...] }
  ],
  "usage": { "prompt_tokens": 11, "total_tokens": 11 }
}
```
{% endcode %}
