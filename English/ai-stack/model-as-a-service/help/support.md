---
description: "How to reach GreenNode, what to include in a report, and the terms used in these docs."
---

# Support & glossary

## Contact

| Channel | Details |
| --- | --- |
| Help Center | [helpdesk.greennode.ai](https://helpdesk.greennode.ai/portal/en/home) |
| Email | [support@greennode.ai](mailto:support@greennode.ai) |
| Hotline | 19001549 |

## What to send

* The `x-kong-request-id` response header.
* The time of the call, with timezone.
* The model ID and the endpoint.
* The HTTP status and `x-ai-error-code`.
* **Never** your API key.

## Glossary

| Term | Meaning |
| --- | --- |
| MaaS | Model as a Service: models served through an API, with no infrastructure to run. |
| Token | The unit models read and write, and the unit of billing. Roughly a word fragment. |
| Context length | The maximum input plus output tokens in one request. |
| Reasoning tokens | Tokens the model spends thinking before the answer. Billed as output. |
| Cached tokens | Input tokens served from the prompt cache, billed at the cache price. |
| RPM / TPM | Requests per minute / tokens per minute. |
| Self-host / Third-party | Where a model runs: on GreenNode infrastructure, or at the model vendor under contract. |
| SSE | Server-sent events, the format used for streaming. |
| RAG | Retrieval-augmented generation: answering from retrieved documents. |
| Prepaid / Postpaid | Pay from credits bought in advance, or be invoiced monthly. |
