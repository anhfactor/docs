---
description: "MiniMax-M2.5 is MiniMax's open-weight Mixture-of-Experts model with 229B total parameters (~10B active per forward pass), purpose-built for advanced coding and agentic workflows. It targets software engineering, agent search and long-horizon tool use, while remaining substantially cheaper and faster than frontier closed models."
---

# MiniMax M2.5

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `minimax/minimax-m2.5` · Loại: Chat

MiniMax-M2.5 is MiniMax's open-weight Mixture-of-Experts model with 229B total parameters (~10B active per forward pass), purpose-built for advanced coding and agentic workflows. It targets software engineering, agent search and long-horizon tool use, while remaining substantially cheaper and faster than frontier closed models.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 192K tokens |
| Output tối đa | 128K tokens |
| Đầu vào | text |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Luôn bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "minimax/minimax-m2.5",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
