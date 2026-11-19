# Kube Reserved

Kube Reserved helps VKS protect system components on each worker node by reserving a portion of CPU and memory upfront — preventing user workloads from consuming all resources and pushing the node into a **NotReady** state.

***

## Overview

Each worker node in a VKS cluster runs two groups of components alongside user workloads:

**Group 1 — System processes running directly on the node OS** (outside the Pod runtime):

* kubelet
* container runtime (containerd)
* OS daemon (systemd, sshd, log agent…)

**Group 2 — System pods running in the `kube-system` namespace** (including DaemonSets and Deployments):

* kube-proxy
* CNI agent
* CoreDNS
* CSI controller
* Load Balancer controller

These two groups draw resources from two separate resource pools:

| Group            | Resource pool   |
| ---------------- | --------------- |
| System processes | **Reserved**    |
| System pods      | **Allocatable** |

```
Node Capacity (vCPU / RAM)
┌──────────────────────┬──────────────────────────────┐
│  kube-reserved       │  Allocatable                 │
│  ├ kubelet           │  ├ User Pods                 │
│  ├ containerd        │  └ kube-system Pods          │
│  └ OS daemon         │    (CoreDNS, CNI, CSI...)    │
└──────────────────────┴──────────────────────────────┘
         ↑                           ↑
   Protects system            kube-scheduler
   processes                  schedules here
```

**Problem:** If all node capacity is allocated to Pods, Group 1 system processes may run out of resources during a workload spike, leading to common failure modes:

* Node transitions to **NotReady** state
* kubelet / containerd is **OOM killed**
* Node becomes unresponsive

**Solution:** VKS **reserves** a portion of CPU and memory for Group 1 at provisioning time. The remainder is allocated to:

* User workload (your Pods)
* Group 2 system pods

**Formula:** In `kubectl describe node` output, the `Allocatable` value is calculated as:

```
Allocatable = Capacity − Reserved − Eviction threshold
```

***

## How VKS calculates reserved resources

VKS applies a **tiered model with decreasing rates** (progressive tiering): the larger the node, the lower the **reserve ratio**, because system overhead grows more slowly than total node capacity.

### CPU reserved

Tiers are accumulated and added to a fixed **100m baseline**:

| CPU tier         | Reserve rate |
| ---------------- | ------------ |
| Core 1           | 6%           |
| Core 2           | 1%           |
| Cores 3 – 4      | 0.5%         |
| Core 5 and above | 0.25%        |

### Memory reserved

Tiers are accumulated and added to a fixed **200 MiB baseline**:

| RAM tier      | Reserve rate |
| ------------- | ------------ |
| 0 – 4 GiB     | 25%          |
| 4 – 8 GiB     | 20%          |
| 8 – 16 GiB    | 10%          |
| 16 – 128 GiB  | 6%           |
| Above 128 GiB | 2%           |

***

## How it is applied on the node

VKS injects the reserved parameters into the kubelet flag at node join time (via bootstrap config). Key behaviors:

* The `kube-reserved` value is **subtracted directly from Allocatable** — kube-scheduler never schedules user Pods into this portion.
* VKS does **not configure `system-reserved`** separately. Resources for OS daemons are protected indirectly through the kubelet's default **eviction threshold**.
* VKS uses `enforce-node-allocatable=pods` (default upstream): kubelet only creates a cgroup hard-limit for **kubepods**; system processes are **not bound** to a dedicated cgroup.
* The reserved amount is calculated from the node group's Flavor at provisioning time and is **immutable for the entire lifecycle of the node group**. To apply a different Flavor, you need to provision a new node group with the desired Flavor, migrate workloads, then delete the old node group.

{% hint style="warning" %}
Reserved is immutable for the lifetime of the node group. To change the Flavor: provision a new node group → migrate workloads → delete the old node group.
{% endhint %}

***

## Examples

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

→ Kubelet flag: `--kube-reserved=cpu=170m,memory=1224Mi`\
→ **Allocatable for Pods ≈ 1830m CPU / 2872 MiB RAM**

### Flavor `4 vCPU / 8 GiB`

* **CPU:** `100 + 60 + 10 + 2000×0.5% = 180m`
* **RAM:** `200 + 4096×25% + 4096×20% = 200 + 1024 + 819.2 ≈ 2044 MiB`

