---
title: "MSModifyPublicDomain"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/MSModifyPublicDomain"
---

Call MSModifyPublicDomain to toggle the public network domain name of the Serverless instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=MSModifyPublicDomain&groupName=Serverless-%E5%85%AC%E5%BC%80&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action**<span data-label="purple"> string </span><span data-api-tag="require|WMIP63">必选</span>`Example value: MSModifyPublicDomain`

Operation to execute, value: MSModifyPublicDomain.



**Version ** <span data-label="purple">string</span><span data-api-tag="require|PYRmUs">必选</span>` Example: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId**<span data-label="purple"> string</span><span data-api-tag="require|obEDod">必选</span> ` Example value: -`

Instance ID.



**EndpointType ** <span data-label="purple">string </span>`optional` `Example value: -`

Access point type.



**EipId ** <span data-label="purple">string </span>`optional` `Example value: -`

Public network ID.



**Enable**<span data-label="purple"> boolean</span><span data-api-tag="require|kvG8Md">必选</span>`  Example value: -`

Turn on or not.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Status ** <span data-label="purple">string </span>`Example: SUCCESSFUL`

Returned operation status.



**Message ** <span data-label="purple">string </span>`Example: -`

Returned note information.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=MSModifyPublicDomain&Version=2023-01-01 HTTP/1.1
Host: /
Content-Type: application/json; charset=UTF-8
X-Date: 20260316T065837Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260316/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "68KxzemMs0",
  "Enable": false
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260316145844215054019241B03624",
    "Action": "MSModifyPublicDomain",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Status": "SUCCESSFUL",
    "Message": "-"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |AccountNoPermission |accountId have no permission |This account does not have permission. |
