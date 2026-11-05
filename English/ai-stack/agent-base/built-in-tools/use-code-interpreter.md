# Use Code Interpreter

> Connect your agent to **Code Interpreter** — run Python, shell commands, and file operations in a sandbox fully isolated per session, integrated over MCP.

---

## Prerequisites

- A GreenNode account, and having completed [Getting Started with AgentBase](../getting-started.md)
- An account enabled in the Built-in Tools whitelist — see [Built-in Tools](README.md) if not yet enabled
- An agent with MCP client support (Claude Code, Cursor, or an MCP SDK)
- Within quota scope: number of Code Interpreters and total sessions per user (see [Sandbox: security and limits](sandbox-security-and-limits.md))

---

## Connecting over MCP

**Step 1:** Get the Code Interpreter MCP endpoint:

```
https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/code
```

**Step 2:** Add it to your MCP client configuration, with a header pointing to the Code Interpreter to use. Example for Claude Code:

```bash
claude mcp add --transport http --scope user code-interpreter \
  "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/code" \
  --header "x-code-interpreter-id: <YOUR_CODE_INTERPRETER_ID>"
```

Or for Cursor / VS Code — add the header to the config:

```json
{
  "mcpServers": {
    "code-interpreter": {
      "url": "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/code",
      "headers": {
        "x-code-interpreter-id": "<YOUR_CODE_INTERPRETER_ID>"
      }
    }
  }
}
```

Replace `<YOUR_CODE_INTERPRETER_ID>` with the `id` of the Code Interpreter you created (see [Usage lifecycle](#usage-lifecycle)) — every call over this MCP connection goes into that exact Code Interpreter.

**Step 3:** Sign in the first time. The endpoint is an OAuth resource server: your client runs the login flow itself (**Dynamic Client Registration**) and opens the GreenNode Portal login URL in the browser. After sign-in, the access token is kept and **refreshed automatically** — no re-login every session.

Tokens from a **Root user, IAM user, or Service Account** all work. If your agent runs headless (no browser available), attach the access token directly in your client's configuration. Once connected, the Code Interpreter tools appear in your agent's MCP tool list.

---

## How it works

Your agent receives a user query, the LLM picks a tool call, and the tool call travels over the MCP connection into the Code Interpreter — running inside its own sandbox and returning the result to the agent:

<figure><img src="../../../.gitbook/assets/Agentbase-image/agentbase-code-interpreter-architecture.svg" alt=""><figcaption><p>Code Interpreter architecture — the agent calls tools over MCP, code runs in an isolated sandbox</p></figcaption></figure>

A Code Interpreter is **created once and reused** across sessions — each session is still its own sandbox.

---

## Usage lifecycle

One round of using Code Interpreter goes through these steps:

```
Create Code Interpreter → wait for ACTIVE → create session → invoke tools → (repeat) → delete
                          (sandbox setup)     (1 sandbox)      (invoke)
```

**Step 1: Create a Code Interpreter**

1. Call `POST /v1/code-interpreters` to create a Code Interpreter.
2. The request returns immediately with status `CREATING` and an `id` — this is the value for the `x-code-interpreter-id` header when connecting over MCP.

**Step 2: Wait for the ACTIVE status**

1. Poll the resource status every few seconds.
2. The first creation takes **a few minutes** because the platform provisions the sandbox infrastructure for the first time. Subsequent sessions are much faster.
3. Before `ACTIVE`, all session/invoke calls are rejected with `409`. Past the wait deadline (5 minutes), the status becomes `FAILED` (terminal).

**Step 3: Create a session**

1. Run the session-creation tool — each session is **its own fully isolated sandbox**.
2. If a sandbox is ready, the session is assigned within seconds; otherwise the platform must provision a new sandbox (noticeably slower).

{% hint style="warning" %}
Sessions **do not expire** — there is no TTL or idle timeout. A forgotten session keeps its sandbox and holds a quota slot until you delete it. Always delete sessions when done.
{% endhint %}

**Step 4: Invoke tools to run code**

Your agent invokes tools; results come back in MCP style (content blocks), ready to feed straight to the model.

---

## Code Interpreter tools

| Tool | What it does | Notes |
|---|---|---|
| `executeCode` | Run code | Currently supports `python` only |
| `executeCommand` | Run a shell command | Holds the request open until it finishes (30 seconds max by default) |
| `listFiles` | List a directory | |
| `writeFiles` / `readFiles` | Upload / download files (base64) | One file per call; default size limit 10 MiB (exceeding returns `413`) |
| `startCommandExecution` + `getTask` | Run in the background, then fetch the result | For work longer than one request; 15 minutes max |

Example `executeCode` invocation:

```json
{
  "name": "executeCode",
  "arguments": { "language": "python", "code": "print(1+1)" }
}
```

Result:

```json
{ "content": [ { "type": "text", "text": "2\n" } ] }
```

{% hint style="info" %}
A command exiting with a non-zero code returns task status `failed`, but the invoke call itself still succeeds (200) — meaning "the invoke succeeded, the command did not". Check the status field in the result, not just the HTTP code.
{% endhint %}

---

## Isolation between sessions

- Files written in session A are **not visible** in session B — they are different sandboxes.
- Accessing another user's Code Interpreter returns `404` (not `403`), so the resource's existence is not revealed.
- When a session is deleted, the sandbox is destroyed and all state disappears — nothing of yours remains in the next sandbox.

---

## Deleting

1. Delete any remaining sessions, then delete the Code Interpreter.
2. Deletion removes the underlying runtime and returns the quota. A second delete still returns `204` but does not return extra quota.

---

## Result

Your agent can run Python, shell commands, and file operations in an environment isolated per session — results return as MCP content blocks fed directly into the agent's conversation.

| I want to... | Go to |
|---|---|
| Let my agent drive a browser | [Use Browser](use-browser.md) |
| See all limits and the security model | [Sandbox: security and limits](sandbox-security-and-limits.md) |
