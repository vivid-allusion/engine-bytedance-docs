---
title: "Node pool overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/NodePool-overview"
---

Node pools are provided in Vital Kubernetes Engine (VKE) to enable you to easily manage nodes in Kubernetes clusters. This topic mainly describes the overview, features, and life cycles of node pools.

<span id=".6IqC54K55rGg566A5LuL"></span>
## Introduction

A node pool consists of one or more nodes that have the same configurations in a cluster. The configurations of a node pool include node attributes, such as node specifications, availability zones (AZ), labels, and taints. You can specify the attributes when you create a node pool, or modify the attributes after the node pool is created. For more information about how to create a node pool, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool). 

You can scale a node pool to add one or more Elastic Compute Service (ECS) instances that function as nodes with the same configurations. For more information about how to scale node pools, see [Scaling out/in node pools](https://docs.byteplus.com/en/docs/vke/Scaling-a-NodePool). Under specific conditions, you can also add your existing ECS nodes to a VKE node pool. For more information about how to add existing nodes, see [Add an existing node](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.5re75Yqg5bey5pyJ6IqC54K5). Node pools enable you to easily manage and perform operation and maintenance on cluster nodes in groups. For example, you can configure worker nodes and configure cluster autoscaling. For more features of node pools, see [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools).

Node pools enable you to achieve mixed deployment and management of different types of nodes in the same cluster.


* In a cluster, you can create node pools with different operating systems, such as veLinux, CentOS\-compatible veLinux version, and Ubuntu.

* In a cluster, you can create node pools with different billing types, including pay\-as\-you\-go, subscription, and preemptible instances.

* You can create multiple node pools with autoscaling enabled in a cluster.

* You can create multiple node pools with different scaling modes in a cluster.


<span id=".6IqC54K55rGg5YiG57G7"></span>
## Categories 

Node pools are categorized into the following types in VKE:


* **Custom node pool**

   You can specify the basic information, worker node configurations, system configurations, and other configurations for a custom node pool. Custom configurations will be applied to all newly added worker nodes in the node pool.

   Some qualified custom node pools let you add existing ECS instances as nodes to meet needs, such as resource reuse and node preheating.

* **Managed node pool**

   The managed node pool is operated and maintained by VKE. It provides default node diagnostics and self\-healing rules to simplify routine O&M and fault handling and improve resource utilization.

* **Default node pool**

   VKE allows you to add existing ECS instances (existing nodes) to VKE clusters. VKE provides the **default node pool**, which is different from standard node pools, to help you manage existing nodes that are added to clusters. The default node pool provides the same configuration items, such as security configurations, advanced configurations, and additional configurations, as standard node pools. However, you cannot scale in or out the default node pool or edit the number of nodes for the default node pool.

   The default node pool is named `vke-default-nodepool` by VKE and cannot be modified.


<span id=".6IqC54K55rGg55Sf5ZG95ZGo5pyf"></span>
## Life cycle

A lifecycle tracks the different statuses of a node pool from its creation to deletion or removal. For descriptions of the node pool lifecycle and status transitions, see [Resource status description](https://docs.byteplus.com/en/docs/vke/Resource-status-description#.6IqC54K55rGg).
