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

Counted from `supported_parameters` of the 18 public chat models on 2026-11-18. Models enabled for a specific account may differ — always check the model's `supported_parameters` via `GET /v1/models`.

| Parameter | Chat models supporting it | Note |
| --- | --- | --- |
| `max_completion_tokens` | 18 / 18 | all public chat models |
| `max_tokens` | 18 / 18 | all public chat models |
| `parallel_tool_calls` | 18 / 18 | all public chat models |
| `reasoning_effort` | 18 / 18 | all public chat models |
| `seed` | 18 / 18 | all public chat models |
| `tool_choice` | 18 / 18 | all public chat models |
| `tools` | 18 / 18 | all public chat models |
| `repetition_penalty` | 17 / 18 | check `supported_parameters` of the model |
| `top_k` | 17 / 18 | check `supported_parameters` of the model |
| `frequency_penalty` | 16 / 18 | check `supported_parameters` of the model |
| `include_reasoning` | 16 / 18 | check `supported_parameters` of the model |
| `min_p` | 16 / 18 | check `supported_parameters` of the model |
| `presence_penalty` | 16 / 18 | check `supported_parameters` of the model |
| `reasoning` | 16 / 18 | check `supported_parameters` of the model |
| `temperature` | 16 / 18 | check `supported_parameters` of the model |
| `top_p` | 16 / 18 | check `supported_parameters` of the model |
| `response_format` | 15 / 18 | check `supported_parameters` of the model |
| `stop` | 14 / 18 | check `supported_parameters` of the model |
| `logprobs` | 11 / 18 | check `supported_parameters` of the model |
| `top_logprobs` | 11 / 18 | check `supported_parameters` of the model |
| `structured_outputs` | 10 / 18 | check `supported_parameters` of the model |
