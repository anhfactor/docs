---
description: "An API key identifies your account on every MaaS request. You need one before you can enable or call any model."
---

# API keys

## Create an API key

1. Sign in to [AI Platform](https://aiplatform.console.greennode.ai) and open **API Keys**.
2. Click **Create an API key**.
3. Enter an **API Key Name**. Optionally tick **Set as default** to make it the default key.
4. Click **Create API key**. The key appears in the list.

{% hint style="info" %}
**Limit**

Each account can have up to 50 API keys. Creating more returns “API key limit exceeded”. All keys of an account share the same enabled models and the same rate-limit counters.
{% endhint %}

## View or delete a key

| Action | Steps |
| --- | --- |
| View / copy | Click ︙ in the **Actions** column → **View API Key**. |
| Delete | Click ︙ → **Delete API Key** and confirm. Requests using that key start failing with 401. |

## Send the key

Always send the key in a header, never in the URL or the body. The three headers below are equivalent; use the one your SDK sends by default.

| Header | Typical client |
| --- | --- |
| `Authorization: Bearer <API_KEY>` | OpenAI SDK, curl |
| `x-api-key: <API_KEY>` | Anthropic SDK, Claude Code |
| `apikey: <API_KEY>` | Legacy integrations |

`GET /v1/models` does not accept the `apikey` header (returns 401); use `Authorization: Bearer` or `x-api-key` for that endpoint.

{% code title="shell" %}
```bash
export GREENNODE_API_KEY="<your API key>"

curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/models \
  -H "Authorization: Bearer $GREENNODE_API_KEY"
```
{% endcode %}

## Key errors

These responses were checked against the production gateway on 2026-11-12. Every one carries the header `x-ai-error-code: request_denied`.

| HTTP | Body | Cause and fix |
| --- | --- | --- |
| 401 | `{"error":{"message":"missing api key","code":"request_denied","type":"request_denied"}}` | No key header was sent. Add one of the headers above. |
| 401 | `{"error":{"message":"unknown api key","code":"request_denied","type":"request_denied"}}` | The key is wrong or was deleted. Copy it again from the portal or create a new one. |
| 403 | `{"error":{"message":"model not allowed for this key","code":"request_denied","type":"request_denied"}}` | The model is not enabled for your account. See [Enable / disable models](enable-models.md). |

## Rotate a key without downtime

1. Create a new key. Give it a dated name such as `backend-2026-11` so you can tell keys apart.
2. Deploy the new key to your application and confirm requests succeed with it.
3. Delete the old key. Requests still using it fail with `401` “unknown api key”.

Use one key per application or environment, so that rotating or revoking one does not affect the others. Keys of one account share enabled models, rate-limit counters and billing.

## If a key is exposed

1. Delete the key on the portal right away. This is the only way to revoke it.
2. Create a replacement key and deploy it.
3. Open **Model Usage** and check for usage you do not recognise in the period the key was exposed.
4. Remove the key from wherever it leaked (repository history, logs, chat) and contact support if you see unexpected charges.

## Keep keys safe

* Never put a key in browser or mobile code. Call MaaS from your backend.
* Store keys in environment variables or a secret manager, not in source code.
* If a key leaks, delete it in the portal and create a new one.
* Never send your key to support. Send the request ID instead.
