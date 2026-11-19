---
description: "Every successful response reports token usage. Record it to track cost and spot runaway reasoning."
---

# Usage accounting

|   | Chat | Messages | Responses |
| --- | --- | --- | --- |
| Input | `prompt_tokens` | `input_tokens` | `input_tokens` |
| Output (incl. reasoning) | `completion_tokens` | `output_tokens` | `output_tokens` |
| of which reasoning | `completion_tokens_details.reasoning_tokens` (some models, e.g. GLM: `reasoning_tokens` at the `usage` top level) | `output_tokens_details.reasoning_tokens` | `output_tokens_details.reasoning_tokens` |
| Cached input | `prompt_tokens_details.cached_tokens` | `cache_read_input_tokens` | `input_tokens_details.cached_tokens` |
| Web search | — | `server_tool_use.web_search_requests` | `server_tool_use.web_search_requests` |

* **Streaming:** on Chat the last chunk before `[DONE]` carries `usage`; you can also set `stream_options.include_usage: true` explicitly. Messages report it in `message_delta`; Responses in `response.completed`.
* **Interrupted streams:** if the connection drops, usage for the tokens generated so far is still recorded (estimated when the provider did not report it).
* **Failed requests** (4xx/5xx before generation) consume no tokens.
