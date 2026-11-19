---
description: "Chấm điểm mức độ liên quan của tài liệu với câu hỏi — thường là bước thứ hai trong RAG, sau tìm kiếm vector."
---

# Rerank

**POST** `/v1/rerank`

## Header

| Header | Bắt buộc | Giá trị | Mô tả |
| --- | --- | --- | --- |
| `Authorization` | **Bắt buộc** | `Bearer <API_KEY>` | API key của bạn. `Authorization: Bearer`, `x-api-key` và `apikey` tương đương nhau. Thiếu → 401 `missing api key`; sai → 401 `unknown api key`. |
| `Content-Type` | **Bắt buộc** | `application/json` | Body là JSON, UTF-8. |

## Tham số body

| Tham số | Kiểu | Bắt buộc | Giá trị nhận | Mặc định | Mô tả |
| --- | --- | --- | --- | --- | --- |
| `model` | string | **Bắt buộc** | baai/bge-reranker-v2-m3 · qwen/qwen3-reranker-8b | — | Model rerank đã bật cho tài khoản. |
| `query` | string | **Bắt buộc** | — | — | Câu truy vấn. |
| `documents` | array | **Bắt buộc** | mảng chuỗi | — | Các đoạn văn ứng viên cần chấm điểm. |
| `top_n` | integer | Tuỳ chọn | ≥ 1 | toàn bộ tài liệu | Chỉ trả N tài liệu tốt nhất. |

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/rerank \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "baai/bge-reranker-v2-m3",
    "query": "What is the capital of Vietnam?",
    "documents": [
      "Hanoi is the capital of Vietnam.",
      "Ho Chi Minh City is the largest city.",
      "Paris is in France."
    ],
    "top_n": 2
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
import os, requests

r = requests.post(
    "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/rerank",
    headers={"Authorization": f"Bearer {os.environ['GREENNODE_API_KEY']}"},
    json={
        "model": "baai/bge-reranker-v2-m3",
        "query": "What is the capital of Vietnam?",
        "documents": ["Hanoi is the capital of Vietnam.",
                      "Ho Chi Minh City is the largest city.",
                      "Paris is in France."],
        "top_n": 2,
    },
    timeout=60,
)
for item in r.json()["results"]:
    print(item["index"], round(item["relevance_score"], 3))
```
{% endtab %}
{% endtabs %}

{% code title="200 OK" %}
```json
{
  "model": "bge-reranker-v2-m3",
  "results": [
    { "index": 0, "relevance_score": 0.99984, "document": { "text": "Hanoi is the capital of Vietnam." } },
    { "index": 1, "relevance_score": 0.54622, "document": { "text": "Ho Chi Minh City is the largest city." } }
  ],
  "usage": { "prompt_tokens": 55, "total_tokens": 55 }
}
```
{% endcode %}

`index` là vị trí trong mảng `documents` bạn gửi. Kết quả được sắp xếp theo `relevance_score` giảm dần.
