---
description: "MiniMax-M3 is MiniMax's natively multimodal frontier model (released 2026-06-01), built on MSA (MiniMax Sparse Attention) which sharply cuts the compute cost of 1M-token context. It accepts text, image and video input with a 1M-token context window and up to 512K output tokens, and exposes both the OpenAI Chat Completions API and the Anthropic Messages API. Reasoning is adaptive by default and can be turned off via thinking.type, or split out of the answer via reasoning_split. Tuned for frontier agentic coding and computer-use workloads."
---

# MiniMax M3

Model ID: `minimax/minimax-m3` · Loại: Chat

MiniMax-M3 is MiniMax's natively multimodal frontier model (released 2026-06-01), built on MSA (MiniMax Sparse Attention) which sharply cuts the compute cost of 1M-token context. It accepts text, image and video input with a 1M-token context window and up to 512K output tokens, and exposes both the OpenAI Chat Completions API and the Anthropic Messages API. Reasoning is adaptive by default and can be turned off via thinking.type, or split out of the answer via reasoning_split. Tuned for frontier agentic coding and computer-use workloads.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 512K tokens |
| Đầu vào | text, image, video |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Luôn bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `seed`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "minimax/minimax-m3",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
