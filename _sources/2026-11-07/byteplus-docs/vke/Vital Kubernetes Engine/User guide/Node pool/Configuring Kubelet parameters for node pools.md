---
title: "Configuring Kubelet parameters for node pools"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring-kubelet-parameters-for-a-NodePool"
---

You can specify the Kubelet parameters to manage the behavior of nodes. VKE allows you to specify the Kubelet parameters of nodes in the console. This topic describes how to specify Kubelet parameters of nodes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">VKE allows you to specify only common Kubelet parameters in the console. For details, see the following content. If you need to specify other parameters, see <a href="https://docs.byteplus.com/en/docs/vke/Custom_cluster_kubelet_parameter">Custom cluster Kubelet parameters</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


* When you upgrade a cluster, the rules for changing and retaining Kubelet parameters are as follows:

   * Kubelet parameters configured through the method described in this topic will not change.

   * Feature Gate parameters incompatible with the target version may be cleaned up. For example, when you upgrade to v1.28 or later, the QoSResourceManager parameter will be automatically cleaned up.

* The default node pool does not support custom Kubelet parameters.

* After you specify Kubelet parameters for a node pool, if you choose to apply the specified parameters to existing nodes for which Kubelet parameters are already specified, the configurations of the same parameters will be overwritten by the node pool configurations.


<span id=".5pSv5oyB55qELWt1YmVsZXQt5Y-C5pWw"></span>
## Supported Kubelet parameters

You can specify the custom Kubelet parameters described in the following table.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Modifying <strong>topology\-manager\-policy</strong>, <strong>topology\-manager\-scope</strong>, and <strong>QoSResourceManager</strong> will restart Kubelet, and the resource allocation of pods will be recalculated based on the modified policy. In this case, running pods may restart or even fail to receive any resources. Proceed with caution.</div>



