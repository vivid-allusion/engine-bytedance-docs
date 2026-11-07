---
title: "rdma-device-plugin"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/rdma-device-plugin-add-on"
---

The rdma\-device\-plugin add\-on enables ‌discovery, allocation, and management of Remote Direct Memory Access (RDMA)‌ NICs in container clusters. This topic describes how to install and upgrade the rdma\-device\-plugin add\-on and lists related considerations.

<span id="CrV7t0gD"></span>
## Add\-on overview

The rdma\-device\-plugin is provided by VKE for high\-throughput scenarios, such as high\-performance computing (HPC), AI training, and AI inference. It adheres to the Kubernetes Device Plugin framework. This add\-on discovers underlying physical RDMA NICs on nodes and reports them to the cluster as extended resources. With this add\-on, Pods can directly request and mount RDMA hardware devices to achieve ultra\-low\-latency and ultra\-high\-bandwidth communication by bypassing the kernel network stack and performing direct memory read/write operations.

This is an unmanaged add\-on that needs to run on your cluster nodes to detect and manage underlying hardware devices. After the add\-on is installed, the following Kubernetes resources will be automatically created and started in your cluster.


|**Add\-on container** |**Resource type** |**Description** |
|---|---|---|
|rdma\-device\-plugin |DaemonSet |The core workload of the add\-on. It is responsible for discovering physical RDMA NICs on the local node and reporting the remaining available resource quota to kubelet. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="yeAckDKP"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/rdma-device-plugin).

<span id="MKqCJHJO"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Network** tab.

4. Hover over the add\-on card and click **Deploy** to install the add\-on.


<span id="e5FLkSQ7"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="ltbxMWQq"></span>
## Monitoring and alerting

<span id="COJaLQGd"></span>
### Add\-on observability

The stability and performance of the rdma\-device\-plugin add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability?lang=en).

<span id="W8O6Whu0"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="7Jr9E1Ls"></span>
## Related documentation


* [Using RDMA resources (RoCE) in clusters](https://docs.byteplus.com/en/docs/vke/Using-RDMA-resources-in-VKE-clusters)

* [Using RDMA resources (InfiniBand) in clusters](https://docs.byteplus.com/en/docs/vke/Using_RDMA_resources_in_VKE_clusters_InfiniBand)

* [AI resource observability](https://docs.byteplus.com/en/docs/vke/AI-resource-observability)
