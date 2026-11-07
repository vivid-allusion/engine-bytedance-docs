---
title: "Scaling out clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Scaling-out-a-cluster"
---

In VKE, you can scale out a cluster by adding new worker nodes or existing ECS instances to it.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage limits


* When adding new or existing nodes, you can add nodes that use either the **Pay\-as\-you\-go** or **Subscription** billing method.

* Scale\-out is limited by the cluster quota. If the quota is insufficient, apply for a quota increase. For details, see [Limits](https://docs.byteplus.com/en/docs/vke/Limits).


<span id=".5paw5aKe6IqC54K5"></span>
## Add nodes

There are two ways to add new nodes to a cluster:


* Automatic scale\-out: Configure an autoscaler rule for the cluster node pool. This enables the cluster to automatically scale out based on the scheduling status of Pods and the usage of node resources within the cluster. For details, see [Node autoscaling overview](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works).

* Manual scale\-out: You can manually add new nodes to the cluster. The methods include:

   * Adding nodes to an existing node pool: Nodes added in this way inherit the existing node pool's billing method, instance specifications, system configuration, and security group settings.

   * Creating a new node pool: A new node pool always contains at least one node. This increases the total number of nodes in the cluster.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For instructions on manually adding nodes to a cluster, see <a href="https://docs.byteplus.com/en/docs/vke/Adding-nodes">Adding nodes</a>.</div>


<span id="OoZz3GSH"></span>
## Add existing nodes

VKE provides a default node pool (`vke-default-nodepool`) that allows cluster scale\-out by adding existing ECS instances to the cluster as nodes. For details, see [Adding existing nodes](https://docs.byteplus.com/en/docs/vke/Adding-existing-nodes).
