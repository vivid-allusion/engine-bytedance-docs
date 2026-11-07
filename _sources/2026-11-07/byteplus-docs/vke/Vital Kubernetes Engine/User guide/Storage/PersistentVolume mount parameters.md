---
title: "PersistentVolume mount parameters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Configuring_advanced_mount_parameters"
---

VKE clusters allow you to specify additional access methods, performance optimization, or security policies of PersistentVolumes (PVs) by using mount parameters when you mount the PVs in pods. This topic describes the parameters for mounting common types of storage.

<span id="M6m6tZzE"></span>
## Background

<span id="gG4VRh1U"></span>
### What are mount parameters

Mount parameters (mountOptions) are options passed to the kernel during the file system mount process. They are used to control the access methods and performance optimizations for storage devices, such as EBS devices or FileNAS devices. The system directly passes your configured parameters to Linux and appends them to the `mount` command for execution. Configuring a PV by using mount parameters delivers the following characteristics:


* Effective dynamically without re\-creation: After you modify the mount parameters of a StorageClass, the changes take effect after you delete and recreate the pod. You do not need to delete the PVC or PV or migrate data, so your workloads are not affected.

* Permanent application: After you specify the mount parameters of an SC, all volumes created through this SC will automatically carry the relevant parameters each time they are mounted to a pod.

* Effective after resizing: After a volume is expanded online, the new mount parameters also take effect when the pod is recreated and the volume is mounted again.


<span id="KJxPP4ia"></span>
### EBS mount parameters

The following table describes common parameters for mounting EBS.


|Category |Mount parameters |Description |
|---|---|---|
|General\-purpose basic parameters |`ro` |Read\-only mount, which prevents accidental writes and applies to static data or system images. |
||`rw` |Read and write mount (default), which allows read and write operations and applies to business data volumes. |
||`noatime` |Disable updating the access time for files (Do not record timestamps when files are read). |
||`nodiratime` |Disable updating the access time for directories. |
||`defaults` |Include the default parameter combination: `rw`, `suid`, `dev`, `exec`, `auto`, `nouser`, and `async`, which are typically used as basic parameters, to which other custom parameters can be added. |
|Common EXT4 parameters |`data=ordered`<br><br>`data=writeback`<br><br>`data=journal` |Controls the mode for writing data to the log (log feature of the EXT file system).<br><br><br>* `data=ordered`: (default) Metadata is written to the log first, and data is written sequentially, which balances performance and security.<br><br>* `data=writeback`: Only metadata instead of data is written to the log, which achieves higher performance. However, a power failure may result in data inconsistency. Therefore, this applies to non\-core data.<br><br>* `data=journal`: Both data and metadata are written to the log, which delivers the highest security but results in significant performance loss. This is rarely used. |
||`barrier=0`<br><br>`barrier=1` |Control write barrier to prevent disk cache data loss.<br><br><br>* `barrier=1`: (Default) Enable the write barrier, which ensures that data is flushed to the disk before the journal transaction is marked as complete. This applies to hard disk drives (HDDs).<br><br>* `barrier=0`: Disable the write barrier to improve SSD performance (You can disable this feature for volumes because they often have built\-in power\-loss protection). |
||`errors=remount-ro` |When an error occurs in a file system, the mount point is automatically switched to read\-only mode to prevent further data corruption. |
|Common XFS parameters |`noatime`<br><br>`nodiratime` |The parameters have the same effect as in the EXT file system. Because XFS is more sensitive to small\-file optimization, we recommend enabling these options to improve performance. |
||`logbufs=<Quantity>` |Specify the number of log buffers. Default value: 8. If you increase the value, write throughput will be increased. For example, logbufs=8. You can adjust the value based on memory. |
||`logbsize=<Size>` |The log buffer size. Default value: 32 KB. For large files, the value can be set to 64 KB or 128 KB. For example, logbsize=65536. |
||`discard`/`nodiscard` |Specify whether to enable the TRIM feature (releasing unused blocks on SSDs to extend lifespan).<br><br><br>* `discard`: Enable the TRIM feature. We recommend that you enable this feature.<br><br>* `nodiscard`: (Default) Disables the TRIM feature, which applies to temporary mounts or performance\-priority scenarios. |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Supported mount parameters vary depending on the file system type selected for EBS volumes.</div>



* <div data-tips="true" data-tips-type="default">When you select EXT4 as the file system type, see the <a href="https://man7.org/linux/man-pages/man8/mount.8.html">official documentation</a> for supported parameters.</div>


* <div data-tips="true" data-tips-type="default">When you select XFS as the file system type, see the <a href="https://man7.org/linux/man-pages/man5/xfs.5.html">official documentation</a> for supported parameters.</div>



<span id="JT40ywqT"></span>
### TOS mount parameters

