---
title: "csi-vepfs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-vepfs-add-on"
---

The csi\-vepfs add\-on is a vePFS driver implemented based on the CSI specification. This topic describes how to install and upgrade the csi\-vepfs add\-on and provides relevant considerations.

<span id="dWiTrG2Y"></span>
## Add\-on overview

csi\-vepfs is a storage add\-on provided by VKE for mounting vePFS to Pods in clusters. This add\-on delivers ‌ultra\-high throughput and ultra\-low latency‌ shared filesystem access for scenarios such as high\-performance computing (HPC) and large\-scale AI model training.

As a ‌non\-managed component‌, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-vepfs\-controller |Deployment |The Pod for the vePFS management controller. It is responsible for monitoring storage requirements (PVCs/PVs) within the cluster and interacting with vePFS to maintain node consistency after storage mounting in the cluster. |
|csi\-vepfs\-node |DaemonSet |The Pod for the vePFS mount service. It runs on each worker node in the cluster and is responsible for executing specific mount actions on the node side to mount storage as a filesystem available to containers. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="gOAcUt1r"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/csi-vepfs).

<span id="pD5s1T7a"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and configure the add\-on parameters.

   
   |Parameter |Description |
   |---|---|
   |Node Label Selector |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   |Pod scheduling based on taints and tolerations |This parameter can be specified only when the **Deployment form** parameter is set to **Elastic Compute Service deployment**. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   |Node Resource configuration |Specify the CPU requests, CPU limits, memory requests, and memory limits of various resources in the add\-on. |
   

5. Click **Confirm** to finish configuration.


<span id="uJCcBaxP"></span>
## Upgrading add\-ons

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="3IQGJNHk"></span>
## Monitoring and alerting

<span id="wuB0RSan"></span>
### Add\-on observability

The stability and performance of the csi\-vepfs add\-on directly affect its proper functioning and overall effectiveness. We recommend enabling add\-on observability in your cluster to monitor add\-on health in real time. For details, see [VKE observability](https://docs.byteplus.com/en/docs/vke/VKE-observability?lang=en).

<span id="tj6u1Sp1"></span>
### Configuring alerts

VKE provides comprehensive cluster monitoring and alerting capabilities based on [VMP](https://docs.byteplus.com/en/docs/vmp/what-is-vital-managed-service-for-prometheus). You can quickly create alert rule groups by using system preset templates or configure custom alert rules by using PromQL statements based on your business requirements. You can also export preset templates in YAML format, adjust the rules, and save them as custom alert templates for reuse across multiple clusters. For details, see the following topics:


* [Configuring alerts through preset templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts)

* [Configuring alerts based on custom templates](https://docs.byteplus.com/en/docs/vke/Configuring_alerts_based_on_custom_templates?lang=en)

* [Configuring alerts through custom alert rules](https://docs.byteplus.com/en/docs/vke/Configure_custom_alert_rules?lang=en)


<span id="mD6qTDDP"></span>
## Related documentation


* [Using static vePFS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-PFS-volumes)

* [Using dynamic vePFS PVs](https://docs.byteplus.com/en/docs/vke/Using-dynamic-PFS-volumes)


&nbsp;
