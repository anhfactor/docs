---
description: "GLM-5.3 is Z.ai's open-weight flagship model of the GLM-5 series, built for agentic coding, reasoning and tool use. Self-hosted on GreenNode infrastructure with a 300K-token context window. Supports chat completions, Anthropic-style messages and the responses API, with function calling, structured output, streaming and reasoning-effort control."
---

# GLM-5.3

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `z-ai/glm-5.3` · Loại: Chat

GLM-5.3 is Z.ai's open-weight flagship model of the GLM-5 series, built for agentic coding, reasoning and tool use. Self-hosted on GreenNode infrastructure with a 300K-token context window. Supports chat completions, Anthropic-style messages and the responses API, with function calling, structured output, streaming and reasoning-effort control.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 300K tokens |
| Output tối đa | 128K tokens |
| Đầu vào | text |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Luôn bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Mức mặc định: `max`

## Tham số hỗ trợ

`frequency_penalty`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning_effort`, `repetition_penalty`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
