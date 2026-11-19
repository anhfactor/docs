---
description: "Accounts can be configured with content-safety guardrails: harmful-content detection, PII protection and keyword policies. Requests are checked before they reach the model."
---

# Content safety

## When a request is blocked

The request is answered with **400** and `x-ai-error-code: request_denied`. The body is not the usual `error` object; it states what was detected:

{% code title="400 · x-ai-error-code: request_denied" %}
```json
{
  "status": "Prompt has been rejected by AI Guard",
  "reason": "Content violates the following categories: ...",
  "violations": [ ... ]
}
```
{% endcode %}

{% code title="400 · keyword policy" %}
```json
{
  "status": "Request blocked due to detected keyword",
  "reason": "..."
}
```
{% endcode %}

* Detect a block by the 400 status together with a `status` field in the body. Do not retry the same content; rephrase or remove the flagged part.
* A blocked request does not reach the model and produces no tokens.
* If a safety service is briefly unavailable you get a 503. That one is retryable.

## Changing guardrail settings

Guardrails are off unless they have been configured for your account. Settings are managed by GreenNode; [contact support](../help/support.md) to turn a guardrail on or adjust it.

{% hint style="info" %}
**Source**

Response shapes are taken from the gateway source code; they were not triggered on production during the check of 2026-11-14.
{% endhint %}
