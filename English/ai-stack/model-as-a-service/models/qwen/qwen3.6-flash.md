---
description: "Qwen3.6-Flash is the cost-optimized, fastest tier of Alibaba's Qwen3.6 commercial lineup (flash / plus / max-preview), served over the OpenAI-compatible Alibaba Cloud DashScope API. It keeps the same capability surface as the higher tiers — 1M-token context window, max 65,536 output tokens, hybrid thinking / non-thinking modes, and built-in first-class tools (web search, code interpreter, web scraping) — while optimising for latency and price, making it the default pick for high-volume chat, classification and lightweight agentic workloads."
---

# Qwen 3.6 Flash

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3.6-flash` · Type: Chat

Qwen3.6-Flash is the cost-optimized, fastest tier of Alibaba's Qwen3.6 commercial lineup (flash / plus / max-preview), served over the OpenAI-compatible Alibaba Cloud DashScope API. It keeps the same capability surface as the higher tiers — 1M-token context window, max 65,536 output tokens, hybrid thinking / non-thinking modes, and built-in first-class tools (web search, code interpreter, web scraping) — while optimising for latency and price, making it the default pick for high-volume chat, classification and lightweight agentic workloads.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 64K tokens |
| Input | text, image, video |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: On by default
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
