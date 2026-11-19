---
description: >-
  Playground is a visual interface on the platform that allows you to quickly
  experiment with and compare AI models without writing code. It is an ideal
  environment to explore capabilities.
---

# Playground

### Access [Playground](https://aiplatform.console.greennode.ai/playground)

### Model Testing Guide

1. Select the model type based on your task: Chat, Embedding, Rerank, OCR
2. Select a model: In the right-hand panel, choose a model from the list
3. Set up the prompt
   * In the System prompt section, define instructions or context for the model. You can also add examples to guide its behavior.
4. [Adjust parameters:](playground.md#model-parameter-tuning-guide)

<figure><img src="../../.gitbook/assets/image (393).png" alt=""><figcaption></figcaption></figure>

5. Start experimenting:

* Enter your prompt and observe how different models respond.

6. Save configuration:

* Copy as code: Click the icon `<> API`
*   Select programming language:

    * Curl: This command can be used in Terminal or Command Prompt, allowing you to test the API directly without writing code.
    * Python: Provides ready-to-use Python code snippets for your projects.
    * TypeScript: Provides TypeScript/Node.js code snippets, suitable for web and server-side applications.

    <figure><img src="../../.gitbook/assets/image (394).png" alt=""><figcaption></figcaption></figure>

### Model Parameter Tuning Guide

When using Playground, you can adjust the following parameters to control model outputs. These parameters may vary depending on the selected model type.

**Chat Models**

* Past messages included: Number of recent messages the model will remember.\
  Range: 1 - 20 (Default: 10).
* Maximum token output: Maximum number of tokens the model can generate.\
  Range and default depend on the model (e.g. 1 - 8,192, default 2,000; or 1 - 32,768, default 4,096; up to 131,072 on some models).
* Temperature: Controls randomness of responses.
  * 0: Deterministic, consistent results.
  * < 1: Focused and accurate results, ideal for summarization or Q\&A.
  * ≈ 1: Encourages creativity and diversity in responses.
  * Range: 0 - 2 (Default: 1).
* Top P: Probability threshold for token selection, balancing naturalness and diversity.
  * Range: 0 - 1 (Default: 0.7 or 0.95 depending on the model).
* Presence Penalty (some models only): Penalizes repeated words, encouraging new topics and reducing repetition.
  * Range: -2 to 2 (Default: 0).

**Embedding Models**

* Encoding format: Output vector format.
  * BGE-M3: Dense, Sparse, Sparse dense (Default: Dense).
  * Qwen3 Embedding 8B: Float.

**Rerank Models**

* Top N: How many candidates to keep after reranking (minimum 1).

**OCR Model (GreenNode IDP)**

* Document type: 15 types (Default: Citizen ID).
* File type: Image (jpg, png, bmp, tif; up to 10 MB) or PDF (up to 50 MB).

For more detailed parameters, refer to the documentation of [vLLM](https://docs.vllm.ai) and [OpenAI](https://platform.openai.com/docs/api-reference/introduction).

### Model Comparison

This feature allows you to run and compare outputs from two models simultaneously.

* Click the Compare button to open two parallel chat windows.
* You can enter a prompt and send it to both models at the same time to evaluate their responses and performance.
