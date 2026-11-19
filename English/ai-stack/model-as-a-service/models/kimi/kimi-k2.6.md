# Kimi K2.6

Model ID: `kimi/kimi-k2.6` · Type: Chat

Kimi K2.6 is Moonshot AI's general-purpose open-source model, supporting text, image and video input with a 256K-token context window. It offers both thinking and non-thinking modes and handles conversational as well as programming/agent tasks. Available over the OpenAI Chat Completions, Anthropic Messages and Responses APIs.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 256K tokens |
| Max output | 256K tokens |
| Input | text, image, video |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: On by default
* `reasoning_effort` levels: `low`, `medium`, `high`, `xhigh`, `max`

## Supported parameters

`include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `tool_choice`, `tools`, `top_k`, `top_logprobs`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimi/kimi-k2.6",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
