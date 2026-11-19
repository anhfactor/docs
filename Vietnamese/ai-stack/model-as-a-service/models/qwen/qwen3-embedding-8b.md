---
description: "Qwen3-Embedding-8B is an 8B text embedding model from Alibaba, fine-tuned from Qwen3-8B-Base. It produces dense vectors for semantic search, RAG, clustering and similarity matching, with a 32K token context window, user-defined embedding dimensions up to 4096, and support for over 100 languages. Apache 2.0."
---

# Qwen 3 Embedding 8B

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `qwen/qwen3-embedding-8b` · Loại: Embedding

Qwen3-Embedding-8B is an 8B text embedding model from Alibaba, fine-tuned from Qwen3-8B-Base. It produces dense vectors for semantic search, RAG, clustering and similarity matching, with a 32K token context window, user-defined embedding dimensions up to 4096, and support for over 100 languages. Apache 2.0.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 33K tokens |
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
    "model": "qwen/qwen3-embedding-8b",
    "input": "Hello"
  }'
```
