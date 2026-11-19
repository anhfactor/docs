---
description: >-
  Gemma 4 31B-IT is Google's open-weight instruction-tuned model from the Gemma
  4 family, featuring 31 billion parameters with native multimodal support for
  text and image inputs. It offers a 256K-token
---

# Gemma 4 31B-IT

> Trang này được sinh tự động từ danh mục model của GreenNode MaaS. Chỉnh sửa tay sẽ bị ghi đè ở lần đồng bộ sau.

Model ID: `google/gemma-4-31b-it` · Loại: Chat

Gemma 4 31B-IT is Google's open-weight instruction-tuned model from the Gemma 4 family, featuring 31 billion parameters with native multimodal support for text and image inputs. It offers a 256K-token context window (262,144 tokens) and is optimized for instruction following, reasoning, coding, and vision-language tasks.

## Thông số

| Thông số      | Giá trị                                                 |
| ------------- | ------------------------------------------------------- |
| Ngữ cảnh      | 262K tokens                                             |
| Output tối đa | 32K tokens                                              |
| Đầu vào       | text, image                                             |
| Đầu ra        | text                                                    |
| Endpoints     | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Trạng thái: Tùy chọn
* Các mức `reasoning_effort`: `low`, `medium`, `high`

## Tham số hỗ trợ

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Ví dụ

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "google/gemma-4-31b-it",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
