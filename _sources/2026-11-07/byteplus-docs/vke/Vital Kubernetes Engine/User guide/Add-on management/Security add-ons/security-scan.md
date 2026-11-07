---
title: "security-scan"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/security-scan-add-on"
---

security\-scan is a fundamental security protection add\-on in VKE clusters. This topic describes the functionality, core resources, and installation and upgrade methods of this add\-on.

<span id="Jp49fwtv"></span>
## Add\-on overview

security\-scan is a baseline inspection add\-on that performs ‌inspections on worker nodes in Kubernetes clusters according to industry\-recognized security standards. It provides security inspection for cluster nodes, enabling timely detection of insecure configurations in cluster nodes and advising users to remediate them to prevent exploitation by attacks. This helps ensure stability and security of applications.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|security\-scan |Deployment |The core workload of the add\-on. It receives, executes, and completes basic inspection instructions. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.</div>


<span id="ASja1e68"></span>
## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/security-scan).

<span id="FLgAEBSG"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Security** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.


<span id="5RaRThp7"></span>
## Upgrade the add\-on

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="PJTpbnHa"></span>
## Related documentation


* [Baseline inspection](https://docs.byteplus.com/en/docs/vke/Baseline-inspection)
