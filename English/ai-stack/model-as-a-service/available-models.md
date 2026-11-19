# Available Models

The MaaS API provides access to model families such as Qwen, DeepSeek, GLM, Kimi, MiniMax, Gemma and more. See the full list below.

{% hint style="info" %}
The model catalog below has been updated under the transition starting **August 3, 2026**, covering models self-hosted by GreenNode and third-party models under official contracts. See the timeline details in [Release Notes](../release-notes.md) and the billing rules in [Pricing](pricing.md).
{% endhint %}

### Rate limit

Applies by default to **every new account** using the MaaS API, counted **separately for each model**:

| Limit | Default value (per model) |
| --- | --- |
| Requests | **10 RPM** — 10 requests/minute |
| Tokens | **1,000,000 TPM** — 1 million tokens/minute |

Each model has its own counter: calling model A does not consume the quota of model B. See [Rate limits](portal/rate-limits.md) for details.

{% hint style="info" %}
Need more? [Contact GreenNode](https://helpdesk.greennode.ai/portal/en/newticket) to be considered for the **whitelist**. Whitelisting is reviewed case by case.
{% endhint %}

***

### Model list

The full model list (Model ID, context length, input, endpoints, reasoning) is kept up to date automatically in **[Model list](models/README.md)**.

Models are offered in one of two ways:

* **GreenNode self-host** — the model runs on GreenNode infrastructure.
* **Third-party** — the request is forwarded to the model vendor under an official contract.

MaaS supports these model types: **Chat**, **Embedding**, **Rerank** and **OCR**.
