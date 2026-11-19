# Delete Selected Nodes in a Node Group

> This guide helps you delete specific nodes in a Node Group on VKS, instead of letting the system pick the nodes when scaling down your cluster.

---

## When to use this feature

By default, when you reduce the number of nodes in a Node Group (the **Resize** feature), the system picks the nodes to delete and you have no control over which one is removed. The selected-node deletion feature lets you specify exactly which nodes are deleted, which is useful when:

* You want to remove a faulty node stuck in a non-working state that the system does not detect by itself.
* You want to remove an idle node instead of one running heavy workloads.
* You want to keep nodes that hold zonal volumes or local storage.

---

## Prerequisites

* A running vKS cluster with at least one Node Group.
* The Node Group is in the **Active** or **Degraded** state.
* The cluster is not performing another operation (for example: upgrade, Node Group update).

---

## Delete nodes using the console

**Step 1: Open the node list of the Node Group**

1. Visit [https://vks.console.greennode.ai/overview](https://vks.console.greennode.ai/overview).
2. Select the cluster that contains the Node Group you want to scale down.
3. On that Node Group, select **View nodes** to open the node list.

**Step 2: Select the nodes to delete**

1. Tick the checkbox at the beginning of each row for the nodes you want to delete. The footer shows the count **N nodes selected**.
2. Tick the checkbox in the table header to quickly select all nodes **currently displayed** on the current page or in the search results. Selections on other pages are preserved.
3. Select **Delete selected nodes**.

{% hint style="info" %}
**Note:**

If **Autoscaling** is enabled, the maximum number of nodes you can delete is `numNodes − Minimum node`. When your selection exceeds this limit, the system shows a warning and disables the delete button — lower the **Minimum node** setting of the Node Group first if you need to delete more nodes.
{% endhint %}

**Step 3: Confirm the deletion**

1. Review the confirmation modal: the title shows the number of nodes to be deleted, along with the list of selected node names.
2. (Optional) Tick **Delete immediately (skip drain)** to delete the nodes right away without draining. When this option is enabled, also tick the risk acknowledgement checkbox to activate the **Delete** button.
3. Select **Delete**.

{% hint style="warning" %}
**Warning:**

* This action cannot be undone. Pods running on the selected nodes are moved to other nodes if there are enough resources; data stored on the nodes is lost.
* By default, a node is deleted after it is drained (respecting PodDisruptionBudget, up to 600 seconds). With **Delete immediately (skip drain)**, pods are terminated immediately without respecting PodDisruptionBudget — workloads may be disrupted, and data on emptyDir volumes or local Persistent Volumes is lost.
{% endhint %}

If you select all of the last running nodes of the cluster (no other Node Group is running any node), the system automatically applies delete-immediately (skip drain) because the evicted pods cannot be moved to other nodes, and shows a corresponding warning in the confirmation modal.

---

Besides the console, you can also delete selected nodes using the API. See the documentation at [VKS API](https://docs.api.greennode.ai/service-docs/vks-api.html#tag/Node-Group-Controller/paths/~1v1~1clusters~1%7BclusterId%7D~1node-groups~1%7BnodeGroupId%7D~1delete-nodes/post).

---

## What happens after you submit the deletion

* The Node Group switches to the **Updating** state during deletion and returns to **Active** when it completes. Only the nodes in the selected list are deleted; the other nodes and the entire Node Group configuration (labels, taints, Autoscaling, image...) stay unchanged.
* If the deletion fails (for example: a node is already being deleted by another operation, or Autoscaling does not allow further scale-down), the Node Group is rolled back to its previous state and configuration, no node is deleted, and a **Warning** event with the reason is recorded in the cluster's event list.
* If **Autoscaling** is enabled and the pods moved off the deleted nodes do not fit on the remaining nodes, the Autoscaler may create new nodes within the configured **Minimum node** – **Maximum node** range.

---

## Result

The nodes you selected have been deleted from the Node Group; the remaining nodes and the Node Group configuration are unchanged. If the deletion fails, check the cluster's event list for the reason.

| I want to... | Go to |
|---|---|
| Learn about Autoscaling | [Auto Scaling](auto-scaling.md) |
| Change the node count without selecting specific nodes | [Node Groups](README.md) |
