---
description: "Qwen3.8-27B is a 27B-parameter open-weight model from the Qwen3.8 family, self-hosted on GreenNode infrastructure. It supports a 1M-token context window, text and image input, hybrid thinking / non-thinking modes and tool calling, exposed over OpenAI Chat Completions, Anthropic Messages and OpenAI Responses APIs."
---

# Qwen 3.8 27B

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `qwen/qwen3.8-27b` · Type: Chat

Qwen3.8-27B is a 27B-parameter open-weight model from the Qwen3.8 family, self-hosted on GreenNode infrastructure. It supports a 1M-token context window, text and image input, hybrid thinking / non-thinking modes and tool calling, exposed over OpenAI Chat Completions, Anthropic Messages and OpenAI Responses APIs.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 1M tokens |
| Input | text, image |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: On by default
* `reasoning_effort` levels: `low`, `medium`, `xhigh`
* Default effort: `xhigh`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.8-27b",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
