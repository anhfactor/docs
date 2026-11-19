---
description: "Every account has a default request and token limit on each model. Higher limits are granted case by case."
---

# Rate limits

## Default limits

| Limit | Value | Counted |
| --- | --- | --- |
| Requests per minute | **10 RPM** on each model | Per account and per model. All API keys of the account share one counter. |
| Tokens per minute | **1,000,000 TPM** on each model | Same as above. |

* Each model has its own counter: calling one model does not consume the quota of another.
* Creating more API keys does not raise the limit, because keys share the account counter.
* A few models carry their own limit instead of the default (for example a daily request and token cap). The model page on the portal and the `x-ratelimit-*` headers of a response show the limit that applies to you.
* An account that has been granted a higher limit uses that limit instead.

{% hint style="info" %}
**Checked on production**

Default limit and counting scope verified against the production gateway configuration on 2026-11-14.
{% endhint %}

## When you hit a limit

The request returns `429` with `x-ai-error-code: request_denied` and a message naming the limit. The `x-ratelimit-*` response headers show which limit applied and how many seconds remain until it resets. See [Rate limits & limits](../api-reference/limits.md).

* Retry with exponential backoff and honour `Retry-After`. See [Errors](../api-reference/errors.md).
* Spread traffic evenly: 10 RPM is one request every 6 seconds.
* Lower the reasoning effort to shorten each call, and batch work into fewer requests.

## Request a higher limit

Need more than 10 RPM or 1,000,000 TPM? [Contact GreenNode](https://helpdesk.greennode.ai/portal/en/newticket) to be considered for the whitelist. Include your account, the model IDs, the RPM/TPM you need and the expected traffic. Requests are reviewed case by case and depend on the capacity of the model.
