---
description: "Qwen3.6-Plus is the balanced tier of Alibaba's Qwen3.6 commercial lineup (flash / plus / max-preview), served over the OpenAI-compatible Alibaba Cloud DashScope API. It sits between Max-Preview (top reasoning) and Flash (fastest / lowest cost), targeting medium-to-high complexity tasks at a balanced price-performance point. It ships with a 1M-token context window, max 65,536 output tokens, hybrid thinking / non-thinking modes, and built-in first-class tools (web search, code interpreter, web scraping) alongside function calling with structured output."
---

# Qwen 3.6 Plus

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3.6-plus` · Type: Chat

Qwen3.6-Plus is the balanced tier of Alibaba's Qwen3.6 commercial lineup (flash / plus / max-preview), served over the OpenAI-compatible Alibaba Cloud DashScope API. It sits between Max-Preview (top reasoning) and Flash (fastest / lowest cost), targeting medium-to-high complexity tasks at a balanced price-performance point. It ships with a 1M-token context window, max 65,536 output tokens, hybrid thinking / non-thinking modes, and built-in first-class tools (web search, code interpreter, web scraping) alongside function calling with structured output.

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
    "model": "qwen/qwen3.6-plus",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
