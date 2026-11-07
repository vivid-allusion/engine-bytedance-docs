---
title: "DescribeSnapshots - Query snapshots"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Describesnapshots"
---

Call the DescribeSnapshots API to query the list of snapshots.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSnapshots&groupName=%E5%BF%AB%E7%85%A7&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only request parameters specific to this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|GYfvYP">必选</span> `Example value: DescribeSnapshots`

The action to be performed: DescribeSnapshots.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|wtUJVq">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**PageSize ** <span data-label="purple">integer </span>`Optional` `Example value: 10`

Page size, default is 10.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example: 1`

Starting page, default is 1.



**Filter.N.Value ** <span data-label="purple">string[] </span>`Optional` `Example: testValue`

Filter keys for querying resources. The value description is as follows:


* CreationStartTime: Query information on resources created after the specified time.

* CreationEndTime: Query information on resources created before the specified time.



**Filter.N.Key ** <span data-label="purple">string[] </span>`Optional` `Example: testkey`

Filter value for querying resources. When specifying this parameter, you must also specify the Filter.N.Key parameter. The format is yyyy\-MM\-ddTHH:mmZ, using UTC +0 time zone.



**ZoneId ** <span data-label="purple">string </span>`Optional` `Example value: ap-southeast-1-a`

Availability Zone ID.



**SnapshotStatus.N ** <span data-label="purple">string[] </span>`Optional` `Example value: available`

Snapshot status. Value descriptions are as follows:


* Available.

* Creating: In process.

* Rolling back.

* Deleted: has been deleted.

* Failed: Error.



**SnapshotName ** <span data-label="purple">string </span>`Optional` `Example: testSnapshotName`

Snapshot name.



**VolumeId ** <span data-label="purple">string </span>`Optional` `Example: vol-bp1s5fnvk4gn2tws0****`

Volume ID related to snapshot.



**NextToken ** <span data-label="purple">string </span>`Optional` `Example value: AAAAGQAAABpzbmFwLTN3Yml2eWNzOHcycnJ2dTFsMTljMjAyNS0wNC0yMyAwNDozNjowNC4xNDI5MTE=`

Pagination token for the next page.



**MaxResults ** <span data-label="purple">integer </span>`Optional` `Example: 100`

The maximum number of records returned per query is 100.



**SnapshotTypes.N ** <span data-label="purple">string[] </span>`Optional` `Example value: user`

Description of snapshot types:


* user: Query manual snapshots.

* auto: Query automatic snapshots.

* share: Query shared snapshots.

   The default is to query all snapshots.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Example value: TagFilters.1.Key=tag`

Specifying the tag key when querying resources by tags. Description as follows:


* TagFilters.N.Key: N refers to the sequence number of the tag key. Value range: 1~10.

* Separate multiple tag keys with &, and do not allow duplicates.

* If this parameter is not provided, it implies querying all tags.

* When an empty string is passed, the error code InvalidTagFilterKey.Malformed is returned.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Example: TagFilters.1.Values.1=tag&TagFilters.1.Values.2=test`

Specifies the tag value when querying resources by tags. Description as follows:


* TagFilters.N.Values.N: The first N indicates the index of the tag key. Value range: 1~10.

* TagFilters.N.Values.N: The second N indicates the index of the tag value. Value range: 1 to 3.

* Use & to separate multiple tag values.

* If this parameter is passed in, you must first pass in TagFilters.N.Key.

* Not providing this parameter means querying all tag values under the same tag key.

* When an empty string is entered, it means querying tags with empty tag values.



**SnapshotIds.N ** <span data-label="purple">string[] </span>`Optional` `Example: snap-3tigy72q3u3vj0x2****`

Snapshot IDs to query.



**ProjectName ** <span data-label="purple">string </span>`Optional` `Example value: default`

Filter snapshots by the name of the project they belong to.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Only response parameters specific to this API are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example: 10`

Page Size.



**PageNumber ** <span data-label="purple">integer </span>`Example: 1`

