---
description: "Chạy các coding agent phổ biến trên model của GreenNode. Lựa chọn tốt cho lập trình dạng agent: z-ai/glm-5.3, kimi/kimi-k2.7-code, qwen/qwen3.8-max, deepseek/deepseek-v4-pro."
---

# Coding agent

## Claude Code

Claude Code dùng Messages API. Đặt các biến môi trường sau trước khi chạy `claude`:

{% code title="shell" %}
```bash
export ANTHROPIC_BASE_URL="https://maas-llm-aiplatform-hcm.api.vngcloud.vn"
export ANTHROPIC_AUTH_TOKEN="$GREENNODE_API_KEY"
export ANTHROPIC_MODEL="z-ai/glm-5.3"
export ANTHROPIC_DEFAULT_HAIKU_MODEL="z-ai/glm-5.3-flash"   # background / quick tasks
export CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS=1             # avoid Anthropic-only beta fields
claude
```
{% endcode %}

Hoặc lưu cố định trong `~/.claude/settings.json`:

{% code title="~/.claude/settings.json" %}
```json
{
  "env": {
    "ANTHROPIC_BASE_URL": "https://maas-llm-aiplatform-hcm.api.vngcloud.vn",
    "ANTHROPIC_AUTH_TOKEN": "vn-...",
    "ANTHROPIC_MODEL": "z-ai/glm-5.3",
    "ANTHROPIC_DEFAULT_HAIKU_MODEL": "z-ai/glm-5.3-flash",
    "CLAUDE_CODE_DISABLE_EXPERIMENTAL_BETAS": "1"
  }
}
```
{% endcode %}

Tool WebSearch có sẵn của Claude Code hoạt động khi model chính hỗ trợ [web search](../features/web-search.md).

## Codex CLI

Codex dùng Responses API. Thêm provider vào `~/.codex/config.toml`:

{% code title="~/.codex/config.toml" %}
```
model = "z-ai/glm-5.3"
model_provider = "greennode"
model_reasoning_effort = "medium"

[model_providers.greennode]
name = "GreenNode MaaS"
base_url = "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1"
env_key = "GREENNODE_API_KEY"
wire_api = "responses"

[features]
multi_agent = false   # sub-agent tools are OpenAI-only
```
{% endcode %}

Giữ `multi_agent = false`: các bản Codex gần đây nếu không sẽ gửi kèm tool sub-agent chỉ dành cho OpenAI, và request bị từ chối với lỗi `400 invalid_request`. Sau đó chạy `codex` với biến `GREENNODE_API_KEY` đã đặt.

## OpenCode

{% code title="opencode.json" %}
```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "greennode": {
      "npm": "@ai-sdk/openai-compatible",
      "name": "GreenNode MaaS",
      "options": {
        "baseURL": "https://maas-llm-aiplatform-hcm.api.vngcloud.vn/v1",
        "apiKey": "{env:GREENNODE_API_KEY}"
      },
      "models": {
        "z-ai/glm-5.3": { "name": "GLM-5.3" },
        "kimi/kimi-k2.7-code": { "name": "Kimi K2.7 Code" }
      }
    }
  },
  "model": "greennode/z-ai/glm-5.3"
}
```
{% endcode %}

## Lưu ý

* Agent gửi lịch sử hội thoại dài và tăng dần — [prompt caching](../features/prompt-caching.md) giúp nhanh hơn đáng kể. Tránh các plugin sửa đổi các lượt trước đó.
* Kiểm tra output tối đa của model ở trang [Danh sách model](../models/README.md) — một số model (ví dụ Kimi, 16k) thấp hơn thiết lập output mặc định của agent.
