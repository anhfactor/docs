# Placement Group

An affinity group is the orchestration policy designed for VM Instances location to ensure your VM Instances meet requirement of high performances or high availability.

## Placement group policy <a href="#servergroup-servergrouppolicy" id="servergroup-servergrouppolicy"></a>

Currently, GreenNode provides two Placement Group policies to better manage VM instances and hosts: soft anti-affinity and soft affinity.

* Soft Anti-affinity: Allocate VM instances in the server group to different hosts as much as possible. If no more hosts are available, the VM instances will be allocated randomly.
* Soft Affinity: Allocate VM instances in the server group to same host as much as possible. If no more resource of host are available, the VM instances will be allocated randomly.

## Scenarios <a href="#servergroup-scenarios" id="servergroup-scenarios"></a>

Some usage examples of soft anti-affinity and soft affinity group policies.

* Soft Anti-affinity group: You might want to deploy nodes with different roles on different hosts to improve the overall system performance.
  * For example, when you deploy a Hadoop system, you might find it difficult to calculate the exact number of nodes of different roles such as NameNode, DataNode, JobTracker, and TaskTracker. However, you might know that deploying these nodes on different hosts is more effective. With the soft anti-affinity policy, you can deploy Hadoop clusters on different hosts as much as possible, which relieves the I/O pressure and improves the overall performance of the system.
* Soft affinity group: You might want to deploy two VM instances that run exactly on the same physical host to ensure lowest latency or maximum network throughput.
  * For example, you deploy two VM instances to run an nginx web application and redis caching, and requires that these two VM instances should locate in the same host to have faster connection between them.

## Work with Placement group <a href="#servergroup-workwithservergroup" id="servergroup-workwithservergroup"></a>

You can create a placement group with the affinity or anti-affinity policy. This option can not be changed after create.

1. Go to GreenNode Portal console, navigate to Placement Group page
2. Create additional Placement Groups and choose the appropriate affinity or anti-affinity policy. Once the Server group is created, you cannot change this policy attribute.
3. You can create virtual servers and select an existing Placement Group according to your needs.

<br>
