---
title: "scheduler-plugin"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/scheduler-plugin-add-on"
---

scheduler\-plugin is an add\-on that extends cluster scheduling capabilities and policies of the native kube\-scheduler. This topic describes how to deploy and use the scheduler\-plugin in a cluster.

<span id="WamwcbCl"></span>
## Add\-on overview

scheduler\-plugin is a scheduler extension add\-on provided by VKE based on the native kube\-scheduler. It leverages the Kubernetes Scheduling Framework and supplements scheduling capabilities for scenarios (such as GPU, AI training, big data, and online\-offline hybrid deployment) in the form of an add\-on. This add\-on is the core enabler for the advanced scheduling features of VKE.

The typical usage scenarios of the scheduler\-plugin add\-on are as follows:


* GPU (mGPU) sharing for containers in the cluster.

* Online\-offline hybrid deployment or batch job scheduling that requires custom bin packing or spreading policies to meet business requirements.

* Collaboration with vci\-virtual\-kubelet to support Serverless containers and elastic resource burst scenarios.


scheduler\-plugin is a managed add\-on. By default, it deploys no Kubernetes resources in your cluster and consumes zero computing resources on cluster nodes.

<span id="LTxUYTMU"></span>
## Add\-on versions

This is a system\-managed add\-on. You do not need to manage its versions, upgrades, or O&M. VKE currently does not disclose historical release records of this add\-on.

<span id="DjnStOFj"></span>
## Installing add\-ons

The system\-managed add\-on is automatically installed with the default configuration during cluster creation. You can modify the add\-on configuration.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">After you configure the add\-on for the first time, you can modify some configurations of the add\-on in clusters running on the following Kubernetes versions.</div>


   * <div data-tips="true" data-tips-type="warning">v1.28 and later</div>


   * <div data-tips="true" data-tips-type="warning">v1.26.6\-vke.7 and later</div>


   * <div data-tips="true" data-tips-type="warning">v1.24.15\-vke.18 and later</div>


   * <div data-tips="true" data-tips-type="warning">v1.20.15\-vke.23 and later</div>


   <div data-tips="true" data-tips-type="warning">The editable configurations are subject to the console. If the Kubernetes version of your cluster does not meet your business requirements, upgrade the cluster control plane first. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Upgrading clusters</a>. For the release notes for Kubernetes versions supported by VKE, see <a href="https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes">Kubernetes version release notes</a>.   </div>
   

