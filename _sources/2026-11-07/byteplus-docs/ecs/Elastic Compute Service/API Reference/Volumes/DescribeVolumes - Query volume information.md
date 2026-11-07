---
title: "DescribeVolumes - Query volume information"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describevolumes"
---

Call the DescribeVolumes API to list volumes

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeVolumes&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

The section below lists only the unique request parameters for this API and some common parameters For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)



**Action ** <span data-label="purple">string </span><span data-api-tag="require|nWke9r">必选</span> `Example value: DescribeVolumes`

The operation to be performed: DescribeVolumes.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|3GCO7o">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**PageSize ** <span data-label="purple">integer </span>`optional` `Example value: 15`

Page size, up to 100. Default is 15.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example value: 1`

The starting page number defaults to 1



**ZoneId ** <span data-label="purple">string </span>`Optional` `Example: cn-beijing-a`

Available zone ID.



**Kind ** <span data-label="purple">string </span>`optional` `Example value: data`

Volume attributes. Value descriptions are as follows:


* system: System disk.

* data: Data disk.



**VolumeType ** <span data-label="purple">string </span>`Optional` `Example value: ESSD_PL0`

Cloud disk type, with the following values:


* PTSSD: Performance SSD.

* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* Extreme Speed SSD Cloud volume, FlexPL specification.

* TSSD_TL0: Throughput SSD volume.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For detailed information on volume specifications, see <a href="https://docs.byteplus.com/en/docs/ecs/Volume-specifications">volume specifications</a>.</div>




**VolumeStatus ** <span data-label="purple">string </span>`Optional` `Example: creating`

Volume status, with values explained as follows:


* Available.

* Attaching.

* Attached: Mounted.

* Detaching: Unmounting.

* Creating: In process.

* Deleting: In process.

* Error: Error.

* Extending: Expanding.

* terminatesuspend: Pending release.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When unsubscribing from yearly or monthly volume, the volume status changes to pending release.</div>




**InstanceId ** <span data-label="purple">string </span>`Optional` `Example value: i-3ti74if6ay3vj0x1****`

ECS instance ID that mounts the volume.



**VolumeName ** <span data-label="purple">string </span>`Optional` `Example value: test-volume`

Display name for the volume. The naming conventions are as follows:


* The first character can only be a Chinese character, letter, or underscore (_).

* May include Chinese characters, letters, numbers, underscores (_), or hyphens (\-).

   The name must be between 1 and 128 characters in length.



**SysTagVisible ** <span data-label="purple">boolean </span>`Optional` `Example value: true`

Invalid parameter (default shows system label).



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Example value: key`

Specifying the tag key when querying resources by tags. Description as follows:


* TagFilters.N.Key: N represents the sequence number of the tag key. Value range: 1~10.

* Use & to separate multiple tag keys. Duplicate keys are not allowed.

* If this parameter is not provided, it implies querying all tags.

