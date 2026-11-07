---
title: "fsxset-controller"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/fsxset-controller-add-on"
---

The fsxset\-controller is a scheduling add\-on provided by VKE to achieve fine\-grained O&M for the FSX client (fsx\-agent). This topic describes how to install and upgrade the fsxset\-controller add\-on and provides relevant considerations.

<span id="Dot3H8Vf"></span>
## Add\-on overview

The fsxset\-controller is an add\-on that manages fsx\-agent Pods across the entire lifecycle, including creation, deletion, and hot upgrade. It supports differentiated FSX client configurations for different nodes within the same cluster. This achieves requirements such as canary validation and hot upgrade of clients.

As a managed add\-on, this add\-on does not consume the computing resources of cluster nodes. After you install this add\-on in a cluster, the system will automatically create the following Kubernetes resources.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|fsxset |CRD |The custom resource settings of the FSX client. After the add\-on is installed, the system will automatically generate a default configuration named `default`. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="ZxaDUomQ"></span>
## Install the add\-on

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When you install the csi\-fsx add\-on, the system will automatically install the fsxset\-controller add\-on.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.


<span id="4FobbgVs"></span>
## Upgrade the add\-on

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="NTul7dYM"></span>
## Related documentation


* [Introduction to FSXSet resources](https://docs.byteplus.com/en/docs/vke/Introduction_to_FSXSet_resources)

* [Using FSXSet to implement client upgrades and differentiated configuration](https://docs.byteplus.com/en/docs/vke/Using_FSXSet_to_implement_differentiated_configurations_for_clients)


&nbsp;

&nbsp;