* <div data-tips="true" data-tips-type="warning">Managed add\-ons have the following characteristics:</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Non\-removable</strong>: As the foundation for cloud resource integration into clusters, this add\-on is locked as a core protected resource to prevent service network disruptions due to accidental deletion.</div>


   * <div data-tips="true" data-tips-type="warning"><strong>Fully managed maintenance</strong>: Updates, security patches and routine maintenance are ‌centrally and automatically managed by VKE.</div>


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card and click **Configuration** to update the add\-on configuration.

   
   |Parameter |Description |
   |---|---|
   |Node scheduling policy |Configure the binpack and spread scheduling policies of nodes.<br><br><br>* binpack: Multiple pods are preferentially scheduled onto the same node. Resource scores, such as those for CPUs, memory, GPU computing power, and GPU video memory, are comprehensively evaluated.<br><br>* spread: Multiple pods are scheduled across different nodes. Resource scores, such as those for CPUs, memory, GPU computing power, and GPU video memory, are comprehensively evaluated.<br><br><br>Click **Advanced settings** to configure the weights of node resources, including CPU, memory, GPU computing power, and GPU video memory. For detailed descriptions, see [Configuring scheduler custom parameters](https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters). |
   |Node affinity weight |Configure the scoring weight of native node affinity. The higher the score, the higher the priority of soft requirements or preferences when pod scheduling is controlled through node affinity.<br><br>This parameter can be specified only for the scheduler\-plugin add\-on of the following versions:<br><br><br>* The add\-on version is v1.0.8 or later. If the add\-on version does not meet your business requirements, [upgrade the add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).<br><br>* The Kubernetes version of the cluster where the add\-on is located needs to meet the following requirements:<br><br>   * v1.24.15\-vke.30 and later<br><br>   * v1.26.10\-vke.17 and later<br><br>   * v1.28.3\-vke.11 and later |
   |Topological scattering policy weight |Configure the scoring weight of the native PodTopologySpread scheduling policy. The higher the score, the higher the priority of topology scattering scheduling, and the greater the probability that the pod will be dispatched to the decentralized topology region. |
   |GPU card scheduling policy |Configure the binpack and spread scheduling policies of GPUs.<br><br><br>* binpack: Multiple pods preferentially use the same GPU.<br><br>* spread: Multiple pods use different GPUs.<br><br><br>If your workload has GPU Accelerated nodes and GPUs, see [Configuring scheduler custom parameters](https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters) for instructions on combining the **node scheduling policy** and **GPU card scheduling policy**. |
   |VCI inventory\-aware scheduling |Disabled by default. It improves the success rate of VCI pod creation by monitoring the quantity of remaining available resources for VCI of different types.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For the description of the VCI inventory\-aware scheduling feature, see <a href="https://docs.byteplus.com/en/docs/vke/VCI-inventory-aware-scheduling">VCI inventory\-aware scheduling</a>.</div><br> |
   |Gang scheduling |Disabled by default. Gang scheduling applies to the all\-or\-nothing scheduling scenario, in which either all pods are scheduled or no pods are scheduled if a group of pods are being scheduled at the same time.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about Gang scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/Gang-scheduling">Gang scheduling</a>.</div><br> |
   |Capacity scheduling |[[Beta - apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] This feature is disabled by default. After you enable this feature, multiple tenants share resources through flexible quotas. This improves overall resource utilization.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about capacity scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/Capacity-scheduling">Capacity scheduling</a>.</div><br> |
   |ResourcePolicy scheduling |This feature is disabled by default. After you enable this feature, click **Advanced configurations** to set the sequence in which workload pods are scheduled to different types of node resources. Pods are scaled in based on the reverse order of the original scheduling sequence.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For instructions on using ResourcePolicy scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling">ResourcePolicy scheduling</a>.</div><br> |
   |Load\-aware scheduling |Disabled by default. Load\-aware scheduling is performed based on the actual resource loads of nodes, which prevents application or node failures caused by excessive load on a single node.<br><br>After you enable this feature, specify scheduling\-related parameters based on your business requirements.<br><br><br>* **Effective scope**: Select the effective scope of load\-aware scheduling. The following two scopes are supported:<br><br>   * **Global**: All pods in the cluster use load\-aware scheduling by default.<br><br>   * **Specific pod**: Load\-aware scheduling is used only when the pod has the load\-aware scheduling annotation. For instructions on configuring load\-aware scheduling on a pod, see [Load-aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling).<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If load\-aware scheduling is enabled for the cluster for the first time, the feature globally takes effect by default.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <strong>Effective scope parameter</strong> can be specified only for clusters of the following Kubernetes versions:   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_26">Kubernetes v1.26</a>: v1.26.15\-vke.33 and later   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v-1_28">Kubernetes v1.28</a>: v1.28.15\-vke.26 and later   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><a href="https://docs.byteplus.com/en/docs/vke/VKE-for-Kubernetes-v1_30">Kubernetes v1.30</a>: v1.30.4\-vke.11 and later   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Other later <a href="https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes">Kubernetes versions</a> released by VKE   </div><br>   <br><br>   * **Advanced configurations**: The parameters of node resources for load\-aware scheduling. The following parameters can be specified:<br><br>   * **Node resource utilization threshold**: Specify the node CPU and memory utilization. Load\-aware scheduling filters nodes based on these values.<br><br>   * **Node scoring resource weight**: Specify the weight for different resources when the load\-aware scheduling add\-on scores nodes based on resource utilization. Valid values: 1 to 10. The higher the weight, the higher the score. |
   |Storage\-aware scheduling |[[Beta · apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] disabled by default. Load\-aware scheduling is performed based on the storage resources of nodes. You need to install the corresponding storage CSI add\-on to make this feature take effect. |
   |NUMA\-aware scheduling |[[Beta · apply for trial](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] disabled by default. NUMA\-aware scheduling provides the NUMA\-aware scheduling capability of central scheduler and stand\-alone cooperation to provide better performance for the load.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For instructions on using NUMA\-aware scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/NUMA-aware-scheduling">NUMA\-aware scheduling</a>.</div><br> |
   |RDMA topology\-aware scheduling |Disabled by default. Pods are scheduled according to RDMA NIC topology information, placing pods from the same Job on topologically adjacent NICs to optimize RDMA inter\-pod communication performance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This feature can be used only in clusters that use the VPC\-CNI network model.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For instructions on using RDMA topology\-aware scheduling, see <a href="https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling">RDMA topology\-aware scheduling</a>.</div><br> |
   

5. Click **Confirm** to finish configuration.


<span id="27reeOsP"></span>
## Upgrading add\-ons

You do not need to be concerned about upgrade issues for system\-managed add\-ons. System\-managed add\-ons prevent issues such as add\-on faults and unsatisfactory performance caused by users. It reduces user maintenance costs and enhances add\-on stability.

<span id="fKAG9Pq5"></span>
## Related documentation


* [ResourcePolicy scheduling](https://docs.byteplus.com/en/docs/vke/ResourcePolicy-scheduling)

* [Load-aware scheduling](https://docs.byteplus.com/en/docs/vke/Load-aware-scheduling)

* [NUMA-aware scheduling](https://docs.byteplus.com/en/docs/vke/NUMA-aware-scheduling)

* [RDMA topology-aware scheduling](https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling)

* [Configuring custom scheduling parameters](https://docs.byteplus.com/en/docs/vke/Configuring-scheduler-parameters)
