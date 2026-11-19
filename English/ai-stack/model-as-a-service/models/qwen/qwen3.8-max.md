---
description: "Qwen3.8-Max is the flagship tier of Alibaba's Qwen3.8 commercial lineup, served over the OpenAI-compatible Alibaba Cloud DashScope API. It offers the strongest reasoning and coding capability of the family with a 1M-token context window, hybrid thinking / non-thinking modes, tool calling and structured output, and is aimed at complex agentic, coding and long-context workloads."
---

# Qwen 3.8 Max

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3.8-max` · Type: Chat

Qwen3.8-Max is the flagship tier of Alibaba's Qwen3.8 commercial lineup, served over the OpenAI-compatible Alibaba Cloud DashScope API. It offers the strongest reasoning and coding capability of the family with a 1M-token context window, hybrid thinking / non-thinking modes, tool calling and structured output, and is aimed at complex agentic, coding and long-context workloads.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 128K tokens |
| Input | text, image, video |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: On by default
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Default effort: `xhigh`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.8-max",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
