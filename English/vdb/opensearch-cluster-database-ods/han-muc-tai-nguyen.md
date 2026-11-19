# Resource Limits

The vDB OpenSearch product establishes resource limits to ensure that we can provide fast and flexible services for all customers. These resource limits are the maximum levels we recommend, and some limits can be customized according to your storage needs. To submit a request for limit increase, please visit the GreenNode Support Center and create a request [here](https://helpdesk.greennode.ai/portal/en/newticket).

## Limits

The limits below apply equally to every supported OpenSearch version: **2.8, 2.12, 2.15 and 2.17**.

| Limit | Value | Adjustable | Notes |
| --- | --- | --- | --- |
| OpenSearch Clusters / account (SSO account email) | 10 | Yes, submit a request to the GreenNode Support Center | Counted per account, shared across all versions |
| Maximum nodes / cluster | 9 | For more than 9 nodes, please contact GreenNode | Node count can only be increased, not decreased |
| Minimum disk size / node | 20 GB | Yes | Can only be increased, not decreased |
| Maximum disk size / node | 5 TB | — | Can only be increased, not decreased |
| Maximum IOPS / node | 60,000 | Yes | IOPS can be both increased and decreased |
| JVM heap | 50% of node memory | Yes | Up to 32 GB |
| Maximum shards / cluster | 1,000 × number of data nodes | Yes, via Configuration Group (about 1 – 10,000 shards / node) | Default is 1,000 shards / node. Example: a 3-node cluster allows up to 3,000 shards; a 9-node cluster up to 9,000 shards |
| Available regions | HCM | — | HAN region is not supported yet |
| Multi-AZ | Not supported | — | Multi-AZ is not supported yet |

## Notes

### Maximum shards

* The limit applies to the whole cluster and equals `cluster.max_shards_per_node` × number of data nodes, counting both primary and replica shards of open indices. Every vDB OpenSearch node is both a master and a data node, so the number of data nodes equals the number of nodes in the cluster.
* When the limit is exceeded, requests that create an index or add replicas are rejected with the error `this action would add [...] total shards, but this cluster currently has [...]/[...] maximum shards open`.
* If `cluster.max_shards_per_cluster` is set (other than -1), `cluster.max_shards_per_node` must not exceed it.

### JVM heap

The OpenSearch service limits the memory of Java processes to 50% of the node's total available memory (up to 32 GiB).
