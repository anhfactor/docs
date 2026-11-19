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

Mức hỗ trợ khác nhau giữa các model. Luôn kiểm tra `supported_parameters` của model qua `GET /v1/models`.

| Tham số | Mức hỗ trợ |
| --- | --- |
| `max_completion_tokens` | Mọi model chat |
| `max_tokens` | Mọi model chat |
| `parallel_tool_calls` | Mọi model chat |
| `reasoning_effort` | Mọi model chat |
| `seed` | Mọi model chat |
| `tool_choice` | Mọi model chat |
| `tools` | Mọi model chat |
| `repetition_penalty` | Tuỳ model, xem `supported_parameters` |
| `top_k` | Tuỳ model, xem `supported_parameters` |
| `frequency_penalty` | Tuỳ model, xem `supported_parameters` |
| `include_reasoning` | Tuỳ model, xem `supported_parameters` |
| `min_p` | Tuỳ model, xem `supported_parameters` |
| `presence_penalty` | Tuỳ model, xem `supported_parameters` |
| `reasoning` | Tuỳ model, xem `supported_parameters` |
| `temperature` | Tuỳ model, xem `supported_parameters` |
| `top_p` | Tuỳ model, xem `supported_parameters` |
| `response_format` | Tuỳ model, xem `supported_parameters` |
| `stop` | Tuỳ model, xem `supported_parameters` |
| `logprobs` | Tuỳ model, xem `supported_parameters` |
| `top_logprobs` | Tuỳ model, xem `supported_parameters` |
| `structured_outputs` | Tuỳ model, xem `supported_parameters` |
