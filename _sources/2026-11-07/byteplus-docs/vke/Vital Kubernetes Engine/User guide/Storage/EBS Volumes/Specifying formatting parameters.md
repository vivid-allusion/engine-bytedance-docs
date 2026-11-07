---
title: "Specifying formatting parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_formatting_parameters"
---

VKE clusters allow you to specify the underlying attributes and features of a PV during formatting by using formatting parameters when you mount the PV in a pod. This topic describes how to specify formatting parameters when you use EBS volumes.

<span id="8wmOr5aw"></span>
## Background information

<span id="Iu2tGEql"></span>
### What are formatting parameters

Formatting parameters are specified when a file system is created (formatted) for the first time. The parameters are mainly used to specify the underlying attributes, performance, features, and adaptation logic of the file system, and replace the default format configuration. This ensures the file system is precisely adapted to business scenarios, such as small file storage, high I/O read/write operations, and large\-capacity disks. It also ensures storage efficiency and data adaptability.

The following table describes common usage scenarios and descriptions of formatting parameters.


|Application scenario |Scenario description |
|---|---|
|Define the basic storage unit of the file system |Configure core attributes, such as block size and inode allocation ratio, which determine how the file system stores data and manages file indexes. For example:<br><br><br>* In scenarios with multiple small files, such as logs and caches, use a smaller block size to reduce disk space waste.<br><br>* In scenarios with multiple large files, such as videos and databases, use a larger block size to improve read and write efficiency. |
|Performance and feature trade\-offs |Enable or disable specific file system features or optimize key performance parameters to balance performance, security, and disk space.<br><br><br>* To achieve optimal write performance, you can disable the log feature, such as `-O ^has_journal` in the EXT4 system.<br><br>* In high I/O business scenarios, you can expand the log buffer, such as `-l size=64m` in the XFS system, to improve log read and write efficiency.<br><br>* In non\-core storage scenarios, you can disable multiple metadata replicas to save disk space. |
|Adapt to underlying hardware and business requirements |Match the file system with the underlying disk (such as sector size) and business scenarios (such as large\-capacity storage and distributed deployment) to prevent incompatibility or performance loss.<br><br><br>* Align the file system with the physical sector size of the disk to reduce extra I/O operations.<br><br>* In large\-capacity disk scenarios, optimize the indexing strategy to prevent decreased file query efficiency. |


<span id="UpumL86c"></span>
### Common formatting parameters

Supported formatting parameters vary depending on the file system type selected for EBS volumes.


