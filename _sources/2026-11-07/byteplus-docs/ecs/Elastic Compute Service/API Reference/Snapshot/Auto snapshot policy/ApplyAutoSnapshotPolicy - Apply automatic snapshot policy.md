---
title: "ApplyAutoSnapshotPolicy - Apply automatic snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Applyautosnapshotpolicy"
---

Use ApplyAutoSnapshotPolicy to assign an automatic snapshot policy to one or more volumes

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions


* Each volume can only have one automatic snapshot policy

* A single automatic snapshot policy can be applied to multiple volumes

* If the target volume already has an automatic snapshot policy, you can use ApplyAutoSnapshotPolicy to replace the current policy


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=ApplyAutoSnapshotPolicy&groupName=%E8%87%AA%E5%8A%A8%E5%BF%AB%E7%85%A7%E7%AD%96%E7%95%A5&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only interface\-specific request parameters and some common parameters are listed below For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)



**Action ** <span data-label="purple">string </span><span data-api-tag="require|AuIHxk">必选</span> `Example value: ApplyAutoSnapshotPolicy`

Operation to execute: ApplyAutoSnapshotPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|K98oKJ">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**AutoSnapshotPolicyId ** <span data-label="purple">string </span><span data-api-tag="require|TZJIX5">必选</span> `Example value: asp-anj2a9gwj49gsbso****`

The automatic snapshot policy ID to associate. A volume can only be associated with one automatic snapshot policy.



**VolumeIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|D8we0W">必选</span>`Example: VolumeIds.1=vol-3tiz8tg97u3vj0x0**** VolumeIds.2=vol-3tj20xxpd63vj0wy****`

The volume ID that needs to be associated with the automatic snapshot policy. You can specify one or more.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Return parameters

This operation interface only returns public parameters and error codes.

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
GET /?Action=ApplyAutoSnapshotPolicy&AutoSnapshotPolicyId=asp-anj2a9gwj49gsbso****&Version=2020-04-01&VolumeIds.1=vol-3tiz8tg97u3vj0x0****VolumeIds.2=vol-3tj20xxpd63vj0wy**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Region: ap-southeast-1
ServiceName: storage_ebs
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022050520041301020405722009C7****",
        "Action": "ApplyAutoSnapshotPolicy",
        "Version": "2020-04-01",
        "Service": "storage_ebs",
        "Region": "ap-southeast-1
    },
    "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and its business logic. For public error codes, see the [Public Error Code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |ErrInvalidVolumeId |The specified volume ID is invalid. |The specified volume ID is invalid. |
|400 |AccountIdNotMatched |The specified account ID does not match. |User ID mismatch. |
|404 |VolumeNotFound |The specified volume does not exist. |Volume does not exist. |
|404 |AutoSnapshotPolicyNotFound |The automatic snapshot policy is not found. |Auto snapshot policy not found. |
|500 |InternalError |An internal error has occurred. |Internal error. Try again. If repeated attempts fail, submit a ticket. |
