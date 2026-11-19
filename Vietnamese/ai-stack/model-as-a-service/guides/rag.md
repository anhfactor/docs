---
description: "Retrieval-augmented generation trả lời câu hỏi dựa trên tài liệu của bạn: embed, truy xuất, rerank, rồi sinh câu trả lời."
---

# Xây RAG với Embeddings và Rerank

## Quy trình

| Bước | Endpoint | Model dùng bên dưới | Mục đích |
| --- | --- | --- | --- |
| 1. Embed tài liệu | `POST /v1/embeddings` | `baai/bge-m3` | Chuyển mỗi đoạn thành vector, làm một lần. |
| 2. Truy xuất | `POST /v1/embeddings` | `baai/bge-m3` | Embed câu hỏi và tìm các đoạn gần nhất. |
| 3. Rerank | `POST /v1/rerank` | `baai/bge-reranker-v2-m3` | Chấm lại các ứng viên theo độ liên quan và giữ phần tốt nhất. |
| 4. Sinh câu trả lời | `POST /v1/chat/completions` | `qwen/qwen3.6-flash` | Trả lời dựa trên ngữ cảnh đã chọn. |

## Ví dụ đầy đủ

{% code title="Python · pip install openai requests" %}
```python
import os, requests
from openai import OpenAI

BASE = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
KEY = os.environ["GREENNODE_API_KEY"]
client = OpenAI(base_url=BASE + "/v1", api_key=KEY, timeout=600)

docs = [
    "GreenNode MaaS bills token-based models per 1,000,000 tokens.",
    "The default rate limit is 10 requests per minute per account.",
    "Hanoi is the capital of Vietnam.",
]

# 1) Embed the documents once and keep the vectors (use a vector database in production).
doc_vecs = [d.embedding for d in client.embeddings.create(model="baai/bge-m3", input=docs).data]

def cosine(a, b):
    dot = sum(x * y for x, y in zip(a, b))
    return dot / ((sum(x * x for x in a) ** 0.5) * (sum(y * y for y in b) ** 0.5))

question = "How many requests per minute can I send?"

# 2) Retrieve: embed the question and take the closest documents.
q_vec = client.embeddings.create(model="baai/bge-m3", input=[question]).data[0].embedding
candidates = sorted(docs, key=lambda d: -cosine(q_vec, doc_vecs[docs.index(d)]))[:3]

# 3) Rerank the candidates and keep the best ones.
r = requests.post(
    BASE + "/v1/rerank",
    headers={"Authorization": f"Bearer {KEY}"},
    json={"model": "baai/bge-reranker-v2-m3", "query": question, "documents": candidates, "top_n": 2},
    timeout=60,
)
r.raise_for_status()
context = "\n".join(candidates[item["index"]] for item in r.json()["results"])

# 4) Generate the answer from the retrieved context only.
answer = client.chat.completions.create(
    model="qwen/qwen3.6-flash",
    reasoning_effort="low",
    max_tokens=1024,
    messages=[
        {"role": "system", "content": "Answer using only the context. If it is not there, say you do not know."},
        {"role": "user", "content": f"Context:\n{context}\n\nQuestion: {question}"},
    ],
)
print(answer.choices[0].message.content)
```
{% endcode %}

{% hint style="warning" %}
**Chưa chạy thử trọn vẹn**

Ví dụ này ghép từ định dạng request và response đã mô tả của từng endpoint; chưa được chạy trên production như một script hoàn chỉnh.
{% endhint %}

## Lưu ý

* Chia tài liệu thành các đoạn vừa context của model embedding (8.192 token với `bge-m3`).
* Dùng cùng một model embedding cho tài liệu và câu hỏi.
* Truy xuất rộng (20–50 đoạn), rồi để rerank lọc còn vài đoạn gửi cho model chat.
* Request embedding và rerank cũng tính vào rate limit, nên gộp input vào một request khi có thể.
