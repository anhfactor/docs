---
description: "GLM-5.2 is Z.ai's open-weight flagship model for agentic engineering, released June 13, 2026. Built on a 744B-parameter Mixture-of-Experts architecture with ~40B active parameters per token, it delivers a 1M-token context window (up to 131K output tokens) and introduces IndexShare sparse-attention reuse for ~2.9x lower per-token FLOPs at 1M context plus improved speculative decoding. It is among the leading open-weight models for long-horizon coding, with function calling, structured output, context caching, streaming, MCP integration and selectable thinking-effort levels (High/Max). Weights are published under the MIT license."
---

# GLM-5.2

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `z-ai/glm-5.2-thirdparty` · Loại: Chat

GLM-5.2 is Z.ai's open-weight flagship model for agentic engineering, released June 13, 2026. Built on a 744B-parameter Mixture-of-Experts architecture with ~40B active parameters per token, it delivers a 1M-token context window (up to 131K output tokens) and introduces IndexShare sparse-attention reuse for ~2.9x lower per-token FLOPs at 1M context plus improved speculative decoding. It is among the leading open-weight models for long-horizon coding, with function calling, structured output, context caching, streaming, MCP integration and selectable thinking-effort levels (High/Max). Weights are published under the MIT license.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 128K tokens |
| Đầu vào | text |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Mặc định bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Mức mặc định: `max`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "z-ai/glm-5.2-thirdparty",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
