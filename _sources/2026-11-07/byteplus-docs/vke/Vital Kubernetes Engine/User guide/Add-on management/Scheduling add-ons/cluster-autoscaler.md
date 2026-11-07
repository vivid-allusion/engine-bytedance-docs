---
title: "cluster-autoscaler"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/cluster-autoscaler-add-on"
---

cluster\-autoscaler is the add\-on that enables node autoscaling in VKE clusters. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="jWDWHzgd"></span>
## Add\-on overview

cluster\-autoscaler is a resource\-layer autoscaling add\-on in VKE clusters. When cluster capacity planning fails to meet scheduling demands, it ‌automatically adds resources (such as ECS or VCI resources) to increase overall scheduling capacity. The add\-on automatically completes the supplement and release of cluster resources to prevent business disruption caused by insufficient resources.

By default, cluster\-autoscaler is a managed add\-on that deploys no Kubernetes resources in your cluster and consumes zero computing resources on cluster nodes.

<span id="UO7cADXw"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/cluster-autoscaler).

<span id="GnWwGRCa"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Management method | **[** [Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features) **]**  The method of managing the cluster\-autoscaler add\-on.<br><br><br>* **Managed**: The system manages the add\-on. You do not perform operation and maintenance on the add\-on, such as upgrades and configuration. Using this management method can prevent issues such as add\-on faults and unsatisfactory performance caused by users. It reduces user maintenance costs and enhances add\-on stability.<br><br>* **Unmanaged**: Users independently perform operation and maintenance on the add\-on, such as upgrading and configuring the add\-on. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. Select the type of nodes on which the add\-on is deployed. This add\-on only supports **Elastic Compute Service deployment**, which means that the add\-on is deployed on ECS nodes in the cluster. |
   |VCI rule |Configure the VCI rule.<br><br><br>* **Scale\-out algorithm**: The type of node pool automatic scale\-out policies. Valid values:<br><br>   * **random**: A random node pool will be selected for scale\-out.<br><br>   * **most\-pods**: The node pool that can accommodate the most pods will be selected for scale\-out.<br><br>   * **least\-waste**: The idle node pool with the least CPU resources will be selected for scale\-out.<br><br>   * **priority**: The node pool with the highest configured priority will be selected for scale\-out.<br><br>* **Elastic sensitivity**: The time interval at which the cluster checks whether the conditions are met for the autoscaler. Available values include **10s**, **15s**, **30s**, **60s**, **120s**, **180s**, and **300s**.<br><br>* **Automatic scale\-in**: After you enable this feature, automatic scale\-in is triggered when the cluster has a relatively large amount of idle node resources. This feature only applies to **pay\-as\-you\-go** nodes.<br><br>* **Startup taints**: Click **Add** to configure the startup taints. The nodes with the taints will be deemed not initialized.<br><br>* **Ignore the taint**: Click **Add** to configure taints to be ignored. During the scale\-out process, the system ignores scheduling attributes related to specified taints of nodes or node pools.<br><br><br>If **Automatic scale\-in** is enabled, you need to specify the following parameters based on your business requirements.<br><br><br>* **Scale\-in threshold for non\-GPU nodes**: Automatic scale\-in may be triggered if both the CPU utilization and memory utilization of a non\-GPU node are lower than the threshold. The utilization is calculated by using the following formula: `usage of that resource / total quantity of that resource × 100%`. The value is an integer. Valid values: 0 to 100. Default value: 50. If the value is set to 0, it indicates that scale\-in is not triggered.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Either the CPU or memory usage of a non\-GPU based node can trigger scale\-in.   </div><br>   <br><br>* **Scale\-in threshold of GPU nodes**: The scale\-in policies of GPU nodes vary based on whether the mGPU capability is enabled. The value is an integer. Valid values: 0 to 100. Default value: 50. If the value is set to 0, it indicates that scale\-in is not triggered.<br><br>   * mGPU disabled: automatic scale\-in may be triggered if the GPU resource usage (calculated with `single resource request amount ÷ single resource total amount * 100%`) of a node falls below this threshold.<br><br>   * mGPU enabled: automatic scale\-in may be triggered if the usage (calculated with `single resource request amount ÷ single resource total amount * 100%`) of any resources in mGPU, including GPU computing power, GPU video memory, system memory, and CPU, falls below this threshold.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">mGPU is currently in <strong>public beta</strong>. For details, see <a href="https://docs.byteplus.com/en/docs/vke/mGPU-overview">mGPU overview</a>.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This value can be set only for the following versions of the cluster\-autoscaler add\-on:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.26.3\-vke.6 or later.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.24.2\-vke.6 or later.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.20.2\-vke.20 or later.   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For the release notes of the cluster\-autoscaler add\-on, see <a href="https://docs.byteplus.com/en/docs/vke/cluster-autoscaler">Cluster\-autoscaler</a>.   </div><br>   <br><br>* **Scale\-in trigger latency**: Automatic scale\-in starts if the node resource usage remains below the threshold for a specified period. 10 minutes by default.<br><br>* **Cooldown period for scale\-in after scale\-out**: The interval to wait before you can perform scale\-in again after a scale\-out. 10 minutes by default.<br><br>* **Calculate scale\-in delay based on node pool local status**: Specify whether to calculate scale\-in delay based on the local node status. If this option is enabled, the cluster maintains an independent "scale\-in delay timer" for each node pool, which can accelerate scale\-in and avoid resource waste.<br><br>* **Cooldown period for scale\-in failure**: The interval to wait before you can perform scale\-in again after a failure. 3 minutes by default.<br><br>* **Maximum concurrent scale\-in capacity**: The maximum number of nodes can be handled simultaneously during the scale\-in process. 5 by default.<br><br>* **Pod termination timeout**: The maximum wait time for pod termination during node draining. Enter an integer from 1 to 10000, measured in seconds. The default value is 600 seconds.<br><br>* **Pod minimum number of replicas**: The minimum number of pods allowed on the node during draining. Enter an integer from 1 to 10000. The default value is 0.<br><br>* **DaemonSet Pod drain**: Specify whether to evict DaemonSet pods on the node before scale\-in.<br><br>   * When it is **checked**, DaemonSet pods on the node will be evicted before scale\-in.<br><br>   * When it is not checked, DaemonSet pods on the node will not be evicted before scale\-in.<br><br>* **Nodes without scale\-in**: Select the nodes that do not need scale\-in. Options are as follows:<br><br>   * Node containing local storage pods.<br><br>   * Nodes containing pods that are not managed by DaemonSet in the kube\-system namespace.<br><br>* **Ignore DaemonSet resource usage when calculating node scale\-in threshold**: If this option is enabled, DaemonSet resource usage will be ignored when calculating node resource usage. |
   |Startup taints |Configure startup taints. If the specified taint exists on a node, the node is considered not fully initialized. |
   |Ignore the taint |Specify taints to be ignored. During scaling, the specified taint attributes of nodes and node pools are ignored. |
   |Node readiness wait timeout |Specify the maximum timeout (in minutes) for waiting for node readiness in the node scale\-in process. The value must be an integer from 1 to 60. |
   

5. Click **Confirm** to finish configuration.


<span id="9dA9bSDv"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="qX5aT3wJ"></span>
## Related documentation


* [Node scaling overview](https://docs.byteplus.com/en/docs/vke/How-Cluster-Autoscaler-works)

* [Configuring node autoscaling (Cluster AutoScaler)](https://docs.byteplus.com/en/docs/vke/Creating-a-Cluster-Autoscaler)
