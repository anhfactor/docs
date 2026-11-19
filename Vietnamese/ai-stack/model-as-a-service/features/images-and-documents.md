---
description: "Model có image trong danh sách đầu vào nhận được ảnh cùng văn bản. Lọc bảng Danh sách model theo \"image\"."
---

# Ảnh & tài liệu

## Ảnh

Gửi URL HTTPS hoặc data URL base64 (`data:image/png;base64,…`). Hỗ trợ PNG, JPEG, WebP và GIF.

{% tabs %}
{% tab title="Chat" %}
```json
{
  "model": "qwen/qwen3.6-flash",
  "messages": [{
    "role": "user",
    "content": [
      {"type": "text", "text": "What color is this image? One word."},
      {"type": "image_url", "image_url": {"url": "data:image/png;base64,iVBORw0KGgo..."}}
    ]
  }]
}
```
{% endtab %}
{% tab title="Messages" %}
```json
{
  "model": "qwen/qwen3.6-flash",
  "max_tokens": 1024,
  "messages": [{
    "role": "user",
    "content": [
      {"type": "image", "source": {"type": "base64", "media_type": "image/png", "data": "iVBORw0KGgo..."}},
      {"type": "text", "text": "What color is this image? One word."}
    ]
  }]
}
```
{% endtab %}
{% tab title="Responses" %}
```json
{
  "model": "qwen/qwen3.6-flash",
  "input": [{
    "role": "user",
    "content": [
      {"type": "input_text", "text": "What color is this image? One word."},
      {"type": "input_image", "image_url": "data:image/png;base64,iVBORw0KGgo..."}
    ]
  }]
}
```
{% endtab %}
{% tab title="Python" %}
```python
import base64

with open("photo.png", "rb") as f:
    b64 = base64.b64encode(f.read()).decode()

completion = client.chat.completions.create(
    model="qwen/qwen3.6-flash",
    messages=[{"role": "user", "content": [
        {"type": "text", "text": "Describe this image."},
        {"type": "image_url", "image_url": {"url": f"data:image/png;base64,{b64}"}},
    ]}],
)
```
{% endtab %}
{% endtabs %}

Ảnh gửi cho model chỉ nhận văn bản bị bỏ qua (request vẫn trả 200); kiểm tra `input_modalities` của model trước khi gửi. Ảnh được tính vào token đầu vào.

## Tài liệu (PDF, Word…)

{% hint style="warning" %}
Đầu vào PDF/file gốc chỉ dùng được trên model có `file` trong các loại đầu vào (xem [Danh sách model](../models/README.md)). Trên model khác, phần `file` và block `document` PDF trả 400: hãy tự trích xuất văn bản và gửi dạng text (hoặc block `document` của Messages với `source.type: "text"`). Với tài liệu scan, dùng model OCR `greennode/idp`.
{% endhint %}

{% code title="Messages — text document" %}
```json
{
  "type": "document",
  "source": { "type": "text", "media_type": "text/plain", "data": "Invoice #123 ... Total: 42 USD" },
  "title": "invoice.pdf"
}
```
{% endcode %}
