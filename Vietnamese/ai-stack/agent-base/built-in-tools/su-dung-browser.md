# Sử dụng Browser

> Hướng dẫn kết nối agent của bạn với **Browser** — điều khiển Chrome thật trong sandbox riêng cho từng session: automation qua CDP, xem trực tiếp màn hình (live view) và xem lại bản ghi (recording), tích hợp qua MCP.

---

## Điều kiện cần

- Tài khoản GreenNode và đã hoàn thành [Bắt đầu với AgentBase](../getting-started.md)
- Account đã được bật whitelist sử dụng Built-in Tools — xem [Built-in Tools](README.md) nếu chưa được bật
- Agent của bạn hỗ trợ MCP client (Claude Code, Cursor, hoặc MCP SDK)
- Nếu agent tự viết automation: dùng client **Chrome DevTools Protocol (CDP)** — Playwright, Puppeteer hoặc client CDP bất kỳ

---

## Kết nối qua MCP

**Bước 1:** Lấy endpoint MCP của Browser:

```
https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser
```

**Bước 2:** Thêm vào cấu hình MCP client của bạn, kèm header chỉ định Browser sẽ dùng. Ví dụ với Claude Code:

```bash
claude mcp add --transport http --scope user browser \
  "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser" \
  --header "x-browser-id: <YOUR_BROWSER_ID>"
```

Hoặc với Cursor / VS Code — thêm header vào config:

```json
{
  "mcpServers": {
    "browser": {
      "url": "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/browser",
      "headers": {
        "x-browser-id": "<YOUR_BROWSER_ID>"
      }
    }
  }
}
```

Thay `<YOUR_BROWSER_ID>` bằng `id` của Browser bạn đã tạo — mọi lời gọi qua kết nối MCP này đi vào đúng Browser đó.

**Bước 3:** Đăng nhập lần đầu — client tự chạy flow đăng nhập (**Dynamic Client Registration**) và mở URL login của GreenNode Portal trên trình duyệt; access token được giữ và **tự refresh** sau đó. Token từ **Root user, IAM user hoặc Service Account** đều dùng được.

---

## Mô hình hoạt động

Mỗi **session** là một trình duyệt Chrome thật chạy trong một sandbox riêng. Có 3 luồng riêng biệt:

```
Agent ──── automation stream (CDP, cổng 9222) ────┐
Người xem ── live view (noVNC, cổng 6080) ────────┤── Chrome trong sandbox
Ghi hình ── recording (lưu khi xoá session) ──────┘
```

- **Automation stream** — agent điều khiển Chrome: relay kết nối CDP của client vào cổng debug của Chrome trong sandbox. Playwright / Puppeteer dùng được như localhost.
- **Live view** — người xem màn hình Chrome trực tiếp qua noVNC, nhúng trong portal bằng iframe.
- **Recording** — bản ghi phiên được lưu lại khi session kết thúc.

Luồng đầy đủ: agent (kèm automation library như Playwright, browser-use) nhận query → LLM chọn tool call (`click`, `type`, `goto`...) → lệnh CDP đi qua automation stream vào Chromium trong session → nội dung trang và screenshot trả về agent:

<figure><img src="../../../.gitbook/assets/Agentbase-image/agentbase-browser-architecture.svg" alt=""><figcaption><p>Kiến trúc Browser — agent điều khiển Chromium trong sandbox qua CDP</p></figcaption></figure>

Browser dùng cùng khuôn với [Code Interpreter](su-dung-code-interpreter.md): tạo tài nguyên, chờ `ACTIVE`, tạo session (một sandbox mỗi session), xoá khi hết dùng.

---

## Điều khiển Chrome bằng automation stream

**Bước 1:** Tạo Browser bằng API `POST /v1/browsers`, chờ trạng thái `ACTIVE` rồi tạo session — giống Code Interpreter. `id` trả về khi tạo là giá trị đi vào header `x-browser-id` khi kết nối MCP.

**Bước 2:** Bật automation stream cho session (tool/API `PUT .../sessions/{sessionId}/streams`). Luồng này bật/tắt được cho từng session.

**Bước 3:** Trỏ client CDP (Playwright, Puppeteer) vào địa chỉ automation stream của session. Service relay kết nối của bạn tới Chrome trong sandbox và tự viết lại địa chỉ debugger để trỏ ngược về chính nó.

---

## Xem trực tiếp (live view)

Màn hình Chrome được phục vụ qua noVNC và nhúng trong portal bằng iframe. Vì iframe và WebSocket không thể gắn header xác thực, live view dùng **URL đã ký** (kiểu presigned URL):

1. Portal ký URL live view cho session (ticket hiệu lực **5 phút**).
2. URL được đặt vào `iframe src` — ticket đi theo đường dẫn WebSocket và bị cắt bỏ trước khi vào sandbox.
3. Kết nối đã thiết lập thì không xác thực lại; mỗi kết nối giữ tối đa **1 giờ**. Hết hạn thì portal ký URL mới và tải lại iframe.

---

## Ghi hình (recording)

File ghi hình nằm bên trong sandbox nên sẽ mất khi session bị xoá. Vì thế, **khi bạn xoá session**, service đọc file ghi hình ra ngay trước khi huỷ sandbox rồi lưu lên object storage. Sau đó lấy bản ghi bằng `GET .../sessions/{sessionId}/recording`.

{% hint style="warning" %}
Recording là **best effort**: nếu không đọc/lưu được file, việc xoá session vẫn tiếp tục và không có bản ghi. Bản ghi lớn hơn 64 MiB (giá trị cấu hình mặc định) không được lưu.
{% endhint %}

---

## API chính

| Đường dẫn dưới `/v1/browsers` | Mục đích |
|---|---|
| `POST`, `GET`, `GET /{id}`, `DELETE /{id}` | Tạo, liệt kê, xem, xoá Browser |
| `POST/GET/DELETE /{id}/sessions[/{sessionId}]` | Quản lý session — mỗi session một Chrome trong một sandbox |
| `PUT /{id}/sessions/{sessionId}/streams` | Bật/tắt automation stream |
| `/{id}/sessions/{sessionId}/automation-stream[/*]` | Relay CDP, mọi method |
| `POST .../live-view-stream-sign` và `GET .../live-view-stream[/*]` | Ký URL xem trực tiếp, và luồng xem |
| `GET .../recording` | Lấy bản ghi đã lưu |

---

## Xoá

1. Xoá session — service lưu recording lại (nếu bật), huỷ sandbox và toàn bộ trạng thái.
2. Xoá Browser khi hết cần — trả lại quota.

---

## Kết quả

Agent của bạn điều khiển được Chrome thật (CDP), bạn xem được màn hình trực tiếp trong portal và tải lại bản ghi phiên sau khi kết thúc.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Cho agent chạy Python / shell | [Sử dụng Code Interpreter](su-dung-code-interpreter.md) |
| Xem toàn bộ giới hạn và mô hình bảo mật | [Sandbox: bảo mật và giới hạn](sandbox-bao-mat-va-gioi-han.md) |
