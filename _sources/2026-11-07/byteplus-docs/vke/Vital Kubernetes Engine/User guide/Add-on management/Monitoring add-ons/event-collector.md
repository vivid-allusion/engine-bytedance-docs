---
title: "event-collector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/event-collector-add-on"
---

The event\-collector is a cluster event collection add\-on that collects cluster events and sends them to TLS. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="Yc56v6wY"></span>
## Add\-on overview

Kubernetes events record status changes within clusters, such as Pod creation, image pull failures, and node exceptions. They can provide you with important clues for cluster diagnosis and troubleshooting. However, native events are saved in memory only for a short period by default. This does not meet the requirements for long\-term tracing and analysis. To address the preceding issues, VKE provides the event\-collector add\-on. It collects various native events generated in clusters (events at the Normal and Warning levels) and sends event information to TLS. This ensures event persistence and provides a unified data source for subsequent event retrieval and statistics.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|event\-collector |Deployment |The core collector of the add\-on. It obtains global events by listening to the cluster APIServer. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="Bn7Er7nO"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/event-collector).

<span id="vvdarCd2"></span>
## Installing add\-ons


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to open the management page of this cluster.

3. In the left navigation bar of the cluster management page, click **Addons**. On the page that appears, click the **Monitoring** tab.

4. Move the pointer over the add\-on card, click **Deploy**, and specify the related parameters for the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   |Project |Select the project to which the TLS belongs. By default, the **default** project is selected. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Log project |Select an existing log project. |
   |Log topic |Select an existing log topic in the log project. |
   |Pod scheduling based on taints and tolerations |After you enable this feature, you can set taint toleration values. The core workloads of the add\-on can be scheduled onto nodes with specified taints. |
   |Node Label Selector |After you enable this feature, you can specify node labels, and the core workloads of the add\-on will be scheduled onto nodes with the specified labels. |
   

5. Click **Confirm** to finish configuration.


<span id="mk5k0PJG"></span>
## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="bC6rq67q"></span>
## Related documentation

[Configuring and viewing persistent events](https://docs.byteplus.com/en/docs/vke/Configuring-and-viewing-persistent-events)
