---
description: "Qwen3 is the new series of Qwen large language models"
---

# Qwen 3 Reranker 8B

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3-reranker-8b` · Type: Rerank

Qwen3 is the new series of Qwen large language models

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
