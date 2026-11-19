---
description: "Kimi K2.7 Code is Moonshot AI's coding-focused open-source model, open-sourced in June 2026. It targets programming and agentic workflows with more reliable instruction following over long contexts and higher task success rates, and supports text, image and video input. The model runs with thinking always enabled. Moonshot reports improved coding and agentic performance over K2.6 together with lower average token consumption on long-context tasks. Available over the OpenAI Chat Completions, Anthropic Messages and Responses APIs."
---

# Kimi K2.7 Code

Model ID: `kimi/kimi-k2.7-code` · Loại: Chat

Kimi K2.7 Code is Moonshot AI's coding-focused open-source model, open-sourced in June 2026. It targets programming and agentic workflows with more reliable instruction following over long contexts and higher task success rates, and supports text, image and video input. The model runs with thinking always enabled. Moonshot reports improved coding and agentic performance over K2.6 together with lower average token consumption on long-context tasks. Available over the OpenAI Chat Completions, Anthropic Messages and Responses APIs.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 256K tokens |
| Output tối đa | 256K tokens |
| Đầu vào | text, image, video |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Luôn bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`

## Tham số hỗ trợ

`include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `tool_choice`, `tools`, `top_k`, `top_logprobs`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimi/kimi-k2.7-code",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
