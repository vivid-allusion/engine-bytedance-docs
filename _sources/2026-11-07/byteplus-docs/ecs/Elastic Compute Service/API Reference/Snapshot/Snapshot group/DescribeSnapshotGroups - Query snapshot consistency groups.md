---
title: "DescribeSnapshotGroups - Query snapshot consistency groups"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/DescribeSnapshotGroups"
---

open.ap\-southeast\-1.byteplusapi.comCall the DescribeSnapshotGroups interface to query snapshot consistency groups.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DescribeSnapshotGroups&groupName=%E5%BF%AB%E7%85%A7%E4%B8%80%E8%87%B4%E6%80%A7%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only unique request parameters for this interface and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|HCmDRi">必选</span>`Example value: DescribeSnapshotGroups`

The action to be performed: DescribeSnapshotGroups.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|KS7rUF">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**SnapshotGroupIds.N ** <span data-label="purple">string[] </span>`Optional` `Example value: sg-4sduwo75f9en37xq****`

ID of the queried snapshot consistency group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>N</code> indicates the snapshot consistency group ID sequence number. Separate multiple snapshot consistency group IDs with <code>&</code>. Valid values: 1 to 10.</div>




**ProjectName ** <span data-label="purple">string </span>`Optional` `Example value: default`

The project that the snapshot consistency group belongs to.



**InstanceId ** <span data-label="purple">string </span>`Optional` `Example value: i-ycmu5f4nfphhw5dh****`

Snapshot consistency group's ECS instance ID.



**Name ** <span data-label="purple">string </span>`Optional` `Example: testName`

Name of the snapshot consistency group.



**Status.N ** <span data-label="purple">string[] </span>`Optional` `Example: available`

Status of the snapshot consistency group:


* Creating: In process.

* Available.

* Failed: error


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>N</code> indicates the sequence number of the snapshot consistency group status. Use <code>&</code> to separate multiple group statuses. Valid values are 1 to 10.</div>




**PageSize ** <span data-label="purple">integer </span>`Optional` `Example value: 10`

Page size, default is 10.



**PageNumber ** <span data-label="purple">integer </span>`Optional` `Example: 1`

Starting page, default is 1.



**TagFilters.N.Key ** <span data-label="purple">string[] </span>`Optional` `Example value: key1`

Label key of the snapshot consistency group.



**TagFilters.N.Values.N ** <span data-label="purple">string[] </span>`Optional` `Example: value`

Label value of the snapshot consistency group.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

