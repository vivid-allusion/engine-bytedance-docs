---
title: "CreateMigrationJob - Creates a migration task"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/CreateMigrationJob"
---

Call the CreateMigrationJob operation to create a migration task.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations

For the prerequisites and precautions for creating a migration task, see [Creating and starting migration tasks](https://docs.byteplus.com/en/docs/smc/Step-2-Create-and-launch-the-migration-task).

<span id=".6K-35rGC6K-05piO"></span>
## Request description

To perform incremental data migration, set the `SyncConfig.TriggerLastSync` parameter to `false`, and specify the interval for synchronizing incremental data using the `SyncConfig.SyncInterval` parameter.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CreateMigrationJob&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|9OW5Dm">必选</span> `Sample value: CreateMigrationJob`

The operation that you want to perform. Valid value: CreateMigrationJob.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|nSqIeI">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**DestinationConfig.AutoReplicate ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to automatically start migration when the migration task passes the precheck. Valid values:


* false: Do not migrate automatically. This is the default value.

* true: Automatically migrate.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to an ECS instance or ECS instance image.</div>




**DiskConfigs.N.Partitions.N.AbortPartition ** <span data-label="purple">boolean[] </span>`Optional` `Sample value: DiskConfigs.0.Partitions.0.AbortPartition=false&DiskConfigs.0.Partitions.1.AbortPartition=false`

Whether to skip this partition during migration. Valid values:


* false: Do not skip. This is the default value.

* true: Skip.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter is supported only for migration of a Linux file to an ECS instance image.</div>


* <div data-tips="true" data-tips-type="tip">Partitions with mount points <code>/</code> and <code>/boot</code> must be migrated.</div>


* <div data-tips="true" data-tips-type="tip">Currently, only system volumes are supported.</div>


* <div data-tips="true" data-tips-type="tip">The first N: the serial number of the disk. Valid range: 0\-14.</div>


* <div data-tips="true" data-tips-type="tip">The second N: the serial number of the partition.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple partition configurations with &.</div>


* <div data-tips="true" data-tips-type="tip">This parameter is in Beta. To request a trial, contact your account manager.</div>




**DiskConfigs.N.DestinationDiskSize ** <span data-label="purple">long[] </span>`Optional` `Sample value: DiskConfigs.0.DestinationDiskSize=40`

The new disk capacity of the target ECS instance image after adjustment. Unit: GiB.


* Parameter \- N: the serial number of the disk. Valid range: 0–14.

* Separate multiple disk serial numbers with `&`.

* The capacity of the system volume ranges from 40 GiB to 2048 GiB. The capacity of the system volume must not be less than the total size of the partitions to be migrated.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is in Beta. To request a trial, contact your account manager.</div>




**DiskConfigs.N.Partitions.N.DestinationPartitionSize ** <span data-label="purple">long[] </span>`Optional` `Sample value: DiskConfigs.0.Partitions.0.DestinationPartitionSize=200&DiskConfigs.0.Partitions.1.DestinationPartitionSize=300`

The new partition capacity of the target ECS instance image after adjustment. Unit: Bytes.


* The first N: the serial number of the disk. Valid range: 0\-14.

* The second N: the serial number of the partition.

* Separate multiple partition sizes with `&`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The size of a partition cannot be smaller than its used space after adjustment, and the total size of all partitions must not exceed the size of the disk they belong to.</div>


* <div data-tips="true" data-tips-type="tip">This parameter is in Beta. To request a trial, contact your account manager.</div>




**LvmInfo.VgInfos.N.Format ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.Format=lvm2`

The format of the logical volume group to be migrated.


* Parameter \- N: the serial number of the logical volume group.

* Separate multiple logical volume groups with `&`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The value of parameter \- N cannot exceed the actual number of volume groups on the source server.</div>




**LvmInfo.VgInfos.N.LvInfos.N.BlockDevices.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.LvInfos.1.BlockDevices.1=/dev/vdb1`

The list of disk block devices used by the logical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* The third N: the serial number of the disk block device.

* Separate multiple disk block devices with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.FsType ** <span data-label="purple">string[] </span>`Optional` `Sample value: --`

The file system type with which the logical volume to be migrated is formatted.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.LvName ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.LvInfos.1.LvName=lv01`

The name of the logical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.LvPath ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.LvInfos.1.LvPath=/dev/vg_01/lv01`

The path of the logical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.LvSize ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.LvInfos.1.LvSize=943718400`

The new size of the logical volume to be migrated. Unit: Bytes.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.LvUUID ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.LvInfos.1.LvUUID=VlMqHc-iZfE-Vo*****`

The UUID of the logical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.VgName ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.LvInfos.1.VgName=vg_01`

The name of the volume group where the logical volume to be migrated is located.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.PvInfos.N.PvName ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.PvInfos.1.PvName=/dev/vdb1`

The name of the physical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the physical volume.

* Separate multiple physical volumes with `&`.



**LvmInfo.VgInfos.N.PvInfos.N.PvSize ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.PvInfos.1.PvSize=1019215872`

The size of the physical volume to be migrated. Unit: Bytes.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the physical volume.

* Separate multiple physical volumes with `&`.



**LvmInfo.VgInfos.N.PvInfos.N.PvUUID ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.PvInfos.1.PvUUID=h3ey9f-VJAi*****`

The UUID of the physical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the physical volume.

* Separate multiple physical volumes with `&`.



**LvmInfo.VgInfos.N.PvInfos.N.VgName ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.PvInfos.1.VgName=vg_01`

The name of the logical volume group where the physical volume to be migrated is located.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the physical volume.

* Separate multiple physical volumes with `&`.



**LvmInfo.VgInfos.N.VgName ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.VgName=vg_01`

The name of the logical volume group to be migrated.


* Parameter \- N: the serial number of the logical volume group.

* Separate multiple logical volume groups with `&`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The value of parameter \- N cannot exceed the actual number of volume groups on the source server.</div>




**LvmInfo.VgInfos.N.VgSize ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.VgSize=1019215872`

The new size of the logical volume group to be migrated. Unit: Bytes.


* Parameter \- N: the serial number of the logical volume group.

* Separate multiple logical volume groups with `&`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The value of parameter \- N cannot exceed the actual number of volume groups on the source server.</div>




**LvmInfo.VgInfos.N.VgUUID ** <span data-label="purple">string[] </span>`Optional` `Sample value: LvmInfo.VgInfos.1.VgUUID=Y2apS5-w7yK-*****`

The UUID of the logical volume group to be migrated.


* Parameter \- N: the serial number of the logical volume group.

* Separate multiple logical volume groups with `&`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The value of parameter \- N cannot exceed the actual number of volume groups on the source server.</div>




**LvmInfo.VgInfos.N.LvInfos.N.LvUsedSize ** <span data-label="purple">string[] </span>`Optional` `Sample value: --`

The used capacity of the logical volume to be migrated. Unit: Bytes.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**LvmInfo.VgInfos.N.LvInfos.N.MountPoint ** <span data-label="purple">string[] </span>`Optional` `Sample value: --`

The mount point of the logical volume to be migrated.


* The first N: the serial number of the logical volume group.

* The second N: the serial number of the logical volume.

* Separate multiple logical volumes with `&`.



**DestinationConfig.AutoInstallBlkNone ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to automatically install blk\-none for the target instance or target image. Valid values:


* true: Install automatically.

* false: Do not install automatically. This is the default value.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to a Linux ECS instance or Linux ECS instance image.</div>




**DestinationConfig.AutoInstallVirtio11 ** <span data-label="purple">boolean </span>`Optional` `Sample value: false`

Whether to automatically install the Virtio1.1 driver for the target instance or target image. Valid values:


* true: Install automatically.

* false: Do not install automatically. This is the default value.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to a Linux ECS instance or Linux ECS instance image.</div>




**DestinationConfig.DestinationSystem ** <span data-label="purple">string </span>`Optional` `Sample value: VeLinux10Centos`

The target operating system. Valid values:


* Unknown: Unknown.

* VeLinux10Centos: Indicates migration to veLinux 1.0 CentOS Compatible operating system.

* VeLinux20Centos: Indicates migration to veLinux 2.0 CentOS Compatible operating system.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>DestinationConfig.DestinationType</code> is set to <code>ECSSystem</code>, this parameter is required.</div>




**DestinationConfig.DestinationType ** <span data-label="purple">string </span><span data-api-tag="require|bgdHn9">必选</span> `Sample value: ECSInstance`

The target type. Valid values:


* ECSInstance: ECS instance.

* ECSImage: ECS instance image.

* ECSSystem: ECS instance operating system.



**DestinationConfig.ImageName ** <span data-label="purple">string </span>`Optional` `Sample value: image-1`

The name of the image.


* It must start with a letter or a Chinese character.

* It can contain only Chinese characters, letters, digits, underscores (_), hyphens (\-), and English periods (.).

* The name must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to an ECS instance image.</div>




**DestinationConfig.InstanceId ** <span data-label="purple">string </span>`Optional` `Sample value: i-3teco18f1w5a71****`

The target instance ID. To query and obtain the instance ID, call the [DescribeInstances](https://docs.byteplus.com/en/docs/ecs/DescribeInstances) operation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to an ECS instance.</div>




**DestinationConfig.Region ** <span data-label="purple">string </span><span data-api-tag="require|gILWkH">必选</span> `Sample value: cn-beijing`

The target region.



**DiskConfigs.N.DiskIndex ** <span data-label="purple">integer[] </span><span data-api-tag="require|fz4laC">必选</span> `Sample value: 0`

The index of the disk on the source server, starting from `0`.


* Parameter \- N: the serial number of the disk. Valid range: 0–14.

* Separate multiple disk serial numbers with &.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The value of parameter \- N cannot exceed the actual number of disks on the source server.</div>




**DiskConfigs.N.DiskSize ** <span data-label="purple">integer[] </span>`Optional` `Sample value: 10`

The capacity of the source server disk. Unit: GB.


* Parameter \- N: the serial number of the disk, which corresponds to the disk serial number identified by `DiskConfigs.N.DiskIndex`. Valid range: 0–14.

* Separate multiple disk serial numbers with &.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The value of parameter \- N cannot exceed the actual number of disks on the source server.</div>




**DestinationConfig.LicenseType ** <span data-label="purple">string </span>`Optional` `Sample value: PlatformLicense`

The license type. Valid values:


* PlatformLicense: Use a license from an official BytePlus channel based on the OS type of your source server.

* BYOL: Bring Your Own License (BYOL).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">This parameter is valid only when the OS type of the source server is RedHat, SUSE Linux Enterprise Server, or Windows. For other OS types, this parameter is invalid.</div>


* <div data-tips="true" data-tips-type="tip">The supported values for each OS type are as follows:</div>


   * <div data-tips="true" data-tips-type="tip">Windows: <code>PlatformLicense</code> and <code>BYOL</code> are supported.</div>


   * <div data-tips="true" data-tips-type="tip">RedHat / SUSE Linux Enterprise Server: </div>


      * <div data-tips="true" data-tips-type="tip">If the source server is <strong>a BytePlus ECS instance</strong>: <code>PlatformLicense</code> and <code>BYOL</code> are supported.</div>


      * <div data-tips="true" data-tips-type="tip">If the source server is <strong>not a BytePlus ECS instance</strong>: Only <code>BYOL</code> is supported.</div>




**MigrationJobDescription ** <span data-label="purple">string </span>`Optional` `Sample value: Migrate local virtual machine`

The task description.


* It must start with a letter or a Chinese character.

* Only Chinese characters, letters, numbers, dots (.), spaces, underscores (_), hyphen (\-), equal signs (=), English comma (,), Chinese comma (，), and Chinese period (。) are allowed.

* The length is limited to 255 characters.



**MigrationJobName ** <span data-label="purple">string </span><span data-api-tag="require|zj8ex9">必选</span> `Sample value: VMToECS`

The task name.


* Start with a letter or a Chinese character.

* Only Chinese characters, letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* It must be 1 to 128 characters in length.



**MigrationSourceId ** <span data-label="purple">string </span><span data-api-tag="require|EBwNAU">必选</span> `Sample value: s-iegs1y963vj0******`

The migration source ID. You can call the [DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) operation to query and obtain the migration source ID.



**NetworkConfig.BandwidthLimit ** <span data-label="purple">integer </span>`Optional` `Sample value: 5`

The maximum transfer rate. Unit: Mbps. The minimum value (default) is 0, which means throttling is disabled.



**NetworkConfig.NetworkTransitionMode ** <span data-label="purple">string </span>`Optional` `Sample value: PublicNetwork`

The network mode. Valid values:


* PublicNetwork: Public network.

* VPC: VPC.



**NetworkConfig.SubnetId ** <span data-label="purple">string </span>`Optional` `Sample value: subnet-h49ihs*****`

Subnet ID. You can query and obtain it by calling the [DescribeSubnets](https://docs.byteplus.com/en/docs/vpc/DescribeSubnets) operation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to an ECS instance image and data is transferred over the intranet.</div>




**NetworkConfig.VpcId ** <span data-label="purple">string </span>`Optional` `Sample value: vpc-bp15zkdt37pq72zv****`

VPC ID. You can query and obtain it by calling the [DescribeVpcs](https://docs.byteplus.com/en/docs/vpc/DescribeVpcs) operation.

This parameter is valid only when the source server is migrated to an ECS instance image and data is transferred over the intranet.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the migration task belongs. Each task can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**SyncConfig.SyncInterval ** <span data-label="purple">integer </span>`Optional` `Sample value: 2`

The incremental synchronization interval. Unit: hours.

Valid range: 1\-168.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When <code>SyncConfig.TriggerLastSync</code> is set to <code>false</code>, this parameter is required.</div>




**SyncConfig.SyncTimes ** <span data-label="purple">integer </span>`Optional` `Sample value: 3`

The number of incremental synchronizations. Valid values:


* Maximum value: 30

* Default value: 0

* Minimum value: 0


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is only supported for one\-click migration.</div>




**SyncConfig.SyncType ** <span data-label="purple">string </span>`Optional` `Sample value: File`

The replication type. Valid values:


* File (default): File replication.

* Block: Block replication.



**SyncConfig.TriggerLastSync ** <span data-label="purple">boolean </span>`Optional` `Sample value: true`

Whether to perform only one full data synchronization. Valid values:


* true (default): Indicates that only one full data synchronization is performed, and no incremental data synchronization is performed.

* false: Indicates that after one full data synchronization, incremental data synchronization will also be performed at intervals specified by the `SyncConfig.SyncInterval` parameter.



**Tags.N.Key ** <span data-label="purple">string[] </span><span data-api-tag="require|4ph1XG">必选</span> `Sample value: Tags.1.Key=k1&Tags.2.Key=k2`

The key of the tag.


* Parameter \- N: specifies the serial number of the tag key. Valid range: 1–20.

* Separate multiple tag keys with `&`.

* Naming rules:

   * It cannot start with `volc:` or `sys:` in any case form.

   * Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

   * It must be 1 to 128 characters in length.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Keys of the same resource must be unique.</div>




**Tags.N.Value ** <span data-label="purple">string[] </span>`Optional` `Sample value: Tags.1.Value=v1&Tags.2.Value=v2`

The user tag value.


* Parameter \- N: specifies the serial number of the tag value. Valid range: 1–20.

* Separate multiple tag values with `&`.

* Naming rules:

   * Only letters, digits, spaces, and the following symbols are allowed: "_", ".", ":", "/", "=", "+", "\-", and "@".

   * It can be empty. Length limit: 0–256 characters.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To pass in this parameter, pass in <code>Tags.N.Key</code> first.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**MigrationJobId ** <span data-label="purple">string </span>`Sample value: job-3tiegs1y963vj0******`

The migration task ID.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=CreateMigrationJob&Version=2020-04-01&DestinationConfig.DestinationType
=ECSInstance&DestinationConfig.Region=cn-beijing&MigrationJobName=VMToECS&MigrationSourceId=s-iegs1y963vj0******&NetworkConfig.NetworkTransitionMode=PublicNetwork&SyncConfig.SyncType=File&SyncConfig.TriggerLastSync=true HTTP/1.1
Host: smc.volcengineapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"202306021637410F150Dxxxxx",
        "Action":"CreateMigrationJob",
        "Version":"2020-04-01",
        "Service":"smc",
        "Region":"cn-beijing"
    },
    "Result":{
        "MigrationJobId": "job-3tiegs1y963vj0******"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |Insufficient.Balance |The request is denied due to the lack of balance. |The account balance is insufficient. |
|400 |InvalidCustomImageName.Malformed |The custom image name is malformed. |The custom image name is invalid. |
|400 |InvalidDestinationInstanceType.Unsupported |Migration to the specified destination type is not supported. |Migration to the specified target instance type is not supported. |
|400 |InvalidDiskConfigForMigration.Unsupported |The specified disk cannot be migrated. |The specified disk cannot be migrated. |
|400 |InvalidFilesystemType.Unsupported |The file system type does not support file sync type. |The file system used by the source environment does not support file replication. |
|400 |InvalidInstanceChargeTypeForMigration.Unsupported |The destination instance charge type does not support migration. |The billing method of the target instance does not support migration. |
|400 |InvalidInstanceForMigration.Unsupported |The specified destination instance does not support migration. |The specified target instance does not support migration. |
|400 |InvalidInstanceStatusForMigration.Unsupported |The specified destination instance does not support migration. |The specified target instance does not support migration. |
|400 |InvalidInstanceTypeForMigtation.Unsupported |The destination instance type does not support migration. |The target instance type does not support migration. |
|400 |InvalidLVMStatus.Unsupported |The lvm status does not support file sync type. |File replication is not supported because LVM exists in the source environment. |
|400 |InvalidLicenseTypeForMigration.Unsupported |The specified license type does not support migration. |The specified license type does not support migration. |
|400 |InvalidMigrationCheckResult.Unsupported |The specified migration source check result is invalid, please make sure that completing migration source check before creating an migration job. |The migration precheck does not pass. Make sure that the migration precheck passes before you create a migration task. |
|400 |InvalidMigrationJobDescription.Malformed |The specified MigrationJobDescription is malformed. |The specified MigrationJobDescription value is invalid. |
|400 |InvalidMigrationJobName.Malformed |The specified MigrationJobName is malformed. |The specified MigrationJobName value is invalid. |
|400 |InvalidMigrationSourceForSystemMigration.Unsupported |The specified migration source does not support operating system migration. |The specified migration source does not support operating system migration. |
|400 |InvalidMigrationSourceStatus |The status of the specified migration source does not support this request. |The status of the specified migration source does not support this operation. |
|400 |InvalidMigrationType.Unsupported |The destination migration type does not support. |The destination migration type is not supported. |
|400 |InvalidOSTypeForFileMigration.Unsupported |The os type does not support file sync type. |The operating system of the source environment does not support file replication. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |InvalidRegion.Malformed |The specified Region is malformed. |The specified Region is invalid. |
|400 |InvalidRsyncStatus.Unsupported |The rsync status does not support file sync type. |Rsync in the source environment does not meet the file replication requirements. Make sure that Rsync exists and the version is not less than 3.1. |
|400 |InvalidSecurityGroupPermission.Conflict |The security group permission is invalid. |SMC requires the target instance to enable ports 8080, 22, 5201, and 5986. Check the security group rules of the target instance. |
|400 |InvalidSubnetIdStatus |The specified subnet status error. |The status of the specified subnet is incorrect. |
|400 |InvalidSyncTypeForMigration.Unsupported |The specified migration job sync type does not support migration. |The replication type of the specified migration task does not support migration. |
|400 |InvalidSystemVolumeSize.Malformed |The specified destination instance system volume size is malformed. |The system volume size of the specified target instance is invalid. Make sure that the system volume size of the target instance is greater than the system volume size of the source instance. |
|400 |InvalidTagKey.Malformed |The specified TagKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagValue.Malformed |The specified TagValue is malformed. |The specified tag value is invalid. |
|400 |InvalidVolumeTypeForCreateWholeImage.UnSupported |The specified VolumeType cannot be used for CreateWholeImage. |Creating a whole image is not supported for the specified volume type. |
|400 |LimitExceeded.MaximumDiskSize |The size of disk exceeds the maximum limit. |The disk size of the specified migration source exceeds the upper limit. |
|400 |LimitExceeded.MaximumImageCount |You've reached the limit on the number of image that you can create. |The number of custom images that you create exceeds the upper limit. |
|400 |LimitExceeded.MaximumSecurityGroupCount |The number of specified networkinterface security groups exceeds the maximum limit. |The number of security groups for the target network interface exceeds the upper limit. |
|400 |LimitExceeded.MaximumSyncInterval |The number of specified SyncInterval exceeds the maximum limit. |The specified SyncInterval value exceeds the upper limit. |
|400 |LimitExceeded.MaximumSyncTimes |The number of specified SyncTimes exceeds the maximum limit. |The specified SyncTimes value exceeds the upper limit. |
|400 |LimitExceeded.MaximumSystemDiskSize |The size of specified system disk exceeds the maximum limit |The specified system volume size exceeds the upper limit. |
|400 |LimitExceeded.MaximumTags |You've reached the limit on the number of tags that you can create. |The specified tag number exceeds the maximum limit. |
|400 |LimitExceeded.MaximumVolumes |You've reached the limit on the number of volumes that you can set in the instance. |The number of volumes mounted to the specified instance exceeds the upper limit. |
|400 |LimitExceeded.MinimumBandwidthLimit |The number of specified BandwidthLimit exceeds the minimum limit. |The specified BandwidthLimit value is below the lower limit. |
|400 |LimitExceeded.MinimumPartitionSize |The number of specified PartitionSize exceeds the minimum limit. |The specified PartitionSize value is below the lower limit. |
|400 |LimitExceeded.MinimumSyncInterval |The number of specified SyncInterval exceeds the minimum limit. |The specified SyncInterval value is below the lower limit. |
|400 |LimitExceeded.MinimumSyncTimes |The number of specified SyncTimes exceeds the minimum limit. |The specified SyncTimes value is below the lower limit. |
|400 |MissingParameter.DestinationConfig |The required parameter DestinationConfig is not supplied. |The DestinationConfig parameter cannot be empty. |
|400 |MissingParameter.InstanceId |The required parameter InstanceId is not supplied. |The instance ID cannot be empty. |
|400 |MissingParameter.MigrationJobName |The required parameter MigrationJobName is not supplied. |The MigrationJobName parameter cannot be empty. |
|400 |MissingParameter.MigrationSourceId |The required parameter MigrationSourceId is not supplied. |The MigrationSourceId parameter cannot be empty. |
|400 |MissingParameter.NetworkConfig |The required parameter NetworkConfig is not supplied. |The NetworkConfig parameter cannot be empty. |
|400 |MissingParameter.NetworkTransitionMode |The required parameter NetworkTransitionMode is not supplied. |The network transfer mode cannot be empty. |
|400 |MissingParameter.Region |The required parameter Region is not supplied. |The region cannot be empty. |
|400 |MissingParameter.SubnetId |The required parameter SubnetId is not supplied. |The subnet ID cannot be empty. |
|400 |MissingParameter.SyncConfig |The required parameter SyncConfig is not supplied. |The SyncConfig parameter cannot be empty. |
|400 |MissingParameter.SyncType |The required parameter SyncType is not supplied. |The replication type cannot be empty. |
|400 |MissingParameter.VpcId |The required parameter VpcId is not supplied. |The vpcId parameter cannot be empty. |
|400 |QuotaExceeded.Common |You've reached the limit of cpu, volume and general cpu that you can create, please submit ticket to request an increase in quota. |The maximum numbers of CPUs, volumes, and general\-purpose CPUs that can be created have been reached. When the source server is migrated to an image, SMC will create volumes and ECS instances in the target region. Make sure that there is at least one availability zone with sufficient volume and CPU balances in the target region to meet the migration requirements. |
|400 |QuotaExceeded.Cpu |You've reached the limit of cpu that you can create, please submit ticket to request an increase in quota. |The maximum number of CPUs that can be created has been reached. SMC will create a temporary instance. Make sure that the number of CPUs in the target availability zone has not reached the upper limit. |
|400 |QuotaExceeded.Eip |You've reached the limit on the number of eip that you can create, please submit ticket to request an increase in quota. |The maximum number of EIPs that can be applied for has been reached. SMC will create a temporary EIP. Make sure that the number of EIPs in the target region has not reached the upper limit. |
|400 |QuotaExceeded.GeneralCpu |You've reached the limit of general cpu that you can create, please submit ticket to request an increase in quota. |The maximum number of general\-purpose CPUs that can be created has been reached. SMC will create a temporary instance. Make sure that the number of general\-purpose CPUs in the target availability zone has not reached the upper limit. |
|400 |QuotaExceeded.MaximumMigrationJob |You've reached the limit on the number of migration jobs that you can create, please submit ticket to request an increase in quota. |The quota for migration tasks is insufficient. Submit a ticket to increase the quota. |
|400 |QuotaExceeded.MaximumRunningMigrationJob |You've reached the limit on the number of running migration jobs that you can create, please submit ticket to request an increase in quota. |The quota for running migration tasks is insufficient. Submit a ticket to increase the quota. |
|400 |QuotaExceeded.SecurityGroup |You've reached the limit on the number of SecurityGroup that you can create, please submit ticket to request an increase in quota. |The maximum number of security groups that can be created has been reached. SMC will create a temporary security group. Make sure that the number of security groups in the target region has not reached the upper limit. |
|400 |QuotaExceeded.SelfImage |You've reached the limit on the number of image that you can create, please submit ticket to request an increase in quota. |The maximum number of custom images that can be created has been reached. SMC will create a temporary custom image. Make sure that the number of custom images has not reached the upper limit. |
|400 |QuotaExceeded.Volume |You've reached the limit of volume that you can create, please submit ticket to request an increase in quota. |The capacity upper limit of this type of volume has been reached. SMC will create a temporary volume. Make sure that the capacity of this type of volume in the target region has not reached the upper limit. |
|400 |QuotaExceeded.Vpc |You've reached the limit on the number of vpc that you can create, please submit ticket to request an increase in quota. |The maximum number of VPCs that can be created has been reached. SMC will create a temporary VPC. Make sure that the number of VPCs in the target region has not reached the upper limit. |
|400 |LimitExceeded.MinimumDestinationDiskSize |The number of specified DestinationDiskSize exceeds the minimum limit. |The specified DestinationDiskSize value is below the lower limit. |
|400 |LimitExceeded.MinimumDestinationPartitionSize |The number of specified DestinationPartitionSize exceeds the minimum limit. |The specified DestinationPartitionSize value is below the lower limit. |
|400 |LimitExceeded.MinimumDiskSize |The number of specified DiskSize exceeds the minimum limit. |The specified DiskSize value is below the lower limit. |
|400 |LimitExceeded.MinimumPartitionUsedSize |The number of specified PartitionUsedSize exceeds the minimum limit. |The specified PartitionUsedSize value is below the lower limit. |
|404 |InvalidActionOrVersion |Could not find operation %s for version %s. |The requested API does not exist. |
|404 |InvalidDestinationRegion.NotFound |The specified destination region does not exist. |The specified region does not exist. |
|404 |InvalidInstance.NotFound |The specified instance does not exist. |The specified instance does not exist. |
|404 |InvalidMigrationSource.NotFound |The specified migration source does not exist. |The specified migration source does not exist. |
|404 |InvalidSourceTransferEip.NotFound |The specified source instance does not associate eip. |No EIP is associated with the specified source instance. |
|404 |InvalidSourceTransferPrivateIp.NotFound |The specified source instance private ip does not exist. |The specified source instance does not have a private IP address. |
|404 |InvalidSubnetId.NotFound |The specified subnet id does not exist. |The specified subnet ID does not exist. |
|404 |InvalidTransferEip.NotFound |The specified destination instance does not associate eip. |No EIP is associated with the specified target instance. |
|409 |InvalidTagKey.Conflict |The specified TagKey already exists. |The specified tag key already exists. |
|412 |InvalidArchitecture.MisMatch |The source, destination architecture does not match. |The architecture of the source and target instances does not match. |
|412 |InvalidMigrationSource.InUse |The specified migration source is in use. |A migration task is currently in progress for the specified migration source. |
|412 |InvalidVolumeConfig.MisMatch |The source, destination volume config does not match. |The disk configuration of the source and target instances does not match. |
|412 |InvalidVpcId.SubnetIdMismatch |The specified VpcId does not match subnetId. |vpcId and subnet ID do not match. |
|412 |OperationDenied.AgentNeedUpgrade |The specified migration agent need upgrade |Upgrade the migration Agent. |
|412 |OperationDenied.SnapshotServiceUnavailable |The specified operation is denied as Snapshot service is unavailable. |The specified operation was denied because the snapshot service is not enabled. |
|412 |PendingVerification |Your account has not passed the real\-name authentication yet. |The account has not completed real\-name verification. |
|500 |InternalError |An internal error has occurred. |An internal error occurred. Try again. If multiple attempts fail, submit a ticket. |
|500 |Insufficient.InstanceTypeCapacity |There is not enough capacity to fulfill your request. |The resources for the instance type are insufficient. |
