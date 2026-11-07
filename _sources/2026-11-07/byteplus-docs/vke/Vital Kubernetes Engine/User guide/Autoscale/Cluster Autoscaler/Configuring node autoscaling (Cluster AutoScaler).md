---
title: "Configuring node autoscaling (Cluster AutoScaler)"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler"
---

Vital Kubernetes Engine (VKE) clusters support node autoscaling by using cluster\-autoscaler. This topic describes how to configure node autoscaling.

<span id="CetgWOXF"></span>
## Background information

<span id="iyvkHLJl"></span>
### Node scale\-out

The procedure of Cluster AutoScaler (CA) scaling out nodes is as follows:


1. By default, CA checks whether pods in the Pending status with a priority higher than your custom priority (default priority: 10) exist in a cluster every 10 seconds.

2. If pods in the Pending status exist due to insufficient resources, CA will create one or more nodes in the node pool based on the user\-defined scale\-out algorithm.

3. The nodes will be added to the cluster, which are in Ready status and are used to create pods.

4. The Kubernetes scheduler allocates pods in the Pending status to new nodes. If some pods are still in the Pending status, the preceding procedure will be repeated to add more nodes to the cluster.


When multiple node pools exist in the cluster, you can configure different scale\-out algorithms to select nodes. The following four algorithms are supported:


* random: A random node pool will be selected for scale\-out.

* most\-pods: The node pool that can accommodate the most pods will be selected for scale\-out.

* least\-waste: The node pool with the least available CPU resources will be selected for scale\-out.

* priority: The node pool with the highest configured priority will be selected for scale\-out.


<span id="NGsoetAX"></span>
### Node scale\-in

The procedure of CA scaling in nodes is as follows:


1. By default, CA monitors the resource usage of nodes every ten seconds.

2. When the resource request of a node falls below a configurable threshold (default 50%), and its pods can be rescheduled to other nodes, CA will automatically delete it if all autoscaling node pools in the cluster have had no scaling activities for a configurable period (default 10 minutes). This helps optimize resource utilization.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">CA determines whether to add or delete nodes based only on pod scheduling status and overall node resource usage. It does not consider the resource metrics of pods or nodes.</div>


* <div data-tips="true" data-tips-type="tip">Pod rescheduling may occur when a node is deleted. Therefore, if automatic scale\-in is configured, your application must be able to tolerate rescheduling and brief interruptions, or a multi\-replica policy is used to prevent business interruption.</div>


* <div data-tips="true" data-tips-type="tip">For node pools with GPU instance types, when CA scales out nodes, CA will wait for GPU resources to be allocated on the new nodes. If GPU resources cannot be allocated for a long period of time, CA cannot perform scaling as expected. Therefore, when you use node pools with GPU instance types, make sure that the nvidia\-device\-plugin add\-on is installed in the cluster. For the add\-on installation method, see <a href="https://docs.byteplus.com/en/docs/vke/Installing-an-add-on#.bnZpZGlhLWRldmljZS1wbHVnaW4t57uE5Lu2">nvidia\-device\-plugin</a>.</div>



<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Usage limits


* The cluster\-autoscaler add\-on and the karpenter add\-on cannot both be installed.

* The autoscaling rule configured during add\-on installation is the same as that described in this topic. It is the node autoscaling configuration. In other words, you can configure an autoscaling rule by using two configuration entries, and the rule from any entry will overwrite the other.

* Node autoscaling only applies to **pay\-as\-you\-go** nodes.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The cluster\-autoscaler add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

