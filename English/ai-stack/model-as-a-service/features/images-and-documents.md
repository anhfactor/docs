---
description: "Models whose input modalities include image accept images alongside text. Filter the Models table by \"image\"."
---

# Images & documents

## Images

Send an HTTPS URL or a base64 data URL (`data:image/png;base64,…`). PNG, JPEG, WebP and GIF are accepted.

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

An image sent to a text-only model is ignored (the request still returns 200); check the model's `input_modalities` before sending. Images count toward input tokens.

## Documents (PDF, Word…)

{% hint style="warning" %}
Native PDF/file input works only on models that list `file` among their input types (see [Models](../models/README.md)). On other models `file` parts and PDF `document` blocks return 400: extract the text on your side and send it as text (or as a Messages `document` block with `source.type: "text"`). For scanned documents use the OCR model `greennode/idp`.
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
