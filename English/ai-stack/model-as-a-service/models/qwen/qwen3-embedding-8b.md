---
description: "Qwen3-Embedding-8B is an 8B text embedding model from Alibaba, fine-tuned from Qwen3-8B-Base. It produces dense vectors for semantic search, RAG, clustering and similarity matching, with a 32K token context window, user-defined embedding dimensions up to 4096, and support for over 100 languages. Apache 2.0."
---

# Qwen 3 Embedding 8B

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3-embedding-8b` · Type: Embedding

Qwen3-Embedding-8B is an 8B text embedding model from Alibaba, fine-tuned from Qwen3-8B-Base. It produces dense vectors for semantic search, RAG, clustering and similarity matching, with a 32K token context window, user-defined embedding dimensions up to 4096, and support for over 100 languages. Apache 2.0.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 33K tokens |
| Max output | — |
| Input | text |
| Output | embeddings |
| Endpoints | `/v1/embeddings` |

## Supported parameters

`encoding_format`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/embeddings \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3-embedding-8b",
    "input": "Hello"
  }'
```
