---
description: "BGE-M3 is a multilingual text embedding model from BAAI. It supports more than 100 languages and inputs of up to 8,192 tokens, for semantic search and retrieval-augmented generation (RAG)."
---

# BGE-M3

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `baai/bge-m3` · Loại: Embedding

BGE-M3 is a multilingual text embedding model from BAAI. It supports more than 100 languages and inputs of up to 8,192 tokens, for semantic search and retrieval-augmented generation (RAG).

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 8K tokens |
| Output tối đa | — |
| Đầu vào | text |
| Đầu ra | embeddings |
| Endpoints | `/v1/embeddings` |

## Tham số hỗ trợ

`encoding_format`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/embeddings \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-m3",
    "input": "Hello"
  }'
```
