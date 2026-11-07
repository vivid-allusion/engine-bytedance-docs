---
title: "Snapshot overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Snapshot-overview"
---

Vital Kubernetes Engine (VKE) provides snapshot support. Snapshots help back up and restore application data and meet various data disaster recovery requirements.

<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits

Currently, only Elastic Block Storage (EBS) supports snapshots.

<span id=".5Yqf6IO96K-05piO"></span>
## Feature description

EBS itself provides a data backup (snapshot) and restore mechanism. However, this mechanism needs to be integrated with Kubernetes and flexibly used within applications in order to maximize its benefits.

VKE provides the following resources through the CustomResourceDefinition (CRD) objects in Kubernetes.


|Resource name |Description |
|---|---|
|VolumeSnapshotClass |Defines a snapshot class that describes the parameters and controller used to create snapshots. It is similar to the StorageClass resource in Kubernetes. |
|VolumeSnapshotContent |Snapshot instances of back\-end storage. These instances are created and maintained by the system administrator and do not belong to a namespace. It is similar to the PersistentVolume (PV) resource in Kubernetes. |
|VolumeSnapshot |Declares a snapshot instance that is created and maintained by the user and belongs to a specific namespace. It is similar to the PersistentVolumeClaim (PVC) resource in Kubernetes. |


The EBS snapshot resources follow the binding rules below:


* VolumeSnapshotContent and VolumeSnapshot have a one\-to\-one binding relationship.

* When using the snapshot feature, you need to bind a VolumeSnapshot to a VolumeSnapshotContent.

* Clusters support dynamic and static creation of a VolumeSnapshotContent:

   * Dynamic creation. After creating a VolumeSnapshotClass, create a VolumeSnapshotContent resource and correctly configure its VolumeSnapshotClassName field. The cluster will then automatically create a VolumeSnapshot.

   * Static creation. Manually create a VolumeSnapshotContent and bind it to a VolumeSnapshot.


<span id=".5L2_55So5Zy65pmv"></span>
## Application scenarios

The cloud disk snapshot feature is applicable to the following scenarios:


* Daily data backup

   By regularly creating snapshots of cloud disks, you can implement daily data backup to handle data loss or inconsistency caused by misoperations, viruses, attacks, or other issues.

* Rapid data recovery

   Before major operations such as upgrading application software, replacing operating systems, or migrating business data, you can use the cloud disk snapshot feature to create one or more snapshots. If any issue occurs during the upgrade or migration, you can promptly restore your business to the state when the snapshot was created.

* Rapid deployment of multiple applications

   You can use the same snapshot to quickly create multiple cloud disks with identical data. This allows you to provide data resources for multiple applications simultaneously.
