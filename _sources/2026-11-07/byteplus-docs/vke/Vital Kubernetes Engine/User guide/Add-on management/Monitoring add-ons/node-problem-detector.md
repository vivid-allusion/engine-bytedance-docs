---
title: "node-problem-detector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/node-problem-detector-add-on"
---

The node\-problem\-detector (NPD) is a health monitoring add\-on for cluster nodes. It is used to monitor and report the abnormal status of nodes. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="mUhMMqTp"></span>
## Add\-on overview

NPD is a node health monitoring add\-on provided by VKE. Its core features are as follows:


1. **Node issue collection**: It continuously monitors various potential issues of nodes, such as hardware failures, kernel deadlocks, read\-only file systems, and unresponsive container runtimes.

2. **Abnormal status reporting**: It exposes the abnormal status of underlying nodes to the Kubernetes control plane. This provides a critical data source for automatic O&M and issue diagnosis. The reported information includes the following:  

   * **Node condition**: For serious permanent or long\-term failures (such as file system corruption), NPD will update node conditions, which may affect Pod scheduling decisions.

   * **Event**: For temporary or informational issues (such as kernel OOM), NPD will create Kubernetes events. This facilitates administrators in tracking issues, but usually does not directly affect scheduling.


After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|node\-problem\-detector |DaemonSet |The core workload of the add\-on. It is used for collecting and reporting exceptions on nodes. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="DERIseJ7"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/node-problem-detector).

<span id="G4Eyw3J3"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Monitoring** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Condition threshold configuration |Configure thresholds for GPU failure detection, including those for **Recoverable memory failure on GPU** and **Unrecoverable memory failure on GPU**. |
   |Resource configuration |Configure the resources of the node\-problem\-detector add\-on, including the CPU request, CPU limit, memory request, and memory limit. |
   |Addon configuration |Specify whether to disable the cloud assistant Agent health check. Cloud assistant Agent is required to perform node fault detection. After you disable this feature, some node diagnostics and node self\-healing features will become unavailable. For details, see [Node diagnosis](https://docs.byteplus.com/en/docs/vke/Node-diagnosis). |
   

5. Click **Confirm** to finish configuration.


<span id="kEkVeMts"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="c35gLKzh"></span>
## Monitoring and alerting

<span id="SL1yLmll"></span>
### Add\-on observability

The stability and performance of the node\-problem\-detector add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

<span id="I2GRqS9J"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="tcEjfekJ"></span>
## Related documentation


* [Configuring node check and auto-recovery](https://docs.byteplus.com/en/docs/vke/NodePool-health-check-and-auto-repair)

* [Custom node check items](https://docs.byteplus.com/en/docs/vke/Custom_Node_check_and_self-healing)
