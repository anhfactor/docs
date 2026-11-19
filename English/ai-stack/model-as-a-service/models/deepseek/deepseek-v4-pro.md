---
description: "DeepSeek-V4 Pro is the flagship tier of the DeepSeek-V4 family — a Mixture-of-Experts (MoE) model built on Multi-head Latent Attention (MLA) and the DeepSeekMoE architecture with an auxiliary-loss-free load-balancing strategy. It delivers state-of-the-art reasoning, math, coding and agentic performance with a 128K token context window, served over an OpenAI-compatible API."
---

# DeepSeek V4 Pro

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `deepseek/deepseek-v4-pro` · Type: Chat

DeepSeek-V4 Pro is the flagship tier of the DeepSeek-V4 family — a Mixture-of-Experts (MoE) model built on Multi-head Latent Attention (MLA) and the DeepSeekMoE architecture with an auxiliary-loss-free load-balancing strategy. It delivers state-of-the-art reasoning, math, coding and agentic performance with a 128K token context window, served over an OpenAI-compatible API.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 384K tokens |
| Input | text |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Always on
* `reasoning_effort` levels: `low`, `medium`, `high`, `xhigh`, `max`
* Default effort: `high`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4-pro",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
