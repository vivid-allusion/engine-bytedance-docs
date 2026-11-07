---
title: "CancelAutoSnapshotPolicy - Remove auto snapshot policy"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Cancelautosnapshotpolicy"
---

Use CancelAutoSnapshotPolicy to remove the auto snapshot policy for one or more volumes

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=CancelAutoSnapshotPolicy&groupName=%E8%87%AA%E5%8A%A8%E5%BF%AB%E7%85%A7%E7%AD%96%E7%95%A5&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Below are request parameters unique to this API and some common parameters For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ZC3p2y">必选</span> `Example: CancelAutoSnapshotPolicy`

Operation to perform: CancelAutoSnapshotPolicy.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|KuZiTL">必选</span> `Example value: 2020-04-01`

The version of the API is: 2020\-04\-01.



**AutoSnapshotPolicyId ** <span data-label="purple">string </span><span data-api-tag="require|U4LlHs">必选</span> `Example: asp-3vke5nbvug3hhwzz****`

Automatic snapshot policy ID.



**VolumeIds.N ** <span data-label="purple">string[] </span><span data-api-tag="require|UbdV4Z">必选</span> `Example: VolumeIds.1=vol-3tiz8tg97u3vj0x0**** VolumeIds.2=vol-3tj20xxpd63vj0wy****`

The ID(s) of the volume(s) for which you want to cancel the automatic snapshot policy. You can specify one or more IDs.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This API has no unique response parameters For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=CancelAutoSnapshotPolicy&Version=2020-04-01&VolumeIds.1=VolumeIds.1%3Dvol-3tiz8tg97u3vj0x0****VolumeIds.2%3Dvol-3tj20xxpd63vj0wy**** HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20251124T032512Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251124/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "AutoSnapshotPolicyId": "asp-********"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "20251124112517068106179177A1****",
    "Action": "CancelAutoSnapshotPolicy",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this API and its business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status code |error code |error message |Create Volume |
|---|---|---|---|
|400 |ErrInvalidVolumeId |The specified volume ID is invalid. |The specified volume ID is invalid. |
|400 |AccountIdNotMatched |The specified account ID does not match. |User ID does not match. |
|400 |InvalidParameters |The request has invalid parameters. |The request contains invalid parameters. |
|404 |VolumeNotFound |The specified volume does not exist. |Volume does not exist. |
|404 |ErrResourceNotFound |resource not found |Resource not found. |
|404 |AutoSnapshotPolicyNotFound |The automatic snapshot policy is not found. |No automatic snapshot policy found. |
|500 |InternalError |An internal error has occurred. |Internal error. Please try again. If several attempts fail, submit a support ticket. |
