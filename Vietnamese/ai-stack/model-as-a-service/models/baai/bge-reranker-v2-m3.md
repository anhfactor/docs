---
description: "BGE-Reranker-v2-m3 is a lightweight multilingual cross-encoder reranker from BAAI, built on the BGE-M3 (XLM-RoBERTa) backbone. Given a query and candidate documents it outputs a relevance score for each pair, used to reorder first-stage retrieval results in RAG/search pipelines. Supports 100+ languages, up to 8,192 tokens per query-document pair, and up to 10,000 documents per request."
---

# BGE Reranker v2 m3

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `baai/bge-reranker-v2-m3` · Loại: Rerank

BGE-Reranker-v2-m3 is a lightweight multilingual cross-encoder reranker from BAAI, built on the BGE-M3 (XLM-RoBERTa) backbone. Given a query and candidate documents it outputs a relevance score for each pair, used to reorder first-stage retrieval results in RAG/search pipelines. Supports 100+ languages, up to 8,192 tokens per query-document pair, and up to 10,000 documents per request.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 8K tokens |
| Output tối đa | — |
| Đầu vào | text |
| Đầu ra | rerank |
| Endpoints | `/v1/rerank` |

## Tham số hỗ trợ

`top_n`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/rerank \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-reranker-v2-m3",
    "query": "GreenNode",
    "documents": ["GreenNode MaaS", "Other"]
  }'
```
