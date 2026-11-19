---
description: "The same concept has a different field name on each endpoint. This table maps them."
---

# Parameters

| Concept | Chat Completions | Messages | Responses |
| --- | --- | --- | --- |
| System prompt | `messages[{role:"system"}]` | `system` | `instructions` |
| Output cap | `max_tokens` / `max_completion_tokens` | `max_tokens` (required) | `max_output_tokens` |
| Reasoning effort | `reasoning_effort` | `output_config.effort` / `thinking` | `reasoning.effort` |
| Stop sequences | `stop` | `stop_sequences` | — |
| Sampling | `temperature`, `top_p` | `temperature`, `top_p` | `temperature`, `top_p` |
| Function tools | `tools[{type:"function",function:{…}}]` | `tools[{name,description,input_schema}]` | `tools[{type:"function",name,parameters}]` |
| Tool choice | `tool_choice` | `tool_choice` | `tool_choice` |
| Web search | `{"type":"web_search"}` | `{"type":"web_search_20250305","name":"web_search"}` | `{"type":"web_search"}` |
| JSON output | `response_format` | — | `text.format` |
| Image input | `image_url` | `image` | `input_image` |
| Answer field | `choices[0].message.content` | `content[type=text]` | `output_text` |
| Reasoning text | `message.reasoning_content` | `content[type=thinking]` | `output[type=reasoning]` |
| Stop reason | `finish_reason` | `stop_reason` | `status` |

{% hint style="info" %}
Not every model supports every parameter. Check `supported_parameters` in [`GET /v1/models`](../models/README.md). `top_k`, `min_p` and `repetition_penalty` are accepted only by models that list them.
{% endhint %}

## Parameter support by model

Support varies by model. Always check the model's `supported_parameters` via `GET /v1/models`.

| Parameter | Support |
| --- | --- |
| `max_completion_tokens` | All chat models |
| `max_tokens` | All chat models |
| `parallel_tool_calls` | All chat models |
| `reasoning_effort` | All chat models |
| `seed` | All chat models |
| `tool_choice` | All chat models |
| `tools` | All chat models |
| `repetition_penalty` | Varies by model, check `supported_parameters` |
| `top_k` | Varies by model, check `supported_parameters` |
| `frequency_penalty` | Varies by model, check `supported_parameters` |
| `include_reasoning` | Varies by model, check `supported_parameters` |
| `min_p` | Varies by model, check `supported_parameters` |
| `presence_penalty` | Varies by model, check `supported_parameters` |
| `reasoning` | Varies by model, check `supported_parameters` |
| `temperature` | Varies by model, check `supported_parameters` |
| `top_p` | Varies by model, check `supported_parameters` |
| `response_format` | Varies by model, check `supported_parameters` |
| `stop` | Varies by model, check `supported_parameters` |
| `logprobs` | Varies by model, check `supported_parameters` |
| `top_logprobs` | Varies by model, check `supported_parameters` |
| `structured_outputs` | Varies by model, check `supported_parameters` |
