---
description: "Qwen3-Reranker-8B is an 8B text reranking model from the Qwen3 family. Given a query and candidate documents it returns a relevance score for each pair, used to reorder retrieval results in search and RAG pipelines."
---

# Qwen 3 Reranker 8B

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3-reranker-8b` · Type: Rerank

Qwen3-Reranker-8B is an 8B text reranking model from the Qwen3 family. Given a query and candidate documents it returns a relevance score for each pair, used to reorder retrieval results in search and RAG pipelines.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 33K tokens |
| Max output | — |
| Input | text |
| Output | rerank |
| Endpoints | `/v1/rerank` |

## Supported parameters

`top_n`

## Example

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
