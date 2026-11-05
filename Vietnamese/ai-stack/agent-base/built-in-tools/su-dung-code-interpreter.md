# Sử dụng Code Interpreter

> Hướng dẫn kết nối agent của bạn với **Code Interpreter** — chạy Python, lệnh shell và thao tác file trong sandbox riêng, cô lập hoàn toàn theo từng session, tích hợp qua MCP.

---

## Điều kiện cần

- Tài khoản GreenNode và đã hoàn thành [Bắt đầu với AgentBase](../getting-started.md)
- Account đã được bật whitelist sử dụng Built-in Tools — xem [Built-in Tools](README.md) nếu chưa được bật
- Agent của bạn hỗ trợ MCP client (Claude Code, Cursor, hoặc MCP SDK)
- Trong scope quota: số Code Interpreter và tổng số session mỗi người dùng (xem [Sandbox: bảo mật và giới hạn](sandbox-bao-mat-va-gioi-han.md))

---

## Kết nối qua MCP

**Bước 1:** Lấy endpoint MCP của Code Interpreter:

```
https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/code
```

**Bước 2:** Thêm vào cấu hình MCP client của bạn, kèm header chỉ định Code Interpreter sẽ dùng. Ví dụ với Claude Code:

```bash
claude mcp add --transport http --scope user code-interpreter \
  "https://gw-greennode-builtin-tools-110718.agentbase-gateway.aiplatform.vngcloud.vn/code" \
  --header "x-code-interpreter-id: <YOUR_CODE_INTERPRETER_ID>"
```

Hoặc với Cursor / VS Code — thêm header vào config:

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

Thay `<YOUR_CODE_INTERPRETER_ID>` bằng `id` của Code Interpreter bạn đã tạo (xem [Vòng đời sử dụng](#vong-doi-su-dung)) — mọi lời gọi qua kết nối MCP này đi vào đúng Code Interpreter đó.

**Bước 3:** Đăng nhập lần đầu. Endpoint là một OAuth resource server: client tự chạy flow đăng nhập (**Dynamic Client Registration**) và mở URL login của GreenNode Portal trên trình duyệt. Sau khi đăng nhập, access token được giữ và **tự refresh** — không cần đăng nhập lại mỗi session.

Token từ **Root user, IAM user hoặc Service Account** đều dùng được. Nếu agent chạy headless (không mở được trình duyệt), gắn access token trực tiếp vào cấu hình của client. Sau khi kết nối, các tool của Code Interpreter xuất hiện trong danh sách MCP tool của agent.

---

## Mô hình hoạt động

Agent nhận query của người dùng, LLM chọn tool call, rồi tool call đi qua kết nối MCP vào Code Interpreter — chạy trong sandbox riêng và trả kết quả về cho agent:

<figure><img src="../../../.gitbook/assets/Agentbase-image/agentbase-code-interpreter-architecture.svg" alt=""><figcaption><p>Kiến trúc Code Interpreter — agent gọi tool qua MCP, code chạy trong sandbox cô lập</p></figcaption></figure>

Code Interpreter tạo **một lần và dùng lại** cho nhiều session — mỗi session vẫn là một sandbox riêng.

---

## Vòng đời sử dụng

Một lần dùng Code Interpreter đi qua các bước sau:

```
Tạo Code Interpreter → chờ ACTIVE → tạo session → gọi tool → (lặp lại) → xoá
                        (chuẩn bị sandbox) (1 sandbox)  (invoke)
```

**Bước 1: Tạo Code Interpreter**

1. Gọi `POST /v1/code-interpreters` để tạo Code Interpreter.
2. Yêu cầu trả về ngay với trạng thái `CREATING`, kèm `id` — đây là giá trị đi vào header `x-code-interpreter-id` khi kết nối MCP.

**Bước 2: Chờ trạng thái ACTIVE**

1. Poll trạng thái tài nguyên mỗi vài giây.
2. Lần tạo đầu mất **vài phút** vì nền tảng chuẩn bị hạ tầng sandbox lần đầu. Sau đó các session tiếp theo nhanh hơn nhiều.
3. Trước khi `ACTIVE`, mọi lời gọi session/invoke bị từ chối với `409`. Quá thời hạn chờ (5 phút) thì trạng thái chuyển `FAILED`.

**Bước 3: Tạo session**

1. Chạy tool tạo session — mỗi session là **một sandbox riêng, cô lập hoàn toàn**.
2. Nếu còn sandbox sẵn sàng, session được cấp sau khoảng vài giây; nếu hết, nền tảng phải chuẩn bị sandbox mới (chậm hơn đáng kể).

{% hint style="warning" %}
Session **không tự hết hạn** — không có TTL hay idle timeout. Session bị quên vẫn giữ sandbox và chiếm slot quota cho tới khi bạn xoá. Hãy luôn xoá session khi dùng xong.
{% endhint %}

**Bước 4: Gọi tool để chạy code**

Agent gọi tool theo dạng invoke, kết quả trả về theo kiểu MCP (content blocks) để đưa thẳng cho model.

---

## Các tool của Code Interpreter

| Tool | Làm gì | Ghi chú |
|---|---|---|
| `executeCode` | Chạy code | Hiện chỉ hỗ trợ `python` |
| `executeCommand` | Chạy lệnh shell | Giữ request mở đến khi xong (tối đa 30 giây) |
| `listFiles` | Liệt kê thư mục | |
| `writeFiles` / `readFiles` | Tải file lên / xuống (base64) | Mỗi lần một file; giới hạn dung lượng mặc định 10 MiB (vượt thì `413`) |
| `startCommandExecution` + `getTask` | Chạy lệnh nền rồi hỏi kết quả | Dùng cho việc dài hơn một request; tối đa 15 phút |

Ví dụ một lời gọi `executeCode`:

```json
{
  "name": "executeCode",
  "arguments": { "language": "python", "code": "print(1+1)" }
}
```

Kết quả:

```json
{ "content": [ { "type": "text", "text": "2\n" } ] }
```

{% hint style="info" %}
Lệnh thoát với mã khác 0 trả trạng thái task `failed`, nhưng bản thân lời gọi invoke vẫn thành công (200) — nghĩa là "invoke thành công, còn lệnh thì không". Kiểm tra trường trạng thái trong kết quả thay vì chỉ mã HTTP.
{% endhint %}

---

## Cô lập giữa các session

- File ghi ở session A **không thấy** ở session B — hai sandbox khác nhau.
- Truy cập Code Interpreter của người dùng khác trả `404` (không phải `403`) để không lộ sự tồn tại của tài nguyên.
- Khi xoá session, sandbox bị huỷ và toàn bộ trạng thái biến mất — không còn dữ liệu của bạn trong sandbox tiếp theo.

---

## Xoá

1. Xoá từng session còn lại, rồi xoá Code Interpreter.
2. Việc xoá gỡ runtime bên dưới, trả lại quota. Xoá lần hai vẫn trả `204` nhưng không trả quota thêm.

---

## Kết quả

Agent của bạn có thể chạy Python, lệnh shell, đọc ghi file trong môi trường cô lập theo từng session — kết quả trả về dạng MCP content blocks đưa thẳng vào cuộc hội thoại của agent.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Cho agent điều khiển trình duyệt | [Sử dụng Browser](su-dung-browser.md) |
| Xem toàn bộ giới hạn và mô hình bảo mật | [Sandbox: bảo mật và giới hạn](sandbox-bao-mat-va-gioi-han.md) |
