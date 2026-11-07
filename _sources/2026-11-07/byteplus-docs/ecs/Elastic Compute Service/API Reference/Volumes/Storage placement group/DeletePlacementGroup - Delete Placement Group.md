---
title: "DeletePlacementGroup - Delete Placement Group"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Deleteplacementgroup"
---

Call DeletePlacementGroup to delete the storage placement group.

<span id=".5rOo5oSP5LqL6aG5"></span>
## precautions

Only storage placement groups without a bound volume can be deleted.

<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/?action=DeletePlacementGroup&groupName=%E5%AD%98%E5%82%A8%E6%94%BE%E7%BD%AE%E7%BB%84&serviceCode=storage_ebs&version=2020-04-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## request parameters

Only the unique request parameters and some common parameters for this API are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|vs8UHr">必选</span> `Example value: DeletePlacementGroup`

Operation to perform: DeletePlacementGroup.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|OCu5KR">必选</span> `Example: 2020-04-01`

The version of the API is: 2020\-04\-01.



**Id ** <span data-label="purple">string </span><span data-api-tag="require|1Pru4e">必选</span> `Example value: pg-bp67acfmxazb4ph****`

Storage placement group ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response Parameters

This API does not have unique response parameters. For more information, see [Return Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```text
POST /?Action=DeletePlacementGroup&Version=2020-04-01 HTTP/1.1
Host: open.ap-southeast-1.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20250730T085947Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250730/ap-southeast-1/storage_ebs/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Id": "pg-bp67acfmxazb4ph****"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Back to example

```json
{
  "ResponseMetadata": {
    "RequestId": "2025073016595900317525006054****",
    "Action": "DeletePlacementGroup",
    "Version": "2020-04-01",
    "Service": "storage_ebs",
    "Region": "ap-southeast-1"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## error code

The table below lists error codes related to this interface and business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |error code |error message |Create Volume |
|---|---|---|---|
|412 |PlacementGroupExistsVolumes |The placement group has volumes associated with it and cannot be deleted. |The anti\-affinity group exists in the volume and cannot be deleted |
