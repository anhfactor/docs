---
description: "Run popular coding agents on GreenNode models. Strong choices for agentic coding: z-ai/glm-5.3, kimi/kimi-k2.7-code, qwen/qwen3.8-max, deepseek/deepseek-v4-pro."
---

# Coding agents

## Claude Code

Claude Code speaks the Messages API. Set these environment variables before running `claude`:

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

Or persist them in `~/.claude/settings.json`:

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

Claude Code's built-in WebSearch tool works when the main model supports [web search](../features/web-search.md).

## Codex CLI

Codex uses the Responses API. Add a provider to `~/.codex/config.toml`:

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

Keep `multi_agent = false`: recent Codex versions otherwise send OpenAI-only sub-agent tools, and the request is rejected with `400 invalid_request`. Then run `codex` with `GREENNODE_API_KEY` set.

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

## Tips

* Agents send long, growing histories — [prompt caching](../features/prompt-caching.md) makes them much faster. Avoid tools/plugins that rewrite earlier turns.
* Check the model's max output on the [Models](../models/README.md) page — some (e.g. Kimi, 16k) are lower than agents' default output settings.
