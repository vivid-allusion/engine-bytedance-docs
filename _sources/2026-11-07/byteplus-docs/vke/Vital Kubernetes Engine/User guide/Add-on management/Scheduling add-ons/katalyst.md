---
title: "katalyst"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/katalyst-add-on"
---

The katalyst add\-on provides fine\-grained resource management capabilities. This topic describes how to deploy and use the katalyst add\-on in a cluster.

> **tip**

> This add\-on is currently in **public beta**.

## Add\-on overview

The katalyst is a Kubernetes resource management add\-on developed by BytePlus. Its name is derived from the word "Catalyst", which originally refers to a substance that accelerates chemical reactions. The add\-on is used to provide powerful resource management capabilities for workloads running on Kubernetes. The Katalyst is mainly used for topology\-aware scheduling and fine\-grained resource management. For example, it supports topology reporting in RDMA scenarios and core binding in NUMA\-aware scheduling.

After the add\-on is installed in a cluster, the system creates the following Kubernetes resources in the katalyst\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|katalyst\-agent |DaemonSet |Performs node\-level resource management and execution, including managing resource allocation policies for CPU, memory, devices, and network. It collects and reports node NUMA/RDMA topology, reclaimed resource information, and other data to support scheduler decisions. It also monitors CPU and memory resource pressure and dynamically calculates node resource headroom and overcommit ratios in real time. |
|katalyst\-controller |Deployment |Performs cluster\-level policy control and coordination, including autoscaler management, PodSLA policy and Katalyst Custom Config (KCC) dynamic configuration management, resource amplification policy and configuration management, admission webhooks, and more. |

> **tip**

> The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other add\-on\-related resources, such as ConfigMaps and Secrets, are not described here. Refer to the actual resources in the cluster.

## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/katalyst).

## Installing add\-ons

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Scheduling** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   |Parameter |Description |
   |---|---|
   |Feature switch |Select one or more resource management feature switches. Select at least one feature switch. Multiple feature switches can be selected.<br><br><br>* **NUMA\-aware scheduling**: Enable resource management capabilities for the NUMA\-aware scheduling and RDMA topology\-aware scheduling features. For more information about NUMA\-aware scheduling, see [NUMA-aware scheduling](https://docs.byteplus.com/en/docs/vke/NUMA-aware-scheduling) and [RDMA topology-aware scheduling](https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling).<br><br>   * **Resource management type**: The type of resource management for topology\-aware scheduling. Currently, only **CPU** resources are supported.<br><br>      > **warning**<br>      <br><br>      * > You can choose not to select **Resource management type**.<br>      <br><br>      * > After you select a **resource management type** and install the add\-on, you cannot modify the configuration.<br>      <br><br>* **IHPA**: Enable the IHPA resource management capability. For more information about IHPA, see [IHPA overview](https://docs.byteplus.com/en/docs/vke/Intelligent_Horizontal_Pod_Autoscaler_overview).<br><br>* **QoS\-aware Scheduling**: Enables fine\-grained resource management. Currently, two scheduling capabilities are supported:<br><br>   * **CPU Burst**: When a container's CPU usage is below its CPU limit, unused CPU time slices can accumulate. When a burst of CPU demand occurs, these accumulated time slices can be used to meet the demand, improving container performance. For CPU Burst usage details, see [CPU Burst](https://docs.byteplus.com/en/docs/vke/Using-pod-CPU-burst-capability).<br><br>   * **CPU QoS**: Provides multi\-tier CPU guarantees and dynamic isolation based on workload priority, ensuring that online workloads are not affected by offline workloads in online/offline Pod co\-location scenarios and improving overall cluster utilization. For CPU QoS usage details, see [CPU QoS](https://docs.byteplus.com/en/docs/vke/CPU_QoS).<br><br>* **Memory compression**: Enable memory resource optimization capability to automatically detect cold memory and compress it for storage. This does not affect business containers and improves memory resource utilization. For information about memory compression, see [Memory compression](https://docs.byteplus.com/en/docs/vke/memory-compression). |
   |Node amplification |After being enabled, it can improve node resource utilization by amplifying the allocatable resources of nodes. It is suitable for scenarios where the actual usage of Pods on the nodes is much smaller than the Request value. For instructions on using this feature, see [Amplifying nodes](https://docs.byteplus.com/en/docs/vke/Amplifying_nodes). |

## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays **Upgradable**, we recommend promptly upgrading it. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

## Monitoring and alerting

### Add\-on observability

The stability and performance of the katalyst add\-on directly affect the functionality and effectiveness of your cluster. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard mainly displays the resource usage and health of the katalyst add\-on, including CPU usage, memory usage, UP, and heartbeat metrics for each workload. You can specify a custom time range for querying information and set the information refresh mode to manual refresh or automatic refresh.

1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the dashboard list on the left side, choose **Resource management monitoring** \> **katalyst monitoring** to view the monitoring dashboard.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_683ca27d346bfe4fd57a023b2753cf02.png)

### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:

* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)

Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

## Related documentation

* [NUMA-aware scheduling](https://docs.byteplus.com/en/docs/vke/NUMA-aware-scheduling)

* [RDMA topology-aware scheduling](https://docs.byteplus.com/en/docs/vke/RDMA-topology-aware-scheduling)

* [How do I handle the impact of the katalyst add-on upgrade?](https://docs.byteplus.com/en/docs/vke/Handling_the_impact_after_Katalyst_add-on_upgrade)
