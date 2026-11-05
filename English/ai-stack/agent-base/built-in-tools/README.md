# Built-in Tools

Built-in Tools let your agent **run code** and **drive a real browser** inside a sandbox that is isolated per session — without provisioning any infrastructure, image, or container of your own.

Two tools are available:

| Tool | Use it to |
|---|---|
| **Code Interpreter** | Run Python and shell commands, read/write files, run background processes — each session in its own fully isolated sandbox |
| **Browser** | Drive a real Chrome (via CDP), watch the screen live over noVNC, and replay session recordings |

Both tools integrate over **MCP** — your agent connects to an MCP endpoint provisioned by GreenNode, and the tools appear like any other MCP tools.

{% hint style="info" %}
Built-in Tools is currently being rolled out by **whitelist**. If your account is not yet enabled, contact [support@greennode.ai](mailto:support@greennode.ai), hotline **19001549**, or the [Support Center](https://helpdesk.greennode.ai/portal/vi/home) to be added to the list.
{% endhint %}

---

## Architecture

Each of your sessions runs inside its own sandbox, provisioned in advance by the platform, so creating a session takes only a few seconds. Both tools share the same sandbox foundation — they differ in the product layer on top:

<figure><img src="../../../.gitbook/assets/Agentbase-image/agentbase-code-interpreter-architecture.svg" alt=""><figcaption><p>Code Interpreter — the agent calls tools over MCP, code runs in an isolated sandbox</p></figcaption></figure>

<figure><img src="../../../.gitbook/assets/Agentbase-image/agentbase-browser-architecture.svg" alt=""><figcaption><p>Browser — the agent drives Chromium inside a sandbox over CDP</p></figcaption></figure>

Main layers:

- **Built-in Tools** — the product layer: manages resources you own (each Code Interpreter / Browser has an id, name, status), plus quotas, authentication, and lifecycle. The sandbox runtime underneath stays hidden — its id and URL are never exposed.
- **AgentBase Runtime** — the platform layer: manages the sandbox lifecycle — assigns a dedicated sandbox to each new session, tracks its status, and reclaims it when the session ends.

### Why one sandbox per session?

Agents need to run code and drive browsers exactly as you ask — and the platform must guarantee that every session operates **fully independently**, even when code hits errors or contains vulnerabilities. That is why each session runs inside its own sandbox: the processes, filesystem, and memory of one session are completely separate from every other session — an incident in one session stays inside that session. When the session ends, the sandbox is destroyed and all state inside it disappears.

---

## Connecting your agent

Each tool has its own MCP endpoint (streamable HTTP) behind the AgentBase Gateway. Connect using any MCP client (Claude Code, Cursor, or an MCP SDK):

| Tool | MCP endpoint |
|---|---|
| Code Interpreter | `https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/code` |
| Browser | `https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser` |

### Authentication

The endpoint is an **OAuth resource server** — your client drives the whole login flow, so you never create or paste tokens by hand:

1. The client calls the endpoint without a token → gets `401` with a `WWW-Authenticate` header pointing to the authorization server.
2. The client registers itself (**Dynamic Client Registration**) and opens the browser at the GreenNode Portal login URL.
3. After sign-in, the client keeps the access token and **refreshes it automatically** — no re-login every session.

Tokens from a **Root user, IAM user, or Service Account** all work — all three issue the same kind of access token. If your agent runs headless (no browser available), attach the access token directly in your client's configuration.

Each MCP connection is pinned to a specific resource via a header — `x-code-interpreter-id` for Code Interpreter, `x-browser-id` for Browser — see each tool's page for detailed connection instructions.

---

## Getting Started with Built-in Tools

| I want to... | Go to |
|---|---|
| Let my agent run Python / shell | [Use Code Interpreter](use-code-interpreter.md) |
| Let my agent drive a browser, watch live, and replay recordings | [Use Browser](use-browser.md) |
| Understand the isolation, security model, and limits | [Sandbox: security and limits](sandbox-security-and-limits.md) |
