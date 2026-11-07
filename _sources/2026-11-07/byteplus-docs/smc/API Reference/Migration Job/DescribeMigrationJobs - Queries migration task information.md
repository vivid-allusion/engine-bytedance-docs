---
title: "DescribeMigrationJobs - Queries migration task information"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/DescribeMigrationJobs"
---

Call the DescribeMigrationJobs operation to query migration task information.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeMigrationJobs&groupName=%E8%BF%81%E7%A7%BB%E4%BB%BB%E5%8A%A1&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|rnGKnN">必选</span> `Sample value: DescribeMigrationJobs`

The operation that you want to perform. Valid value: DescribeMigrationJobs.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|n8vJcy">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**MigrationSourceIds.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: MigrationSourceIds.1=s-3tiegs1y963vj0******&MigrationSourceIds.2=s-9ksguxl923******`

The migration source ID. After this parameter is provided, migration tasks will be filtered based on the migration source. Up to 50 IDs are supported. You can call the [DescribeMigrationSources](https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources) operation to query and obtain the migration source ID.


* Parameter \- N: Specifies the serial number of the migration source.

* Separate multiple migration source IDs with `&`.



**DestinationRegion ** <span data-label="purple">string </span>`Optional` `Sample value: cn-beijing`

The target region. It can contain up to 255 characters in length. You can call the [DescribeRegions](https://docs.byteplus.com/en/docs/ecs/DescribeRegions) operation to query and obtain the region.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when you query migration tasks by target region.</div>




**DestinationType.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: DestinationType.1=ECSInstance&DestinationType.2=ECSImage`

The migration destination type. Up to 5 types are supported. Value:


* ECSInstance: ECS instance.

* ECSImage: ECS instance image.

* ECSSystem: ECS instance operating system.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Parameter \- N: Specifies the serial number of the migration destination type.</div>


* <div data-tips="true" data-tips-type="tip">Separate multiple <code>DestinationType</code> values with <code>&</code>.</div>


* <div data-tips="true" data-tips-type="tip">This parameter is required when you query migration tasks by migration destination type.</div>




**MigrationJobId ** <span data-label="purple">string </span>`Optional` `Sample value: job-3tiegs1y963vj0******`

The migration task ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when you query migration tasks by migration task ID.</div>




**MigrationJobName ** <span data-label="purple">string </span>`Optional` `Sample value: VM migration to ECS`

The migration task name. It can contain up to 255 characters in length.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when you query migration tasks by migration task name.</div>




**MigrationJobState ** <span data-label="purple">string </span>`Optional` `Sample value: Success`

The migration task status. Valid values:


* Preparing: Preparing.

* Replicating: Migrating.

* Success: Completed.

* Failed: Failed.

* Waiting: Waiting.

* Cleaning: Clearing.

* Terminated: Terminated.

* Terminating: Terminating.

* Warning: Abnormal.

* Pausing: Pausing.

* Paused: Paused.

* Pending: To start.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The page number.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

The page size.


* Valid range: 1–50.

* Default value: 10



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the migration task belongs. Each task can only belong to one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1`

The specified tag key when querying resources based on tags.


* Argument \- N: specifies the serial number of the tag key. Valid range: 1–10.

* Separate multiple tag keys with `&`. Duplicate tag keys are not allowed.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you do not pass in the parameter, all tags are queried.</div>


* <div data-tips="true" data-tips-type="tip">When an empty string is passed in, the error code <code>InvalidTagFilterKey.Malformed</code> is returned.</div>




**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Values.1=v1&TagFilters.1.Values.2=v2`

The tag value specified when resources are queried based on tags.


* The first N: the serial number of the tag key. Value range: 1–10.

* The second N: specifies the serial number of a tag value. Value range: 1–3.

* Separate multiple key values with ampersands (`&`).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, you need to pass in <code>TagFilters.N.Key</code> first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Jobs ** <span data-label="purple">object[] </span>`Sample value: --`

The information of the migration task that meets the conditions.


**LvmInfo ** <span data-label="purple">object </span>`Sample value: --`

The LVM information of the migration task.


**VgInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The volume group list of the migration task.


**Format ** <span data-label="purple">string </span>`Sample value: lvm2`

The logical volume group format.



**VgName ** <span data-label="purple">string </span>`Sample value: vg_01`

The logical volume group name.



**VgSize ** <span data-label="purple">long </span>`Sample value: 1019215872`

The size of the logical volume group. Unit: Bytes.



**VgUUID ** <span data-label="purple">string </span>`Sample value: Y2apS5-w7yK-*****`

The UUID of the logical volume group.



**PvInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The list of physical volume information under the logical volume group.


**PvName ** <span data-label="purple">string </span>`Sample value: /dev/vdb1`

The physical volume name.



**PvSize ** <span data-label="purple">long </span>`Sample value: 1019215872`

The size of the physical volume. Unit: Bytes.



**PvUUID ** <span data-label="purple">string </span>`Sample value: h3ey9f-VJAi*****`

The UUID of the physical volume.



**VgName ** <span data-label="purple">string </span>`Sample value: vg_01`

The name of the volume group where the physical volume resides.




**LvInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The list of logical volume information under the logical volume group.


**FsType ** <span data-label="purple">string </span>`Sample value: --`

The file system type with which the logical volume is formatted.



**BlockDevices ** <span data-label="purple">string[] </span>`Sample value: ["/dev/vdb1"]`

The list of disk block devices used by the logical volume.



**LvName ** <span data-label="purple">string </span>`Sample value: lv01`

The logical volume name.



**LvPath ** <span data-label="purple">string </span>`Sample value: /dev/vg_01/lv01`

The logical volume path.



**LvSize ** <span data-label="purple">long </span>`Sample value: 943718400`

The size of the logical volume. Unit: Bytes.



**LvUUID ** <span data-label="purple">string </span>`Sample value: VlMqHc-iZfE-Vo*****`

The UUID of the logical volume.



**LvUsedSize ** <span data-label="purple">long </span>`Sample value: --`

The used capacity of the logical volume. Unit: Bytes.



**MountPoint ** <span data-label="purple">string </span>`Sample value: --`

The logical volume mount point.



**VgName ** <span data-label="purple">string </span>`Sample value: vg_01`

The name of the volume group where the logical volume resides.






**MigrationSourceInfo ** <span data-label="purple">object </span>`Sample value: --`

The migration source information.


**MigrationSourceName ** <span data-label="purple">string </span>`Sample value: s-ydgrjgha*****`

The hostname of the migration source.



**SourceProjectName ** <span data-label="purple">string </span>`Sample value: project_a`

The project to which the migration source belongs.



**MigrationSourceOS ** <span data-label="purple">string </span>`Sample value: Linux`

The migration source operating system. Value:


* Windows.

* Linux.



**MigrationSourcePlatform ** <span data-label="purple">string </span>`Sample value: CentOS`

The migration source operating system platform.



**MigrationSourcePlatformVersion ** <span data-label="purple">string </span>`Sample value: 7.9`

The migration source operating system version.



**MigrationSourcePrivateIp ** <span data-label="purple">string </span>`Sample value: 192.xxx.x.x`

The private IP address of the migration source.



**MigrationSourcePublicIp ** <span data-label="purple">string </span>`Sample value: 10.2xx.xxx.xx`

The EIP of the migration source.



**MigrationSourceState ** <span data-label="purple">string </span>`Sample value: Offline`

The migration source status. Valid values:


* Online: Online.

* Offline: Offline.

* Migrating: Migrating.

* Error: Abnormal.




**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2024-11-05T16:14:03+08:00`

The time when the migration task is created.



**DestinationConfig ** <span data-label="purple">object </span>`Sample value: --`

The target configuration.


**AutoInstallBlkNone ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to automatically install blk\-none for the target instance or target image. Value:

true: Install automatically.

false: Do not install automatically.



**AutoInstallVirtio11 ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to automatically install the Virtio1.1 driver for the target instance or target image. Value:

true: Install automatically.

false: Do not install automatically.



**AutoReplicate ** <span data-label="purple">boolean </span>`Sample value: false`

Whether to automatically start migration when the migration task passes the precheck. Value:


* false: Do not automatically start migration.

* true: Automatically start migration.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is valid only when the source server is migrated to an ECS instance or ECS instance image.</div>




**DestinationSystem ** <span data-label="purple">string </span>`Sample value: VeLinux10Centos`

The target operating system. Value:


* Unknown: unknown.

* VeLinux10Centos: Indicates migration to veLinux 1.0 CentOS Compatible operating system.



**DestinationType ** <span data-label="purple">string </span>`Sample value: ECSInstance`

The destination type.



**ImageId ** <span data-label="purple">string </span>`Sample value: image-3tefr6wgx63vj0****`

The ID of the target image.



**ImageName ** <span data-label="purple">string </span>`Sample value: testImage`

The target image name.



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-3tigy72q3u3vj0x2****`

The target instance ID.



**InstanceName ** <span data-label="purple">string </span>`Sample value: instance-test`

The target instance name.



**Region ** <span data-label="purple">string </span>`Example: cn-beijing`

The target region.




**FinishedAt ** <span data-label="purple">string </span>`Sample value: 2024-11-05T16:46:29+08:00`

The time when the migration task finishes.



**LastSyncTime ** <span data-label="purple">string </span>`Sample value: 2024-11-05T16:14:03+08:00`

The most recent synchronization time.



**MigrationJobDescription ** <span data-label="purple">string </span>`Sample value: Migrate local virtual machine`

The migration task description.



**MigrationJobId ** <span data-label="purple">string </span>`Sample value: job-3tiegs1y963vj0******`

The migration task ID.



**MigrationJobName ** <span data-label="purple">string </span>`Sample value: VM migration to ECS`

The migration task name.



**MigrationSourceId ** <span data-label="purple">string </span>`Sample value: s-iegs1y963vj0******`

The migration source ID.



**MigrationSourceName ** <span data-label="purple">string </span>`Sample value: s-iegs1y963vj0****`

The migration source name.



**MigrationStateTips ** <span data-label="purple">string </span>`Sample value: --`

The status prompt information of the migration task.



**NetworkConfig ** <span data-label="purple">object </span>`Sample value: --`

The network migration configuration.


**BandwidthLimit ** <span data-label="purple">integer </span>`Sample value: 5`

The network transfer bandwidth. Unit: Mbps.



**NetworkTransitionMode ** <span data-label="purple">string </span>`Sample value: PublicNetwork`

The network transmission mode. Value:


* PublicNetwork: Public network transmission.

* VPC: Intranet transmission.



**SubnetId ** <span data-label="purple">string </span>`Sample value: subnet-3tispp1nai4e8i****`

Subnet ID.



**TransferIP ** <span data-label="purple">string </span>`Sample value: 172.0.**.**`

The network transfer IP address.



**VpcId ** <span data-label="purple">string </span>`Sample value: vpc-bp15zkdt37pq72zv****`

VPC ID.




**Progress ** <span data-label="purple">integer </span>`Sample value: 10`

The progress of the migration task (expressed as a percentage). For example, `10` indicates the task progress is `10%`.



**ProjectName ** <span data-label="purple">string </span>`Sample value: project_a`

The project to which the migration task belongs.



**SourceProjectName ** <span data-label="purple">string </span>`Sample value: project_a`

The project to which the migration source of the migration task belongs.



**SourceType ** <span data-label="purple">string </span>`Sample value: Normal`

The migration source type. Value:


* Normal: Common migration.

* Batch: One\-click migration.



**StartedAt ** <span data-label="purple">string </span>`Sample value: 2024-11-05T16:14:03+08:00`

The time when the migration task starts.



**State ** <span data-label="purple">string </span>`Sample value: Success`

The status of the migration task. Value:


* Preparing: Preparing.

* Replicating: Migrating.

* Success: Completed.

* Failed: Failed.

* Waiting: Waiting.

* Cleaning: Clearing.

* Terminated: Terminated.

* Terminating: Terminating.

* Warning: Abnormal.

* Pending: To start.



**SyncConfig ** <span data-label="purple">object </span>`Sample value: --`

The migration configuration.


**SyncInterval ** <span data-label="purple">integer </span>`Sample value: 2`

The incremental synchronization interval. Unit: hours.

Valid range: 1–168.



**SyncTimes ** <span data-label="purple">integer </span>`Sample value: 1`

The number of incremental synchronizations.



**SyncType ** <span data-label="purple">string </span>`Sample value: File`

The replication type. Value:


* File: File replication.

* Block: Block replication.



**TriggerLastSync ** <span data-label="purple">boolean </span>`Sample value: true`

Whether to perform only one full data synchronization. Value:


* true: Indicates that only one full data synchronization is performed, and no incremental data synchronization is performed.

* false: Indicates that after one full data synchronization, incremental data synchronization will also be performed at intervals specified by the `SyncConfig.SyncInterval` parameter.




**SystemConfig ** <span data-label="purple">object </span>`Sample value: --`

The operating system configuration.


**SourceImageInfo ** <span data-label="purple">object </span>`Sample value: --`

The instance image information before migration.


**OS ** <span data-label="purple">string </span>`Sample value: Linux`

The operating system. Value:


* Linux: The instance runs on the Linux operating system.

* Windows: The instance runs on the Windows operating system.



**Platform ** <span data-label="purple">string </span>`Sample value: CentOS`

The operating system version.



**PlatformVersion ** <span data-label="purple">string </span>`Sample value: 7.6`

The operating system version number.




**TargetImageInfo ** <span data-label="purple">object </span>`Sample value: --`

The information of the instance image after migration.


**OS ** <span data-label="purple">string </span>`Sample value: Linux`

The operating system. Value:


* Linux: The instance runs on the Linux operating system.

* Windows: The instance runs on the Windows operating system.



**Platform ** <span data-label="purple">string </span>`Sample value: CentOS`

The operating system version.



**PlatformVersion ** <span data-label="purple">string </span>`Sample value: 7.6`

The operating system version number.





**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The information of tags associated with resources.


**Key ** <span data-label="purple">string </span>`Sample value: Key=k1`

The specified tag key when querying resources based on tags.



**Value ** <span data-label="purple">string </span>`Sample value: Value=v1`

The tag value specified when resources are queried based on tags.




**TemporaryResources ** <span data-label="purple">object[] </span>`Sample value: --`

The temporary resource information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is returned only when you query specific task information by passing in the <code>MigrationJobId</code> (migration task ID) parameter.</div>



**AssociatedResource ** <span data-label="purple">object[] </span>`Sample value: --`

The cloud resources associated with this temporary resource.


**ResourceId ** <span data-label="purple">string </span>`Sample value: i-3tigy72q3u3vj0x2****`

The ID of the cloud resource associated with the temporary resource.



**ResourceType ** <span data-label="purple">string </span>`Sample value: Instance`

The type of cloud resource associated with the temporary resource. Value:


* Instance: Instance.

* KeyPair: Key pair.

* Image: Image.

* Volume: Volume.

* SecurityGroup: Security group.

* Subnet: Subnet.

* Vpc: VPC.

* Eip: EIP.




**ProjectName ** <span data-label="purple">string </span>`Sample value: default`

The project to which the temporary resource belongs.



**ResourceId ** <span data-label="purple">string </span>`Sample value: kp-ybp0x6i30gep29******`

The ID of the temporary resource.



**ResourceName ** <span data-label="purple">string </span>`Sample value: MigrationKey-job-yd0d5s8n*****`

The temporary resource name.



**ResourceStatus ** <span data-label="purple">string </span>`Sample value: Exist`

The status of temporary resources. Value:


* Exist: Not deleted.

* Deleted: Deleted.



**ResourceType ** <span data-label="purple">string </span>`Sample value: KeyPair`

The temporary resource type. Value:


* Instance: Instance.

* KeyPair: Key pair.

* Image: Image.

* Volume: Volume.

* SecurityGroup: Security group.

* Subnet: Subnet.

* Vpc: VPC.

* Eip: EIP.





**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The page size.



**TotalCount ** <span data-label="purple">integer </span>`Sample value: 30`

The total number of migration tasks.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeMigrationJobs&Version=2020-04-01&MigrationJobId=job-ycg7dvqn59b5oz**** HTTP/1.1
Host: smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202306051605204303A34A*****",
    "Action": "DescribeMigrationJobs",
    "Version": "2020-04-01",
    "Service": "smc",
    "Region": "cn-beijing"
  },
  "Result": {
    "TotalCount": 16,
    "PageNumber": 1,
    "PageSize": 10,
    "Jobs": [
      {
        "MigrationJobId": "job-ycg79lm7wg7grbxxxx",
        "MigrationJobName": "VM migration to ECS",
        "MigrationJobDescription": "",
        "SourceProjectName": "project_a",
        "CreatedAt": "2024-11-05T16:14:03+08:00",
        "StartedAt": "2024-11-05T16:14:03+08:00",
        "FinishedAt": "",
        "State": "Replicating",
        "Progress": 0,
        "MigrationSourceId": "s-ycg79jgyp8b5ozxxxx",
        "MigrationSourceName": "s-ycg79jgyp8b5oxxxx",
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          }
        ],
        "DestinationConfig": {
          "AutoReplicate": false,
          "Region": "cn-beijing",
          "DestinationType": "ECSInstance",
          "InstanceId": "i-ycg4zh1r13ebgy4xxxx",
          "InstanceName": "VMwareMigrationTarget",
          "ImageId": "",
          "ImageName": "",
          "AutoInstallVirtio11": true,
          "AutoInstallBlkNone": true
        },
        "NetworkConfig": {
          "NetworkTransitionMode": "PublicNetwork",
          "BandwidthLimit": 0,
          "TransferIP": "180.xxx.xx.xxx",
          "VpcId": "",
          "SubnetId": ""
        },
        "SyncConfig": {
          "SyncInterval": 1,
          "TriggerLastSync": false,
          "SyncType": "Block",
          "HasSyncedTimes": ""
        },
        "SystemConfig": {
          "SourceImageInfo": {
            "OS": "Linux",
            "Platform": "CentOS",
            "PlatformVersion": "7.6"
          },
          "TargetImageInfo": {
            "OS": "Linux",
            "Platform": "veLinux",
            "PlatformVersion": "1.0"
          }
        },
        "LvmInfo": {
          "VgInfos": []
        },
        "TemporaryResources": [
          {
            "AssociatedResource": {
              "ResourceId": "i-3tigy72q3u3vj0x2****",
              "ResourceType": "Instance"
            },
            "ProjectName": "default",
            "ResourceId": "kp-ybp0x6i30gep29******",
            "ResourceName": "MigrationKey-job-yd0d5s8n*****",
            "ResourceStatus": "Exist",
            "ResourceType": "KeyPair"
          }
        ],
        "MigrationSourceInfo": {
          "MigrationSourceState": "Error",
          "MigrationSourcePublicIp": "10.xxx.xxx.5",
          "MigrationSourcePrivateIp": "192.xxx.xx.2",
          "MigrationSourcePlatform": "CentOS",
          "MigrationSourcePlatformVersion": "7.9",
          "MigrationSourceOS": "Linux",
          "MigrationSourceName": "s-ydajtznkgpgh9xxfab55",
          "SourceProjectName": "default"
        },
        "MigrationStateTips": "",
        "LastSyncTime": "2024-11-05T16:14:03+08:00"
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDestinationRegion.Malformed |The specified DestinationRegion is malformed. |The specified DestinationRegion value is invalid. |
|400 |InvalidMigrationJobName.Malformed |The specified MigrationJobName is malformed. |The specified MigrationJobName value is invalid. |
|400 |InvalidMigrationJobState.Malformed |The specified MigrationJobState is malformed. |The specified MigrationJobState parameter is invalid. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue already exists. |The specified tag filter value already exists. |
|400 |LimitExceeded.MaximumResourceIds |You've reached the limit on the number of ResourceIds that you can set. |The number of specified resource IDs exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The number of tag keys specified for filtering exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The number of tag values specified for filtering exceeds the upper limit. |
|404 |InvalidMigrationSource.NotFound |The specified migration source does not exist. |The specified migration source does not exist. |