|Field |Default value |Description |
|---|---|---|
|cpu\-manager\-policy |none |The CPU manager policy. Valid values:<br><br><br>* **none**: The policy is the default policy.<br><br>* **static**: This policy allows pods with specific resource characteristics on the node to be granted enhanced CPU affinity and exclusivity. |
|eviction\-hard |* imagefs.available < 15%<br><br>* memory.available < 300Mi<br><br>* nodefs.available < 10%<br><br>* nodefs.inodesFree < 5% |A set of hard eviction thresholds that trigger pod eviction. For detailed parameter descriptions, see the[ official documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/). |
|fail\-swap\-on |true |Specifies whether kubelet can run when swap is enabled on the node. Valid values:<br><br><br>* **true**: Prevents kubelet from running when swap is enabled on the node. This is the default protection mechanism in Kubernetes. Swap can interfere with precise memory limit control. As a result, containers may use more memory than expected, affecting the accuracy of Pod scheduling and out\-of\-memory (OOM) detection.<br><br>* **false**: Allows kubelet to run when swap is enabled on the node. This option applies when strict memory isolation is not required or when Kubernetes must run on existing nodes with swap configured. |
|feature\-gates |\- |The feature gates, which are a set of key\-value pairs that describe Kubernetes features. For detailed descriptions, see the **Feature gate list** section of this topic.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The feature gate takes effect only in clusters of the following versions:</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.24.15\-vke.13 ≤ Cluster version < v1.26</div><br><br><br>* <div data-tips="true" data-tips-type="warning">v1.26.10\-vke.13 ≤ Cluster version < v1.28</div><br> |
|image\-gc\-high\-threshold\-percent |85 |The threshold for triggering image garbage collection. When disk utilization exceeds this value, garbage collection will be triggered. Unused images will be cleaned up to release disk space.<br><br><br>* The value is an integer. Valid values: 0 to 100.<br><br>* Unit: percentage.<br><br><br><div data-tips="true" data-tips-type="warning">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When specifying this parameter, make sure that <code>image-gc-low-threshold-percent</code> is less than <code>image-gc-high-threshold-percent</code>. Even if only one of the parameters is modified, the system validates it against the default value or the original configuration of the other parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can set this parameter to 100. However, this value triggers cleanup only when disk usage reaches 100%. This value is extremely conservative and not recommended in production environments.</div><br> |
|image\-gc\-low\-threshold\-percent |80 |The threshold for stopping Image garbage collection. During image garbage collection, collection stops when disk usage falls below this percentage.<br><br><br>* The value is an integer. Valid values: 0 to 100.<br><br>* Unit: percentage.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When specifying this parameter, make sure that <code>image-gc-low-threshold-percent</code> is less than <code>image-gc-high-threshold-percent</code>. Even if only one of the parameters is modified, the system validates it against the default value or the original configuration of the other parameter.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">You can set this parameter to 0. However, this value stops cleanup only after disk usage reaches 0%, which is almost impossible and has no practical value.</div><br> |
|image\-maximum\-gc\-age |0s |The maximum retention duration for unused images before they are garbage collected. Images that have remained unused for longer than this period will be cleaned up during the next garbage collection cycle.<br><br><br>* The value is a string. It supports time units, such as 30m and 168h.<br><br>* The default value is 0s, which indicates that images are not cleaned up based on time limits and are garbage collected only based on disk utilization (image\-gc\-high\-threshold\-percent).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">When this parameter is not set to 0s, it must be greater than <code>image-minimum-gc-age</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter is supported only in clusters running on Kubernetes v1.30 or later.</div><br> |
|image\-minimum\-gc\-age |2m |The minimum retention duration for unused images before they are garbage collected. During this time, the image will not be garbage collected even if disk utilization exceeds the garbage collection threshold.<br><br><br>* The value is a string. It supports time units, such as 2m and 30m.<br><br>* This parameter prevents a newly pulled image from being garbage collected immediately. This keeps the image available during the window between the pull and container startup.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Do not set a value that is too high. Otherwise, newly downloaded images that are not used in the short term cannot be cleaned up in time when disk space is tight. This potentially increases disk pressure.</div><br> |
|kube\-api\-burst |100 |The maximum burst requests sent to the API server per second.<br><br><br>* Enter an integer from 1 to 1000.<br><br>* The default value is 100.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value of this parameter must be greater than or equal to the value of the <code>kube-api-qps</code> parameter.</div><br> |
|kube\-api\-qps |50 |The number of QPS for communication with the API server. <br><br><br>* The value is an integer. Valid values: 1 to 500.<br><br>* The default value is 50. |
|kube\-reserved |For information about the system default resource reservation policies, see [Node resource reservation policies](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |The system reserved resources of Kubernetes. You can specify the amount of reserved CPU and memory resources. If `kube-reserved` is not specified, the system will use the default value to configure resource reservation. |
|system\-reserved |For information about the system default resource reservation policies, see [Node resource reservation policies](https://docs.byteplus.com/en/docs/vke/Node-resource-reservation-policies). |The system\-reserved resources of VKE. You can specify the amount of reserved CPU and memory resources. If `system-reserved` is not specified, the system will use the default value to configure resource reservation. |
|max\-pods |110 |The maximum number of pods supported by the node. |
|pod\-max\-pids |\-1 |This parameter limits the maximum number of process IDs (PIDs) that all containers in a single Pod can use. This prevents a single Pod from creating excess processes and exhausting the PID resources of the node.<br><br><br>* The value is an integer. Valid values: \-1 or a positive integer. Unit: count.<br><br>* When the value is set to \-1, it indicates that the number of PIDs that a single Pod can use is not limited.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">This configuration only limits the number of PIDs that a single Pod can use. The actual number of PIDs available to a Pod is also affected by the PID limit of the node kernel and the PID usage of other processes on the node.</div><br><br><br>* <div data-tips="true" data-tips-type="default">We do not recommend setting the value to \-1. We recommend setting the value based on the PID capacity of the node, the number of processes required by each Pod, and the number of Pods the node can run. This prevents a single Pod from exhausting the PID resources of the node. In addition, do not set a value that is too low. Otherwise, the Pod cannot create processes as expected.</div><br> |
|registry\-burst |10 |The maximum number of images concurrently pulled from CR. The value is an integer. Valid values: 1 to 100. The value must be greater than or equal to the value of the `registry-qps` parameter. |
|registry\-qps |5 |The QPS threshold for a cluster pulling images from Container Registry (CR). The value is an integer. Valid values: 1 to 50. |
|serialize\-image\-pulls |false |Specify whether to serially pull images. Valid values:<br><br><br>* **true**: Serially pull images.<br><br>* **false**: (Default) Pull images in parallel to accelerate pod startup. |
|topology\-manager\-policy |none |The topology management policy. Valid values:<br><br><br>* **none**: The topology management policy is disabled by default.<br><br>* **restricted**: Kubelet accepts only pods that achieve optimal non\-uniform memory access (NUMA) alignment on the requested resources.<br><br>* **best\-effort**: Kubelet preferentially selects pods that achieve NUMA alignment on CPU and device resources.<br><br>* **single\-numa\-node**: Kubelet allows only pods that are aligned to the same NUMA node in terms of CPU and device resources. |
|topology\-manager\-scope |container |The resource alignment granularity of the topology management policy. Set the value to **container**. |


**Feature gate list**


|Feature gate |Default value |Description |
|---|---|---|
|QoSResourceManager |false |Specify whether to enable quality of service (QoS) Resource Manager to support micro\-topology scheduling. Valid values:<br><br><br>* **true**: Enable QoS Resource Manager.<br><br>* **false**: (Default) Disable QoS Resource Manager. |


<span id=".6YWN572uLWt1YmVsZXQt6Ieq5a6a5LmJ5Y-C5pWw"></span>
## Specify custom Kubelet parameters

<span id=".5Yib5bu66ZuG576k5pe26YWN572u"></span>
### Specify parameters during cluster creation

You can specify custom Kubelet parameters when you create a cluster.

Specify custom Kubelet parameters in the **Advanced settings** section of the **Node pool configuration** step. For more configurations, see [Creating clusters](https://docs.byteplus.com/en/docs/vke/Creating-a-cluster).

<span id=".5Yib5bu66IqC54K55rGg5pe26YWN572u"></span>
### Specify parameters during node pool creation

You can create new node pools in the cluster and specify custom Kubelet parameters.

Specify custom Kubelet parameters in the **Advanced settings** section of the **Node pool configuration** step. For more configurations, see [Creating node pools](https://docs.byteplus.com/en/docs/vke/Creating-a-NodePool).

<span id=".6YWN572u5a2Y6YeP6IqC54K55rGg"></span>
### Specify custom Kubelet parameters of existing node pools

You can specify custom Kubelet parameters for existing node pools in the cluster.

On the **Node pool** page, ****find the target node pool and click `...` \> **Kubelet configs** in the Actions column to specify custom Kubelet parameters. For more configurations, see [Managing node pools](https://docs.byteplus.com/en/docs/vke/Managing-NodePools).

<span id=".5a2Y6YeP6IqC54K55Y-C5pWw5ZCM5q2l"></span>
### Apply the new configurations to existing nodes

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When you add custom Kubelet parameters to an existing node pool, the configurations only take effect on new nodes and do not apply to existing nodes by default. If you need the configurations to take effect on existing nodes, you need to perform the operations described in this section.</div>


* <div data-tips="true" data-tips-type="tip">When you apply custom Kubelet parameters to existing nodes for which Kubelet parameters are already specified, the configurations of the same parameters will be overwritten by the node pool configurations.</div>


1. On the **Node pool** page, click the name of the target node pool to go to the node pool details page.

2. Click the **Kubelet configs** tab and click **Existing node config synchronization**. Custom parameters will be synchronized to existing nodes after a secondary confirmation.

3. After parameters are synchronized, you can view the result and details of the synchronization task in the **Job log list** section.


<span id=".5p-l55yLLWt1YmVsZXQt6Ieq5a6a5LmJ5Y-C5pWw"></span>
## View custom Kubelet parameters


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar of the cluster management page, click **Nodes** \> **Node pool**.

4. Click the name of the target node pool. On the page that appears, click the **Kubelet configs** tab to view the Kubelet parameter configurations for the node pool.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click <strong>Edit</strong> to update the Kubelet parameters for the node pool.   </div>
