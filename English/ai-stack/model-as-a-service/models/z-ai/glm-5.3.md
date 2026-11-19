---
description: "GLM-5.3 is Z.ai's open-weight flagship model of the GLM-5 series, built for agentic coding, reasoning and tool use. Self-hosted on GreenNode infrastructure with a 300K-token context window. Supports chat completions, Anthropic-style messages and the responses API, with function calling, structured output, streaming and reasoning-effort control."
---

# GLM-5.3

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `z-ai/glm-5.3` · Type: Chat

GLM-5.3 is Z.ai's open-weight flagship model of the GLM-5 series, built for agentic coding, reasoning and tool use. Self-hosted on GreenNode infrastructure with a 300K-token context window. Supports chat completions, Anthropic-style messages and the responses API, with function calling, structured output, streaming and reasoning-effort control.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 300K tokens |
| Max output | 128K tokens |
| Input | text |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Always on
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Default effort: `max`

## Supported parameters

`frequency_penalty`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning_effort`, `repetition_penalty`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
