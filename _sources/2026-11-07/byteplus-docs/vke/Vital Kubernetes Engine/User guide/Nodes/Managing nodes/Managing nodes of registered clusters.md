---
title: "Managing nodes of registered clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Registered_cluster_node_management"
---

VKE allows you to flexibly access and manage Kubernetes clusters in any region or on any infrastructure, and provides a unified management view. However, you can view and perform basic operations on infrastructure resources, but cannot create and delete these resources.

<span id=".5Yib5bu66IqC54K5"></span>
## Creating nodes

VKE does not allow you to create or delete infrastructure resources of registered clusters, such as nodes, storage resources, and network resources. To add or delete nodes, go to the source platform.

<span id=".5p-l55yL6IqC54K5"></span>
## Viewing nodes

After a registered cluster is created, the node information from the source cluster will be synchronized.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, click the name of the target registered cluster.

3. In the left navigation bar of the registered cluster management page, click **Nodes \> Node** to go to the node management page and view node\-related information.


<span id=".566h55CG6IqC54K5"></span>
## Managing nodes

After nodes are synchronized, find the target node and click `...` in the Actions column on the Node page to perform the corresponding operation on the node. Detailed descriptions are as follows:


|Parameter |Description |
|---|---|
|InActive |During routine cluster maintenance, nodes may need to go offline to ensure data security in scenarios such as upgrades, node scale\-out, maintenance downtime, node reclaim, and change operations.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When a node is taken offline, all pods on that node, except DaemonSet, will be migrated to other nodes in the cluster, and the node will be set to unschedulable status (new pods cannot be scheduled on this node). This action may adversely affect business operations. We recommend doing it during low\-traffic hours.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Taking a node offline will reduce the remaining ResourceQuota of the cluster to which the node belongs. If the cluster does not have sufficient resource reservations, this action will adversely affect the scheduling of new services and the running of existing workloads.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the current cluster is registered through proxy mode, do not take all nodes offline. Otherwise, the cluster connection status will become abnormal as the proxy add\-on is unavailable.</div><br> |
|Cordon |Unlike taking nodes offline, the action of cordoning nodes does not migrate pods to other nodes in the cluster. Instead, the node is set to cordoned and unschedulable status, and the pods already running on the node are not affected.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Cordoning a node reduces the remaining resource quota of its cluster. If the cluster has insufficient available resources, node cordoning will affect the scheduling of new applications and the operation of existing ones.</div><br> |
|Make it schedulable |You can restore scheduling capability for nodes to allow them to accept new pods. After a node is restored to schedulable status, the remaining ResourceQuota of the cluster to which the node belongs will increase. |
|Label management |Create different labels for nodes to define specific attributes and support scenarios such as batch filtering. You can manage node labels in the console by adding, editing, or deleting them. |
|Taint management |Create one or more taints for a node to enable the node to repel specific pods, which prevents the pods from being scheduled onto the node. You can manage node taints in the console, including adding, editing, and deleting node taints. |
