---
description: "Qwen3.6-Flash is the cost-optimized, fastest tier of Alibaba's Qwen3.6 commercial lineup (flash / plus / max-preview), served over the OpenAI-compatible Alibaba Cloud DashScope API. It keeps the same capability surface as the higher tiers — 1M-token context window, max 65,536 output tokens, hybrid thinking / non-thinking modes, and built-in first-class tools (web search, code interpreter, web scraping) — while optimising for latency and price, making it the default pick for high-volume chat, classification and lightweight agentic workloads."
---

# Qwen 3.6 Flash

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `qwen/qwen3.6-flash` · Loại: Chat

Qwen3.6-Flash is the cost-optimized, fastest tier of Alibaba's Qwen3.6 commercial lineup (flash / plus / max-preview), served over the OpenAI-compatible Alibaba Cloud DashScope API. It keeps the same capability surface as the higher tiers — 1M-token context window, max 65,536 output tokens, hybrid thinking / non-thinking modes, and built-in first-class tools (web search, code interpreter, web scraping) — while optimising for latency and price, making it the default pick for high-volume chat, classification and lightweight agentic workloads.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 64K tokens |
| Đầu vào | text, image, video |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Mặc định bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
