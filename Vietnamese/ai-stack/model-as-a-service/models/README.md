---
description: "Danh sách model GreenNode MaaS: độ dài ngữ cảnh, đầu vào, endpoint và reasoning của từng model."
---

# Danh sách model

Mỗi model được gọi theo dạng `vendor/model`. Bấm vào tên model để xem chi tiết và ví dụ gọi API.

Cột **Reasoning**: **Luôn bật** = model luôn suy luận, chỉ giảm được mức `reasoning_effort` chứ không tắt được; **Mặc định bật** = có suy luận khi không truyền gì, tắt được; **Tùy chọn** = chỉ suy luận khi bạn bật; **—** = model không hỗ trợ suy luận.

## Chat

| Model ID | Tên | Ngữ cảnh | Output tối đa | Đầu vào | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`deepseek/deepseek-v4-flash`](deepseek/deepseek-v4-flash.md) | DeepSeek V4 Flash | 1M | 384K | text | chat, responses, messages | Luôn bật |
| [`deepseek/deepseek-v4-pro`](deepseek/deepseek-v4-pro.md) | DeepSeek V4 Pro | 1M | 384K | text | chat, responses, messages | Luôn bật |
| [`deepseek/deepseek-v4.1-flash-thirdparty`](deepseek/deepseek-v4.1-flash-thirdparty.md) | DeepSeek V4.1 Flash | 1M | 384K | text, image | chat, responses, messages | Mặc định bật |
| [`google/gemma-4-31b-it`](google/gemma-4-31b-it.md) | Gemma 4 31B-IT | 262K | 32K | text, image | chat, responses, messages | Tùy chọn |
| [`kimi/kimi-k2.6`](kimi/kimi-k2.6.md) | Kimi K2.6 | 256K | 256K | text, image, video | chat, responses, messages | Mặc định bật |
| [`kimi/kimi-k2.7-code`](kimi/kimi-k2.7-code.md) | Kimi K2.7 Code | 256K | 256K | text, image, video | chat, responses, messages | Luôn bật |
| [`minimax/minimax-m2.5`](minimax/minimax-m2.5.md) | MiniMax M2.5 | 192K | 128K | text | chat, responses, messages | Luôn bật |
| [`minimax/minimax-m3`](minimax/minimax-m3.md) | MiniMax M3 | 1M | 512K | text, image, video | chat, responses, messages | Luôn bật |
| [`qwen/qwen3.6-flash`](qwen/qwen3.6-flash.md) | Qwen 3.6 Flash | 1M | 64K | text, image, video | chat, responses, messages | Mặc định bật |
| [`qwen/qwen3.6-plus`](qwen/qwen3.6-plus.md) | Qwen 3.6 Plus | 1M | 64K | text, image, video | chat, responses, messages | Mặc định bật |
| [`qwen/qwen3.7-plus`](qwen/qwen3.7-plus.md) | Qwen 3.7 Plus | 1M | 128K | text, image, video | chat, responses, messages | Mặc định bật |
| [`qwen/qwen3.8-27b`](qwen/qwen3.8-27b.md) | Qwen 3.8 27B | 1M | 1M | text, image | chat, responses, messages | Mặc định bật |
| [`qwen/qwen3.8-flash`](qwen/qwen3.8-flash.md) | Qwen 3.8 Flash | 1M | 128K | text, image, video | chat, responses, messages | Mặc định bật |
| [`qwen/qwen3.8-max`](qwen/qwen3.8-max.md) | Qwen 3.8 Max | 1M | 128K | text, image, video | chat, responses, messages | Mặc định bật |
| [`z-ai/glm-5.2-thirdparty`](z-ai/glm-5.2-thirdparty.md) | GLM-5.2 | 1M | 128K | text | chat, responses, messages | Mặc định bật |
| [`z-ai/glm-5.3`](z-ai/glm-5.3.md) | GLM-5.3 | 300K | 128K | text | chat, responses, messages | Luôn bật |
| [`z-ai/glm-5.3-flash`](z-ai/glm-5.3-flash.md) | GLM-5.3 Flash | 1M | 128K | text, image, file, video | chat, responses, messages | Luôn bật |
| [`z-ai/glm-5.3-flash-thirdparty`](z-ai/glm-5.3-flash-thirdparty.md) | GLM-5.3 Flash | 1M | 128K | text, image, video | chat, responses, messages | Luôn bật |

## Embedding

| Model ID | Tên | Ngữ cảnh | Output tối đa | Đầu vào | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`baai/bge-m3`](baai/bge-m3.md) | BGE-M3 | 8K | — | text | embedding | — |
| [`qwen/qwen3-embedding-8b`](qwen/qwen3-embedding-8b.md) | Qwen 3 Embedding 8B | 33K | — | text | embedding | — |

## Rerank

| Model ID | Tên | Ngữ cảnh | Output tối đa | Đầu vào | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`baai/bge-reranker-v2-m3`](baai/bge-reranker-v2-m3.md) | BGE Reranker v2 m3 | 8K | — | text | rerank | — |
| [`qwen/qwen3-reranker-8b`](qwen/qwen3-reranker-8b.md) | Qwen 3 Reranker 8B | 33K | — | text | rerank | — |

## OCR

| Model ID | Tên | Ngữ cảnh | Output tối đa | Đầu vào | Endpoints | Reasoning |
| --- | --- | --- | --- | --- | --- | --- |
| [`greennode/idp`](greennode/idp.md) | GreenNode IDP | 164K | — | image, file | ocr | — |
