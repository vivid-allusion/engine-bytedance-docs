---
title: "Auto scaling"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/vke_auto_scaling"
---

Volcano Engine EMR on VKE provides elastic scaling functionality, supporting automatic and dynamic expansion and contraction of cluster computing resources according to business demand fluctuations. This article introduces how to configure elastic scaling rules for resources and use this feature.

<span id="d96da2c2"></span>
# Context

When using EMR virtual clusters, if resources frequently experience peaks and troughs, temporary computing capacity can be automatically expanded during computing peaks to help you handle business surges; after the business peak, automatic contraction reduces your computing resource usage costs.

EMR virtual clusters support node elastic scaling. When the cluster's capacity planning cannot meet scheduling capacity, ECS (Elastic Compute Service, cloud server) instances are added to supplement the overall cluster scheduling capacity.

<span id="1d9ea831"></span>
# Important notes


* Node elastic scaling only applies to the node resources of **billing by volume**.

* The cluster must have the karpenter component installed. If your cluster does not have this component, it will be automatically installed when elastic scaling takes effect.


<span id="2f24fff2"></span>
# Feature entry


1. Log in to [EMR Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home). Then, from the left navigation bar, go to **Resource Management \> on VKE\>**  \*\*Virtual clusterDetails \> Elastic Scaling \*\*tab, and click Go to configure on the page to start configuring cluster elastic scaling rules.

2. Select the scaling type for elastic scaling as prompted on the interface, and configure the detailed parameters for the corresponding type.

   Currently, EMR supports two scaling types: node instant elasticity and node automatic scaling.

   * Node instant elasticity: Expansion of nodes can be triggered by event listening, offering superior elasticity performance. This method is recommended.

   * Node automatic scaling\*\*:\*\* Automatically expands or contracts cluster nodes by polling and detecting node resource usage.

      When selecting different elastic scaling methods, configure the detailed parameters as prompted on the interface. See below for details.


<span id="df6ad82a"></span>
# Configure elastic scaling rules

<span id="df6ad82a"></span>
## Scaling type: node instant elasticity


1. Configure basic information. **Node instant elasticity type** enables the auto scale\-down switch by default and does not support disabling it.

2. Auto scale\-down configuration.

   
   |Parameters |Note |
   |---|---|
   |Scale\-in threshold for non\-GPU nodes |When the CPU or memory resource utilization of non\-GPU nodes (`resource request / total resource * 100%`) falls below this threshold, automatic scale\-in may be triggered. Default is 50%. The configurable range is 0–100.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If either the CPU or memory resource of a non\-GPU node reaches the scale\-down threshold, this rule is triggered.</div><br> |
   |Scale\-in threshold for GPU nodes |The scale\-in strategy for GPU nodes varies depending on whether mGPU capability is used. The default threshold is 50%:<br><br><br>* Without mGPU: When the GPU resource utilization of the node (`resource request / total resource * 100%`) falls below this threshold, automatic scale\-in may be triggered.<br><br>* With mGPU: When the utilization of any of mGPU's GPU computing power, GPU memory, memory, or CPU resources (`resource request / total resource * 100%`) falls below this threshold, automatic scale\-in may be triggered.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">mGPU is currently in the <strong>public beta</strong> phase. For a detailed description of the functionality, see <a href="https://docs.byteplus.com/en/docs/vke/mGPU-overview">mGPU overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the installed version of the cluster\-autoscaler component in the VKE cluster is outdated, please upgrade the component. For detailed instructions, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on">Upgrade the component</a>; for the release notes of the cluster\-autoscaler component, see <a href="https://docs.byteplus.com/en/docs/vke/cluster-autoscaler">cluster\-autoscaler</a>.</div><br> |
   |Scale\-in trigger delay |When the node resource utilization falls below the threshold and persists for this duration, the cluster will trigger auto scale\-down. The default is 10 minutes. |
   |Pod termination timeout |The maximum wait time for Pod termination during node draining. Integer value, range: 1–10000. Unit: seconds. Default: 600 seconds. |
   


<span id="df6ad82a"></span>
## Scaling type: Node auto scaling


