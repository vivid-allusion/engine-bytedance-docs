---
title: "csi-cloudfs"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/csi-cloudfs-add-on"
---

The csi\-cloudfs add\-on is a CloudFS driver implemented based on the CSI specification. This topic describes how to install and upgrade the csi\-cloudfs add\-on and provides relevant considerations.

> **tip**

> [[**Beta \- apply for trial**](https://docs.byteplus.com/en/docs/vke/How-do-I-apply-for-beta-features)] To use this add\-on, submit an application.

## Add\-on overview

csi\-cloudfs is a storage add\-on provided by VKE for mounting CloudFS to Pods in clusters. This add\-on enables your application to efficiently access large amounts of data and is ideal for scenarios such as data lakes and AI training acceleration.

As a ‌non\-managed component‌, it runs on your cluster nodes and consumes a small amount of node\-level compute resources. After the add\-on is installed, the following Kubernetes resources will be automatically created in the kube\-system namespace.

|Resource name |**Resource type** |**Resource description** |
|---|---|---|
|csi\-cloudfs\-controller |Deployment |The Pod for the CloudFS management controller. It is responsible for monitoring storage requirements (PVCs/PVs) within the cluster and interacting with CloudFS to manage PVs. |
|csi\-cloudfs\-node |DaemonSet |The Pod for the CloudFS mount controller. It runs on each worker node in the cluster and is responsible for executing specific mount actions on the node side to mount storage as a filesystem available to containers. |

> **tip**

> The preceding table only lists the main resources of the add\-on, as well as resources that may be used when the add\-on or the corresponding feature is configured. This helps you understand the main components of this add\-on. Other resources, such as ConfigMap and Secret, related to the add\-on are not described here. The actual resources in the cluster shall prevail.

## Add\-on versions

For information about the historical release records of the add\-on, as well as new features and optimization descriptions for each version, see [Add-on release records](https://docs.byteplus.com/en/docs/vke/csi-cloudfs).

## Installing add\-ons

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. In the right part of the page, click the target cluster name to open the management page of this cluster.

3. In the left navigation pane, select **Addons** and click the **Storage** tab.

4. Hover over the add\-on card and click **Deploy** to install the add\-on.

## Upgrading add\-ons

The add\-on is released in new versions at irregular intervals to provide new features or fix known bugs. When the add\-on card displays that a new version is available, we recommend upgrading the add\-on promptly. To ensure a smooth business transition, we recommend upgrading the add\-on during business off\-peak hours. For upgrade procedures and considerations, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

## Related documentation

[Using static CloudFS PVs](https://docs.byteplus.com/en/docs/vke/Using-static-CFS-Volumes)
