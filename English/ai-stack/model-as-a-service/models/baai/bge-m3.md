# BGE-M3

Model ID: `baai/bge-m3` · Type: Embedding

BGE-M3 is a multilingual text embedding model from BAAI. It supports more than 100 languages and inputs of up to 8,192 tokens, for semantic search and retrieval-augmented generation (RAG).

## Specs

| Spec | Value |
| --- | --- |
| Context length | 8K tokens |
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
    "model": "baai/bge-m3",
    "input": "Hello"
  }'
```
