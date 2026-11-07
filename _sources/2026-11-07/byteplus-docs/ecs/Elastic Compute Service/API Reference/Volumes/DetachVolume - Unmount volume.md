---
title: "DetachVolume - Unmount volume"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Detachvolume"
---

Call the DetachVolume API to unmount the volume from an ECS instance.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DetachVolume&groupName=%E4%BA%91%E7%9B%98&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only request\-specific parameters and some common parameters for this API are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|v6rNqt">必选</span> `Example: DetachVolume`

Action to be performed: DetachVolume



**Version ** <span data-label="purple">string </span><span data-api-tag="require|bRAB1y">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**VolumeId**<span data-label="purple">string</span><span data-api-tag="require|ul79BF">必选</span>`Example value: vol-3tir92lne23vj0x1****`

ID of the volume to be detached.



**InstanceId ** <span data-label="purple">string </span><span data-api-tag="require|2dfMQ3">必选</span> `Example: i-3tiefmkskq3vj0x0****`

The ECS instance ID where the volume is mounted.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=DetachVolume&Version=2020-04-01&InstanceId=i-3tir90q84q3vj0x1****&VolumeId=vol-3tir92lne23vj0x1**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "86f352ba-e528-46db-bd4c-1ca786b5****",
        "Action": "DetachVolume",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1"
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The following table lists error codes related to this API and business logic. For common error codes, refer to the [public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |MissingInstanceID |Missing instance ID. |Instance ID is missing. |
|400 |MissingVolumeID |The specified parameter VolumeId is missing. |Volume ID is missing. |
|400 |ErrorInstanceNotMatched |The attached volume does not match the instance parameters. |The cloud host attached to the volume does not match the cloud host parameters. |
|400 |ErrorMissingVolumeID |Missing volume ID. |Missing volume ID. |
|400 |ErrorMissingInstanceID |Missing instance ID. |Instance ID is missing. |
|400 |ErrorSystemVolumeCannotDetach |System volume cannot be directly detached. |System volume cannot be directly detached. |
|404 |VolumeNotFound |The specified volume does not exist. |Volume does not exist. |
|404 |ErrorInvalidInstanceStatus |Instance status exception. |Abnormal cloud server status. |
|412 |SystemVolumeCannotDetach |System volume cannot be directly detached. |The system disk cannot be detached directly. |
|412 |ErrorPrepaidVolumeCannotDetach |Postpaid volumes cannot be detached. |Subscription volumes cannot be detached. |
|412 |ErrorVolumeStatusInMigration |Volume is undergoing data migration. |The volume is migrating data. |
|412 |ErrorVolumeStatusInChanging |Volume type is being changed. |The volume is being reconfigured. |
|412 |VolumeStatusCannotDetach |Volumes in this state cannot be detached. |The volume cannot be detached in this status. |
|412 |VolumeCannotDetach |Detach is not supported for this type of volume. |This type of volume does not support detachment. |
|412 |AlreadyExitOrder |Order in progress, cannot perform operation. |The order is in progress and cannot be processed. |
