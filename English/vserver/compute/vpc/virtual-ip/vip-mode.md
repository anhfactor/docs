# VIP mode

In high availability (HA) systems, a **Virtual IP (VIP)** is an abstract IP. It can move between nodes/servers to keep services reachable.

When you design a VIP-based HA setup, you typically choose one mode: **Active/Active** or **Active/Passive**.

Choosing the right mode affects architecture, performance, and cost.

### Product recommendation on vMarketplace

Use the mode below when you deploy firewall appliances on vMarketplace:

* **pfSense**: choose **Active/Active**.
* **Palo Alto**: choose **Active/Passive**.

{% hint style="info" %}
If you also use **Public Virtual IP Address** on vMarketplace, the HA VIP workflow currently runs in **Active-Passive** at the VIP layer.
{% endhint %}

## 1. Active/Active Mode

#### Definition

In **Active/Active**, **all nodes** are active at the same time. They all receive and process traffic. Nodes coordinate to keep data consistent and performance stable.

#### Key characteristics

* **Load distribution**: A load balancer spreads traffic across nodes.
* **Higher throughput and easier scale-out**: Add nodes with minimal disruption.
* **High availability**: If one node fails, others keep serving traffic.
* **More complexity**: Requires solid data sync and load-balancing design.

#### Real-world examples

* **Web server clusters**: Run multiple web nodes behind NGINX or AWS ELB.
* **Distributed databases**: Systems like **Cassandra** or **CockroachDB**.
* **CDNs**: **Cloudflare** or **Akamai** run many edge nodes in parallel.

## 2. Active/Passive Mode

#### Definition

In **Active/Passive**, only one node is **Active** at any time. The other node is **Passive** and stays on standby.

If the active node fails, the VIP moves to the passive node. Service resumes after a short failover window.

#### Key characteristics

* **Simpler operations**: One active node is easier to observe and debug.
* **Safe redundancy**: The standby node is ready to take over.
* **Lower cost**: One node serves traffic, one waits.
* **Brief downtime on failover**: Seconds to minutes, depending on setup.

#### Real-world examples

* **Database failover**: SQL Server clusters, or MySQL primary/replica.
* **HA firewalls**: One active firewall, one standby firewall.
* **Internal enterprise apps**: ERP/CRM/accounting systems with steady traffic.

## 3. Overall comparison

<table data-header-hidden><thead><tr><th width="184"></th><th width="273"></th><th></th></tr></thead><tbody><tr><td><strong>Criteria</strong></td><td><strong>Active/Active</strong></td><td><strong>Active/Passive</strong></td></tr><tr><td><strong>Performance</strong></td><td>High, traffic shared across nodes</td><td>Lower, only one node handles traffic</td></tr><tr><td><strong>Availability</strong></td><td>Minimal interruption (near-zero downtime)</td><td>Brief interruption during failover</td></tr><tr><td><strong>Cost</strong></td><td>Higher (multiple active nodes)</td><td>Lower (one active, one standby)</td></tr><tr><td><strong>Complexity</strong></td><td>Higher (sync, load balancing)</td><td>Lower (mainly failover configuration)</td></tr><tr><td><strong>Best fit</strong></td><td>Large web systems, distributed platforms</td><td>Internal apps, cost-sensitive systems</td></tr></tbody></table>

## 4. Recommended model

* **Active/Active** fits **mission-critical** systems and high traffic workloads. It also fits multi-zone or multi-region designs.
* **Active/Passive** fits **internal** apps and cost-focused setups. It also fits workloads that can tolerate brief failover.

<table><thead><tr><th width="469">Your system needs</th><th>Recommended mode</th></tr></thead><tbody><tr><td><strong>No downtime tolerated</strong></td><td>Active/Active</td></tr><tr><td><strong>High throughput required</strong></td><td>Active/Active</td></tr><tr><td><strong>Small system, cost first</strong></td><td>Active/Passive</td></tr><tr><td><strong>Can tolerate brief downtime</strong></td><td>Active/Passive</td></tr></tbody></table>
