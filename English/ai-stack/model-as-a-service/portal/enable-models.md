---
description: "A model must be enabled for your account before your API keys can call it. You manage this on the Models page of AI Platform."
---

# Enable / disable models

## Before you enable

| Requirement | Details |
| --- | --- |
| An API key | Create at least one key first. See [API keys](api-keys.md). |
| Billing is activated | Prepaid accounts must also add quota before enabling; postpaid accounts can enable and use models right away. See [Billing & pricing](../pricing.md). |
| The model is still offered | A retired model cannot be enabled. |

## Enable or disable

1. Open [Models](https://aiplatform.console.greennode.ai/models) in AI Platform.
2. Click **Toggle models**. A popup lists the models; search or filter by Provider, Status or Type.
3. Switch models on or off, one by one or in bulk.
4. Save your changes.

## Find a model

The Models page has filters in the left sidebar:

| Filter | Values |
| --- | --- |
| Provider | BAAI, DeepSeek, Google, GreenNode, Kimi, Minimax, Qwen, Z.ai |
| Model Type | Chat, Messages, Responses, Embedding, Rerank, OCR |
| Use case | Vietnamese, General Tasks, Translation, Research, Finance, Marketing, Technology |

## Model status

| Status | Meaning |
| --- | --- |
| ENABLED | Your keys can call the model. |
| DISABLED | Requests are rejected with `403 request_denied`. |
| UPDATING | The change is being applied on the gateway. |
| ERROR | The change failed. You can retry right away; if it keeps failing, contact support. |

## Rules to know

* Enabling is never delayed. Disabling a model you have just switched is blocked for a 5-minute cool-down; the portal answers 429 until it passes.
* If any model in a bulk change is still cooling down, the whole change is rejected — nothing is applied partially.
* An account may have a cap on how many models can be enabled at once.
* When a prepaid account runs out of quota or its credits expire, all models are disabled automatically.

## Self-hosted and third-party

A model is either hosted on GreenNode infrastructure (**GreenNode self-host**) or forwarded to the model vendor under an official contract (**Third-party**). Some model families are offered both ways; the partner variant has an ID ending in `-thirdparty` and its own on/off switch.

## Check the result

`GET /v1/models` returns only the models your key can use, so it is the quickest check after a change. Calling a disabled model returns `403 request_denied` — “model not allowed for this key”. See [Models](../models/README.md).