Page number.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 1`

Total number of snapshots.



**Snapshots ** <span data-label="purple">object[] </span>`Example value: -`

Snapshot detail set.


**SnapshotType ** <span data-label="purple">string </span>`Example: auto`

Description of snapshot types:


* User: Manual snapshot.

* Auto: Automatic snapshot.



**Description ** <span data-label="purple">string </span>`Example: test`

Snapshot description information.



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

Available zone ID. If the snapshot has ultra\-fast availability enabled, you can create volumes from this snapshot in the corresponding available zone.



**CreationTime ** <span data-label="purple">string </span>`Example: 2021-12-12 03:33:04.374716`

Snapshot creation time.



**SnapshotName ** <span data-label="purple">string </span>`Example: snapshotname`

Snapshot name.



**Status ** <span data-label="purple">string </span>`Example value: creating`

Snapshot status. Values are as follows:


* Available.

* Creating: In process.

* Rolling back.

* Deleted: has been deleted.

* Failed: Error.



**VolumeId ** <span data-label="purple">string </span>`Example value: vol-bp1s5fnvk4gn2tws0****`

Volume ID.



**VolumeSize ** <span data-label="purple">long </span>`Example: 20`

Volume size, in GiB.



**VolumeType ** <span data-label="purple">string </span>`Example: TSSD_TL0`

Cloud disk type, with the following values:


* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* ESSD_FlexPL: High\-speed SSD volume of FlexPL specification.

* TSSD_TL0: Throughput\-type SSD volume



**SnapshotId ** <span data-label="purple">string </span>`Example: snap-3tigy72q3u3vj0x2****`

Snapshot ID.



**VolumeName ** <span data-label="purple">string </span>`Example value: test`

Cloud disk name.



**ProjectName ** <span data-label="purple">string </span>`Example value: default`

Snapshot belongs to the project.



**VolumeKind ** <span data-label="purple">string </span>`Example value: system`

Volume type. Value descriptions are as follows:


* system: System disk.

* data: Data disk.



**VolumeStatus ** <span data-label="purple">string </span>`Example value: attaching`

Volume status, with values explained as follows:


* available: Available

* attaching: Attaching

* attached: Attached

* detaching: Detaching

* creating: In creation

* deleting: Deleting

* error: Error

* Extending: Expanding



**RetentionDays ** <span data-label="purple">integer </span>`Example: 3`

Automatic snapshot retention days.



**Progress ** <span data-label="purple">integer </span>`Example: 20`

Dump progress



**SnapshotGroupId ** <span data-label="purple">string </span>`Example: sg-3wrulg6iwi4p5d64****`

Snapshot Consistency Group ID.



**ImageId ** <span data-label="purple">string </span>`Example: sg-3wrulg6iwi4p5d64****`

Image ID.



**Shared ** <span data-label="purple">boolean </span>`Example value: true`

Indicates whether the snapshot is shared with others.


* True: the snapshot has been shared with others.

* False: the snapshot has not been shared with others.



**Tags ** <span data-label="purple">object[] </span>`Example value: -`

Tag information.


**Key ** <span data-label="purple">string </span>`Example: tag`

Snapshot tag key.



**Value ** <span data-label="purple">string </span>`Example value: test`

Snapshot Tag Value.




**InstantAccess ** <span data-label="purple">boolean </span>`Example: true`

Indicates whether Instant Access is enabled for the snapshot. Description as follows:


* true: Instant Access is enabled.

* false: Turbo capability is not enabled.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DescribeSnapshots&SnapshotIds.1=snap-31akybwsxi8rudc6m***&SnapshotIds.2=snap-31ak39j5bh8rubsn9***&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "20220311010333010194099035060C0***",
        "Action": "DescribeSnapshots",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "Snapshots": [
            {
                "CreationTime": "2022-03-10T22:33:46+08:00",
                "Description": "test",
                "SnapshotId": "snap-31ak39j5bh8rubsn****",
                "SnapshotName": "snapshot2",
                "SnapshotType": "user",
                "Status": "creating",
                "Tags": [
                    {
                        "Key": "tag",
                        "Value": "value"
                    }
                ],
                "VolumeId": "vol-31ale588uo8rud93****",
                "VolumeKind": "data",
                "VolumeName": "snap_test",
                "VolumeSize": 20,
                "VolumeStatus": "available",
                "VolumeType": "ESSD_PL0",
                "ZoneId": "ap-southeast-1-b",
                "InstantAccess": true,
                "ProjectName": "default"
            },
            {
                "CreationTime": "2022-03-10T21:57:14+08:00",
                "Description": "test",
                "SnapshotId": "snap-31akybwsxi8rudc6****",
                "SnapshotName": "snapshot",
                "SnapshotType": "user",
                "Status": "available",
                "Tags": [
                    {
                        "Key": "tag",
                        "Value": "value"
                    }
                ],
                "VolumeId": "vol-31ale588uo8rud93****",
                "VolumeKind": "data",
                "VolumeName": "snap_test",
                "VolumeSize": 20,
                "VolumeStatus": "available",
                "VolumeType": "ESSD_PL0",
                "ZoneId": "ap-southeast-1-b",
                "InstantAccess": false,
                "ProjectName": "default"
            }
        ],
        "TotalCount": 2
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, see the [public error code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |InvalidRequest |The operation is not permitted due to the request is invalid. |Invalid request. |
|400 |ErrInvalidAccountId |account id invalid |Account ID is invalid. |
|400 |ErrMaximumTagFilterKeys |too many tag filter keys |The tag filter key exceeds the limit. |
|400 |ErrTagFilterKeyConflict |tag filter key conflict |Tag filter key conflict. |
|400 |ErrInvalidTagFilterKey |tag filter key invalid |Invalid tag filter key. |
|400 |ErrMaximumTagFilterValues |too many tag filter value |Tag filter value exceeds the limit. |
|400 |ErrInvalidTagFilterValue |tag filter value invalid |Invalid tag filter value. |
|400 |SnapshotServiceNonactivated |Snapshot service is nonactivated, need activate snapshot service from user console. |Snapshot service is not enabled. Activate it in the user console. |
