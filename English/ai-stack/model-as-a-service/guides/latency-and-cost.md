---
description: "Most slow or expensive requests come from reasoning, long outputs or repeated prompts. These settings have the largest effect."
---

# Optimise latency and cost

## What to tune

| Lever | What to do | Effect |
| --- | --- | --- |
| Reasoning effort | Set `minimal` or `low` for extraction, classification and short answers. The default is often `max`. See [Reasoning](../features/reasoning.md). | Fewer output tokens: faster and cheaper. |
| Streaming | Set `stream: true`. See [Streaming](../api-reference/streaming.md). | Users see the first words sooner; total time is unchanged. |
| Prompt caching | Keep the system prompt and tools identical and first, and only append to the conversation. See [Prompt caching](../features/prompt-caching.md). | Cached input is cheaper and faster. |
| Output length | Ask for a short answer and set `max_tokens` with headroom for reasoning. | Output tokens cost the most. |
| Model choice | Use a Flash-class model for simple tasks and a flagship only where quality requires it. | Lower price per token and faster responses. |
| Context size | Send only the history and documents the model needs; rerank before generation. | Fewer input tokens per request. |

## Measure it

* `usage` in every response shows input, output, reasoning and cached tokens.
* `x-kong-upstream-latency` is the time spent waiting for the model; `x-kong-proxy-latency` is the time added by the gateway. Both are in milliseconds.
* The [Model Usage](https://aiplatform.console.greennode.ai/model-usage) page shows tokens and cost over time.
