---
description: "Repeated prompt prefixes are cached automatically. Cache hits are faster and reported as cached_tokens. No code change is required — but how you build prompts decides how often you hit."
---

# Prompt caching

## Seeing cache hits

| Endpoint | Field |
| --- | --- |
| Chat | `usage.prompt_tokens_details.cached_tokens` |
| Responses | `usage.input_tokens_details.cached_tokens` |
| Messages | `usage.cache_read_input_tokens` (when reported) |

## Maximising hits

* **Stable prefix:** put the system prompt and tool definitions first and keep them byte-identical across calls (same text, same tool order).
* **Append-only history:** add new turns at the end; never edit, reorder or summarise earlier turns mid-conversation. Any change at turn _n_ is a miss from turn _n_ on.
* **Put variable content last:** timestamps, user IDs, retrieved documents go after the stable part.
