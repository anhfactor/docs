---
description: "GreenNode MaaS models: context length, input modalities, endpoints and reasoning for each model."
---

# Model list

> This page is generated from the GreenNode MaaS model catalog. Manual edits are overwritten on the next sync.

Every model is addressed as `vendor/model`. Click a model for details and a ready-to-run request.

**Reasoning** column: **Always on** = the model always reasons; you can lower `reasoning_effort` but not turn it off; **On by default** = reasons unless you turn it off; **Optional** = reasons only when you turn it on; **—** = no reasoning support.

## Chat

| Model ID | Name | Context | Max output | Input | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`deepseek/deepseek-v4-flash`](deepseek/deepseek-v4-flash.md) | DeepSeek V4 Flash | 1M | 384K | text | chat, responses, messages | Always on |
| [`deepseek/deepseek-v4-pro`](deepseek/deepseek-v4-pro.md) | DeepSeek V4 Pro | 1M | 384K | text | chat, responses, messages | Always on |
| [`deepseek/deepseek-v4.1-flash-thirdparty`](deepseek/deepseek-v4.1-flash-thirdparty.md) | DeepSeek V4.1 Flash | 1M | 384K | text, image | chat, responses, messages | On by default |
| [`google/gemma-4-31b-it`](google/gemma-4-31b-it.md) | Gemma 4 31B-IT | 262K | 32K | text, image | chat, responses, messages | Optional |
| [`kimi/kimi-k2.6`](kimi/kimi-k2.6.md) | Kimi K2.6 | 256K | 256K | text, image, video | chat, responses, messages | On by default |
| [`kimi/kimi-k2.7-code`](kimi/kimi-k2.7-code.md) | Kimi K2.7 Code | 256K | 256K | text, image, video | chat, responses, messages | Always on |
| [`minimax/minimax-m2.5`](minimax/minimax-m2.5.md) | MiniMax M2.5 | 192K | 128K | text | chat, responses, messages | Always on |
| [`minimax/minimax-m3`](minimax/minimax-m3.md) | MiniMax M3 | 1M | 512K | text, image, video | chat, responses, messages | Always on |
| [`qwen/qwen3.6-flash`](qwen/qwen3.6-flash.md) | Qwen 3.6 Flash | 1M | 64K | text, image, video | chat, responses, messages | On by default |
| [`qwen/qwen3.6-plus`](qwen/qwen3.6-plus.md) | Qwen 3.6 Plus | 1M | 64K | text, image, video | chat, responses, messages | On by default |
| [`qwen/qwen3.7-plus`](qwen/qwen3.7-plus.md) | Qwen 3.7 Plus | 1M | 128K | text, image, video | chat, responses, messages | On by default |
| [`qwen/qwen3.8-27b`](qwen/qwen3.8-27b.md) | Qwen 3.8 27B | 1M | 1M | text, image | chat, responses, messages | On by default |
| [`qwen/qwen3.8-flash`](qwen/qwen3.8-flash.md) | Qwen 3.8 Flash | 1M | 128K | text, image, video | chat, responses, messages | On by default |
| [`qwen/qwen3.8-max`](qwen/qwen3.8-max.md) | Qwen 3.8 Max | 1M | 128K | text, image, video | chat, responses, messages | On by default |
| [`z-ai/glm-5.2-thirdparty`](z-ai/glm-5.2-thirdparty.md) | GLM-5.2 | 1M | 128K | text | chat, responses, messages | On by default |
| [`z-ai/glm-5.3`](z-ai/glm-5.3.md) | GLM-5.3 | 300K | 128K | text | chat, responses, messages | Always on |
| [`z-ai/glm-5.3-flash`](z-ai/glm-5.3-flash.md) | GLM-5.3 Flash | 1M | 128K | text, image, file, video | chat, responses, messages | Always on |
| [`z-ai/glm-5.3-flash-thirdparty`](z-ai/glm-5.3-flash-thirdparty.md) | GLM-5.3 Flash | 1M | 128K | text, image, video | chat, responses, messages | Always on |

## Embedding

| Model ID | Name | Context | Max output | Input | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`baai/bge-m3`](baai/bge-m3.md) | BGE-M3 | 8K | — | text | embedding | — |
| [`qwen/qwen3-embedding-8b`](qwen/qwen3-embedding-8b.md) | Qwen 3 Embedding 8B | 33K | — | text | embedding | — |

## Rerank

| Model ID | Name | Context | Max output | Input | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`baai/bge-reranker-v2-m3`](baai/bge-reranker-v2-m3.md) | BGE Reranker v2 m3 | 8K | — | text | rerank | — |
| [`qwen/qwen3-reranker-8b`](qwen/qwen3-reranker-8b.md) | Qwen 3 Reranker 8B | 33K | — | text | rerank | — |

## OCR

| Model ID | Name | Context | Max output | Input | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`greennode/idp`](greennode/idp.md) | GreenNode IDP | 164K | — | image, file | ocr | — |
