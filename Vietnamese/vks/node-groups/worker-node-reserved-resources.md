# Worker Node Reserved Resources

Worker Node Reserved Resources giúp VKS bảo vệ system component trên mỗi worker node bằng cách dành riêng trước một phần CPU và memory — ngăn user workload chiếm hết tài nguyên và đẩy node vào trạng thái **NotReady**.

---

## Tổng quan

Mỗi worker node trong VKS cluster vận hành hai nhóm component bên cạnh user workload:

**Nhóm 1 — System processes chạy trực tiếp trên node OS** (ngoài Pod runtime):
- kubelet
- container runtime (containerd)
- OS daemon (systemd, sshd, log agent…)

**Nhóm 2 — System pods chạy trong namespace `kube-system`** (gồm cả DaemonSet và Deployment):
- kube-proxy
- CNI agent
- CoreDNS
- CSI controller
- Load Balancer controller

Hai nhóm này được cấp tài nguyên từ hai resource pool tách biệt:

| Nhóm | Resource pool |
|---|---|
| System processes | **Reserved** |
| System pods | **Allocatable** |

```
Node Capacity (vCPU / RAM)
┌──────────────────────┬──────────────────────────────┐
│  kube-reserved       │  Allocatable                 │
│  ├ kubelet           │  ├ User Pods                 │
│  ├ containerd        │  └ kube-system Pods          │
│  └ OS daemon         │    (CoreDNS, CNI, CSI...)    │
└──────────────────────┴──────────────────────────────┘
         ↑                           ↑
   Bảo vệ system             kube-scheduler
   process                   schedule vào đây
```

**Vấn đề:** Nếu toàn bộ node capacity được cấp cho Pod, system process ở Nhóm 1 có thể bị thiếu resource khi workload spike, dẫn tới các failure mode điển hình:

- Node chuyển trạng thái **NotReady**
- kubelet / containerd bị **OOM kill**
- Node mất khả năng phục vụ (unresponsive)

**Giải pháp:** VKS **reserve** trước một phần CPU và memory cho Nhóm 1 ngay tại provisioning time. Phần còn lại được phân bổ cho:

- User workload (Pod của bạn)
- System pod ở Nhóm 2

**Công thức:** Trong output `kubectl describe node`, giá trị `Allocatable` được tính bởi:

```
Allocatable = Capacity − Reserved − Eviction threshold
```

---

## Cách VKS tính tài nguyên reserved

VKS áp dụng **tiered model với rate giảm dần** (progressive tiering): node size càng lớn thì **reserve ratio** càng thấp, vì system overhead tăng chậm hơn so với tổng capacity của node.

### CPU reserved

Cộng dồn theo từng tier, cộng thêm **100m baseline** cố định:

| Tier CPU | Reserve rate |
|---|---|
| Core thứ 1 | 6% |
| Core thứ 2 | 1% |
| Core thứ 3 – 4 | 0.5% |
| Core thứ 5 trở đi | 0.25% |

### Memory reserved

Cộng dồn theo từng tier, cộng thêm **200 MiB baseline** cố định:

| Tier RAM | Reserve rate |
|---|---|
| 0 – 4 GiB | 25% |
| 4 – 8 GiB | 20% |
| 8 – 16 GiB | 10% |
| 16 – 128 GiB | 6% |
| Trên 128 GiB | 2% |

---

## Cơ chế áp dụng trên node

VKS inject các tham số reserved vào kubelet flag tại thời điểm node join cluster (qua bootstrap config). Một số đặc điểm quan trọng:

- Giá trị `kube-reserved` được **subtract trực tiếp khỏi Allocatable** — kube-scheduler không schedule user pod vào phần này.
- VKS hiện **không cấu hình `system-reserved`** riêng. Tài nguyên cho OS daemon được bảo vệ gián tiếp qua **eviction threshold** mặc định của kubelet.
- VKS dùng `enforce-node-allocatable=pods` (default upstream): kubelet chỉ tạo cgroup hard-limit cho **kubepods**, các system process **không bị bound** vào dedicated cgroup riêng.
- Mức reserved được tính theo flavor của node group tại provisioning time và **immutable trong suốt lifecycle của node group**. Để áp dụng flavor khác, bạn cần provision một node group mới với flavor mong muốn, migrate workload sang, rồi xóa node group cũ.

{% hint style="warning" %}
Mức reserved immutable trong suốt lifecycle của node group. Để thay đổi Flavor: provision node group mới → migrate workload → xóa node group cũ.
{% endhint %}

---

## Ví dụ

### Flavor `2 vCPU / 4 GiB`

**CPU reserved:**
```
100m (baseline)
+ 1000m × 6%    = 60m   (core 1)
+ 1000m × 1%    = 10m   (core 2)
─────────────────────────
= 170m
```

**Memory reserved:**
```
200 MiB (baseline)
+ 4096 MiB × 25% = 1024 MiB
─────────────────────────
= 1224 MiB
```

→ Kubelet flag: `--kube-reserved=cpu=170m,memory=1224Mi`  
→ **Allocatable cho Pod ≈ 1830m CPU / 2872 MiB RAM**

