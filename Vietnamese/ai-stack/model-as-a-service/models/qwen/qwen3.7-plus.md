---
description: "Qwen3.7-Plus is the balanced flagship tier of Alibaba's Qwen3.7 commercial lineup (plus / flash / max), served over the OpenAI-compatible Alibaba Cloud DashScope API. It positions inference quality, cost and speed between the Max and Flash tiers — ideal for medium-to-high complexity tasks. It ships with a 1M-token context window, hybrid thinking / non-thinking modes, built-in tools with adaptive tool use, and strong agentic coding, reasoning and multilingual capabilities across the Qwen3 series."
---

# Qwen 3.7 Plus

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `qwen/qwen3.7-plus` · Loại: Chat

Qwen3.7-Plus is the balanced flagship tier of Alibaba's Qwen3.7 commercial lineup (plus / flash / max), served over the OpenAI-compatible Alibaba Cloud DashScope API. It positions inference quality, cost and speed between the Max and Flash tiers — ideal for medium-to-high complexity tasks. It ships with a 1M-token context window, hybrid thinking / non-thinking modes, built-in tools with adaptive tool use, and strong agentic coding, reasoning and multilingual capabilities across the Qwen3 series.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 128K tokens |
| Đầu vào | text, image, video |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Mặc định bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.7-plus",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
