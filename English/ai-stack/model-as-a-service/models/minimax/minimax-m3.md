---
description: "MiniMax-M3 is MiniMax's natively multimodal frontier model (released 2026-06-01), built on MSA (MiniMax Sparse Attention) which sharply cuts the compute cost of 1M-token context. It accepts text, image and video input with a 1M-token context window and up to 512K output tokens, and exposes both the OpenAI Chat Completions API and the Anthropic Messages API. Reasoning is adaptive by default and can be turned off via thinking.type, or split out of the answer via reasoning_split. Tuned for frontier agentic coding and computer-use workloads."
---

# MiniMax M3

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `minimax/minimax-m3` · Type: Chat

MiniMax-M3 is MiniMax's natively multimodal frontier model (released 2026-06-01), built on MSA (MiniMax Sparse Attention) which sharply cuts the compute cost of 1M-token context. It accepts text, image and video input with a 1M-token context window and up to 512K output tokens, and exposes both the OpenAI Chat Completions API and the Anthropic Messages API. Reasoning is adaptive by default and can be turned off via thinking.type, or split out of the answer via reasoning_split. Tuned for frontier agentic coding and computer-use workloads.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 512K tokens |
| Input | text, image, video |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Always on
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `seed`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "minimax/minimax-m3",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
