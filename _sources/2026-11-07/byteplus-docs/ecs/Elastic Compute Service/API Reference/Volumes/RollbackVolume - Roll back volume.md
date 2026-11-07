---
title: "RollbackVolume - Roll back volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Rollbackvolume"
---

Call the RollbackVolume API to roll back the volume using a snapshot.

<span id=".5L2_55So6K-05piO"></span>
## Usage instructions


* Currently, only rolling back snapshot data to the source volume is supported. Therefore, before rolling back, ensure the source volume has not been deleted.

* The source volume is in one of the following states:

   * The source volume is in the "available" state (i.e., not attached to an instance) and can be rolled back directly.

   * The source volume is in the "attached" state (attached to an instance); the corresponding instance must be in the "stopped" state to perform the rollback.

* The source volume has no snapshots being created.

* The snapshot status is "available".

* After changing the operating system, previous system volume snapshots cannot be used to roll back the new system volume.


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=RollbackVolume&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the request parameters unique to this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|CqgyqO">必选</span> `Example value: RollbackVolume`

Action to be performed: RollbackVolume



**Version ** <span data-label="purple">string </span><span data-api-tag="require|sbdDz8">必选</span> `Sample value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**SnapshotId ** <span data-label="purple">string </span><span data-api-tag="require|a8Ie17">必选</span> `Example: snap-bp1s5fnvk4gn2tws0****`

Snapshot ID used.



**VolumeId ** <span data-label="purple">string </span><span data-api-tag="require|1W9Xot">必选</span> `Example: vol-bp1s5fnvk4gn2tws0****`

ID of the volume to be rolled back.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=RollbackVolume&Version=2020-04-01&VolumeId=vol-xxxx&SnapshotId=snap-xxxx HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "21ec0c83-2c65-4cb5-a6x3-631c4368****",
        "Action": "RollbackVolume",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to business logic for this API. For public error codes, refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |ErrorSnapshotNotAvailable |Snapshot is not available. |Snapshots are not available. |
|400 |VolumeSnapshotNotMatch |Volume and snapshot do not match. |The volume and snapshot do not match. |
|400 |VolumeInCreatingSnapshot |The operation is not permitted due to the volume is creating a snapshot. |The specified volume is creating a snapshot. |
|400 |IncorrectSnapshotStatus |The specified snapshot status is invalid. |The specified snapshot status is invalid. |
|400 |IncorrectVolumeStatus |The specified volume status is invalid. |The specified volume status is invalid. |
|403 |IncorrectInstanceStatus |The rollback condition is not permitted due to the instance which volume attached must be in stopped status. |Rollback conditions are not met. The instance attached to the volume must be in a stopped state. |
|403 |SnapshotJobQuotaExceed |The number of snapshot task exceeds the limit. |The number of snapshot tasks exceeds the limit. |
|403 |OperationDenied.InstanceIsCreatingImage |The operation is not permitted due to the instance is creating an image. |The instance is creating an image. |
|404 |VolumeNotFound |The specified volume does not exist. |The volume does not exist. |
|404 |SnapshotNotFound |The specified snapshot does not exist. |The specified snapshot does not exist. |
