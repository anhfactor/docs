---
description: "GLM-5.2 is Z.ai's open-weight flagship model for agentic engineering, released June 13, 2026. Built on a 744B-parameter Mixture-of-Experts architecture with ~40B active parameters per token, it delivers a 1M-token context window (up to 131K output tokens) and introduces IndexShare sparse-attention reuse for ~2.9x lower per-token FLOPs at 1M context plus improved speculative decoding. It is among the leading open-weight models for long-horizon coding, with function calling, structured output, context caching, streaming, MCP integration and selectable thinking-effort levels (High/Max). Weights are published under the MIT license."
---

# GLM-5.2

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `z-ai/glm-5.2-thirdparty` · Type: Chat

GLM-5.2 is Z.ai's open-weight flagship model for agentic engineering, released June 13, 2026. Built on a 744B-parameter Mixture-of-Experts architecture with ~40B active parameters per token, it delivers a 1M-token context window (up to 131K output tokens) and introduces IndexShare sparse-attention reuse for ~2.9x lower per-token FLOPs at 1M context plus improved speculative decoding. It is among the leading open-weight models for long-horizon coding, with function calling, structured output, context caching, streaming, MCP integration and selectable thinking-effort levels (High/Max). Weights are published under the MIT license.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 128K tokens |
| Input | text |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: On by default
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Default effort: `max`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.2-thirdparty",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
