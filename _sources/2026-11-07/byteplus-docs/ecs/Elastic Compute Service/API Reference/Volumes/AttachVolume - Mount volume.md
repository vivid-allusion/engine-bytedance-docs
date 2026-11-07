---
title: "AttachVolume - Mount volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Attachvolume"
---

Call the AttachVolume API to mount a volume to a cloud host.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=AttachVolume&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are the unique request parameters for this API as well as some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|Q21zVc">必选</span> `Example value: AttachVolume`

Action to be performed: AttachVolume



**Version**<span data-label="purple">string</span><span data-api-tag="require|v5uknW">必选</span>`Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**DeleteWithInstance ** <span data-label="purple">boolean </span>`Optional` `Example: true`

When releasing an instance, should the volume be released with it? The default value is `false`.


* true: The volume is released along with the instance.

* false: The volume is not released with the instance.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|qS6jfE">必选</span> `Example: i-3tiefmkskq3vj0x0****`

The ID of the mounted ECS instance.



**VolumeId ** <span data-label="purple">string </span><span data-api-tag="require|6KgiJp">必选</span> `Example value: vol-3tir92lne23vj0x****`

ID of the volume to attach



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have any unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=AttachVolume&Version=2020-04-01&InstanceId=i-3tir90q84q3vj0x1****&VolumeId=vol-3tir92lne23vj0x1**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "202106232008120102251331430A0D****",
        "Action": "AttachVolume",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, please refer to the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |MissingVolumeID |The specified parameter VolumeId is missing. |Missing volume ID. |
|400 |MissingInstanceID |Missing instance ID. |Missing instance ID. |
|403 |VolumeCannotAttachAcrossZones |Volumes cannot be attached across different availability zones. |Volumes cannot be attached across availability zones |
|403 |VolumeCannotAttachAcrossAccount |Volumes cannot be attached across different master accounts. |Volumes and instances cannot be attached across primary accounts |
|403 |ErrorVolumeStatusCannotAttach |Invalid volume status for volume attaching. |Volumes in this state do not support mounting. |
|404 |VolumeNotFound |The specified volume does not exist. |Volume does not exist. |
|404 |ErrorInvalidInstanceStatus |Instance status exception. |Abnormal cloud server status |
|404 |ErrorInstanceNotFound |Instance not found. |Cloud host not found. |
|412 |ErrorVolumeStatusInMigration |Volume is undergoing data migration. |The volume is currently migrating data. |
|412 |ErrorVolumeStatusInChanging |Volume type is being changed. |The volume is being resized |
|412 |VolumeStatusInRollbacking |Volume is being rolled back. |Volume is rolling back. |
|412 |VolumeStatusCannotAttach |Invalid volume status for volume attaching. |Volumes in this status do not support mounting |
|412 |AlreadyExitOrder |Order in progress, cannot perform operation. |The order is in progress and cannot be operated. |
|412 |ErrInstanceLimitExceeded |You've reached the limit on the number of volumes that can be attached to the instance. |You have reached the limit for the number of volumes that can be attached to an instance |
|500 |ResourceLockError |Failed to lock resource: [resourceId] |Failed to lock the resource: [resourceId]. |
