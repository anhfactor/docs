---
description: >-
  AI Platform provides Model as a Service (MaaS), enabling developers and
  enterprises to easily integrate powerful AI models into their applications.
---

# Model as a Service (MaaS)

Access the [Models ](https://aiplatform.console.greennode.ai/models)section in AI Platform:

* To use and enable any model, you need an API key. [See more details](../ai-platform/getting-started-with-ai-platform.md).

You can filter models using the options on the left sidebar:

* Provider: Google, Anthropic, OpenAI, GreenNode, ...
* Model Type:
  * Chat: Designed for interactive conversations. Called through Chat Completions, Messages (Anthropic) or Responses, depending on the model.
  * Embedding: Converts data (text, images, audio, etc.) into high-dimensional vectors, allowing machines to understand and compare semantics for search, classification, or recommendation.
  * Rerank: Reorders a list of documents by relevance to a query.
  * OCR: Extracts text and data from images and documents.
* Use Case::
  * Vietnamese: Optimized for Vietnamese language tasks.
  * General Tasks: Suitable for a wide range of general-purpose tasks.
  * Translation: Specialized for translation tasks.
  * Research: Supports research-related tasks.
  * Finance: Focused on financial domain applications.
  * Marketing: Optimized for marketing use cases.
  * Technology: Designed for technology-related tasks.

### Enable / Disable Models

1. Click the "Toggle models" button. Users must activate billing to enable models. For Prepaid users, quota must be added before enabling models, while Postpaid users can enable and use models immediately. Refer to [pricing details](pricing.md).\
   ![](<../../.gitbook/assets/image (390).png>)
2. Model Selection: A popup window will appear, allowing you to search and filter models by Provider, Status, or Type.
3. Enable/disable models individually or in bulk.
4. Save your changes.

<figure><img src="../../.gitbook/assets/image (391).png" alt=""><figcaption></figcaption></figure>

To start experimenting and comparing models before integration, you can use the [Playground](playground.md)

<figure><img src="../../.gitbook/assets/image (392).png" alt=""><figcaption></figcaption></figure>

### Experiment with AI Platform Playground

Before integrating into your application, explore model capabilities in the Playground:

* Compare different models based on latency, accuracy, and capabilities.
* Send test requests interactively and evaluate outputs.
* Fine-tune parameters to find the best model for your specific use case.

[**Build with AI Platform MaaS API**](maas-api.md)

After testing in the Playground, you can access models via AI Platform MaaS:

* Supports both synchronous requests and streaming for real-time applications.

### Data Security and Privacy

* Data in transit is encrypted with **TLS 1.2 or later**.