### Flavor `4 vCPU / 8 GiB`

- **CPU:** `100 + 60 + 10 + 2000×0.5% = 180m`
- **RAM:** `200 + 4096×25% + 4096×20% = 200 + 1024 + 819.2 ≈ 2044 MiB`

→ `--kube-reserved=cpu=180m,memory=2044Mi`

### Flavor `8 vCPU / 16 GiB`

- **CPU:** `100 + 60 + 10 + 10 + 4000×0.25% = 190m`
- **RAM:** `200 + 1024 + 819.2 + 8192×10% = 2863 MiB`

→ `--kube-reserved=cpu=190m,memory=2863Mi`

### Flavor `16 vCPU / 32 GiB`

- **CPU:** `100 + 60 + 10 + 10 + 12000×0.25% = 210m`
- **RAM:** `200 + 1024 + 819.2 + 819.2 + 16384×6% ≈ 3846 MiB`

→ `--kube-reserved=cpu=210m,memory=3846Mi`

---

## Bảng tham chiếu nhanh

| Flavor | CPU reserved | RAM reserved | CPU overhead ratio | RAM overhead ratio |
|---|---|---|---|---|
| 2c / 4 GiB | 170m | 1224 MiB | ~8.5% | ~30% |
| 4c / 8 GiB | 180m | 2044 MiB | ~4.5% | ~25% |
| 8c / 16 GiB | 190m | 2863 MiB | ~2.4% | ~17% |
| 16c / 32 GiB | 210m | 3846 MiB | ~1.3% | ~12% |
| 32c / 64 GiB | 250m | 5810 MiB | ~0.8% | ~9% |

{% hint style="info" %}
**Best practice:** Node càng lớn thì utilization cho workload càng cao. Với production workload cần tối đa hóa resource efficiency, nên ưu tiên **fewer larger nodes** thay vì **many small nodes**.
{% endhint %}

---

## Kiểm tra trên cluster

### Xem cấu hình kubelet đang chạy

```bash
kubectl get --raw "/api/v1/nodes/<node-name>/proxy/configz" \
  | jq '.kubeletconfig | {kubeReserved, systemReserved, enforceNodeAllocatable, evictionHard}'
```

Output mẫu trên node VKS:

```json
{
  "kubeReserved": { "cpu": "180m", "memory": "2044Mi" },
  "systemReserved": null,
  "enforceNodeAllocatable": ["pods"],
  "evictionHard": { "memory.available": "100Mi", "nodefs.available": "10%" }
}
```

### Đối chiếu Capacity và Allocatable

```bash
kubectl describe node <node-name>
```

```
Capacity:
  cpu:     4
  memory:  8Gi
Allocatable:
  cpu:     3820m       ← Capacity − kube-reserved − eviction-threshold
  memory:  ~6Gi
```

Phần chênh lệch giữa `Capacity` và `Allocatable` chính là `kube-reserved + eviction-threshold`.

### Quan sát mức tiêu thụ của system process

Để quan sát mức tiêu thụ thực tế của các system process được `kube-reserved` bảo vệ (kubelet, containerd, OS daemon), SSH vào node và inspect cgroup:

```bash
systemd-cgtop
systemctl status kubelet containerd
```

---

## Câu hỏi thường gặp

**Có thể override mức reserved cho node của tôi không?**  
Không. VKS managed kubelet config để đảm bảo node stability. Reserved được tính tự động từ flavor của node group, không expose cấu hình ra user.

**Vì sao flavor nhỏ có RAM overhead ratio cao?**  
Vì system component có fixed overhead (~200 MiB baseline). Trên node 4 GiB, baseline này chiếm tỷ lệ đáng kể, nhưng trên node 64 GiB thì negligible. Đây là lý do production nên dùng flavor lớn để tối ưu utilization.

**Reserved có thay đổi runtime không?**  
Không. Reserved được set tại node join time và immutable trong suốt node lifecycle.

**Tôi có thể change flavor của node group hiện tại để giảm overhead?**  
Node group có flavor immutable trong suốt lifecycle. Nếu cần flavor lớn hơn để giảm overhead ratio, **provision node group mới** với flavor mong muốn → migrate workload sang → decommission node group cũ.

**Vì sao Allocatable nhỏ hơn `Capacity − kube-reserved` một chút?**  
Allocatable trừ thêm **eviction threshold** (default `memory.available<100Mi`) — buffer này để kubelet kịp evict pod trước khi node OOM. Công thức đầy đủ: `Allocatable = Capacity − kube-reserved − eviction-threshold`.

---

## Bắt đầu với Node Groups

| Tôi muốn... | Đi đến |
|---|---|
| Xem danh sách Flavor và thông số kỹ thuật | [Danh sách Flavor tại zone HCM03-C](../reference/node-flavors/danh-sach-flavor-tai-zone-hcm03-c.md) |
| Tạo Node Group mới | [Node Groups](README.md) |
| Cấu hình Auto Scaling cho Node Group | [Auto Scaling](auto-scaling.md) |
