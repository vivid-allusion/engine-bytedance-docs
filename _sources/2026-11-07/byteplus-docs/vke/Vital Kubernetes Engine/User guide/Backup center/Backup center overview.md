---
title: "Backup center overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Backup_center_overview"
---

The VKE backup center allows container application metadata and PersistentVolume data to be backed up to TOS, and supports one\-click restore to a specified cluster based on backup data. This feature is applicable to scenarios such as disaster recovery for containerized applications, application migration from IDCs to the cloud, and cross\-cloud application migration.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">[Public beta]: The backup center is currently in public beta.</div>


<span id="jH8koKGL"></span>
## How it works

The backup center is based on Velero to implement application backup and restore in clusters, with backup data securely stored in TOS buckets. For more details, see the [Velero documentation](https://velero.io/docs/v1.10/how-velero-works/).

Unlike other tools that directly access the Kubernetes etcd database for backup and restore, Velero uses the Kubernetes API to capture the status of cluster resources and restore them when necessary. This API\-driven approach offers the following key advantages:


* Backups can capture a subset of cluster resources, which can be filtered by namespace, resource type, and/or label selector, providing a high degree of flexibility in what is backed up and restored.

* No direct access to etcd is required for backup or restore, which addresses scenarios where users of managed Kubernetes cannot access etcd directly.

* Resources exposed via the Aggregated API Server can be easily backed up and restored, even if they are stored in a separate etcd database.


<span id="LcG5Man0"></span>
## Core resources

<span id="KzjX9Ck9"></span>
### Backup repositories

VKE allows you to add  TOS to the backup center as backup repositories for storing and managing backups.

<span id="u51Es527"></span>
### Backup/Restore target clusters

All VKE clusters, such as managed clusters and registered clusters, can serve as backup/restore target clusters.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The recommended Kubernetes version range for backup/restore target clusters is v1.24.x to v1.32.x.</div>


<span id="HAUtbH4q"></span>
### Backup/restore resource scope

The backup center provides namespace\-level application metadata backup and restore, including Kubernetes\-native resources, CustomResourceDefinition (CRD) resources, and volume resources. The following types of data are supported for backup and restore:


* **Application metadata**, which refers to the definition data of Kubernetes objects.

* **Volume data**, which refers to the data in volumes mounted to pods. Volume types include PVC, local, emptyDir, and more.


<span id="HPyCBAHE"></span>
### PV backup

The backup center currently provides storage volume backup using the CSI snapshot method. This method is typically applicable to backup and restore scenarios within the same cloud environment, cluster, and storage system. The following considerations should be noted when you back up PVs:


* Ensure that the corresponding VolumeSnapshotClass already exists in the Kubernetes cluster.

* Ensure that all PVCs are created through CSI.

* If there are multiple PVCs created by different CSI drivers within a namespace, ensure that each CSI driver has a corresponding VolumeSnapshotClass.

* If a single CSI driver has multiple eligible VolumeSnapshotClasses, a random VolumeSnapshotClass will be selected for backup.


<span id="6RdW8avI"></span>
## Application scenarios

<span id="VKdtjF9N"></span>
### Cloud migration of container application data

The backup center provides an easy\-to\-use data migration method that enables enterprises to flexibly and independently select or switch cloud service providers while avoiding infrastructure lock\-in.

<span id="Sq3QMTCL"></span>
### System or hardware failure

Backup and restore effectively reduce the risk of business disruption caused by failures and ensure the continuity of core businesses in Kubernetes clusters.

<span id="ZT4dgDwd"></span>
### Environment changes in development and testing

The backup center enables quick restoration of data backed up at any time or in any repository when the environment changes or configuration adjustments occur during development, testing, or similar processes.

<span id="3H4FiDpY"></span>
### Malicious attacks or misoperations

The backup center prevents data loss caused by malicious attacks or misoperations through backup and recovery, ensuring data integrity and availability.

<span id="UlqjudtE"></span>
### Multi\-cluster and multi\-storage collaborative protection

With the capabilities of the backup center, you can easily implement multi\-location, on\-demand backup/restore and disaster recovery protection across infrastructure, including across clusters, cloud providers, and storage regions. Examples include backing up and restoring applications within a VKE cluster, migrating applications across VKE clusters in the same region, migrating applications across VKE clusters in different regions, and migrating applications from third\-party clusters to VKE clusters.

<span id="YPq1orv2"></span>
## Usage process

You can refer to the following tasks to back up and restore cluster data:


1. [Adding repositories](https://docs.byteplus.com/en/docs/vke/Add_warehouse): Use  TOS as backup repositories.

2. [Creating backup plans](https://docs.byteplus.com/en/docs/vke/Create_backup_plan). Back up application metadata to TOS for subsequent restore jobs.

3. [Creating restore jobs](https://docs.byteplus.com/en/docs/vke/Create_a_recovery_job). You can restore backup data in the Success or Partially failed status to the specified cluster with one click.