When accessing static TOS PVs through an FSX client, you can enable additional features for the PVs using mount parameters.​ For details on mount parameters, see [FSX mount parameters](https://docs.byteplus.com/en/docs/tos/FSX-mount-parameter-description).

When accessing EFS PVs through an FSX client, you can enable additional features for the PVs using mount parameters.​ For details about mount parameters, see [Mounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Mounting_file_systems_FSX).

<span id="CZ1wkDTT"></span>
## Procedure

<span id="kgBbnqyK"></span>
### Configuring PVs

You can specify PV mount parameters by using the console or kubectl.


<Tabs>
<Tab zoneid="h008clBnJn" title="Configuring through the console">
<TabTitle>Configuring through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> PersistentVolume**.

4. Click **Create PersistentVolume** and configure parameters on the page that appears. In the **Advanced configurations** section, click **Add mount parameter** to specify the mount parameters for the PV.

5. After the configuration is complete, you can create a PersistentVolumeClaim (PVC), associate it with the StorageClass (SC), and then mount it in the container.


</Tab>
<Tab zoneid="jV4OIgFRxj" title="Configuring through kubectl">
<TabTitle>Configuring through kubectl</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The configuration methods for different PV types vary. This topic provides an example configuration of EBS ESSDs.</div>



1. When you configure a PV by using kubectl, you can specify mount parameters.

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
         zone: cn-shanghai-a
       volumeHandle: vol-cmukmy9yi5bi254b****
     mountOptions: # PV mount parameters, which support dynamic modification and only take effect on newly mounted disks instead of those already mounted.
     - noatime
     - nodiratime
     - discard
     - nobarrier
     volumeMode: Filesystem
   ```
   

2. After the configuration is complete, you can create a PersistentVolumeClaim (PVC), associate it with the StorageClass (SC), and then mount it in the container.


</Tab>
</Tabs>


<span id="bAjKtsBa"></span>
### Configuring an SC

When you configure an SC for the cluster, you can specify the mount parameters for the PV file system by using the console or kubectl.


<Tabs>
<Tab zoneid="qwUML9eM" title="Configuring through the console">
<TabTitle>Configuring through the console</TabTitle>

1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. Click the name of the target cluster to go to the cluster management page.

3. In the left navigation bar on the cluster management page, click **Storage \> StorageClass**.

4. Click **Create StorageClass** and configure parameters on the page that appears. In the **Advanced configurations** section, click **Add mount parameter** to specify the mount parameters for the SC.

5. After the configuration is complete, you can create a PersistentVolumeClaim (PVC), associate it with the StorageClass (SC), and then mount it in the container.


</Tab>
<Tab zoneid="Ghu3dYjD" title="Configuring through kubectl">
<TabTitle>Configuring through kubectl</TabTitle>

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The configuration methods for different StorageClass types vary. This topic provides an example configuration of EBS ESSDs.</div>



1. When you configure an SC by using kubectl, you can specify mount parameters.

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
     zone: cn-shanghai-a
     projectName: default
   mountOptions: # Volume mount parameters, which support dynamic modification and only take effect on newly mounted disks instead of those already mounted.
   - noatime
   - nodiratime
   - discard
   - nobarrier
   reclaimPolicy: Delete
   allowVolumeExpansion: true
   volumeBindingMode: Immediate
   ```
   

2. After the configuration is complete, you can create a PersistentVolumeClaim (PVC), associate it with the StorageClass (SC), and then mount it in the container.


</Tab>
</Tabs>


<span id="yiPCHwYA"></span>
## Validate results

After you create a workload and mount it to a PV as described in the preceding steps, verify whether the mount parameters of the volume take effect by using the following methods.


1. Run the following command to check whether the PV is mounted to the specified path in the pod.

   ```Bash
   kubectl exec pod-demo-xxx -- df | grep data
   ```
   

   The expected response is as follows. `/dev/vdc` is the logical identifier of the volume when it is mounted on the node.

   ```Bash
   /dev/vdc        20466256      24  20449848   1% /data
   ```
   

2. Run the following command to check whether the mountOptions mount parameters have taken effect.

   ```Bash
   mount
   ```
   

   The expected output is as follows: The content in the parentheses after the `/dev/vdc` path shows the mount parameters. This indicates that the mount parameters have taken effect.

   ```Bash
   ...
   /dev/vdc on /data type ext4 (rw,noatime,nodiratime,discard,nobarrier)
   ...
   ```
   


<span id="4NGfdrmb"></span>
## Related documentation


* [Using static PersistentVolume of cloud disks](https://docs.byteplus.com/en/docs/vke/Using-static-EBS-Volumes)

* [Using dynamic PersistentVolume of cloud disks](https://docs.byteplus.com/en/docs/vke/Using-dynamic-EBS-Volumes)

* [Accessing static TOS PVs by using the FSX client](https://docs.byteplus.com/en/docs/vke/Using_static_TOS_Volumes_through_the_FSX_client)
