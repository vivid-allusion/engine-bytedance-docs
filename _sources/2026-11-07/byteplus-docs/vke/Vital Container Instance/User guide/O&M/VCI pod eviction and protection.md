---
title: "VCI pod eviction and protection"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/VCI-pod-eviction-and-protection"
---

Pod eviction is normal behavior when workloads are running on Kubernetes. During some scheduled or unscheduled events in VCI, including but not limited to node upgrades, node failures, and node resource operations, pods may be evicted to ensure that the underlying nodes that you use remain healthy and to optimize node resource utilization. To ensure the availability of your application service, we provide a series of protection policies that you need to configure based on the characteristics of your own business.

<span id=".5Zy65pmv6K-05piO"></span>
## Scenario description

VCI may initiate eviction for business pods in scenarios including, but not limited to, the following scenarios:


* Node exception (NotReady): VCI business nodes are managed by the system. Users do not need to be aware of these nodes. However, business pods still need to be scheduled and run on them. When a node fails or is in the NotReady state, VCI will initiate node self\-healing. In this case, the pods on the node will be evicted.

* Node upgrade: When the kernel or other modules of a node are being upgraded, the node may need to be restarted. Before the node restarts, VCI will first evict all pods on the node.

* Resource scheduling and operations: To improve resource utilization, VCI performs operations and maintenance on resources at irregular intervals, during which some pods on the resources may be evicted to perform operations, such as resource fragment consolidation.


VCI categorizes the preceding eviction scenarios into the following two types:


* **Passive eviction in abnormal scenarios**: The scenarios include node failures. In such scenarios, VCI **does not** take extensive protective measures for pod evictions because exceptions have occurred and self\-healing is in progress.

* **Proactive eviction in normal scenarios**: The scenarios include node upgrades and resource scheduling. In such scenarios, VCI provides some protective policies for evictions because both pods and nodes are in a normal status.


<span id=".6amx6YCQ6Ziy5oqk6K-05piO"></span>
## Eviction protection description

<span id=".5bmy5omw6aKE566X5py65Yi2"></span>
### PDB

A Pod Disruption Budget (PDB) is an application\-level eviction protection policy provided by Kubernetes, which is used to ensure service availability at the workload layer during evictions. It applies to any workload type that supports [scale subresources](https://kubernetes.io/zh-cn/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/#scale-subresource), including native deployments or custom resource definitions (CRDs). For instructions on setting PDBs for pods, see the [official Kubernetes documentation](https://kubernetes.io/zh-cn/docs/tasks/run-application/configure-pdb/).

<span id=".dmNpLemYsuaKpOetlueVpQ=="></span>
### VCI protection policy

You can configure operational protection policies for VCIs based on the following descriptions:


* Cluster\-level configuration: Set the annotation key to `vci.volcengine.com/evict-min-available` in the vci\-profile file, with the value as a percentage (default value: 50%). This indicates the minimum number of available pods after eviction. For more operating instructions, see [Using VCIs by configuring vci-profile](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile).

* Application\-level configuration: Directly specify the minAvailable field in the Kubernetes PDB. For detailed operations, see the [official Kubernetes documentation](https://kubernetes.io/zh-cn/docs/tasks/run-application/configure-pdb/).


The preceding two protection policies can coexist in the same cluster and take effect simultaneously.

<span id=".5pyf5pyb6L-Q6KGM5pe26ZW_5L-d6Zqc"></span>
### Expected execution time guarantee

For some compute\-optimized tasks that cannot be interrupted, to ensure that such pods are not proactively evicted within a specified period of time, you can estimate the maximum execution time of the compute\-optimized tasks and set the expected execution time by adding the annotation key `vci.volcengine.com/evict-delay-time` to the pods, with the value as the specific duration in seconds. For example, if you add the annotation `vci.volcengine.com/evict-delay-time: 3600` to a pod, VCI will delay proactive eviction of the pod. Using `Pod.Status.StartTime` as the baseline, VCI ensures that the pod can only be proactively evicted after 3600 seconds (1 hour).

<span id=".6amx6YCQ6YCa55-l"></span>
## Eviction notification

VCI provides various policies to protect application availability during evictions. Except for unscheduled passive eviction scenarios, such as node failures, VCI only performs eviction operations based on the protection policies and expected execution time that you set by default, and pushes event notifications to your cluster through Kubernetes events a few minutes before eviction. Eviction notifications consist of the following three parts:


* Before proactive operation and maintenance is performed, an instance eviction notification will be sent to affected VCIs (pods). You can set the advanced notification time for this event by using the annotation: `vci.volcengine.com/evict-notification-time`. The event content specifies the specific time when the operation and maintenance will be performed:

   
   |level |reason |message |
   |---|---|---|
   |Warning |EvictNotification |The pod will be evicted by VCI after {second}, reason: {} |
   

* The content of the Kubernetes event related to instance eviction is as follows:

   
   |level |reason |message |
   |---|---|---|
   |Warning |Evicted |Pod has been evicted by VCI, reason: {} |
   

* If the protection policy does not allow eviction or eviction fails to be executed, the content of the Kubernetes event related to pod eviction cancellation is as follows:

   
   |level |reason |message |
   |---|---|---|
   |Warning |EvictCanceled |The pod evict by VCI is canceled, reason {} |
   


You can configure the corresponding alerting rule in the event center. For detailed operations, see [Event monitoring](https://docs.byteplus.com/en/docs/vke/Event-monitoring-overview).

<span id=".6YWN572u5L-h5oGv"></span>
## Configurations

The following table describes annotation configurations supported by the VCI operational protection policy and operational process policy. For multiple VCIs, you can perform global configuration through vci\-profile. For detailed operations, see [Using VCI by configuring vci-profile](https://docs.byteplus.com/en/docs/vke/Using-VCI-by-configuring-vci-profile).


|Parameter |default value |Meaning |
|---|---|---|
|vci.volcengine.com/evict\-min\-available |50% |The minimum proportion of available pods after eviction during proactive operation and maintenance. |
|vci.volcengine.com/evict\-notification\-time |600 |The lead time for eviction notifications during proactive operation and maintenance. Unit: seconds. |
|vci.volcengine.com/evict\-delay\-time |0 |The duration to delay the eviction execution during proactive operation and maintenance. Unit: seconds. |
