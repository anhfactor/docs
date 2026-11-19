# Xóa các node được chọn trong Node Group

> Hướng dẫn này giúp bạn xóa các node cụ thể trong một Node Group trên VKS, thay vì để hệ thống tự chọn node khi thu nhỏ (scale down) cluster.

---

## Khi nào nên dùng

Theo mặc định, khi bạn giảm số node của Node Group (tính năng **Resize**), hệ thống sẽ tự chọn node để xóa và bạn không kiểm soát được node nào bị loại bỏ. Tính năng xóa node được chọn cho phép bạn chỉ định chính xác node nào sẽ bị xóa, phù hợp khi:

* Muốn bỏ node bị lỗi, kẹt ở trạng thái không hoạt động mà hệ thống không tự phát hiện.
* Muốn bỏ node đang trống thay vì xóa node đang chạy workload nặng.
* Muốn giữ lại node có Volume gắn theo zone (zonal) hoặc storage cục bộ.

---

## Điều kiện cần (Prerequisites)

* Đã có cluster vKS đang hoạt động với ít nhất một Node Group.
* Node Group đang ở trạng thái **Active** hoặc **Degraded**.
* Cluster không đang thực hiện thao tác khác (ví dụ: upgrade, update Node Group).

---

## Xóa node trên giao diện console

**Bước 1: Mở danh sách node của Node Group**

1. Truy cập [https://vks.console.greennode.ai/overview](https://vks.console.greennode.ai/overview).
2. Chọn cluster chứa Node Group bạn muốn thu nhỏ.
3. Tại Node Group đó, chọn **View nodes** để mở danh sách node.

**Bước 2: Chọn node cần xóa**

1. Tick checkbox ở đầu dòng của từng node bạn muốn xóa. Footer hiển thị số lượng **Đã chọn N node**.
2. Tick checkbox ở dòng đầu bảng để chọn nhanh tất cả các node **đang hiển thị** trên trang hiện tại hoặc trong kết quả tìm kiếm. Lựa chọn ở các trang khác vẫn được giữ nguyên.
3. Nhấn **Xóa các node đã chọn**.

{% hint style="info" %}
**Chú ý:**

Nếu **Autoscaling** đang bật, số node tối đa bạn có thể xóa là `numNodes − Minimum node`. Khi chọn vượt giới hạn, hệ thống hiển thị cảnh báo và vô hiệu hóa nút xóa — hãy giảm thiết lập **Minimum node** của Node Group trước nếu cần xóa thêm node.
{% endhint %}

**Bước 3: Xác nhận việc xóa**

1. Kiểm tra modal xác nhận: tiêu đề hiển thị số node sắp xóa, kèm danh sách tên các node được chọn.
2. (Tùy chọn) Tick **Xóa ngay (bỏ qua drain)** nếu muốn xóa node ngay lập tức mà không drain. Khi bật tùy chọn này, tick thêm ô xác nhận rủi ro để kích hoạt nút **Xóa**.
3. Nhấn **Xóa**.

{% hint style="warning" %}
**Cảnh báo:**

* Hành động này không thể hoàn tác. Các pod đang chạy trên node được chọn sẽ được chuyển sang node khác nếu còn đủ tài nguyên; dữ liệu lưu trên node sẽ bị mất.
* Mặc định, node được xóa sau khi drain (tuân thủ PodDisruptionBudget, tối đa 600 giây). Khi dùng **Xóa ngay (bỏ qua drain)**, pod bị terminate ngay lập tức, không tuân thủ PodDisruptionBudget — workload có thể bị gián đoạn, và dữ liệu trên emptyDir hoặc Persistent Volume cục bộ sẽ mất.
{% endhint %}

Nếu bạn chọn xóa toàn bộ node đang chạy cuối cùng của cluster (không còn Node Group nào khác đang chạy node), hệ thống tự động áp dụng xóa ngay (bỏ qua drain) vì pod bị evict không thể chuyển sang node khác, và hiển thị cảnh báo tương ứng trong modal xác nhận.

---

## Xóa node qua API

Ngoài giao diện console, bạn có thể xóa node được chọn bằng API:

**Endpoint:**

```
POST /v1/clusters/{clusterId}/node-groups/{nodeGroupId}/delete-nodes
```

**Body:**

```json
{
  "nodeIds": ["<node-id-1>", "<node-id-2>"],
  "force": false
}
```

| Trường | Kiểu | Bắt buộc | Mô tả |
|---|---|---|---|
| `nodeIds` | string[] | Có | Danh sách ID của các node cần xóa. ≥ 1 phần tử, không trùng, và mọi ID phải thuộc Node Group này. |
| `force` | boolean | Không | Mặc định `false` — node được drain trước khi xóa. Đặt `true` để bỏ qua drain. |

**Response thành công:** HTTP `202` với `{"status": "UPDATING"}` — việc xóa được thực hiện bất đồng bộ. Số node còn lại được hệ thống tự tính theo số node thực tế trên cluster; bạn chỉ cần gửi danh sách node cần xóa.

**Lỗi thường gặp:**

| HTTP | Điều kiện | Message |
|---|---|---|
| 400 | `nodeIds` thiếu hoặc rỗng | `nodeIds must contain at least one node id.` |
| 400 | Có ID rỗng/blank | `nodeIds must not contain blank node ids.` |
| 400 | ID trùng nhau | `Duplicate node id in nodeIds: <id>.` |
| 400 | Số ID vượt số node hiện tại | `Cannot delete <n> nodes: the node group has only <m> nodes.` |
| 400 | ID không thuộc Node Group | `Node <id> does not belong to this node group.` |
| 400 | Số node còn lại dưới Minimum node (Autoscaling bật) | `Cannot scale down to <x> nodes: it is below the auto scale minimum size (<min>). Lower the 'Minimum node' setting of the node group first.` |
| 409 | Cluster đang bận thao tác khác | `Cluster is not ready to update node group.` |
| 409 | Node Group không ở trạng thái cho phép | `Could not update the node group currently.` |
| 404 | Node Group không tồn tại | Not Found |

---

## Hành vi sau khi gửi yêu cầu xóa

* Node Group chuyển trạng thái **Updating** trong lúc xóa và trở về **Active** khi hoàn tất. Chỉ đúng các node trong danh sách được chọn bị xóa; các node khác và toàn bộ cấu hình của Node Group (labels, taints, Autoscaling, image...) giữ nguyên.
* Nếu quá trình xóa thất bại (ví dụ: node đang bị xóa bởi một thao tác khác, hoặc Autoscaling không cho phép giảm thêm), Node Group được rollback về trạng thái và cấu hình trước đó, không node nào bị xóa, và một event dạng **Warning** kèm lý do được ghi vào danh sách event của cluster.
* Nếu **Autoscaling** đang bật mà các pod bị chuyển khỏi node xóa không đủ chỗ trên các node còn lại, Autoscaler có thể tự động tạo node mới trong khoảng **Minimum node** – **Maximum node** đã cấu hình.

---

## Kết quả

Các node bạn chọn đã được xóa khỏi Node Group; các node còn lại và cấu hình Node Group không thay đổi. Nếu việc xóa thất bại, kiểm tra danh sách event của cluster để xem lý do.

| Tôi muốn tiếp theo... | Đi đến |
|---|---|
| Tìm hiểu về Autoscaling | [Auto Scaling](auto-scaling.md) |
| Thay đổi số node mà không chọn cụ thể node | [Node Groups](README.md) |