→ `--kube-reserved=cpu=180m,memory=2044Mi`

### Flavor `8 vCPU / 16 GiB`

* **CPU:** `100 + 60 + 10 + 10 + 4000×0.25% = 190m`
* **RAM:** `200 + 1024 + 819.2 + 8192×10% = 2863 MiB`

→ `--kube-reserved=cpu=190m,memory=2863Mi`

### Flavor `16 vCPU / 32 GiB`

* **CPU:** `100 + 60 + 10 + 10 + 12000×0.25% = 210m`
* **RAM:** `200 + 1024 + 819.2 + 819.2 + 16384×6% ≈ 3846 MiB`

→ `--kube-reserved=cpu=210m,memory=3846Mi`

***

## Quick reference table

| Flavor       | CPU reserved | RAM reserved | CPU overhead ratio | RAM overhead ratio |
| ------------ | ------------ | ------------ | ------------------ | ------------------ |
| 2c / 4 GiB   | 170m         | 1224 MiB     | \~8.5%             | \~30%              |
| 4c / 8 GiB   | 180m         | 2044 MiB     | \~4.5%             | \~25%              |
| 8c / 16 GiB  | 190m         | 2863 MiB     | \~2.4%             | \~17%              |
| 16c / 32 GiB | 210m         | 3846 MiB     | \~1.3%             | \~12%              |
| 32c / 64 GiB | 250m         | 5810 MiB     | \~0.8%             | \~9%               |

{% hint style="info" %}
**Best practice:** The larger the node, the higher the workload utilization. For production workloads that need to maximize resource efficiency, prefer **fewer larger nodes** over **many small nodes**.
{% endhint %}

***

## Verify on your cluster

### View the running kubelet configuration

```bash
kubectl get --raw "/api/v1/nodes/<node-name>/proxy/configz" \
  | jq '.kubeletconfig | {kubeReserved, systemReserved, enforceNodeAllocatable, evictionHard}'
```

Sample output on a VKS node:

```json
{
  "kubeReserved": { "cpu": "180m", "memory": "2044Mi" },
  "systemReserved": null,
  "enforceNodeAllocatable": ["pods"],
  "evictionHard": { "memory.available": "100Mi", "nodefs.available": "10%" }
}
```

### Compare Capacity and Allocatable

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

The gap between `Capacity` and `Allocatable` equals `kube-reserved + eviction-threshold`.

### Observe system process resource consumption

To observe the actual resource consumption of system processes protected by `kube-reserved` (kubelet, containerd, OS daemon), SSH into the node and inspect cgroups:

```bash
systemd-cgtop
systemctl status kubelet containerd
```

***

## FAQ

**Can I override the reserved amounts for my node?**\
No. VKS manages the kubelet config to ensure node stability. Reserved is calculated automatically from the node group's Flavor and is not user-configurable.

**Why do smaller Flavors have a higher RAM overhead ratio?**\
Because system components have a fixed overhead (\~200 MiB baseline). On a 4 GiB node, this baseline is a significant fraction of total memory, but on a 64 GiB node it is negligible. This is why production environments should use larger Flavors to optimize utilization.

**Can reserved amounts change at runtime?**\
No. Reserved is set at node join time and is immutable for the entire node lifecycle.

**Can I change the Flavor of my current node group to reduce overhead?**\
Node group Flavor is immutable for the lifetime of the node group. If you need a larger Flavor to reduce the overhead ratio, **provision a new node group** with the desired Flavor → migrate workloads → decommission the old node group.

**Why is Allocatable slightly smaller than `Capacity − kube-reserved`?**\
Allocatable also subtracts the **eviction threshold** (default `memory.available<100Mi`) — a buffer that gives kubelet time to evict Pods before the node runs out of memory. Full formula: `Allocatable = Capacity − kube-reserved − eviction-threshold`.

***

## Getting Started with Node Groups

| I want to...                                 | Go to                                                                                                            |
| -------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| View the list of available Flavors and specs | [Flavor List at zone HCM03-C (VN)](https://docs.vngcloud.vn/vng-cloud-document/vn/vks/reference/node-flavors/danh-sach-flavor-tai-zone-hcm03-c) |
| Create a new Node Group                      | [Node Groups](./)                                                                                                |
| Configure Auto Scaling for a Node Group      | [Auto Scaling](auto-scaling.md)                                                                                  |
