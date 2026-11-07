---
title: "snapshot-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/snapshot-controller-add-on"
---

The snapshot\-controller is a storage snapshot control add\-on. This topic describes its functionality, use cases, core resources, and how to install and upgrade it.

<span id="R2v3fDL0"></span>
## Add\-on overview

snapshot\-controller is a standard Kubernetes add\-on that introduces a series of CustomResourceDefinitions (CRDs) and enables users to manage snapshots of PersistentVolumes (PVs) through a declarative API. In short, it provides unified snapshot management logic for CSI\-compatible storage add\-ons.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|snapshot\-controller |Deployment |The core controller of the add\-on. It is responsible for monitoring and processing API objects related to storage snapshots. |
|VolumeSnapshot/VolumeSnapshotContent |CRD |User\-created snapshot requests, and objects that represent a specific snapshot instance in the storage system. |
|VolumeSnapshotClass |CRD |Defines a policy for creating a snapshot. For example, it describes the CSI driver to use and the snapshot reclaim policy. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="p9KTZjO4"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/snapshot-controller).

<span id="Lt7MfXNQ"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on a VCI with 2 vCPUs and 4 GiB specifications. This will incur extra fees. For a detailed description of fees, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Resource configuration |Specify the CPU requests, CPU limits, memory requests, and memory limits of various resources in the add\-on. |
   

5. Click **Confirm** to finish configuration.


<span id="tpwlSDhM"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="0KtyjhNO"></span>
## Monitoring and alerting

<span id="WHZ0e1st"></span>
### Add\-on observability

The stability and performance of the snapshot\-controller add\-on directly affect its functionality and effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [CSI Storage observability](https://docs.byteplus.com/en/docs/vke/CSI-storage-observability?lang=en).

After you enable add\-on observability, you can view the preset observability dashboard for the add\-on in the console. This dashboard primarily displays the real\-time load and end\-to\-end latency of snapshot operations handled by the snapshot\-controller add\-on. It includes sections such as overview, snapshot creation (CSI invocation phase), and end\-to\-end snapshot creation (including waiting for Ready). The dashboard covers metrics such as the number of concurrent snapshot operations, QPS, average/P90/P99 latency, and latency distribution comparison among different operation stages. You can specify a custom time range for querying information and set the information refresh mode to manual or automatic refresh.


1. In the left navigation pane of the cluster management page, click **Monitoring center** \> **Dashboard**.

2. In the left dashboard list, select **Storage service monitoring** \> **Snapshot Controller monitoring** to view the monitoring dashboard.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d1cb00b39969aae790f358c03947e65c.png) </span>


<span id="vJDGVwqt"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


Preset alert templates are provided by the system based on common O&M scenarios. They are applicable to building an alert system for the first time or quickly supplementing basic monitoring items. This helps you promptly detect insufficient resources or abnormal operation of add\-ons. For details about the alert rules in preset alert templates, see [Preset alert templates](https://docs.byteplus.com/en/docs/vke/Preset_alert_templates?lang=en).

<span id="GppCunch"></span>
## Related documentation


* [Using EBS snapshots](https://docs.byteplus.com/en/docs/vke/Using-EBS-volume-snapshots)

* [Using dynamic PersistentVolumes created from LVM-managed local storage](https://docs.byteplus.com/en/docs/vke/Using_LVM_type_for_dynamic_Local_Volumes)

* [Using dynamic PersistentVolumes created from dedicated local storage](https://docs.byteplus.com/en/docs/vke/Using_exclusive_type_for_dynamic_Local_Volumes)

* [Using LVM-managed local volumes as ephemeral volumes](https://docs.byteplus.com/en/docs/vke/Using_local_storage_LVM_through_the_temporary_volume)
