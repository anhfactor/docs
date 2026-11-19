---
description: "Thêm tool web_search vào request, gateway sẽ thực hiện tìm kiếm thay model và trả về câu trả lời có dẫn nguồn. Bạn không cần tự thực thi gì."
---

# Tìm kiếm web

{% hint style="info" %}
Có trên `google/gemma-4-31b-it` (đã đối chiếu production ngày 2026-11-14). Các model khác từ chối tool (400 `invalid_request`) hoặc trả lời mà không tìm kiếm.
{% endhint %}

## Thêm tool

| Endpoint | `tools` entry |
| --- | --- |
| Chat | `{"type": "web_search"}` |
| Responses | `{"type": "web_search"}` |
| Messages | `{"type": "web_search_20250305", "name": "web_search"}` |

Tùy chọn trên tool:

| Option | Ý nghĩa |
| --- | --- |
| `max_uses` | Số lần tìm kiếm tối đa mỗi request. |
| `allowed_domains` | Chỉ dùng kết quả từ các domain này (gồm cả subdomain). |
| `blocked_domains` | Không dùng kết quả từ các domain này. |

Model tự quyết định có tìm kiếm hay không. Câu hỏi model tự trả lời được có thể không phát sinh lượt tìm nào (`web_search_requests: 0`).

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

Chat không có trường trích dẫn, nên nguồn được liệt kê ở cuối câu trả lời:

{% code title="choices[0].message.content" %}
```
**Python 3.15.2** is the latest stable release (released October 25, 2026) [5][6].

Sources:
- [5] Download Python | Python.org — https://www.python.org/downloads
- [6] Python | endoflife.date — https://endoflife.date/python
```
{% endcode %}

Có thể dùng `web_search` cùng function tool của bạn; nếu model gọi tool của bạn, bạn nhận `tool_calls` như bình thường (`finish_reason: "tool_calls"`).

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

Web search hoạt động với `stream: true` trên cả ba endpoint. Việc tìm kiếm diễn ra trước khi câu trả lời được stream, nên sẽ có vài giây chờ trước token văn bản đầu tiên.

| Endpoint | Nội dung trong stream |
| --- | --- |
| Chat | Chỉ có văn bản trả lời (kèm danh sách `Sources:`) dưới dạng chunk `delta.content` bình thường. |
| Messages | `content_block_start` cho `server_tool_use` → `web_search_tool_result` → `text` |
| Responses | `response.output_item.added` (`web_search_call`) → `response.web_search_call.in_progress` → `response.web_search_call.completed` → item message và `response.output_text.delta` |

## Usage

Messages và Responses báo số lần tìm kiếm trong `usage.server_tool_use.web_search_requests`. Kết quả tìm kiếm được đưa vào model như input, nên một request có tìm kiếm dùng thêm vài nghìn token đầu vào.

## Lưu ý hội thoại nhiều lượt

* Gửi lại các block/item của assistant **nguyên vẹn** ở lượt sau — kể cả `encrypted_content` (Messages) và `results` (Responses). Chúng chứa kết quả tìm kiếm model đã thấy, giúp trả lời các câu hỏi tiếp theo.
* Không tự tạo kết quả cho server tool — gateway tự thực hiện các lời gọi đó.
* Mỗi lượt tìm kiếm làm tăng độ trễ vài giây.
