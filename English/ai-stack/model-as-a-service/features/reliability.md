---
description: "What the gateway does when a model backend fails, and what is left to your client."
---

# Reliability

## Handled by the gateway

* **Failover to a backup provider.** Models that have a backup provider switch to it when the primary answers 429, 502, 503 or 504. For non-streaming requests this happens inside the same request, so you only see the successful answer.
* **Cool-down.** A failing backend is skipped for about 60 seconds, then tried again.
* **Not every model has a backup.** A model served by a single backend returns the backend error (`upstream_error`) to you.
* **Capacity protection.** When every backend of a model is unavailable or full, the gateway answers `pool_exhausted` (503 or 529) instead of queueing indefinitely.

## Your client's job

* Retry 429 and 5xx with exponential backoff and jitter, honouring `Retry-After`. See [Errors](../api-reference/errors.md).
* A streaming request that fails is not retried by the gateway, and a stream that breaks after it started cannot be resumed. Retry the whole request.
* For critical paths keep a second model (for example the `-thirdparty` variant, or another family) and switch to it on repeated `pool_exhausted` or `upstream_error`.
* Make requests idempotent on your side: a retried request is a new generation and is billed again if the first one produced output.

## Timeouts

| Setting | Recommended | Why |
| --- | --- | --- |
| Connect timeout | 10 s | A connection that does not open quickly will not recover; fail fast and retry. |
| Read timeout, non-streaming | 10 min | The gateway waits up to 10 minutes for the model on `/v1/…`. A shorter client timeout abandons answers that are still being generated. |
| Read timeout, streaming | a few minutes between chunks | Reasoning models can stay silent while thinking before the first token. |
| Retries | 3–5, with backoff | Enough to ride out a cool-down without amplifying an outage. |
