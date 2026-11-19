---
description: "DeepSeek-V4.1-Flash is the lightweight flagship of DeepSeek's new Causal Encoder-Decoder architecture: a 552B-parameter Mixture-of-Experts model with 8B active parameters for input and 16B for output, out-performing DeepSeek-V4-Pro on key benchmarks. It offers native visual understanding (text + image input), deep thinking, a 1M-token context window and up to 384K output tokens. Served here via third-party providers (Alibaba Cloud Model Studio, Tencent Cloud TokenHub) over OpenAI Chat Completions, Anthropic Messages and Responses APIs."
---

# DeepSeek V4.1 Flash

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `deepseek/deepseek-v4.1-flash-thirdparty` · Loại: Chat

DeepSeek-V4.1-Flash is the lightweight flagship of DeepSeek's new Causal Encoder-Decoder architecture: a 552B-parameter Mixture-of-Experts model with 8B active parameters for input and 16B for output, out-performing DeepSeek-V4-Pro on key benchmarks. It offers native visual understanding (text + image input), deep thinking, a 1M-token context window and up to 384K output tokens. Served here via third-party providers (Alibaba Cloud Model Studio, Tencent Cloud TokenHub) over OpenAI Chat Completions, Anthropic Messages and Responses APIs.

## Thông số

| Thông số | Giá trị |
| --- | --- |
| Ngữ cảnh | 1M tokens |
| Output tối đa | 384K tokens |
| Đầu vào | text, image |
| Đầu ra | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Mặc định bật
* Các mức `reasoning_effort`: `minimal`, `low`, `medium`, `high`, `xhigh`, `max`
* Mức mặc định: `high`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `max_completion_tokens`, `max_tokens`, `min_p`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v4.1-flash-thirdparty",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
