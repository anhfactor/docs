---
description: "Set \"stream\": true to receive tokens as server-sent events (SSE) while they are generated. Each endpoint streams in its native event format."
---

# Streaming

## Chat Completions

{% tabs %}
{% tab title="curl" %}
```bash
curl -N https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "qwen/qwen3.6-flash",
    "messages": [{"role": "user", "content": "Count 1 to 3."}],
    "stream": true,
    "stream_options": {"include_usage": true}
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
stream = client.chat.completions.create(
    model="qwen/qwen3.6-flash",
    messages=[{"role": "user", "content": "Count 1 to 3."}],
    stream=True,
    stream_options={"include_usage": True},
)
for chunk in stream:
    if chunk.choices and chunk.choices[0].delta.content:
        print(chunk.choices[0].delta.content, end="", flush=True)
    if chunk.usage:
        print("\n", chunk.usage)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
const stream = await client.chat.completions.create({
  model: "qwen/qwen3.6-flash",
  messages: [{ role: "user", content: "Count 1 to 3." }],
  stream: true,
  stream_options: { include_usage: true },
});
for await (const chunk of stream) {
  process.stdout.write(chunk.choices[0]?.delta?.content ?? "");
  if (chunk.usage) console.log("\n", chunk.usage);
}
```
{% endtab %}
{% endtabs %}

{% code title="SSE (trimmed)" %}
```text
data: {"object":"chat.completion.chunk","choices":[{"index":0,"delta":{"role":"assistant","content":""}}]}

data: {"object":"chat.completion.chunk","choices":[{"index":0,"delta":{"reasoning_content":"Thinking"}}]}

data: {"object":"chat.completion.chunk","choices":[{"index":0,"delta":{"content":"1, 2"}}]}

data: {"object":"chat.completion.chunk","choices":[{"index":0,"delta":{"content":", 3."}}]}

data: {"object":"chat.completion.chunk","choices":[{"index":0,"delta":{},"finish_reason":"stop"}]}

data: {"object":"chat.completion.chunk","choices":[],"usage":{"prompt_tokens":17,"completion_tokens":394,"total_tokens":411,"completion_tokens_details":{"reasoning_tokens":381}}}

data: [DONE]
```
{% endcode %}

* Reasoning streams in `delta.reasoning_content`; the answer in `delta.content`.
* With `include_usage`, the last chunk before `[DONE]` has empty `choices` and the `usage` object.

## Messages

Standard Anthropic event sequence:

{% code title="event order" %}
```
message_start → content_block_start → content_block_delta (×N) → content_block_stop
             → message_delta (stop_reason, usage) → message_stop
```
{% endcode %}

{% tabs %}
{% tab title="Python" %}
```python
with client.messages.stream(
    model="qwen/qwen3.6-flash",
    max_tokens=1024,
    messages=[{"role": "user", "content": "Count 1 to 3."}],
) as stream:
    for text in stream.text_stream:
        print(text, end="", flush=True)
```
{% endtab %}
{% tab title="TypeScript" %}
```typescript
const stream = client.messages.stream({
  model: "qwen/qwen3.6-flash",
  max_tokens: 1024,
  messages: [{ role: "user", content: "Count 1 to 3." }],
});
stream.on("text", (t) => process.stdout.write(t));
await stream.finalMessage();
```
{% endtab %}
{% endtabs %}

## Responses

{% code title="event order" %}
```
response.created → response.in_progress
[reasoning models only]
→ response.output_item.added (reasoning) → response.reasoning_summary_part.added
→ response.reasoning_summary_text.delta (×N) → response.reasoning_summary_text.done
→ response.reasoning_summary_part.done → response.output_item.done
[answer]
→ response.output_item.added → response.content_part.added
→ response.output_text.delta (×N) → response.output_text.done
→ response.content_part.done → response.output_item.done → response.completed (usage)
```
{% endcode %}

## Tips

* Reasoning models may spend a while thinking before the first `content` token. Show a "thinking…" state, and don't treat silence as failure — set read timeouts of several minutes.
* The gateway does not retry a streaming request. If the request fails or the stream breaks, your client must retry the whole request.
* Errors that happen before streaming starts come back as normal JSON error responses with an HTTP error status, not as SSE.
