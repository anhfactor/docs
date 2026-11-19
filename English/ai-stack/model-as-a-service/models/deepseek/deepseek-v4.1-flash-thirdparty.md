---
description: "DeepSeek-V4.1-Flash is the lightweight flagship of DeepSeek's new Causal Encoder-Decoder architecture: a 552B-parameter Mixture-of-Experts model with 8B active parameters for input and 16B for output, out-performing DeepSeek-V4-Pro on key benchmarks. It offers native visual understanding (text + image input), deep thinking, a 1M-token context window and up to 384K output tokens. Served here via third-party providers (Alibaba Cloud Model Studio, Tencent Cloud TokenHub) over OpenAI Chat Completions, Anthropic Messages and Responses APIs."
---

# DeepSeek V4.1 Flash

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Model ID: `deepseek/deepseek-v4.1-flash-thirdparty` · Type: Chat

DeepSeek-V4.1-Flash is the lightweight flagship of DeepSeek's new Causal Encoder-Decoder architecture: a 552B-parameter Mixture-of-Experts model with 8B active parameters for input and 16B for output, out-performing DeepSeek-V4-Pro on key benchmarks. It offers native visual understanding (text + image input), deep thinking, a 1M-token context window and up to 384K output tokens. Served here via third-party providers (Alibaba Cloud Model Studio, Tencent Cloud TokenHub) over OpenAI Chat Completions, Anthropic Messages and Responses APIs.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 1M tokens |
| Max output | 384K tokens |
| Input | text, image |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: On by default
* `reasoning_effort` levels: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Default effort: `high`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4.1-flash-thirdparty",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
