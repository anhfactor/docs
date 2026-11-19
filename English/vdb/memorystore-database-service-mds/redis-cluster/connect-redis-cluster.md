# Connect to Redis Cluster

This guide describes how to connect to a Redis Cluster on vDB using redis-cli, via IP or Domain, with ACL user authentication.

---

## Prerequisites

* A Redis Cluster has been created on vDB. See [Create a Redis Cluster](create-redis-cluster.md).
* **redis-cli** is installed on the connecting machine (or an equivalent redis client).
* The connecting machine is in the same Network as the Instance, or in a Network with an ACL rule to the Instance's Endpoint Private.

---

## Install redis-cli

If you don't have redis-cli, on Linux download and build the source as follows:

```bash
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make distclean  # Ubuntu systems only
make
sudo make install
```

---

## Step 1 - Identify Endpoint & credentials

1. Open the Database management console and select the Redis Cluster to connect to.
2. Select the **Connectivity & Security** tab and review the **Endpoint & Port** section.
3. Note the Instance **IP** or **Domain** and the **Port**:
   * `6379` — write endpoint, always points to the Master.
   * `6380` — read endpoint, round-robin across Replicas. Data read from this endpoint may lag behind the latest write; for read-your-writes, use `6379`.
4. Get the authentication credentials: the ACL user (default `master-user`) and password.

![](../../../.gitbook/assets/Redis-cluster/ket-noi-redis-cluster-endpoint.png)

{% hint style="info" %}
Redis Cluster supports connecting via **IP** or **Domain** — either value works.
{% endhint %}

## Step 2 - Configure Security Group Rules (optional)

1. Open the **Connectivity & Security** tab, under **Security Group Rules**, select **EDIT**.
2. Enter the trusted **Remote IP** in CIDR notation, or select **ADD RULE** to add a new rule.
3. Select **Save** and wait for the change to be saved.

![](../../../.gitbook/assets/Redis-cluster/ket-noi-redis-cluster-security-group.png)

{% hint style="warning" %}
By default the Instance allows access from anywhere (`0.0.0.0/0`). GreenNode recommends restricting access to only trusted Remote IPs.
{% endhint %}

## Step 3 - Connect with redis-cli

When you create a Redis Cluster, a default ACL user named `master-user` is created automatically. You connect using `master-user` with the password set during creation.

Connect via **IP**:

```bash
redis-cli -h 10.0.0.10 -p 6379 --user master-user --pass '<PASSWORD>'
```

Connect via **Domain**:

```bash
redis-cli -h my-redis-cluster.vdb-redis.vngcloud.vn -p 6379 --user master-user --pass '<PASSWORD>'
```

Replace `10.0.0.10` or `my-redis-cluster.vdb-redis.vngcloud.vn` with your Instance IP/Domain, and `<PASSWORD>` with the password set during creation.

{% hint style="info" %}
For long-time queries, configure **tcp_keepalive** or **healthcheck_interval** to avoid connection drops. See [Notes & limitations](../../announcements/luu-y-and-han-che.md#e.-long-time-query).
{% endhint %}

---

## Result

After a successful connection, you get the redis-cli prompt:

```bash
<IP>:6379>
```

You can now run Redis commands against the Redis Cluster.
