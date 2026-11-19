---
description: "Cùng một khái niệm nhưng tên trường khác nhau trên mỗi endpoint. Bảng dưới đây đối chiếu chúng."
---

# Tham số

| Khái niệm | Chat Completions | Messages | Responses |
| --- | --- | --- | --- |
| System prompt | `messages[{role:"system"}]` | `system` | `instructions` |
| Giới hạn đầu ra | `max_tokens` / `max_completion_tokens` | `max_tokens` (required) | `max_output_tokens` |
| Reasoning effort | `reasoning_effort` | `output_config.effort` / `thinking` | `reasoning.effort` |
| Chuỗi dừng | `stop` | `stop_sequences` | — |
| Sampling | `temperature`, `top_p` | `temperature`, `top_p` | `temperature`, `top_p` |
| Function tool | `tools[{type:"function",function:{…}}]` | `tools[{name,description,input_schema}]` | `tools[{type:"function",name,parameters}]` |
| Tool choice | `tool_choice` | `tool_choice` | `tool_choice` |
| Web search | `{"type":"web_search"}` | `{"type":"web_search_20250305","name":"web_search"}` | `{"type":"web_search"}` |
| JSON output | `response_format` | — | `text.format` |
| Ảnh đầu vào | `image_url` | `image` | `input_image` |
| Trường câu trả lời | `choices[0].message.content` | `content[type=text]` | `output_text` |
| Nội dung suy luận | `message.reasoning_content` | `content[type=thinking]` | `output[type=reasoning]` |
| Lý do dừng | `finish_reason` | `stop_reason` | `status` |

{% hint style="info" %}
Không phải model nào cũng hỗ trợ mọi tham số. Kiểm tra `supported_parameters` trong [`GET /v1/models`](../models/README.md). `top_k`, `min_p`, `repetition_penalty` chỉ dùng được với model có liệt kê chúng.
{% endhint %}

## Mức hỗ trợ tham số theo model

Đếm từ `supported_parameters` của 18 model chat công khai ngày 2026-11-18. Model được bật riêng cho từng tài khoản có thể khác — luôn kiểm tra `supported_parameters` của model qua `GET /v1/models`.

| Tham số | Số model chat hỗ trợ | Ghi chú |
| --- | --- | --- |
| `max_completion_tokens` | 18 / 18 | mọi model chat công khai |
| `max_tokens` | 18 / 18 | mọi model chat công khai |
| `parallel_tool_calls` | 18 / 18 | mọi model chat công khai |
| `reasoning_effort` | 18 / 18 | mọi model chat công khai |
| `seed` | 18 / 18 | mọi model chat công khai |
| `tool_choice` | 18 / 18 | mọi model chat công khai |
| `tools` | 18 / 18 | mọi model chat công khai |
| `repetition_penalty` | 17 / 18 | xem `supported_parameters` của model |
| `top_k` | 17 / 18 | xem `supported_parameters` của model |
| `frequency_penalty` | 16 / 18 | xem `supported_parameters` của model |
| `include_reasoning` | 16 / 18 | xem `supported_parameters` của model |
| `min_p` | 16 / 18 | xem `supported_parameters` của model |
| `presence_penalty` | 16 / 18 | xem `supported_parameters` của model |
| `reasoning` | 16 / 18 | xem `supported_parameters` của model |
| `temperature` | 16 / 18 | xem `supported_parameters` của model |
| `top_p` | 16 / 18 | xem `supported_parameters` của model |
| `response_format` | 15 / 18 | xem `supported_parameters` của model |
| `stop` | 14 / 18 | xem `supported_parameters` của model |
| `logprobs` | 11 / 18 | xem `supported_parameters` của model |
| `top_logprobs` | 11 / 18 | xem `supported_parameters` của model |
| `structured_outputs` | 10 / 18 | xem `supported_parameters` của model |
