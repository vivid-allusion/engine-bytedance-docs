---
title: "Configuring control plane parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_control_plane_parameters"
---

VKE supports managing and configuring custom parameters of core Kubernetes components within clusters. This topic describes how to view and configure custom parameters for components, including kube\-apiserver, kube\-controller\-manager, and kube\-scheduler, by using the console.

<span id="kJFsRTmS"></span>
## Considerations


* Modifying the control plane parameter settings will cause a cluster restart. Thoroughly assess the business impact before proceeding.

* Configurable control plane parameters vary across Kubernetes versions in VKE clusters. Refer to the actual console interface for available options.


<span id="tUB8hmId"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. In the right part of the page, click the target cluster name to go to its management page.

3. In the left navigation pane of the cluster management page, select **Overview**. On the **Overview** page, click the **Control plane parameter configuration** tab to view and manage custom parameters of core Kubernetes components in the cluster.

   You can click the edit icon next to a specific control plane component to update its parameter settings. Descriptions for each component's parameters are provided below. For parameters without value instructions provided below, configure them according to the requirements indicated in the web interface.

   
   <Tabs>
   <Tab zoneid="TqxovWUIV0" title="Kube-apiserver parameter configuration">
   <TabTitle>Kube-apiserver parameter configuration</TabTitle>
   
   Custom kube\-apiserver parameters are described below.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |AdmissionPlugins |Additional admission control plugins enabled for kube\-apiserver. The following admission control plugins are currently supported:<br><br><br>* **AlwaysPullImages**: When this option is enabled, image repulling is forced on every Pod modification.<br><br>* **PodNodeSelector**: When it is enabled, ‌a node selector is added to all Pods in the namespace, restricting scheduling to nodes with specific labels.<br><br>* **PodTolerationRestriction**: When this option is enabled, Pod tolerations within the namespace are centrally managed to prevent abuse of high\-privilege taints. |
   |RequestTimeout |The request timeout duration for kube\-apiserver. This parameter determines the maximum time API requests remain open on the server side. |
   |DefaultNotReadyTolerationSeconds |Default toleration duration for Pods toward **NotReady** nodes. This parameter affects the default toleration behavior of Pods toward NotReady nodes. |
   |DefaultUnreachableTolerationSeconds |Default toleration duration for Pods toward the node status **Unreachable**. This parameter affects the default toleration behavior of Pods when the node controller cannot access a node. |
   |FeatureGates |Kubernetes feature gates for kube\-apiserver. The supported feature gates are as follows:<br><br><br>* **SidecarContainers**: Whether to enable the SidecarContainers feature gate to support native sidecar containers. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only by the following VKE cluster versions:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.30 ≤ cluster version ≤ v1.32   </div><br>   <br><br>* **StatefulSetAutoDeletePVC**: Whether to enable the StatefulSetAutoDeletePVC feature gate to support automatic deletion of PVCs by StatefulSets. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only by the following VKE cluster versions:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.28 ≤ Cluster version ≤ v1.30   </div><br>   <br><br>* **InPlacePodVerticalScaling**: Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only in VKE clusters running Kubernetes v1.34.   </div><br>   <br><br>* **MaxUnavailableStatefulSet**: Whether to enable the MaxUnavailableStatefulSet feature gate to support adding the `maxUnavailable` configuration for StatefulSet rolling updates. This configuration allows multiple Pods to be unavailable during an update. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only by the following VKE cluster versions:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Cluster version ≥ v1.36   </div><br>    |
   
   
   
   </Tab>
   <Tab zoneid="OQL4BxwQrz" title="Kube-controller-manager parameter configuration">
   <TabTitle>Kube-controller-manager parameter configuration</TabTitle>
   
   Custom kube\-controller\-manager parameters are described below.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |KubeApiQps |QPS limit for kube\-controller\-manager accessing the API Server. This parameter affects the request rate for the controller to access the API Server. |
   |KubeApiBurst |The maximum burst request limit for kube\-controller\-manager access to the API Server. This parameter is usually used together with **KubeApiQps**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value of <strong>KubeApiBurst</strong> must be greater than or equal to the value of <strong>KubeApiQps</strong>.</div><br> |
   |NodeMonitorGracePeriod |Duration before marking disconnected nodes as **NotReady** or **Unknown**. |
   |NodeEvictionRate |The Pod eviction rate in node failure scenarios. When the availability zone is healthy, this parameter controls the number of nodes from which Pods are evicted per second. For example, a value of 0.1 means that 0.1 nodes per second (namely, 1 node every 10 seconds) are selected for pod eviction. |
   |SecondaryNodeEvictionRate |The secondary node draining rate during large\-scale failures. This parameter specifies the number of nodes from which Pods are evicted per second when the availability zone is deemed “unhealthy” (for example, when the failure ratio exceeds the configured `UnhealthyZoneThreshold`) and nodes fail. For example, a value of 0.01 means that 0.01 nodes per second (namely, 1 node every 100 seconds) are selected for pod eviction. |
   |UnhealthyZoneThreshold |The unhealthy threshold for availability zones. When the proportion of nodes in the NotReady state within the same availability zone exceeds this threshold, the control plane determines that the availability zone has experienced an infrastructure\-wide failure and triggers a zone\-level rate\-limited eviction policy. |
   |LargeClusterSizeThreshold |The large cluster size threshold. The node controller uses this threshold to determine whether the cluster is a large\-scale cluster, which determines the Pod eviction policy. |
   |TerminatedPodGCThreshold |The garbage collection threshold for terminated Pods (namely, the maximum number of terminated Pods that can be retained). |
   |ConcurrentTTLAfterFinishedSyncs |The number of concurrent synchronization goroutines of the TTLAfterFinished controller that is responsible for cleaning up expired Jobs. |
   |HorizontalPodAutoscalerTolerance |When Horizontal Pod Autoscaler (HPA) is used, if the deviation between the actual metric and the desired metric is less than this tolerance rate, scaling will not be triggered. |
   |HorizontalPodAutoscalerSyncPeriod |The period for the HPA to synchronize the number of Pods. |
   |ConcurrentHorizontalPodAutoscalerSyncs |The number of HPA objects that can be concurrently synchronized. A larger value results in faster processing response for HPA objects, but consumes more CPU and network resources.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This parameter is supported only in clusters running on Kubernetes v1.26 or later.</div><br> |
   |FeatureGates |Kubernetes feature gates for kube\-controller\-manager. The supported feature gates are as follows:<br><br><br>* **StatefulSetAutoDeletePVC**: Whether to enable the StatefulSetAutoDeletePVC feature gate to support automatic deletion of PVCs by StatefulSets. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only by the following VKE cluster versions:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.28 ≤ Cluster version ≤ v1.30   </div><br>   <br><br>* **InPlacePodVerticalScaling**: Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only in VKE clusters running Kubernetes v1.34.   </div><br>   <br><br>* **MaxUnavailableStatefulSet**: Whether to enable the MaxUnavailableStatefulSet feature gate to support adding the `maxUnavailable` configuration for StatefulSet rolling updates. This configuration allows multiple Pods to be unavailable during an update. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only by the following VKE cluster versions:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Cluster version ≥ v1.36   </div><br>    |
   
   
   
   </Tab>
   <Tab zoneid="abJSkwIhUt" title="Kube-Scheduler parameter configuration">
   <TabTitle>Kube-Scheduler parameter configuration</TabTitle>
   
   Custom kube\-scheduler parameters are described below.
   
   
   |**Parameter** |**Description** |
   |---|---|
   |KubeApiQps |QPS limit for kube\-scheduler accessing the API Server. This parameter affects the request rate for the controller to access the API Server. |
   |KubeApiBurst |The maximum burst request limit for kube\-scheduler access to the API Server. This parameter is usually used together with **KubeApiQps**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The value of <strong>KubeApiBurst</strong> must be greater than or equal to the value of <strong>KubeApiQps</strong>.</div><br> |
   |Parallelism |The number of Goroutines (Golang coroutines) that kube\-scheduler executes concurrently when running scheduling algorithms. This parameter affects the scheduler's capacity to process scheduling tasks simultaneously. |
   |PercentageOfNodesToScore |The proportion of nodes that can run Pods evaluated when Pods are being scheduled. Filtering stops after the specified proportion is reached. |
   |PodInitialBackoffSeconds |The initial scheduling backoff duration for Pods. This parameter affects the retry interval after a Pod scheduling failure. |
   |PodMaxBackoffSeconds |The maximum backoff delay for rescheduling pods in seconds. After a pod fails to be scheduled, the pod cannot be rescheduled until the delay ends. |
   |FeatureGates |Kubernetes feature gate for kube\-scheduler. The supported feature gates are as follows:<br><br><br>* **SidecarContainers**: Whether to enable the SidecarContainers feature gate to support native sidecar containers. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only by the following VKE cluster versions:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">v1.30 ≤ cluster version ≤ v1.32   </div><br>   <br><br>* **InPlacePodVerticalScaling**: Whether to enable the InPlacePodVerticalScaling feature gate, which supports in\-place vertical scaling for Pods. Valid values:<br><br>   * **true**: Enabled.<br><br>   * **false**: Disable.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">This feature gate is supported only in VKE clusters running Kubernetes v1.34.   </div><br>    |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id="BATxmhmO"></span>
## Subsequent operations

After the configuration is complete, we recommend checking whether critical workloads are functioning normally and monitoring node status, Pod scheduling status, HPA behavior, and Kubernetes events. If parameter adjustments affect business operations, revert the parameters to the default values shown in the parameter configuration interface. If recovery fails, contact your ‌BytePlus account manager or ‌[submit a ticket](https://console.byteplus.com/workorder/create?step=1) for technical support.

<span id="hfsE06vg"></span>
## Related documentation

[UpdateClusterConfig](https://docs.volcengine.com/docs/6460/115189)