1. Configure basic information.

   
   |Parameters |Note |
   |---|---|
   |Scaling algorithm |The types of scaling algorithms used for node pool auto\-scaling include:<br><br><br>* **random**: Randomly selects a node pool for scaling.<br><br>* **most\-pods**: Selects the node pool that can schedule the most Pods for scaling.<br><br>* **least\-waste**: Selects the node pool with the least idle CPU resources for scaling.<br><br>* **priority**: Selects the node pool with the highest priority for scaling, based on the priority set after enabling **elastic scaling** for the node pool. |
   |Elastic sensitivity |The interval for determining cluster elastic scaling; supported values are: **10s**, **15s**, **30s**, **60s**, **120s**, **180s**, and **300s**. |
   |Auto Scaling Down |Whether to enable automatic node scale\-in:<br><br><br>* **Enable**: Scale\-in will be triggered when there are many idle nodes in the cluster. Applies only to pay\-as\-you\-go node resources.<br><br>* **Disable**: After node scale\-out, automatic scale\-in will not occur even if utilization decreases. |
   |Startup stain |Click **Add Taint** to set the startup taint. When this taint exists on a node, the system considers the node as not fully initialized. |
   

2. (Optional) Auto scale\-down configuration. After the "auto scale\-down" switch is enabled in the basic information, you must also configure the auto scale\-down settings.

   
   |Parameters |Note |
   |---|---|
   |Scale\-in threshold for non\-GPU nodes |When the CPU or memory resource utilization of non\-GPU nodes (`resource request / total resource * 100%`) falls below this threshold, automatic scale\-in may be triggered. Default is 50%. The configurable range is 0–100.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If either the CPU or memory resource of a non\-GPU node reaches the scale\-down threshold, this rule is triggered.</div><br> |
   |Scale\-in threshold for GPU nodes |The scale\-in strategy for GPU nodes varies depending on whether mGPU capability is used. The default threshold is 50%:<br><br><br>* Without mGPU: When the GPU resource utilization of the node (`resource request / total resource * 100%`) falls below this threshold, automatic scale\-in may be triggered.<br><br>* With mGPU: When the utilization of any of mGPU's GPU computing power, GPU memory, memory, or CPU resources (`resource request / total resource * 100%`) falls below this threshold, automatic scale\-in may be triggered.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">mGPU is currently in <strong>public beta</strong>. For detailed feature descriptions, see <a href="https://www.volcengine.com/docs/6460/132501">mGPU overview</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If the cluster\-autoscaler component installed in the VKE cluster is an earlier version, please upgrade the component. For detailed instructions, see <a href="https://www.volcengine.com/docs/6460/159826">Upgrade component</a>; for cluster\-autoscaler component release notes, see <a href="https://www.volcengine.com/docs/6460/178290">cluster\-autoscaler</a></div><br> |
   |Scale\-in trigger delay |When node resource utilization falls below the threshold and persists for this duration, the cluster will trigger automatic scale\-in. Default is 1 minute. |
   |Scale\-in cooldown time after scale\-out |The waiting interval required before scale\-in can be executed again after node scale\-out. Default is 10 minutes. |
   |Cooldown time after scale\-down failure |The interval that must be waited before scale\-down can be executed again after a node scale\-down failure. Default: 3 minutes. |
   |Maximum concurrent scale\-downs |The maximum number of concurrent scale\-downs allowed when scaling down nodes. Default: 5. |
   |Pod termination timeout |The maximum wait time for Pod termination during node draining. Integer value, range: 1–10000. Unit: seconds. Default: 600 seconds. |
   |Minimum Pod replicas |The minimum number of Pods allowed to exist during node draining. Integer value, range: 1–10000. Default: 0. |
   |DaemonSet Pod eviction |Whether to evict DaemonSet\-type Pods on the node before node scale\-down.<br><br><br>* **Enabled**: Indicates that DaemonSet\-type Pods on the node will be evicted before node scale\-down.<br><br>* **Disabled**: Indicates that DaemonSet\-type Pods on the node will not be evicted before node scale\-down. |
   |Do not scale down nodes |Select nodes that should not be scaled down. Available options:<br><br><br>* Nodes containing Pods with local storage.<br><br>* Nodes containing Pods not managed by DaemonSet in the kube\-system namespace. |
   


<span id="69abeeaa"></span>
# Enable or disable elastic scaling

After completing the elastic scaling rule configuration, this scale is in the default "disabled" state. You can enable or disable elastic scaling for the node pool on the elastic scaling tab.

<span id="511f51ff"></span>
# Edit elastic scaling configuration

After enabling the elastic scaling rule, you can also adjust the elastic scaling rule as needed.


1. After entering the cluster's elastic scaling configuration page, click the **Operation** column's **Configure** button for the node pool's elastic scaling rule to enter the configuration edit page.

2. Modify the node count and priority according to the interface prompts.

   
   |Parameters |Note |
   |---|---|
   |Node count range |The range of node counts that can be dynamically adjusted during elastic scaling. Default: 0–10. |
   |Priority |When the elastic scaling algorithm is set to Priority, node pools with higher priority are scaled out. The larger the number, the higher the priority. Default: 10. |
