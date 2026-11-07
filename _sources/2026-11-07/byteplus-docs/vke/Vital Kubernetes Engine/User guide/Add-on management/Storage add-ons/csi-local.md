---
title: "csi-local"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-local-add-on"
---

The csi\-local add\-on is a local storage driver implemented based on the standard CSI specification. This topic describes how to install and upgrade the csi\-local add\-on and provides relevant considerations.

## Add\-on overview

csi\-local is a storage add\-on provided by VKE. It is used to mount local disks of cluster nodes to Pods in the form of LVM\-managed logical volumes or dedicated physical disks, delivering storage support for I/O\-intensive applications.

As a non\-managed add\-on, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-local\-controller |Deployment |The Pod for the local disk management controller. It monitors storage requirements (PVCs/PVs) within the cluster and completes dynamic provisioning and scheduling of local PersistentVolumes. |
|csi\-local\-agent |DaemonSet |The Pod for the local disk mount controller. It runs on each worker node in the cluster and is responsible for automatic discovery of local disks on nodes, management of LVM\-managed volume groups, and mounting of PVs. |

> **tip**

> The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.

## Install the add\-on

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Hover over the add\-on card and click **Deploy** to install the add\-on.

## Upgrade the add\-on

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

## Related documentation

* [Using dynamic PersistentVolumes created from LVM-managed local storage](https://docs.byteplus.com/en/docs/vke/Using_LVM_type_for_dynamic_Local_Volumes)

* [Using dynamic PersistentVolumes created from dedicated local storage](https://docs.byteplus.com/en/docs/vke/Using_exclusive_type_for_dynamic_Local_Volumes)

* [Using LVM-managed local volumes as ephemeral volumes](https://docs.byteplus.com/en/docs/vke/Using_local_storage_LVM_through_the_temporary_volume)