* When you select EXT4 as the file system type, see the [official documentation](https://linux.die.net/man/8/mkfs.ext4) for supported parameters.

* When you select XFS as the file system type, see the [official documentation](https://man7.org/linux/man-pages/man8/mkfs.xfs.8.html) for supported parameters.


<span id="IQpQKdhP"></span>
## Usage limits


* To specify volume formatting parameters, the csi\-ebs add\-on must be upgraded to v1.3.0 or later. For details, see [Upgrading add-ons](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

* Formatting parameters take effect only if the volume is formatted for the first time, and do not support dynamic modification.


<span id="sKGouhFT"></span>
## Procedure

<span id="z7MrfwUd"></span>
### Configuring PVs

When you configure a PersistentVolume (PV) of the EBS type, you can specify formatting parameters by using the console or kubectl.


<Tabs>
<Tab zoneid="zZUFmKWr" title="Configuring through the console">
<TabTitle>Configuring through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**.

4. Click **Create PersistentVolume** and configure parameters on the page that appears. In the **Advanced settings ** section, click **Add formatting parameter** to specify the formatting parameters for the PV.

5. After the configuration is complete, you can create a PersistentVolumeClaim (PVC), associate it with the PV, and then mount it in the container. For details, see [Using static PVs of the EBS type](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes).


</Tab>
<Tab zoneid="cMEdbIUE" title="Configuring through kubectl">
<TabTitle>Configuring through kubectl</TabTitle>

1. When you configure a PV by using kubectl, you can specify formatting parameters.

   ```YAML
   apiVersion: v1
   kind: PersistentVolume
   metadata:
     name: pv-ebs-static
   spec:
     accessModes:
     - ReadWriteOnce 
     capacity:
       storage: 20Gi
     csi:
       driver: ebs.csi.volcengine.com
       fsType: ext4
       volumeAttributes:
         ChargeType: PostPaid
         type: ESSD_FlexPL
         mkfsOptions: "-O bigalloc -C 16384" # The volume formatting parameters, which take effect if the volume is formatted for the first time, and do not support dynamic modification.
         zone: cn-shanghai-a
       volumeHandle: vol-cmukmy9yi5bi254b****
     volumeMode: Filesystem
   ```
   

2. After the configuration is complete, you can create a PVC, associate it with the PV, and then mount it in the container. For details, see [Using static PVs of the EBS type](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes).


</Tab>
</Tabs>


<span id="H1V39ssP"></span>
### Configuring an SC

When you configure a StorageClass (SC) of the EBS type, you can specify formatting parameters by using the console or kubectl.


<Tabs>
<Tab zoneid="8fCXpj10" title="Configuring through the console">
<TabTitle>Configuring through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> StorageClass**.

4. Click **Create StorageClass** and configure parameters on the page that appears. In the **Advanced settings ** section, click **Add formatting parameter** to specify the formatting parameters for the SC.

5. After the configuration is complete, you can create a PVC, associate it with the SC, and then mount it in the container. For details, see [Using dynamic PVs of the EBS type](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes).


</Tab>
<Tab zoneid="9iBKGY3M" title="Configuring through kubectl">
<TabTitle>Configuring through kubectl</TabTitle>

1. When you configure an SC by using kubectl, you can specify formatting parameters.

   ```YAML
   apiVersion: storage.k8s.io/v1
   kind: StorageClass
   metadata:
     name: storage-class-ebs
   provisioner: ebs.csi.volcengine.com
   parameters:
     ChargeType: PostPaid
     fsType: ext4
     type: ESSD_FlexPL
     mkfsOptions: "-O bigalloc -C 16384" # The volume formatting parameters, which take effect if the volume is formatted for the first time, and do not support dynamic modification.
     zone: cn-shanghai-a
     projectName: default
   reclaimPolicy: Delete
   allowVolumeExpansion: true
   volumeBindingMode: Immediate
   ```
   

2. After the configuration is complete, you can create a PVC, associate it with the SC, and then mount it in the container. For details, see [Using dynamic PVs of the EBS type](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes).


</Tab>
</Tabs>


<span id="zVMmrqic"></span>
## Validating results

If you specify formatting parameters when you create a PV of the EBS type, you can check whether the parameters take effect after the configuration is complete. This topic uses the formatting configuration `mkfsOptions: "-O bigalloc -C 16384"` as an example.


1. Use **ECS Terminal** to log in to the node where the pod is located. For details, see [ECS Terminal](https://docs.byteplus.com/en/docs/vke/Managing-nodes#ecs-terminal).

2. Run the following command to check whether the mkfsOptions formatting parameters have taken effect. `/dev/vdc` is the logical identifier of the volume when it is mounted on the node.

   ```Bash
   tune2fs -l /dev/vdc
   ```
   

   The expected result is as follows.

   * In the `Filesystem features` line, the `bigalloc` field can be found, which indicates that the bigalloc feature of the EXT4 file system has been enabled.

   * In the `Block size` line, the value is `4096`, which indicates the default block size in the EXT4 system is 4096 bytes (4 KB). In this case, the formatting parameter `-C 16384` allocates a total size of `16384 * 4096 = 64 MB` for the log buffer.

   ```Bash
   tune2fs 1.44.5 (15-Dec-2018)
   ...
   Filesystem features:      has_journal ext_attr resize_inode dir_index filetype needs_recovery extent 64bit flex_bg sparse_super large_file huge_file dir_nlink extra_isize bigalloc metadata_csum
   ...
   Block size:               4096
   Journal inode:            8
   ...
   ```
