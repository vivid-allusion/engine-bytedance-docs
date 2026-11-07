---
title: "DescribeMigrationSources - Queries migration source information"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/DescribeMigrationSources"
---

Call the DescribeMigrationSources operation to query migration source information.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeMigrationSources&groupName=Migration%20Source&serviceCode=smc&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the request parameters specific to this operation and some common parameters are listed below. For more information, refer to [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|PLLo9u">必选</span> `Sample value: DescribeMigrationSources`

The operation that you want to perform. Valid value: DescribeMigrationSources.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|daKxS2">必选</span> `Sample value: 2020-04-01`

The API version. Valid value: 2020\-04\-01.



**Order ** <span data-label="purple">string </span>`Optional` `Sample value: Desc`

The sorting order. Valid values:


* Desc: Descending.

* Asc: Ascending.



**OrderByColumn ** <span data-label="purple">string </span>`Optional` `Sample value: CreatedAt`

The sorting field. Valid values:


* CreatedAt: The import time.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Sample value: 1`

The page number.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Sample value: 10`

The page size.


* Valid range: 1–50.

* Default value: 10



**ProjectName ** <span data-label="purple">string </span>`Optional` `Sample value: project_a`

The project to which the migration source belongs. Each migration source can belong to only one project.


* Only letters, digits, underscores (_), hyphens (\-), and dots (.) are allowed.

* The length is limited to 64 characters.



**SourceId ** <span data-label="purple">string </span>`Optional` `Sample value: s-3tiegs1y963vj0******`

The migration source ID, which can be obtained when you import the migration source or by calling this operation.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when you query migration source information by migration source ID.</div>




**SourceName ** <span data-label="purple">string </span>`Optional` `Sample value: Local VM`

The migration source name. It can contain up to 255 characters in length.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is required when you query migration source information by migration source name.</div>




**SourceState ** <span data-label="purple">string </span>`Optional` `Sample value: Online`

The migration source status. Valid values:


* Online: Online.

* Offline: Offline.

* Migrating: Migrating.

* Error: Abnormal.



**SourceType ** <span data-label="purple">string </span>`Optional` `Sample value: Normal`

The migration source type. Value:


* Normal: Common migration.

* Batch: One\-click migration.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Sample value: TagFilters.1.Key=k1&Tags.2.Key=k2`

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



* <div data-tips="true" data-tips-type="tip">To pass in this parameter, you need to pass in TagFilters.N.Key first.</div>


* <div data-tips="true" data-tips-type="tip">If you do not pass in the TagFilters.N.Key parameter, all tag values corresponding to the same tag key are queried.</div>


* <div data-tips="true" data-tips-type="tip">If you specify an empty string, you query tags with an empty tag value.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this operation are listed below. For more information, refer to the [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageNumber ** <span data-label="purple">integer </span>`Sample value: 1`

The page number.



**PageSize ** <span data-label="purple">integer </span>`Sample value: 10`

The page size.



**Sources ** <span data-label="purple">object[] </span>`Sample value: --`

The information of the migration source that meets the conditions.


**AgentVersion ** <span data-label="purple">string </span>`Sample value: linux-1.4`

The migration Agent version.



**CreatedAt ** <span data-label="purple">string </span>`Sample value: 2023-06-01T10:27:16+08:00`

The time when the migration source is imported.



**DiskInfo ** <span data-label="purple">object[] </span>`Sample value: --`

The migration source disk information.


**DiskUsedSize ** <span data-label="purple">long </span>`Sample value: 100`

The disk usage. Unit: Bytes.



**DiskIndex ** <span data-label="purple">integer </span>`Sample value: 0`

The disk index.



**DiskName ** <span data-label="purple">string </span>`Sample value: vda`

The drive letter.



**DiskSize ** <span data-label="purple">integer </span>`Sample value: 20`

The disk capacity. Unit: GB.



**FileSystemFormat ** <span data-label="purple">string </span>`Sample value: vfat`

The file system format.



**IsSystemDisk ** <span data-label="purple">boolean </span>`Sample value: true`

Whether it is a system volume. Value:


* true: Yes, it is a system volume.

* false: No, it is not a system volume.



**Partitions ** <span data-label="purple">object[] </span>`Sample value: --`

The disk partition information.


**FileSystemFormat ** <span data-label="purple">string </span>`Sample value: vfat`

The file system format.



**Mountpoint ** <span data-label="purple">string </span>`Sample value: /boot/efi`

The partition mount point.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the return value is empty, the partition is not mounted.</div>




**PartitionIndex ** <span data-label="purple">integer </span>`Sample value: 0`

The partition index, starting from `0`.



**PartitionSize ** <span data-label="purple">long </span>`Sample value: 209715200`

The partition capacity. Unit: Bytes.



**PartitionUsedSize ** <span data-label="purple">long </span>`Sample value: 200015200`

The disk partition usage. Unit: Bytes.



**PartitionName ** <span data-label="purple">string </span>`Sample value: vda1`

The disk partition name.





**Hostname ** <span data-label="purple">string </span>`Sample value: localhost.localdomain`

The hostname of the migration source.



**ImageInfo ** <span data-label="purple">object </span>`Sample value: --`

The migration source image information.


**BootMode ** <span data-label="purple">string </span>`Sample value: BIOS`

The system boot mode. Valid values:


* UEFI.

* BIOS.



**KernelVersion ** <span data-label="purple">string </span>`Sample value: 3.10.0-1160.102.1.el7.x86_64`

The kernel version.



**OS ** <span data-label="purple">string </span>`Sample value: Linux`

The operating system. Valid values:


* Linux.

* Windows.



**Platform ** <span data-label="purple">string </span>`Sample value: CentOS`

The operating system platform.



**PlatformVersion ** <span data-label="purple">string </span>`Sample value: 7.9.2009`

The operating system version number.



**VirtualizationSystem ** <span data-label="purple">string </span>`Sample value: kvm`

The virtualization system.




**InstanceInfo ** <span data-label="purple">object </span>`Sample value: --`

The information of the migration source instance.


**BlkNoneCanInstall ** <span data-label="purple">boolean </span>`Sample value: true`

Whether blk\-none can be installed on the source instance. Value:


* true: Supported.

* false: Not supported.



**BlkNoneInstall ** <span data-label="purple">boolean </span>`Sample value: true`

Whether blk\-none has been installed on the source instance. Value:


* true: Installed.

* false: Uninstalled.



**InnerInstance ** <span data-label="purple">boolean </span>`Sample value: false`

Whether the source instance is a BytePlus ECS instance. Value:


* true: The source instance is a BytePlus ECS instance.

* false: The source instance is not a BytePlus ECS instance.



**InstanceId ** <span data-label="purple">string </span>`Sample value: i-3teco18f1w5a71****`

The ID of the source instance in BytePlus.



**RegionId ** <span data-label="purple">string </span>`Sample value: cn-beijing`

The region of the source instance in BytePlus.



**Virtio11CanInstall ** <span data-label="purple">boolean </span>`Sample value: true`

Whether Virtio11 can be installed on the source instance. Value:


* true: Supported.

* false: Not supported.



**Virtio11Install ** <span data-label="purple">boolean </span>`Sample value: true`

Whether the source instance has the Virtio 1.1 driver installed. Valid values:


* true: Installed.

* false: Uninstalled.




**LastMigrationJobInfo ** <span data-label="purple">object </span>`Sample value: --`

The information of the most recent migration task.


**DestinationType ** <span data-label="purple">string </span>`Sample value: ECSInstance`

The destination type of the most recent migration task. Value:


* ECSInstance: ECS instance.

* ECSImage: ECS instance image.

* ECSSystem: ECS instance operating system.



**MigrationJobId ** <span data-label="purple">string </span>`Sample value: job-3tiegs1y963vj0******`

The ID of the most recent migration task.



**MigrationJobName ** <span data-label="purple">string </span>`Sample value: VMware Migration`

The name of the most recent migration task.



**MigrationJobState ** <span data-label="purple">string </span>`Sample value: Replicating`

The status of the most recent migration task. Valid values:


* Preparing: Preparing.

* Replicating: Migrating.

* Success: Completed.

* Failed: Failed.

* Waiting: Waiting.

* Cleaning: Clearing.



**ProjectName ** <span data-label="purple">string </span>`Sample value: project_a`

The project to which the migration task belongs.




**LvmInfo ** <span data-label="purple">object </span>`Sample value: --`

The LVM information of the migration source.


**VgInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The list of logical volume groups.


**Format ** <span data-label="purple">string </span>`Sample value: lvm2`

The logical volume group format.



**LvInfos ** <span data-label="purple">object[] </span>`Sample value: --`

The list of logical volume information under the logical volume group.


**BlockDevices ** <span data-label="purple">string[] </span>`Sample value: ["/dev/vdb1"]`

The list of disk block devices used by the logical volume.



**FsType ** <span data-label="purple">string </span>`Sample value: --`

The file system type with which the logical volume is formatted.



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




**VgName ** <span data-label="purple">string </span>`Sample value: vg_01`

The logical volume group name.



**VgSize ** <span data-label="purple">long </span>`Sample value: 1019215872`

The size of the logical volume group. Unit: Bytes.



**VgUUID ** <span data-label="purple">string </span>`Sample value: Y2apS5-w7yK-*****`

The UUID of the logical volume group.





**MigrationSourceDescription ** <span data-label="purple">string </span>`Sample value: Local virtual machine`

The migration source description.



**PrivateIpAddress ** <span data-label="purple">string </span>`Sample value: 172.xx.xx.xxx`

The private IP address of the migration source.



**ProjectName ** <span data-label="purple">string </span>`Sample value: project_a`

The project to which the migration source belongs.



**PublicIpAddress ** <span data-label="purple">string </span>`Sample value: 119.x.xxx.xxx`

The EIP of the migration source.



**SourceId ** <span data-label="purple">string </span>`Sample value: s-iegs1y963vj0******`

The migration source ID.



**SourceName ** <span data-label="purple">string </span>`Sample value: s-ycg9hd3nfb8r****`

The migration source name.



**SourceState ** <span data-label="purple">string </span>`Sample value: Migrating`

The migration source status.



**SourceType ** <span data-label="purple">string </span>`Sample value: Normal`

The migration source type.



**SuggestSyncType ** <span data-label="purple">string </span>`Sample value: Block`

The recommended migration method. Value:


* File: File replication.

* Block: Block replication.



**SyncTypeSupportStatuses ** <span data-label="purple">object[] </span>`Sample value: --`

The migration method supported by the migration source.


**BlockReason ** <span data-label="purple">string </span>`Sample value: --`

The reason why this migration method is not supported.



**IsSupport ** <span data-label="purple">boolean </span>`Sample value: true`

Whether this migration method is supported. Value:


* true: Supported.

* false: Not supported.



**SyncType ** <span data-label="purple">string </span>`Sample value: File`

The migration method. Value:


* File: File replication.

* Block: Block replication.




**SystemInfo ** <span data-label="purple">object </span>`Sample value: --`

The migration source system information.


**Architecture ** <span data-label="purple">string </span>`Sample value: x86_64`

The CPU architecture. Value:


* x86_64



**CPU ** <span data-label="purple">integer </span>`Sample value: 2`

The number of CPU cores in the instance.



**CPUUsage ** <span data-label="purple">float </span>`Sample value: 10`

The CPU usage, in percentage. For example, `10` indicates a CPU usage of `10%`.



**Memory ** <span data-label="purple">long </span>`Sample value: 8236490752`

The memory size. Unit: Bytes.



**MemoryUsage ** <span data-label="purple">float </span>`Sample value: 10`

The memory usage, in percent. For example, `47.86` means the memory usage is `47.86%`.




**Tags ** <span data-label="purple">object[] </span>`Sample value: --`

The tag information of the migration source.


**Key ** <span data-label="purple">string </span>`Sample value: Key=k1`

The specified tag key when querying resources based on tags.



**Value ** <span data-label="purple">string </span>`Sample value: Value=v1`

The tag value specified when resources are queried based on tags.





**TotalCount ** <span data-label="purple">integer </span>`Sample value: 1`

The total number of migration sources.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
GET /?Action=DescribeMigrationSources&Version=2020-04-01 HTTP/1.1
Host:  smc.byteplusapi.com
Region: cn-beijing
Service: smc
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202306021637410F150D*****",
    "Action": "DescribeMigrationSources",
    "Version": "2020-04-01",
    "Service": "smc",
    "Region": "cn-beijing"
  },
  "Result": {
    "TotalCount": 1,
    "PageNumber": 1,
    "PageSize": 10,
    "Sources": [
      {
        "SourceId": "s-ycg9hd3nfb8rx6****",
        "SourceName": "s-ycg9hd3nfb8r****",
        "Hostname": "localhost.localdomain",
        "CreatedAt": "2023-06-01T10:27:16+08:00",
        "SourceState": "Migrating",
        "PublicIpAddress": "119.x.xxx.xxx",
        "PrivateIpAddress": "172.xx.xx.xxx",
        "MigrationSourceDescription": "Local VM",
        "AgentVersion": "linux-1.4",
        "ProjectName": "project_a",
        "SourceType": "Normal",
        "SuggestSyncType": "Block",
        "SyncTypeSupportStatuses": [
          {
            "SyncType": "File",
            "IsSupport": true,
            "BlockReason": ""
          },
          {
            "SyncType": "Block",
            "IsSupport": true,
            "BlockReason": ""
          }
        ],
        "SystemInfo": {
          "CPU": 1,
          "Memory": 1019027456,
          "CPUUsage": 4,
          "MemoryUsage": 47.86,
          "Architecture": "x86_64"
        },
        "ImageInfo": {
          "OS": "Linux",
          "Platform": "CentOS",
          "PlatformVersion": "7.9.2009",
          "BootMode": "UEFI",
          "VirtualizationSystem": "",
          "KernelVersion": "3.10.0-1160.102.1.el7.x86_64"
        },
        "InstanceInfo": {
          "InnerInstance": "true",
          "InstanceId": "i-3teco18f1w5a71****",
          "RegionId": "cn-beijing",
          "Virtio11CanInstall": true,
          "Virtio11Install": true,
          "BlkNoneCanInstall": true,
          "BlkNoneInstall": true
        },
        "DiskInfo": [
          {
            "DiskIndex": 0,
            "DiskSize": 20,
            "DiskUsedSize": 100,
            "Partitions": [
              {
                "PartitionIndex": 0,
                "PartitionSize": 209715200,
                "Mountpoint": "/boot/efi",
                "FileSystemFormat": "vfat",
                "PartitionName": "vda1",
                "PartitionUsedSize": "200015200"
              },
              {
                "PartitionIndex": 1,
                "PartitionSize": 1073741824,
                "Mountpoint": "/boot",
                "FileSystemFormat": "xfs",
                "PartitionName": "vdb1",
                "PartitionUsedSize": "1003741824"
              }
            ],
            "FileSystemFormat": "",
            "DiskName": "vda",
            "IsSystemDisk": true
          }
        ],
        "Tags": [
          {
            "Key": "k1",
            "Value": "v1"
          }
        ],
        "LvmInfo": {
          "VgInfos": []
        },
        "LastMigrationJobInfo": {
          "DestinationType": "ECSInstance",
          "ProjectName": "project_a",
          "MigrationJobId": "job-ycg9hghuv7****",
          "MigrationJobName": "VMware Migration",
          "MigrationJobState": "Replicating"
        }
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists the business\-related error codes of the operation. For more information, refer to [Common error codes](https://docs.byteplus.com/en/docs/smc/Public_error_codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |InvalidOrder.Malformed |The specified Order is malformed. |The specified Order value is invalid. |
|400 |InvalidOrderByColumn.Malformed |The specified OrderByColumn is malformed. |The specified OrderByColumn value is invalid. |
|400 |InvalidProjectName.Malformed |The specified ProjectName is malformed. |The specified ProjectName is invalid. |
|400 |InvalidSourceName.Malformed |The specified SourceName is malformed. |The specified SourceName parameter is invalid. |
|400 |InvalidSourceState.Malformed |The specified SourceState is malformed. |The specified SourceState value is invalid. |
|400 |InvalidSourceType.Malformed |The specified SourceType is malformed. |The specified SourceType value is invalid. |
|400 |InvalidTagFilterKey.Conflict |The specified TagFilterKey already exists. |The specified tag filter key already exists. |
|400 |InvalidTagFilterKey.Malformed |The specified TagFilterKey is malformed. |The specified tag key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified TagFilterValue already exists. |The specified tag filter value already exists. |
|400 |LimitExceeded.MaximumTagFilterKeys |You've reached the limit on the number of TagFilterKeys that you can set. |The number of tag keys specified for filtering exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterResults |You've reached the limit on the number of resources that you can describe by TagFilters. |The number of resources filtered by tag exceeds the upper limit. |
|400 |LimitExceeded.MaximumTagFilterValues |You've reached the limit on the number of TagFilterValues that you can set. |The number of tag values specified for filtering exceeds the upper limit. |
