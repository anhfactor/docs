---
description: "Qwen3.8-27B is a 27B-parameter open-weight model from the Qwen3.8 family, self-hosted on VNG infrastructure (SGLang). It supports a 1M-token context window, text and image input, hybrid thinking / non-thinking modes and tool calling, exposed over OpenAI Chat Completions, Anthropic Messages and OpenAI Responses APIs."
---

# Qwen 3.8 27B

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `qwen/qwen3.8-27b` · Loại: Chat

Qwen3.8-27B is a 27B-parameter open-weight model from the Qwen3.8 family, self-hosted on VNG infrastructure (SGLang). It supports a 1M-token context window, text and image input, hybrid thinking / non-thinking modes and tool calling, exposed over OpenAI Chat Completions, Anthropic Messages and OpenAI Responses APIs.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 1M tokens |
| Đầu vào | text, image |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Mặc định bật
* Các mức `reasoning_effort`: `low`, `medium`, `xhigh`
* Mức mặc định: `xhigh`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.8-27b",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