Only unique response parameters for this interface are listed below. For more information, refer to [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**PageSize ** <span data-label="purple">integer </span>`Example value: 10`

Page Size.



**PageNumber ** <span data-label="purple">integer </span>`Example value: 1`

Page number.



**TotalCount ** <span data-label="purple">integer </span>`Example value: 2`

Total number of snapshot consistency groups.



**SnapshotGroups ** <span data-label="purple">object[] </span>`Example: /`

Details of the snapshot consistency group.


**ImageId ** <span data-label="purple">string </span>`Example value: image-yubc9nsmoghyu8v****`

Image ID of the snapshot consistency group.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

Project name.



**Snapshots ** <span data-label="purple">object[] </span>`Example value: /`

Snapshot details.


**SnapshotType ** <span data-label="purple">string </span>`Example value: user`

Description of snapshot types:


* User: Manually created snapshot.

* Auto: Snapshot created through an automatic snapshot policy.



**Description ** <span data-label="purple">string </span>`Example value: data`

Snapshot description.



**ZoneId ** <span data-label="purple">string </span>`Example value: cn-beijing-a`

The availability zone the snapshot belongs to.



**CreationTime ** <span data-label="purple">string </span>`Example value: 2023-11-06T06:38:51+08:00"`

Snapshot creation time.



**SnapshotName ** <span data-label="purple">string </span>`Example: Created-from-sg-4sduwo75f9en37xq74xh`

Snapshot name.



**Status ** <span data-label="purple">string </span>`Example: available`

Snapshot status, values include:


* Available.

* Creating: In process.

* Rolling back.

* Deleted: has been deleted.

* Failed: Error.



**VolumeId ** <span data-label="purple">string </span>`Example value: vol-g8blwv5s83lzq2h5****`

Volume ID.



**VolumeSize ** <span data-label="purple">long </span>`Example value: 200`

Volume size, in GB.



**VolumeType ** <span data-label="purple">string </span>`Example value: data`

Cloud disk type, with the following values:


* ESSD_PL0: High\-speed SSD volume of PL0 specification.

* Extreme Speed SSD Cloud volume, FlexPL specification.



**SnapshotId ** <span data-label="purple">string </span>`Example value: snap-4sduwo75faen383x****`

Snapshot ID.



**VolumeName ** <span data-label="purple">string </span>`Example: cm-test-img-reserved-volume-1-2`

Cloud disk name.



**ProjectName ** <span data-label="purple">string </span>`Example: default`

Snapshot belongs to the project.



**VolumeKind ** <span data-label="purple">string </span>`Example value: data`

Types of cloud disks, with the following values:


* system: System disk.

* data: Data disk.



**VolumeStatus ** <span data-label="purple">string </span>`Example value: available`

Volume status, with values explained as follows:


* Available.

* Attaching.

* Attached: Mounted.

* Detaching: Unmounting.

* Creating: In process.

* Deleting: In process.

* Error: Error.

* Extending: Expanding.



**RetentionDays ** <span data-label="purple">integer </span>`Example: 30`

Automatic snapshot retention days.



**Progress ** <span data-label="purple">integer </span>`Example value: 20`

Snapshot dump progress.



**SnapshotGroupId ** <span data-label="purple">string </span>`Example value: sg-3wr1z86cky4p5d6d****`

Snapshot Consistency Group ID.



**ImageId ** <span data-label="purple">string </span>`Example: image-yubc9nsmoghyu8v****`

The image ID of the snapshot.



**Shared ** <span data-label="purple">boolean </span>`Example: true`

Is this snapshot shared with others?



**Tags ** <span data-label="purple">object[] </span>`Example: /`

Snapshot tags.


**Key ** <span data-label="purple">string </span>`Example value: user`

Label key of the snapshot consistency group.



**Value ** <span data-label="purple">string </span>`Example: aaa`

Label value of the snapshot consistency group.




**InstantAccess ** <span data-label="purple">boolean </span>`Example: true`

Whether the snapshot enables the Ultra Available capability. The possible values are:


* true: Enabled

* false: Not enabled




**SnapshotGroupId ** <span data-label="purple">string </span>`Example value: sg-4sduwo75f9en37xq****`

Snapshot consistency group ID.



**InstanceId ** <span data-label="purple">string </span>`Example value: i-ycmu5f4nfphhw5dh****`

ECS instance ID of the snapshot consistency group



**CreationTime ** <span data-label="purple">string </span>`Example: 2023-11-06T06:38:51+08:00`

Creation time of the snapshot consistency group.



**Description ** <span data-label="purple">string </span>`Example value: data`

Description of the snapshot consistency group.



**Name ** <span data-label="purple">string </span>`Example: test-name`

Name of the snapshot consistency group.



**Status ** <span data-label="purple">string </span>`Example value: available`

Status of the snapshot consistency group.



**Tags ** <span data-label="purple">object[] </span>`Example value: /`

Snapshot consistency group tags.


**Key ** <span data-label="purple">string </span>`Example value: user`

Label key of the snapshot consistency group.



**Value ** <span data-label="purple">string </span>`Example value: aaa`

Label value of the snapshot consistency group.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action= DescribeSnapshotGroups&Version=2020-04-01&SnapshotGroupIds.1=sg-4sduwo75f9en37xq**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "c5725893-f888-43f2-90a7-770c67a0****",
    "Action": "DescribeSnapshotGroups",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 15,
    "SnapshotGroups": [
      {
        "CreationTime": "2023-11-06T06:38:51+08:00",
        "Description": "",
        "ImageId": "",
        "InstanceId": "i-ycmu5f4nfphhw5dh****",
        "Name": "test-name",
        "ProjectName": "default",
        "SnapshotGroupId": "sg-4sduwo75f9en37xq****",
        "Snapshots": [
          {
            "CreationTime": "2023-11-06T06:38:51+08:00",
            "Description": "",
            "ImageId": "",
            "ProjectName": "default",
            "SnapshotGroupId": "sg-4sduwo75f9en37xq****",
            "SnapshotId": "snap-4sduwo75faen383x****",
            "SnapshotName": "Created-from-sg-4sduwo75f9en37x****",
            "SnapshotType": "user",
            "Status": "available",
            "VolumeId": "vol-g8blwv5s83lzq2h5****",
            "VolumeKind": "system",
            "VolumeName": "cm-test-img-reserved-volume-1-2",
            "VolumeSize": 200,
            "VolumeStatus": "",
            "VolumeType": "ESSD_PL0",
            "ZoneId": "ap-southeast-1-a"
          }
        ],
        "Status": "available",
        "Tags": [
          {
            "Key": "key1",
            "Value": "value1"
          }
        ]
      }
    ],
    "TotalCount": 1
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |ErrInvalidAccountId |account id invalid |Account ID is invalid. |
