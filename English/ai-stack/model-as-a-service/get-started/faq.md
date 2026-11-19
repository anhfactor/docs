---
description: "Common questions from developers and business analysts."
---

# FAQ

### The response has empty `content` and `finish_reason: "length"`. Why?

The model spent the whole `max_tokens` budget on reasoning before it could write the answer. Lower the effort (`"reasoning_effort": "low"`) and/or raise `max_tokens`. Check `usage.completion_tokens_details.reasoning_tokens` to confirm.

### Which endpoint should I use — Chat, Messages or Responses?

Use whichever your SDK or tool speaks — the same models are behind all three. Chat Completions is the most widely supported. Messages suits Anthropic SDKs and Claude Code. Responses suits Codex CLI and newer OpenAI SDK code.

### What is the difference between 429 and 503?

**429**: either your own rate limit is exceeded (code `request_denied`; the message names the limit and when it resets) or the model provider is throttling (code `rate_limited`). Slow down and retry with backoff. **503/529 `pool_exhausted`**: every backend of the model is temporarily unavailable — retry after the `Retry-After` header, or switch to another model.

### How are tokens counted?

Input tokens = everything you send (system prompt, history, tool definitions, images). Output tokens = everything generated, **including reasoning**. Cached input tokens are reported separately in `cached_tokens`. See [Usage accounting](../features/usage-accounting.md).

### If my client disconnects mid-stream, is usage still recorded?

Yes. Tokens generated up to the disconnect are recorded; when the provider did not report final usage, the gateway estimates it.

### Will the same prompt give the same answer?

Not guaranteed. Use `temperature: 0` and `seed` (where supported) to reduce variation, and [structured outputs](../features/structured-outputs.md) when you need a fixed shape.

### Is my data used for training? Is it logged?

Please refer to your GreenNode MaaS service agreement for data handling and retention terms.

### How do I report a problem?

Send GreenNode support: the `x-kong-request-id` response header, the time of the call (with timezone), the model ID, the endpoint, and the HTTP status / `x-ai-error-code`. Never send your API key.
