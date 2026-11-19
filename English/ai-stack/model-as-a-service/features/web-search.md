---
description: "Add a web_search tool to your request and the gateway runs the searches for the model, then returns a grounded answer with sources. You don't execute anything."
---

# Web search

{% hint style="info" %}
Available on `google/gemma-4-31b-it` (checked on production 2026-11-14). Other models reject the tool (400 `invalid_request`) or answer without searching.
{% endhint %}

## Adding the tool

| Endpoint | `tools` entry |
| --- | --- |
| Chat | `{"type": "web_search"}` |
| Responses | `{"type": "web_search"}` |
| Messages | `{"type": "web_search_20250305", "name": "web_search"}` |

Optional settings on the tool entry:

| Option | Meaning |
| --- | --- |
| `max_uses` | Max searches per request. |
| `allowed_domains` | Only use results from these domains (subdomains included). |
| `blocked_domains` | Never use results from these domains. |

The model decides whether to search. A question it can answer on its own may come back without any search (`web_search_requests: 0`).

## Chat Completions

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/chat/completions \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "google/gemma-4-31b-it",
    "messages": [{"role": "user", "content": "What is the latest stable version of Python? Answer briefly."}],
    "tools": [{"type": "web_search", "max_uses": 2}]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
completion = client.chat.completions.create(
    model="google/gemma-4-31b-it",
    messages=[{"role": "user", "content": "What is the latest stable version of Python? Answer briefly."}],
    tools=[{"type": "web_search", "max_uses": 2}],
)
print(completion.choices[0].message.content)
```
{% endtab %}
{% endtabs %}

Chat has no citation field, so sources are listed at the end of the answer text:

{% code title="choices[0].message.content" %}
```
**Python 3.15.2** is the latest stable release (released October 25, 2026) [5][6].

Sources:
- [5] Download Python | Python.org — https://www.python.org/downloads
- [6] Python | endoflife.date — https://endoflife.date/python
```
{% endcode %}

You can mix `web_search` with your own function tools; if the model calls one of yours you get normal `tool_calls` (`finish_reason: "tool_calls"`).

## Messages

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/messages \
  -H "x-api-key: $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "google/gemma-4-31b-it",
    "max_tokens": 2048,
    "messages": [{"role": "user", "content": "What is the latest stable version of Python? Answer briefly."}],
    "tools": [{"type": "web_search_20250305", "name": "web_search", "max_uses": 2}]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
message = client.messages.create(
    model="google/gemma-4-31b-it",
    max_tokens=2048,
    messages=[{"role": "user", "content": "What is the latest stable version of Python? Answer briefly."}],
    tools=[{"type": "web_search_20250305", "name": "web_search", "max_uses": 2}],
)
for block in message.content:
    if block.type == "text":
        print(block.text)
```
{% endtab %}
{% endtabs %}

{% code title="content (trimmed)" %}
```json
[
  { "type": "text", "text": "I'll search for that." },
  { "type": "server_tool_use", "id": "call_99f25267ef81a553", "name": "web_search",
    "input": { "query": "latest stable Python version" } },
  { "type": "web_search_tool_result", "tool_use_id": "call_99f25267ef81a553", "content": [
    { "type": "web_search_result", "url": "https://en.wikipedia.org/wiki/History_of_Python",
      "title": "History of Python - Wikipedia", "encrypted_content": "..." },
    ...
  ]},
  { "type": "text", "text": "The latest stable version of Python is **Python 3.15** ... [1]",
    "citations": [
      { "type": "web_search_result_location", "url": "https://en.wikipedia.org/wiki/History_of_Python",
        "title": "History of Python - Wikipedia", "cited_text": "As of October 2026 Python 3.15 is ..." }
    ] }
]
// usage.server_tool_use: { "web_search_requests": 1, "web_fetch_requests": 0 }
```
{% endcode %}

## Responses

{% tabs %}
{% tab title="curl" %}
```bash
curl https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1/responses \
  -H "Authorization: Bearer $GREENNODE_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "google/gemma-4-31b-it",
    "input": "What is the latest stable version of Python? Answer briefly.",
    "tools": [{"type": "web_search", "max_uses": 2}]
  }'
```
{% endtab %}
{% tab title="Python" %}
```python
response = client.responses.create(
    model="google/gemma-4-31b-it",
    input="What is the latest stable version of Python? Answer briefly.",
    tools=[{"type": "web_search"}],
)
print(response.output_text)
```
{% endtab %}
{% endtabs %}

{% code title="output (trimmed)" %}
```json
[
  { "type": "web_search_call", "id": "call_8c0e53a414e5a6af", "status": "completed",
    "action": { "type": "search", "query": "latest stable version of Python" },
    "results": [
      { "url": "https://en.wikipedia.org/wiki/History_of_Python",
        "title": "History of Python - Wikipedia", "content": "As of October 2026 Python 3.15 is ..." },
      ...
    ] },
  { "type": "message", "role": "assistant", "status": "completed", "content": [
    { "type": "output_text",
      "text": "The latest stable version of Python is **Python 3.15** ... [1]\n\nSources:\n- [1] History of Python - Wikipedia — https://en.wikipedia.org/wiki/History_of_Python",
      "annotations": [
        { "type": "url_citation", "url": "https://en.wikipedia.org/wiki/History_of_Python",
          "title": "History of Python - Wikipedia", "cited_text": "As of October 2026 Python 3.15 is ..." }
      ] }
  ] }
]
```
{% endcode %}

## Streaming

Web search works with `stream: true` on all three endpoints. The search runs before the answer streams, so expect a pause of a few seconds before the first text token.

| Endpoint | What you see in the stream |
| --- | --- |
| Chat | Only the answer text (with the `Sources:` list) as normal `delta.content` chunks. |
| Messages | `content_block_start` for `server_tool_use` → `web_search_tool_result` → `text` blocks |
| Responses | `response.output_item.added` (`web_search_call`) → `response.web_search_call.in_progress` → `response.web_search_call.completed` → the message item and `response.output_text.delta` |

## Usage

Messages and Responses report the number of searches in `usage.server_tool_use.web_search_requests`. Search results are fed to the model as input, so a searched request uses several thousand extra input tokens.

## Multi-turn tips

* Send the assistant's blocks/items back **unchanged** in the next turn — including `encrypted_content` (Messages) and `results` (Responses). They carry the search results the model saw, so follow-up questions are answered from them.
* Never invent a tool result for a server tool call — the gateway runs those itself.
* Each search adds a few seconds of latency.
