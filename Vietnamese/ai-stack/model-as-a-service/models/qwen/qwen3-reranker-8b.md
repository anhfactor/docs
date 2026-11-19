# Qwen 3 Reranker 8B

Model ID: `qwen/qwen3-reranker-8b` · Loại: Rerank

Qwen3-Reranker-8B is an 8B text reranking model from the Qwen3 family. Given a query and candidate documents it returns a relevance score for each pair, used to reorder retrieval results in search and RAG pipelines.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 33K tokens |
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
    "model": "qwen/qwen3-reranker-8b",
    "query": "GreenNode",
    "documents": ["GreenNode MaaS", "Other"]
  }'
```
