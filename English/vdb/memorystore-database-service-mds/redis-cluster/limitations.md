# Limitations

This page lists the current limitations and constraints of **Redis Cluster (Non-sharding)** on vDB — covering topology and scaling, connectivity, and security.

***

## 1. Topology & Scaling

| Item                      | Limitation                                                                                                                                            |
| ------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Architecture              | Non-sharding — a single shard, 1 Master + 2–9 Replicas (3–10 nodes total)                                                                             |
| Write scaling             | Not supported — all writes go through 1 Master (single writer)                                                                                        |
| Replica scaling           | Each change is ±1 node (increase or decrease by exactly 1); multi-step jumps are not allowed. The cluster always keeps 3–10 nodes                      |
| Scale down                | If the Master is among the nodes being removed, the system automatically fails over to a Replica → brief write interruption while the Master switches |
| Vertical scaling (flavor) | Nodes are recreated step by step → connections to the node being replaced are dropped and reconnect automatically; no data is lost                   |

***

## 2. Connectivity & Client

| Item             | Limitation / Behavior                                                                                                                             |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Write endpoint   | Port `6379` — always points to the Master                                                                                                         |
| Read endpoint    | Port `6380` — round-robin across Replicas                                                                                                         |
| Read consistency | Replicas sync asynchronously → data read from endpoint `6380` may lag behind the latest write. For read-your-writes, use the write endpoint `6379` |
| Idle connection  | Connections idle for more than 3,600 seconds (1 hour) are closed by the LoadBalancer — applications should implement auto-reconnect               |

{% hint style="info" %}
For keepalive and health check settings on long-lived connections, see section **E. Long-time query** in [Attention & Limitations](../../announcements/luu-y-and-han-che.md).
{% endhint %}

***

## 3. Security

* If you set your own password (app-password): 9–32 characters, using only `a-z A-Z 0-9 $ ^ _ < > % #`, starting with a letter, ending with a letter or digit, and containing all 4 groups (uppercase, lowercase, digit, special character).
* Access is only through the LoadBalancer endpoint; restrict access sources with a whitelist (security group) configured when creating or editing the cluster. See [Connect a Redis Cluster](connect-redis-cluster.md).
