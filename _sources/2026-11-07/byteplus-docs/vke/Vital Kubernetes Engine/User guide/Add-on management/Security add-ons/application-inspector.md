---
title: "application-inspector"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/application-inspector-add-on"
---

application\-inspector is an intelligent diagnosis and health inspection add\-on for containerized applications. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="IrNMhwHy"></span>
## Add\-on overview

application\-inspector is an application inspection add\-on for VKE clusters. It provides application security inspection capabilities based on industry\-recognized security requirements and container security best practices. Application inspection can promptly detect and block unsafe configurations and prompt you to fix these issues to prevent applications from being attacked or exploited. This helps ensure application security and stability.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|application\-inspector |Deployment |The core workload of the add\-on. It receives, executes, and completes inspection instructions. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="NDB4nzKq"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/application-inspector).

<span id="f9R9bhKz"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Security** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Deployment method |The deployment method of the add\-on. This parameter is fixed and cannot be modified. |
   |Deployment mode |This parameter is displayed only for clusters for which the vci\-virtual\-kubelet add\-on is installed. You can deploy the add\-on on the following two types of nodes.<br><br><br>* **Elastic Compute Service deployment**: Deploys the add\-on on ECS nodes in the cluster.<br><br>* **Vital Container Instance deployment**: Deploys the add\-on on VCIs, which are the virtual nodes in the cluster. Fees will be incurred if you deploy the add\-on on VCI. For detailed fee descriptions, see [VCI service billing](https://docs.byteplus.com/en/docs/vke/VCI-billing-overview). |
   

5. Click **Confirm** to finish configuration.


<span id="nmvDzKsw"></span>
## Upgrade the add\-on

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="CYNkys8p"></span>
## Related documentation


* [Application inspection](https://docs.byteplus.com/en/docs/vke/Application-inspection)
