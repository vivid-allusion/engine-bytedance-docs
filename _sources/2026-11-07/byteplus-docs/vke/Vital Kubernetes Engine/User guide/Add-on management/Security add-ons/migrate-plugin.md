---
title: "migrate-plugin"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/migrate-plugin-add-on"
---

The migrate\-plugin add\-on is used to back up and restore application data in VKE clusters. This topic describes the functionality, core resources, and installation and upgrade instructions of this add\-on.

<span id="Ay7zGqPt"></span>
## Add\-on overview

The migrate\-plugin add\-on is used to back up and restore application data in VKE clusters. It can back up container application metadata and PV data to TOS and quickly restore data to a specified cluster based on backup data. This feature is applicable to scenarios such as disaster recovery for containerized applications, application migration from IDCs to the cloud, and cross\-cloud application migration.

After the add\-on is installed in a cluster, the system will create the following Kubernetes resources under the kube\-system namespace.


|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|node\-agent |DaemonSet |A node\-level add\-on for backing up and restoring PV data. It reads the PV data from nodes and uploads it to the backup repository. |
|migrate\-plugin |Deployment |The core control process of the add\-on. It is used to schedule and coordinate all backup and restoration tasks. |
|migrate\-plugin\-server |ClusterRole |The permission resources. When backup or restoration tasks fail due to insufficient permissions, you can check and add the permissions required by this ClusterRole. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. You should refer to the actual resources in the cluster.</div>


<span id="OllzeY5E"></span>
## Install the add\-on


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Addons**. On the page that appears, click the **Security** tab.

4. Move the pointer over the add\-on card and click **Deploy** to install the add\-on.

   
   |Parameter |Description |
   |---|---|
   |Pod scheduling based on taints and tolerations |Whether to enable taint\-based scheduling for the add\-on. After it is enabled, you can configure taint tolerations, allowing the core workloads of the add\-on to be scheduled to nodes with the specified taints. |
   

5. Click **Confirm** to finish configuration.


<span id="UQp7bZMr"></span>
## Upgrade the add\-on

New versions of the add\-on are released at irregular intervals to provide new features or fix known issues. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth service transition, perform the upgrade during off\-peak hours whenever possible. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

<span id="R4bXAbSU"></span>
## Related documentation


* [Backup center overview](https://docs.byteplus.com/en/docs/vke/Backup_center_overview)

* [Creating backup plans](https://docs.byteplus.com/en/docs/vke/Create_backup_plan)

* [Viewing backup jobs](https://docs.byteplus.com/en/docs/vke/View_backup_job)

* [Managing backup plans](https://docs.byteplus.com/en/docs/vke/Manage_backup_plans)

* [Creating restore jobs](https://docs.byteplus.com/en/docs/vke/Create_a_recovery_job)
