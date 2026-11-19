# Gemma 4 31B-IT

Model ID: `google/gemma-4-31b-it` · Type: Chat

Gemma 4 31B-IT is Google's open-weight instruction-tuned model from the Gemma 4 family, featuring 31 billion parameters with native multimodal support for text and image inputs. It offers a 256K-token context window (262,144 tokens) and is optimized for instruction following, reasoning, coding, and vision-language tasks.

## Specs

| Spec | Value |
| --- | --- |
| Context length | 262K tokens |
| Max output | 32K tokens |
| Input | text, image |
| Output | text |
| Endpoints | `/v1/chat/completions`, `/v1/responses`, `/v1/messages` |

## Reasoning

* Mode: Optional
* `reasoning_effort` levels: `low`, `medium`, `high`

## Supported parameters

`frequency_penalty`, `include_reasoning`, `logprobs`, `max_completion_tokens`, `max_tokens`, `parallel_tool_calls`, `presence_penalty`, `reasoning`, `reasoning_effort`, `repetition_penalty`, `response_format`, `seed`, `stop`, `structured_outputs`, `temperature`, `tool_choice`, `tools`, `top_k`, `top_logprobs`, `top_p`

## Example

```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "google/gemma-4-31b-it",
    "messages": [{"role": "user", "content": "Hello"}]
  }'
```
