---
description: "MiniMax-M2.5 is MiniMax's open-weight Mixture-of-Experts model with 229B total parameters (~10B active per forward pass), purpose-built for advanced coding and agentic workflows. It targets software engineering, agent search and long-horizon tool use, while remaining substantially cheaper and faster than frontier closed models."
---

# MiniMax M2.5

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `minimax/minimax-m2.5` · Type: Chat

MiniMax-M2.5 is MiniMax's open-weight Mixture-of-Experts model with 229B total parameters (~10B active per forward pass), purpose-built for advanced coding and agentic workflows. It targets software engineering, agent search and long-horizon tool use, while remaining substantially cheaper and faster than frontier closed models.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 192K tokens |
| Max output | 128K tokens |
| Input | text |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Always on
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "minimax/minimax-m2.5",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
