---
description: "Qwen3 is the new series of Qwen large language models"
---

# Qwen 3 Reranker 8B

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `qwen/qwen3-reranker-8b` · Loại: Rerank

Qwen3 is the new series of Qwen large language models

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
