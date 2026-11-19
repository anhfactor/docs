---
description: "Retrieval-augmented generation answers questions from your own documents: embed, retrieve, rerank, then generate."
---

# Build RAG with Embeddings and Rerank

## The pipeline

| Step | Endpoint | Model used below | Purpose |
| --- | --- | --- | --- |
| 1. Embed documents | `POST /v1/embeddings` | `baai/bge-m3` | Turn each passage into a vector, once. |
| 2. Retrieve | `POST /v1/embeddings` | `baai/bge-m3` | Embed the question and find the nearest passages. |
| 3. Rerank | `POST /v1/rerank` | `baai/bge-reranker-v2-m3` | Re-score the candidates by relevance and keep the best. |
| 4. Generate | `POST /v1/chat/completions` | `qwen/qwen3.6-flash` | Answer from the selected context. |

## Complete example

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
**Not run end to end**

This example is assembled from the documented request and response shapes of each endpoint; it has not been executed against production as one script.
{% endhint %}

## Tips

* Split documents into passages that fit the embedding model's context (8,192 tokens for `bge-m3`).
* Use the same embedding model for documents and questions.
* Retrieve generously (20–50 passages), then let rerank cut down to the few you send to the chat model.
* Embedding and rerank calls count toward your rate limit, so batch inputs into one request where possible.
