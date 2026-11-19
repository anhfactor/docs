---
description: "Go through this list before sending real traffic."
---

# Production checklist

## Keys and access

* The API key is stored in a secret manager or environment variable, and never shipped to a browser or mobile app.
* Only the models you use are enabled.
* You know how to delete and replace a key if it leaks.

## Reliability

* 429 and 5xx responses are retried with exponential backoff, honouring `Retry-After`. See [Errors](../api-reference/errors.md).
* 400, 401, 403 and 404 responses are not retried.
* HTTP timeouts are at least 10 minutes, or the call streams.
* A broken stream is retried from the start.
* A fallback model is configured for critical paths.

## Limits and cost

* Expected peak traffic fits the rate limit, or a higher limit has been granted. See [Rate limits](../portal/rate-limits.md).
* `reasoning_effort` and `max_tokens` are set explicitly on every request.
* Prepaid accounts have enough quota and a top-up routine; all models are disabled when quota reaches 0. See [Billing & pricing](../pricing.md).
* `usage` from each response is recorded.

## Observability and support

* `x-kong-request-id` is logged for every request.
* Error rate, 429 rate and latency are on a dashboard with alerts.
* The team knows how to reach [Support](../help/support.md).
