---
description: "GLM-5.3-Flash is the first natively multimodal model in Z.ai's GLM-5 series, released 2026-08-25 under the MIT license. Built on a 320B-parameter Mixture-of-Experts architecture with ~18B active parameters per token, it supports a 1M-token context window and uses a hybrid linear + sparse attention design for markedly lower attention compute and KV-cache cost. Available through the OpenAI Chat Completions, Anthropic Messages and Responses APIs."
---

# GLM-5.3 Flash

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `z-ai/glm-5.3-flash-thirdparty` · Loại: Chat

GLM-5.3-Flash is the first natively multimodal model in Z.ai's GLM-5 series, released 2026-08-25 under the MIT license. Built on a 320B-parameter Mixture-of-Experts architecture with ~18B active parameters per token, it supports a 1M-token context window and uses a hybrid linear + sparse attention design for markedly lower attention compute and KV-cache cost. Available through the OpenAI Chat Completions, Anthropic Messages and Responses APIs.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 128K tokens |
| Đầu vào | text, image, video |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Luôn bật
* Các mức `reasoning_effort`: `low`, `high`, `xhigh`, `max`
* Mức mặc định: `max`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.3-flash-thirdparty",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
