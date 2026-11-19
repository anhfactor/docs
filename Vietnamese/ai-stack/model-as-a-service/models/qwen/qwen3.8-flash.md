---
description: "Qwen3.8-Flash is the cost-optimized, fastest tier of Alibaba's Qwen3.8 commercial lineup, served over the OpenAI-compatible Alibaba Cloud DashScope API. It keeps the 1M-token context window of the family while allowing up to 128K output tokens, supports hybrid thinking / non-thinking modes, tool calling and structured output, and targets high-volume chat, classification and latency-sensitive agentic workloads."
---

# Qwen 3.8 Flash

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `qwen/qwen3.8-flash` · Loại: Chat

Qwen3.8-Flash is the cost-optimized, fastest tier of Alibaba's Qwen3.8 commercial lineup, served over the OpenAI-compatible Alibaba Cloud DashScope API. It keeps the 1M-token context window of the family while allowing up to 128K output tokens, supports hybrid thinking / non-thinking modes, tool calling and structured output, and targets high-volume chat, classification and latency-sensitive agentic workloads.

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
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Mức mặc định: `xhigh`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.8-flash",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
