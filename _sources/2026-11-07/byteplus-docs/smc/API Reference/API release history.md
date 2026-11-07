---
title: "API release history"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/API_release_notes"
---

This topic describes the API updates for the server\-side Server Migration Center (SMC).

<span id="Kyhfqzn0"></span>
## December 2025


|API |Change record |Associated feature |
|---|---|---|
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |Added a new error code: 500, InternalError |Migration task |
|[TagResources](https://docs.byteplus.com/en/docs/smc/TagResources) |Added new error codes: 400, InvalidResourceIds.NotFound, 400, InvalidTagKey.Malformed, 404, InvalidActionOrVersion |Tag |


<span id="Kyhfqzn0"></span>
## November 2025


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added response parameters:<br><br>The `DiskUsedSize` parameter, which indicates the disk usage, is added to the `Sources.DiskInfo` structure. |Migration source |
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Added request parameter:<br><br>   * `LvmInfo.VgInfos.N.Format` indicates the format of the logical volume group to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.BlockDevices.N` indicates the list of disk block devices used by the logical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.FsType` indicates the file system type the logical volume to be migrated is formatted with.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.LvName` indicates the name of the logical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.LvPath` indicates the path of the logical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.LvSize` indicates the new size of the logical volume to be migrated after the size is adjusted.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.LvUUID` indicates the UUID of the logical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.LvUsedSize` indicates the used size of the logical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.MountPoint` indicates the mount point of the logical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.LvInfos.N.VgName` indicates the name of the volume group where the logical volume to be migrated is located.<br><br>   * `LvmInfo.VgInfos.N.PvInfos.N.PvName` indicates the name of the physical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.PvInfos.N.PvSize` indicates the size of the physical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.PvInfos.N.PvUUID` indicates the UUID of the physical volume to be migrated.<br><br>   * `LvmInfo.VgInfos.N.PvInfos.N.VgName` indicates the name of the volume group where the physical volume to be migrated is located.<br><br>   * `LvmInfo.VgInfos.N.VgName` indicates the name of the logical volume group to be migrated.<br><br>   * `LvmInfo.VgInfos.N.VgSize` indicates the new size of the logical volume group to be migrated after the size is adjusted.<br><br>   * `LvmInfo.VgInfos.N.VgUUID` indicates the UUID of the logical volume group to be migrated.<br><br>* Added new error codes:<br><br>   * 400, LimitExceeded.MinimumSystemDiskSize<br><br>   * 400, MissingParameter.BlockDevices<br><br>   * 400, MissingParameter.Format<br><br>   * 400, MissingParameter.LvInfos<br><br>   * 400, MissingParameter.LvName<br><br>   * 400, MissingParameter.LvPath<br><br>   * 400, MissingParameter.LvSize<br><br>   * 400, MissingParameter.LvUUID<br><br>   * 400, MissingParameter.PvInfos<br><br>   * 400, MissingParameter.PvName<br><br>   * 400, MissingParameter.PvSize<br><br>   * 400, MissingParameter.PvUUID<br><br>   * 400, MissingParameter.VgName<br><br>   * 400, MissingParameter.VgSize<br><br>   * 400, MissingParameter.VgUUID |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Added response parameters:<br><br>The `LvmInfo` parameter, which indicates the LVM information of the migration target, is added to the `Jobs` structure. ||


<span id="N3HI6dS9"></span>
## May 2025


|API |Change record |Associated feature |
|---|---|---|
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |Add new error code:<br><br>400, InvalidDestinationInstanceStatus.Malformed |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Added response parameters:<br><br>Jobs structure added MigrationSourceInfo parameter, representing the migration source information. ||


<span id="N3HI6dS9"></span>
## April 2025


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added response parameters:<br><br>The `Sources.Partitions` structure is added with:<br><br><br>* `PartitionName`, indicates disk partition name.<br><br>* `PartitionUsedSize`, indicates disk partition usage. |Migration source |


&nbsp;

<span id="N3HI6dS9"></span>
## February 2025


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added response parameters:<br><br>`Sources` structure is added with the `MigrationSourceDescription` parameter, indicating migration source description. |Migration source |
|[DeleteMigrationSource](https://docs.byteplus.com/en/docs/smc/DeleteMigrationSource) |Added new error codes:<br><br>412, InvalidMigrationSource.InUse ||
|[ModifyMigrationSourceAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationSourceAttribute) |* Added request parameter:<br><br><br>`MigrationSourceDescription`, optional, indicating the description of the migration source<br><br><br>* Added new error codes:<br><br>   * 400, InvalidMigrationSourceDescription.Malformed<br><br>   * 400, InvalidMigrationSourceName.Malformed ||
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |Added error code:<br><br><br>* 400, InvalidCustomImageName.Malformed<br><br>* 400, InvalidDestinationInstanceType.Unsupported<br><br>* 400, InvalidDiskConfigForMigration.Unsupported<br><br>* 400, InvalidInstanceForMigration.Unsupported<br><br>* 400, InvalidInstanceTypeForMigtation.Unsupported<br><br>* 400, InvalidLicenseTypeForMigration.Unsupported<br><br>* 400, InvalidMigrationSourceForSystemMigration.Unsupported<br><br>* 400, InvalidMigrationType.Unsupported<br><br>* 400, InvalidOSTypeForFileMigration.Unsupported<br><br>* 400, InvalidVolumeTypeForCreateWholeImage.UnSupported<br><br>* 400, LimitExceeded.MaximumSecurityGroupCount<br><br>* 400, LimitExceeded.MaximumVolumes<br><br>* 400, MissingParameter.NetworkTransitionMode<br><br>* 400, MissingParameter.SyncType<br><br>* 404, InvalidInstance.NotFound<br><br>* 412, PendingVerification |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Added error code:<br><br><br>* 400, LimitExceeded.MaximumResourceIds<br><br>* 404, InvalidMigrationSource.NotFound ||
|[ChangeMigrationJobAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationJobAttribute) |Added new error codes:<br><br><br>* 400, InvalidDestinationTypeForOperate.Unsupported<br><br>* 400, InvalidJobStateForOperate.Unsupported<br><br>* 400, InvalidNetworkTransitionMode.Malformed<br><br>* 404, InvalidSourceTransferEip.NotFound<br><br>* 404, InvalidSourceTransferPrivateIp.NotFound<br><br>* 404, InvalidTransferEip.NotFound<br><br>* 412, OperationDenied.AgentNeedUpgrade ||
|[DescribeMigrationLogs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationLogs) |Added error code:<br><br><br>* 404, InvalidMigrationJob.NotFound<br><br>* 404, InvalidMigrationJobLog.NotFound ||
|[TagResources](https://docs.byteplus.com/en/docs/smc/TagResources) |* Added error code:<br><br><br>     400, MissingParameter.Tags<br><br><br>* Added a single error code for batch operations:<br><br><br>      MissingParameter.ResourceIds |Tag |
|[UnTagResources](https://docs.byteplus.com/en/docs/smc/UnTagResources) |* Added new error codes:<br><br><br>     400, LimitExceeded.MaximumTags<br><br><br>* Added batch operation single error code .<br><br><br>      InvalidTagKey.Malformed ||


<span id=".MjAyNOW5tDEx5pyI"></span>
## November 2024


|API |Change record |Associated feature |
|---|---|---|
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Added request parameter:<br><br>   `DestinationConfig.AutoReplicate` (optional), indicates whether the migration task automatically starts migration after pre\-check.<br><br>* Updated error code:<br><br>   400, InvalidSecurityGroupPermission.Conflict, description updated to "The migration service requires the destination instance to enable ports 8080, 22, 5201, and 5986. Please check the destination instance's security group rules." |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |* Updated request parameter:<br><br>   The `MigrationJobStateSourceState` parameters is added with new enumeration values:<br><br>   * `Pending`, to be started.<br><br>* Added response parameters:<br><br>   `Jobs.DestinationConfig` structure is added with the `AutoReplicate` parameter, indicating whether the migration task automatically starts migration after pre\-checking. ||
|[ChangeMigrationJobAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationJobAttribute) |Added request parameter:<br><br>`NetworkTransitionMode` (optional), indicating the network transmission mode. ||


<span id=".MjAyNOW5tDEw5pyI"></span>
## October 2024


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Updated request parameter:<br><br>New enumeration values added to the `MigrationJobStateSourceState` parameter:<br><br><br>* `Pausing`, Pausing.<br><br>* `Paused`, has been paused. |Migration task |


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added response parameters:<br><br>Sources.InstanceInfo structure is added with:<br><br><br>* `BlkNoneInstall`, indicates whether the source instance has blk\-none installed.<br><br>* `Virtio11CanInstall`, indicates whether the source instance supports Virtio1.1 installation. |Migration source |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Added request parameter:<br><br><br>* The new `MigrationSourceIds.N` parameter is added. After this parameter is passed in, corresponding migration task will be filtered based on migration source. |Migration task |


<span id=".MjAyNOW5tDA35pyIMTjml6U="></span>
## July 2024


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added response parameters:<br><br><br>* Added `SuggestSyncType` parameter, representing the recommended migration method.<br><br>* Added `SyncTypeSupportStatuses` structure, representing migration methods supported by the migration source. |Migration source |
|[DescribeMigrationSystemSupportTypes](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSystemSupportTypes) |Added new API for querying operating systems on the source server that support migration to target operating systems. |Migration task |
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Updated request parameter:<br><br>   * `DestinationConfig.DestinationSystem` parameter adds a new enumeration value `VeLinux20Centos`, indicating the migration to the VeLinux 2.0 CentOS\-compatible operating system.<br><br>* Added new error code:<br><br>   400, InvalidSystemVolumeSize.Malformed ||


<span id=".MjAyNOW5tDA15pyIMjLml6U="></span>
## May 2024


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |* Added response parameter:<br><br>   * Sources.DiskInfo structure adds the following parameters:<br><br>      * `DiskName`, drive letter of the disk.<br><br>      * `FileSystemFormat`, disk file system format.<br><br>      * `IsSystemDisk`, whether the disk is a system disk.<br><br>* Source structure is added with the `LvmInfo` parameter, indicating migration source LVM information. |Migration source |
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Modify request parameters<br><br>   * The `DiskConfigs.N.DiskIndex` parameter is set as a required parameter.<br><br>* Added error code .<br><br>   * InvalidFilesystemType.Unsupported<br><br>   * InvalidLVMStatus.Unsupported<br><br>   * InvalidMigrationCheckResult.Unsupported<br><br>   * InvalidRsyncStatus.Unsupported<br><br>   * LimitExceeded.MinimumPartitionSize<br><br>   * QuotaExceeded.GeneralCpu<br><br>* Error code modification:<br><br>   * The InvalidSecurityGroupPermission.Conflict description is modified to “Migration service requires the destination instance to enable ports 8080, 22, and 5986; please check the destination instance security group rule.”<br><br>   * QuotaExceeded.Cpu Description is modified to “The maximum number of CPUs that can be created has been reached. The migration service will create temporary instances; please ensure the destination Availability Zone's CPU count has not reached its limit.”<br><br>   * QuotaExceeded.Common error code:<br><br>      * The error message is modified to “You've reached the limit of CPUs, volumes, and general CPUs that you can create; please submit a ticket to request an increase in quota.”<br><br>      * The description is modified to “The maximum number of CPUs, volumes, and general CPUs that can be created has been reached. The migration service will create volumes and ECS instance in the destination region; please ensure the destination region has at least one Availability Zone with a sufficient volume and CPU balance to meet migration service requirements.”<br><br>   * The description of QuotaExceeded.Volume is modified to "The maximum capacity of the volume that can be created has been reached. The migration service will create a temporary volume. Please ensure that the capacity of this type of volume in the target region has not reached the limit."<br><br>   * The error message for LimitExceeded.MaximumDiskSize is modified to "The size of disk exceeds the maximum limit."<br><br>* Deleted error code:<br><br>   * QuotaExceeded.GereralCpu |Migration task |


<span id=".MjAyNOW5tDA05pyIMDLml6U="></span>
## April 2024


|API |Change record |Associated feature |
|---|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/smc/TagResources) |* Updated request parameter:<br><br>   * New limit added to the `Tags.N.Key` parameter: Cannot start with `sys:` in any case. |Tag |
|[UnTagResources](https://docs.byteplus.com/en/docs/smc/UnTagResources) |* Updated request parameter:<br><br>   * New limit added to the `Tags.N.Key` parameter: Cannot start with `sys:` in any case. ||
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |* Updated request parameter:<br><br>   * `PageSize`, the value range is modified to 1~50.<br><br>* Added response parameters:<br><br>   * `Sources.` `InstanceInfo` structure is added with the `BlkNoneCanInstall` parameter, indicating whether the source instance supports installing blk\-none. |Migration source |
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Added request parameter:<br><br>   * `DestinationConfig.AutoInstallBlkNone`, indicating whether to automatically install blk\-none for the target instance or target image<br><br>* Updated request parameter:<br><br>   * New limit added to the `Tags.N.Key` parameter: Cannot start with `sys:` in any case.<br><br>* Added new error codes:<br><br>   * 400, InvalidSyncTypeForMigration.Unsupported, the specified replication Type for migration task does not support migration<br><br>   * 412, OperationDenied.SnapshotServiceUnavailable, the specified operation was denied because the snapshot service is not activated. |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |* Updated request parameter:<br><br>   * `MigrationJobStateSourceState` parameteris added new enumeration value:<br><br>      * `Terminated`, terminated.<br><br>      * `Terminating`, terminating.<br><br>      * `Warning`, exception.<br><br>   * `PageSize`, value range modified to 1~50.<br><br>* Added response parameters:<br><br>   * `Jobs` structure adds `TemporaryResources`, representing temporary resource information. ||


<span id=".MjAyNOW5tDAx5pyIMTjml6U="></span>
## January 2024


|API |Change record |Associated feature |
|---|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/smc/TagResources) |Added new API for creating and associating tags for the specified SMC migration source and migration task. |Tag |
|[UnTagResources](https://docs.byteplus.com/en/docs/smc/UnTagResources) |Added new API for disassociating and deleting tags for the specified SMC migration source and migration task. ||
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |* Added request parameter:<br><br>   * `TagFilters.N.Key`, representing the tag key of user tags.<br><br>   * `TagFilters.N.Values.N`, representing the tag value of the user tag<br><br>* Added Response parameters:<br><br>   * `ImageInfo.KernelVersion`, representing the kernel version of the image<br><br>   * `InstanceInfo.Virtio11Install`, indicating whether the Virtio1.1 driver is installed on the source instance<br><br>   * `LastMigrationJobInfo.DestinationType`, representing the target type of the latest migration task<br><br>   * `LastMigrationJobInfo.ProjectName`, representing the project to which the migration task belongs<br><br>   * `Tags`, representing the tag information of the migration source<br><br>* Added new error codes:<br><br>   * 400, InvalidTagFilterKey.Conflict, the specified tag filter key already exists<br><br>   * 400, InvalidTagFilterKey.Malformed, the specified Tag key is invalid.<br><br>   * 400, InvalidTagFilterValue.Malformed, the specified tag filter value already exists.<br><br>   * 400, LimitExceeded.MaximumTagFilterKeys, the specified tag filter key exceeds the maximum limit.<br><br>   * 400, LimitExceeded.MaximumTagFilterResults, the number of resources filtered by tags exceeds the upper limit.<br><br>   * 400, LimitExceeded.MaximumTagFilterValues, the specified tag filter value exceeds the maximum limit. |Migration source |
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Added request parameter:<br><br>   * `DestinationConfig.AutoInstallVirtio11`, indicating whether to auto\-install the virtio1.1 driver.<br><br>   * `Tag.N.Key`, represents the tag key of the user tag.<br><br>   * `Tag.N.Value`, represents the tag value of the user tag.<br><br>* Added new error codes:<br><br>   * 400, InvalidTagKey.Malformed, the specified tag key is invalid.<br><br>   * 400, InvalidTagValue.Malformed, the specified tag value is invalid.<br><br>   * 400, LimitExceeded.MaximumTags, the specified number of tags exceeds the maximum limit.<br><br>   * 409, InvalidTagKey.Conflict, the specified tag key already exists. |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |* Added request parameter:<br><br>   * `TagFilters.N.Key`, representing the tag key of user tags.<br><br>   * `TagFilters.N.Values.N`, representing the tag value of the user tag<br><br>* Added response parameters:<br><br>   * `DestinationConfig.AutoInstallVirtio11`, indicating whether Virtio1.1 drivers are automatically installed.<br><br>   * `SourceProjectName`, representing the project to which the migration source of the migration task belongs.<br><br>   * `Tags`, representing the tag information of the migration source<br><br>* Added new error codes:<br><br>   * 400, InvalidTagFilterKey.Conflict, the specified tag filter key already exists<br><br>   * 400, InvalidTagFilterKey.Malformed, the specified Tag key is invalid.<br><br>   * 400, InvalidTagFilterValue.Malformed, the specified tag filter value already exists.<br><br>   * 400, LimitExceeded.MaximumTagFilterKeys, the specified tag filter key exceeds the maximum limit.<br><br>   * 400, LimitExceeded.MaximumTagFilterResults, the number of resources filtered by tags exceeds the upper limit.<br><br>   * 400, LimitExceeded.MaximumTagFilterValues, the specified tag filter value exceeds the maximum limit. ||


<span id=".MjAyM-W5tDEx5pyIMjfml6U="></span>
## November 2023


|API |Change record |Associated feature |
|---|---|---|
|[ModifyMigrationSourceAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationSourceAttribute) |Added new API for modifying basic migration source information |Migration source |
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |* Added request parameter:<br><br>   * `ProjectName`, indicating the project to which the migration source belongs.<br><br>* Added response parameters.<br><br>   * `Sources` structure is added with the `ProjectName` parameter, indicating the project to which the migration source belongs.<br><br>* Added new error code:<br><br>   * 400, InvalidProjectName.Malformed, the specified ProjectName is invalid. ||
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Added request parameter:<br><br>   * `ProjectName`, indicates the project the migration task belongs to.<br><br>* Added new error code:<br><br>   * 400, InvalidProjectName.Malformed, the specified ProjectName is invalid. |Migration task |
|[ChangeMigrationJobAttribute](https://docs.byteplus.com/en/docs/smc/ModifyMigrationJobAttribute) |Added new API for modifying basic information of migration task. ||
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |* Added request parameter:<br><br>   * `ProjectName`, representing the project to which the migration task belongs.<br><br>* Added response parameter:<br><br>   * The `Jobs` structure is added with the `ProjectName` parameter, representing the project to which the migration task belongs.<br><br>* Added new error code:<br><br>   * 400, InvalidProjectName.Malformed, the specified ProjectName is invalid. ||


<span id=".MjAyM-W5tDA55pyIMTPml6U="></span>
## September 2023


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added a new interface for querying migration source information. |Migration source |
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |* Added request parameter:<br><br>   * `DestinationConfig.DestinationSystem`, representing the target operating system.<br><br>* Modified request parameter:<br><br>   * `DestinationConfig.DestinationType`, added enumeration value:<br><br>      * `ECSSystem`, representing the operating system of the ECS instance.<br><br>   * `SyncConfig.SyncType`, changed to an optional parameter.<br><br>   * `SyncConfig.TriggerLastSync`, modified to an optional parameter.<br><br>* Delete error code:<br><br>   * 400, MissingParameter.TriggerLastSync, parameter TriggerLastSync cannot be empty. |Migration task |
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |* Added request parameter:<br><br>   * `DestinationType.N`, which filters migration task based on the Migration Target Type<br><br>* Added response parameters<br><br>   * `SystemConfig.Jobs` structure, added `SystemConfig` parameter, representing operating system configuration<br><br>   * `SystemConfig.Jobs.DestinationConfig` structure is added with the `DestinationSystem` parameter, representing target operating system ||


<span id=".MjAyM-W5tDA35pyIMTjml6U="></span>
## July 2023


|API |Change record |Associated feature |
|---|---|---|
|[DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) |Added new API for querying migration source information. |Migration source |
|[DeleteMigrationSource](https://docs.byteplus.com/en/docs/smc/DeleteMigrationSource) |Added new API for deleting a migration source. ||
|[CreateMigrationJob](https://docs.byteplus.com/en/docs/smc/CreateMigrationJob) |Add a new interface for creating migration tasks. |Migration task |
|[DeleteMigrationJob](https://docs.byteplus.com/en/docs/smc/DeleteMigrationJob) |Added a new interface for deleting a migration task. ||
|[DescribeMigrationJobs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs) |Added new API for querying migration task information. ||
|[DescribeMigrationLogs](https://docs.byteplus.com/en/docs/smc/DescribeMigrationLogs) |Add a new interface for querying migration logs. ||
|[SetIncrementalSyncInterval](https://docs.byteplus.com/en/docs/smc/SetIncrementalSyncInterval) |Added new API for setting Incremental Synchronization. ||
|[TriggerLastIncrementalSync](https://docs.byteplus.com/en/docs/smc/TriggerLastIncrementalSync) |Added new API for performing the last Incremental Synchronization. ||
