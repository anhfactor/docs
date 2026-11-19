---
description: "Chuyển văn bản thành vector cho tìm kiếm, phân cụm và RAG. Tương thích OpenAI."
---

# Embeddings

**POST** `/v1/embeddings`

## Header

| Header | Bắt buộc | Giá trị | Mô tả |
| --- | --- | --- | --- |
| `Authorization` | **Bắt buộc** | `Bearer <API_KEY>` | API key của bạn. `Authorization: Bearer`, `x-api-key` và `apikey` tương đương nhau. Thiếu → 401 `missing api key`; sai → 401 `unknown api key`. |
| `Content-Type` | **Bắt buộc** | `application/json` | Body là JSON, UTF-8. |

## Tham số body

| Tham số | Kiểu | Bắt buộc | Giá trị nhận | Mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Bắt buộc** | baai/bge-m3 · qwen/qwen3-embedding-8b | — | Model embedding đã bật cho tài khoản. |
| `input` | string \| array | **Bắt buộc** | một chuỗi hoặc mảng chuỗi | — | Mỗi phần tử phải vừa context của model: 8.192 token với `bge-m3`, 32.768 với `qwen3-embedding-8b`. |
| `encoding_format` | string | Tuỳ chọn | float · base64 | float | Định dạng vector trả về. |

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