* When an empty string is passed, the error code InvalidTagFilterKey.Malformed is returned.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Example value: value`

Specifies the tag value when querying resources by tags. Description as follows:


* TagFilters.N.Values.N: The first N indicates the tag key index. Value range: 1~10.

* TagFilters.N.Values.N: The second N indicates the index of the tag value. Value range: 1 to 3.

* Multiple tag values are separated by "&".

* If this parameter is passed in, you must first pass in TagFilters.N.Key.

* Not providing this parameter means querying all tag values under the same tag key.

* When an empty string is entered, it means querying tags with empty tag values.



**BillingType ** <span data-label="purple">integer </span>`Optional` `Example value: 1`

Payment type: the values are explained as follows:


* pre: Prepaid (subscription based).

* post: Postpaid (billed by usage).



**ProjectName ** <span data-label="purple">string </span>`optional` `Example value: default`

The project associated with the volume.



**VolumeIds.N ** <span data-label="purple">string[] </span>`Optional` `Example: vol-3wqdkgao8i4p5d65****`

Volume ID list.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The section below lists only the unique response parameters for this API For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)



**TotalCount ** <span data-label="purple">integer </span>`Example value: 2`

Total number of eligible volumes.



**PageNumber ** <span data-label="purple">integer </span>`Example value: 1`

Starting page number.



**PageSize ** <span data-label="purple">integer </span>`Example: 50`

Page Size.



**Volumes ** <span data-label="purple">object[] </span>`Example value: -`

Volume information that meets the criteria.


**VolumeName ** <span data-label="purple">string </span>`Example value: datavolume`

Cloud disk name.



**VolumeType ** <span data-label="purple">string </span>`Example value: ESSD_PL0`

Volume type.



**Description ** <span data-label="purple">string </span>`Example value: aaaa`

Volume description



**InstanceId ** <span data-label="purple">string </span>`Example: i-3tirbh6lka3vj0x1****`

Instance ID where the volume is mounted.



**ImageId ** <span data-label="purple">string </span>`Example value: image-3thdzjcwq23vj0wy****`

Image ID in the volume.



**Status ** <span data-label="purple">string </span>`Example value: attached`

Volume status, explained as follows:


* available: Available

* attaching: Attaching

* attached: Attached

* Detaching: Unmounting

* creating: In creation

* Deleting: In process

* Error

* Extending: In progress

* Pending release


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When unsubscribing from a subscription volume, the volume status changes to pending release</div>




**Kind ** <span data-label="purple">string </span>`Example: data`

Volume properties are described as follows:


* system: System disk.

* data: Data disk.



**VolumeId ** <span data-label="purple">string </span>`Example value: vol-3wqdkgao8i4p5d65****`

Volume ID.



**Size ** <span data-label="purple">string </span>`Example value: 1024`

Volume capacity, unit GiB.



**BillingType ** <span data-label="purple">integer </span>`Example: 2`

Billing type description:


* 1: Subscription.

* 2: Pay\-as\-you\-go.



**OverdueReclaimTime ** <span data-label="purple">string </span>`Example: 2200-01-01 00:00:00`

Volume overdue reclaim time.



**ProjectName ** <span data-label="purple">string </span>`Example value: default`

The project that owns the volume.



**CreatedAt ** <span data-label="purple">string </span>`Example: 2025-11-03T14:50:48+08:00`

Volume creation time.



**UpdatedAt ** <span data-label="purple">string </span>`Example: 2025-11-05T14:50:48+08:00`

Volume update time.



**DeleteWithInstance ** <span data-label="purple">boolean </span>`Example value: true`

Whether the volume is released when the instance is released. Value descriptions are as follows:


* true: The volume is released together with the instance.

* false: The volume is not released together with the instance.



**TradeStatus ** <span data-label="purple">integer </span>`Example: 0`

Transaction status. The values are explained as follows:


* 0: Creating.

* 1: Running.

* 2: Creation failed.



**PayType ** <span data-label="purple">string </span>`Example: Post`

Payment type descriptions:


* Pre: Prepaid (subscription based).

* Post: Pay\-as\-you\-go (billed by usage).



**ExpiredTime ** <span data-label="purple">string </span>`Example: 2025-11-05T14:50:48+08:00`

Subscription expiration time.



**OverdueTime ** <span data-label="purple">string </span>`Example value: 2200-01-01 00:00:00`

Volume suspension time for overdue payment.



**RenewType ** <span data-label="purple">integer </span>`Example value: 1`

Renewal method. The value description is as follows:


* 1: Manual renewal.

* 2: Automatic renewal.

* 3: No renewal upon expiration.



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Available zone ID.



**Tags ** <span data-label="purple">object[] </span>`Example value: -`

Tag information for the volume.


**Key ** <span data-label="purple">string </span>`Example: tag`

Volume tag key.



**Value ** <span data-label="purple">string </span>`Example value: test`

The tag value of the volume.




**ErrorDetail ** <span data-label="purple">string </span>`Example: error`

Specific error.



**SnapshotCount ** <span data-label="purple">integer </span>`Example value: 3`

Snapshot count.



**SourceSnapshotId ** <span data-label="purple">string </span>`Example: snap-3wqu6ajcau57gta1****`

Source Snapshot.



**AutoSnapshotPolicyName ** <span data-label="purple">string </span>`Example value: testablei`

Name of the automatic snapshot policy.



**AutoSnapshotPolicyId ** <span data-label="purple">string </span>`Example value: asp-3vke5nbvug3hhwzz****`

Automatic snapshot policy.



**BaselinePerformance ** <span data-label="purple">object </span>`Example value: -`

The baseline performance of the volume.


**IOPS ** <span data-label="purple">integer </span>`Example value: 2040`

The baseline IOPS of the volume, measured in operations per second.



**Throughput ** <span data-label="purple">integer </span>`Example: 105`

Baseline throughput for the volume in MB/s.




**ExtraPerformance ** <span data-label="purple">object </span>`Example value: -`

Additional performance for the volume.


**IOPS ** <span data-label="purple">integer </span>`Example value: 34160`

Additional IOPS for the volume.



**Throughput ** <span data-label="purple">integer </span>`Example value: 232`

Additional throughput of the volume.



**ExtraPerformanceTypeId** <span data-label="purple">string</span> `Example: IOPS`

Type of additional performance.


* Balance: Balanced additional performance.

* IOPS: IOPS additional performance.

* Throughput: Throughput additional performance.




**TotalPerformance ** <span data-label="purple">object </span>`Example value: -`

Total performance of the volume.


**IOPS ** <span data-label="purple">integer </span>`Example: 34160`

The total IOPS of the volume, which is the sum of the baseline IOPS and additional IOPS.



**Throughput ** <span data-label="purple">integer </span>`Example value: 232`

Total throughput of the volume, which includes both the baseline throughput and additional throughput.




**PlacementGroupId ** <span data-label="purple">string </span>`Example value: pg-d5ard493uxd44up7****`

Storage placement group ID



**SubgroupNumber ** <span data-label="purple">Integer </span>`Example value: 2`

Store the subgroup placement number.



**DetachedTime ** <span data-label="purple">string </span>`Example value: -`

The most recent detachment time for the volume.



**DeleteProtection ** <span data-label="purple">boolean </span>`Example value: true`

Enable volume delete protection.



**DeleteProtectionRetentionDays ** <span data-label="purple">integer </span>`Example value: 3`

Snapshot data related to deletion protection is kept permanently by default. You can also select a specific retention period, ranging from 1 to 65,536 days (default is 30 days). After the set period, snapshots are automatically deleted.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DescribeVolumes&Version=2020-04-01 HTTP/1.1
Host: open.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20251217T084931Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251217/cn-beijing/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "2025112117474114322108521783****",
    "Action": "DescribeVolumes",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "cn-beijing"
  },
  "Result": {
    "TotalCount": 2,
    "PageNumber": 1,
    "PageSize": 50,
    "Volumes": [
      {
        "VolumeName": "datavolume",
        "VolumeType": "ESSD_PL0",
        "Description": "aaaa",
        "InstanceId": "i-3tirbh6lka3vj0x1****",
        "ImageId": "image-3thdzjcwq23vj0wy****",
        "Status": "attached",
        "Kind": "data",
        "VolumeId": "vol-3wqdkgao8i4p5d65****",
        "Size": "1024",
        "BillingType": 2,
        "OverdueTime": "2200-01-01 00:00:00",
        "OverdueReclaimTime": "2200-01-01 00:00:00",
        "ProjectName": "default",
        "CreatedAt": "2025-11-03T14:50:48+08:00",
        "UpdatedAt": "2025-11-05T14:50:48+08:00",
        "DeleteWithInstance": true,
        "TradeStatus": 0,
        "PayType": "Post",
        "ExpiredTime": "2025-11-05T14:50:48+08:00",
        "ZoneId": "cn-beijing-a",
        "RenewType": 1,
        "Tags": [
          {
            "Key": "tag",
            "Value": "test"
          }
        ],
        "AutoSnapshotPolicyId": "asp-3vke5nbvug3hhwzz****",
        "AutoSnapshotPolicyName": "testablei",
        "ErrorDetail": "error",
        "SourceSnapshotId": "snap-3wqu6ajcau57gta1****",
        "SnapshotCount": 3,
        "BaselinePerformance": {
          "IOPS": 2040,
          "Throughput": 105
        },
        "ExtraPerformance": {
          "IOPS": 34160,
          "Throughput": 232,
          "ExtraPerformanceTypeId": "IOPS"
        },
        "TotalPerformance": {
          "IOPS": 34160,
          "Throughput": 232
        },
        "PlacementGroupId": "pg-d5ard493uxd44up7****",
        "SubgroupNumber": 2
      }
    ]
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists the error codes related to the business logic of this API. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |ErrInvalidTagFilterKey |tag filter key invalid |Tag filter key is invalid. |
|400 |ErrTagFilterKeyConflict |tag filter key conflict |Tag filter key conflict. |
|400 |ErrMaximumTagFilterKeys |too many tag filter keys |Tag filter key exceeds the limit. |
|400 |ErrInvalidTagFilterValue |tag filter value invalid |Tag filter value is invalid. |
|400 |ErrMaximumTagFilterValues |too many tag filter value |Tag filter value exceeds the limit. |
