---
description: "Kimi K2.7 Code is Moonshot AI's coding-focused open-source model, open-sourced in June 2026. It targets programming and agentic workflows with more reliable instruction following over long contexts and higher task success rates, and supports text, image and video input. The model runs with thinking always enabled. Moonshot reports improved coding and agentic performance over K2.6 together with lower average token consumption on long-context tasks. Served here over Tencent Cloud TokenHub, which exposes the OpenAI Chat Completions, Anthropic Messages and Responses APIs for this model."
---

# Kimi K2.7 Code

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `kimi/kimi-k2.7-code` · Type: Chat

Kimi K2.7 Code is Moonshot AI's coding-focused open-source model, open-sourced in June 2026. It targets programming and agentic workflows with more reliable instruction following over long contexts and higher task success rates, and supports text, image and video input. The model runs with thinking always enabled. Moonshot reports improved coding and agentic performance over K2.6 together with lower average token consumption on long-context tasks. Served here over Tencent Cloud TokenHub, which exposes the OpenAI Chat Completions, Anthropic Messages and Responses APIs for this model.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 256K tokens |
| Max output | 256K tokens |
| Input | text, image, video |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Always on
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`

## Supported parameters

`include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `tool_choice`, `tools`, `top_k`, `top_logprobs`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimi/kimi-k2.7-code",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
