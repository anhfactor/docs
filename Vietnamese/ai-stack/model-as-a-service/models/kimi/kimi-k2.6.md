---
description: "Kimi K2.6 is Moonshot AI's general-purpose open-source model, supporting text, image and video input with a 256K-token context window. It offers both thinking and non-thinking modes and handles conversational as well as programming/agent tasks. Served here over Tencent Cloud TokenHub, which exposes the OpenAI Chat Completions, Anthropic Messages and Responses APIs for this model."
---

# Kimi K2.6

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `kimi/kimi-k2.6` · Loại: Chat

Kimi K2.6 is Moonshot AI's general-purpose open-source model, supporting text, image and video input with a 256K-token context window. It offers both thinking and non-thinking modes and handles conversational as well as programming/agent tasks. Served here over Tencent Cloud TokenHub, which exposes the OpenAI Chat Completions, Anthropic Messages and Responses APIs for this model.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 256K tokens |
| Output tối đa | 256K tokens |
| Đầu vào | text, image, video |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Mặc định bật
* Các mức `reasoning_effort`: `low`, `medium`, `high`, `xhigh`, `max`

## Tham số hỗ trợ

`include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `tool_choice`, `tools`, `top_k`, `top_logprobs`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kimi/kimi-k2.6",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
