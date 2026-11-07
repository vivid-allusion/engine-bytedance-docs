---
title: "ReleaseInstance"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/ReleaseInstance"
---

Call ReleaseInstance to delete instance.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/?action=ReleaseInstance&groupName=%E5%AE%9E%E4%BE%8B%E7%AE%A1%E7%90%86&serviceCode=milvus&version=2023-01-01)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters of this API and some common parameters are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string</span><span data-api-tag="require|o7PcFh">必选</span>` Example value: ReleaseInstance`

The action to execute; value: ReleaseInstance.



**Version**<span data-label="purple">string</span><span data-api-tag="require|PMRrsd">必选</span>`Example value: 2023-01-01`

API version, value: 2023\-01\-01.



**InstanceId**<span data-label="purple"> string </span><span data-api-tag="require|dqEfgq">必选</span>` Example: milvus-xxx`

Instance ID.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters unique to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Status ** <span data-label="purple">string </span>`Example: SUCCESSFUL`

Delete status.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request example

```json
POST /?Action=ReleaseInstance&Version=2023-01-01 HTTP/1.1
Host: milvus.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20251027T125554Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251027/cn-beijing/milvus/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "PyexG"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202510272055580781130901214DCA38",
    "Action": "ReleaseInstance",
    "Version": "2023-01-01",
    "Service": "milvus",
    "Region": "cn-beijing"
  },
  "Result": {
    "Status": "RfU5v9"
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For more information, see [Public error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|200 |InstanceNotFound |InstanceNotFound |The specified instance does not exist. |
|200 |InstanceIsReleased |InstanceIsReleased |Instance released. |
|200 |AccountNoPermission |accountId have no permission |This account does not have permission. |
|200 |InternalServerError |InternalServerError |Internal server exception. |