* A node pool has been created, and the **autoscaling** feature has been enabled.

   * You can directly enable autoscaling when you create a node pool. For details, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

   * You can edit an existing node pool to enable autoscaling. For detailed instructions, see [Editing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools#.57yW6L6R6IqC54K55rGg).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VKE console ](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Node pool**. On the page that appears, click **Autoscaling configuration**.

5. On the **Autoscaling configuration** page, click **Edit rules** to specify the parameters of the autoscaling rule.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The configurations displayed in the <strong>Autoscaling rule</strong> dialog box match those on the add\-on installation page. Any changes to the rule will overwrite the one configured during add\-on installation.   </div>
   

   
   |Parameter |Description |
   |---|---|
   |Cluster name |The name of the current cluster cannot be modified. |
   |Scale\-out algorithm |The automatic scale\-out algorithm for node pools. Valid values:<br><br><br>* **random**: A random node pool will be selected for scale\-out.<br><br>* **most\-pods**: The node pool that can accommodate the most pods will be selected for scale\-out.<br><br>* **least\-waste**: A node pool with the least available CPU resources will be selected for scale\-out.<br><br>* **Priority**: When **Autoscaling** is enabled, the node pool with the highest priority is selected for scale\-out. |
   |Elastic sensitivity |The time interval at which the cluster checks whether the conditions are met for the autoscaler. Available values include **10s**, **15s**, **30s**, **60s**, **120s**, **180s**, and **300s**. |
   |Automatic scale\-in |Whether to enable automatic node scale\-in:<br><br><br>* Enable: Automatic scale\-in starts if there are a certain number of idle nodes. Effective only for Pay\-as\-you\-go node resources.<br><br>* If you do not enable this option, no automatic scale\-in will be triggered, even if the request rate decreases after a node scale\-out. |
   |Startup taints |Click **Add** to configure the startup taints. The nodes with this taint will be regarded by the system as not initialized. |
   |Ignore the taint |Click **Add** to configure taints to be ignored. During the scale\-out process, the system ignores scheduling attributes related to specified taints of nodes or node pools. |
   

   If **Enable automatic scale\-in** is selected, you need to specify the following parameters.

   
   |Parameters |Description |
   |---|---|
   |Scale\-in threshold for non\-GPU nodes |Automatic scale\-in may be triggered if both the CPU and memory request rates of a non\-GPU node are lower than the threshold. The request rate is calculated by using the following formula: `request amount for that resource / total quantity of that resource × 100%`. The default threshold is 50%. |
   |Scale\-in threshold of GPU nodes |The scale\-in policy varies for GPU\-based nodes depending on whether the mGPU capability is enabled. The default threshold is 50%:<br><br><br>* mGPU disabled: Automatic scale\-in may be triggered if the GPU resource request rate of a node is lower than the threshold. The request rate is calculated by using the following formula: `single resource request amount/single resource total amount × 100%`. <br><br>* mGPU enabled: Automatic scale\-in may be triggered if the request rate of any mGPU resource is lower than the threshold. These resources include GPU computing power, GPU video memory, system memory, and CPU. The request rate is calculated using the following formula: `single resource request amount/single resource total amount × 100%`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">mGPU is currently in <strong>public beta</strong>. For details, see <a href="https://docs.byteplus.com/en/docs/vke/mGPU-overview">mGPU overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Scale\-in threshold is only effective for the following versions of the cluster\-autoscaler add\-ons:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">v1.26.3\-vke.6 or later.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">v1.24.2\-vke.6 or later.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">v1.20.2\-vke.20 or later.</div><br><br><br>   <div data-tips="true" data-tips-type="warning">You can update the cluster\-autoscaler add\-on if necessary. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrading add\-ons</a>. For the release notes of the cluster\-autoscaler add\-on, see <a href="https://docs.byteplus.com/en/docs/vke/cluster-autoscaler">Cluster\-autoscaler</a>   </div><br>    |
   |Scale\-in trigger latency |Automatic cluster scale\-in is triggered if the node resource request rate remains lower than the threshold for the specified period. 10 minutes by default. |
   |Cooldown period for scale\-in after scale\-out |The interval to wait before scale\-in can be performed again after a scale\-out. 10 minutes by default. |
   |Calculate scale\-in delay based on node pool local state |Whether to calculate scale\-in delays based on the local status of nodes. Values:<br><br><br>* If this option is enabled, an independent "scale\-in delay timer" is maintained for each node pool to accelerate scale\-in and avoid resource waste.<br><br>* If this option is disabled, after a node scale\-out, all node pools in the cluster will not experience a scale\-in within the scale\-in cooldown period by default. |
   |Cooldown period after scale\-in failure |The interval to wait before scale\-in can be performed again after a scale\-out. 3 minutes by default. |
   |Maximum concurrent scale\-in capacity |The maximum number of nodes processed simultaneously during scale\-in is 5 by default. |
   |Pod termination timeout |The maximum wait time for pod termination during draining. Enter an integer from 1 to 10000, measured in seconds. The default value is 600 seconds. |
   |The minimum number of pod replicas |The minimum number of pods allowed on the node during draining. Enter an integer from 1 to 10000. The default value is 0. |
   |DaemonSet Pod drain |Whether to evict DaemonSet pods on the node before scale\-in starts.<br><br><br>* If you enable this feature, DaemonSet pods on the node will be evicted first before a node scale\-in.<br><br>* If you disable this feature: DaemonSet pods on the node will not be evicted before a node scale\-in. |
   |Nodes without scale\-in |Select the nodes that do not need scale\-in. Options are as follows:<br><br><br>* Node containing local storage pods.<br><br>* Nodes containing pods that are not managed by DaemonSet in the kube\-system namespace. |
   |Ignoring DaemonSet resource usage when calculating node scale\-in thresholds |Whether to ignore resources consumed by DaemonSets when calculating node resource usage.<br><br><br>* If you check this option, resource usage of DaemonSets is ignored during calculation of node resource usage.<br><br>* If you do not check this option, resource usage of DaemonSets is not ignored during calculation of node resource usage. |
   |Startup taints |Configure startup taints. If the specified taint exists on a node, the node is considered not fully initialized. |
   |Ignore the taint |Specify taints to be ignored. During scaling, the specified taint attributes of nodes and node pools are ignored. |
   |Node readiness wait timeout |Specify the maximum timeout time (in minutes) for waiting for node readiness in the node scale\-in process. The value must be an integer from 1 to 60. |
   

6. Click **Confirm**.


<span id=".57uT5p6c6aqM6K-B"></span>
## Validating results

After the configuration is complete, you can view the autoscaling rule and node pools for which autoscaling is enabled.

When nodes in a cluster are insufficient, pods enter the Pending status. The system will then automatically scale cluster nodes. Click the node pool name to access its details page. Click the **Scaling record** tab to view the node pool's autoscaling records.

<span id="CEkSCZtK"></span>
## Related documentation

For the principles of cluster scaling in Kubernetes, see [Community documentation](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md).
