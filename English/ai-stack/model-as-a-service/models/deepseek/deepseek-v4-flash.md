---
description: "DeepSeek-V4 Flash is the speed- and cost-optimized tier of the DeepSeek-V4 family. On the same MLA + DeepSeekMoE backbone it activates fewer experts per token to deliver high-throughput, low-latency responses for chat, summarization and lightweight reasoning, while preserving a 128K token context window. Served over an OpenAI-compatible API."
---

# DeepSeek V4 Flash

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `deepseek/deepseek-v4-flash` · Type: Chat

DeepSeek-V4 Flash is the speed- and cost-optimized tier of the DeepSeek-V4 family. On the same MLA + DeepSeekMoE backbone it activates fewer experts per token to deliver high-throughput, low-latency responses for chat, summarization and lightweight reasoning, while preserving a 128K token context window. Served over an OpenAI-compatible API.

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
    "model": "deepseek/deepseek-v4-flash",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
