---
title: "DeleteRole - Delete role"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/deleterole-delete-role"
---

Delete roles.

<span id="请求参数"></span>
## Request parameters

This table only lists the request parameters specific to this interface and some common parameters. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Param |Type |Required |Example Value |description |
|---|---|---|---|---|
|Action |String |Yes |DeleteRole |Required Action: DeleteRole. |
|Version |String |Yes |2024\-08\-31 |API Version: 2024\-08\-31. |
|RoleID |Integer |Yes |12345 |Role ID |


<span id="返回参数"></span>
## Response parameters

This table only lists the back parameters specific to this interface. For more details, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example Value |Description |
|---|---|---|---|---|
|Message | |String |None |Top Response Information |
|Data | |Object |{<br><br>"Message": "delete role successfully"<br><br>} |Return data |
| |Message |String |delete role successfully |Response message |


<span id="请求示例"></span>
## Request example

```text
POST /?Action=DeleteRole&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T135957Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
  "RoleID": 12345
}
```


<span id="返回示例"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409122200022160352452061F8027",
    "Action": "DeleteRole",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "delete role successfully"
    }
  }
}
```


<span id="错误码"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|400 |FailedToGetRoleInMetadata |failed to get role in metadata |Failed to retrieve Role metadata |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|403 |DeleteGrantedRoleNotAllowed |delete already granted role is not allowed |Deleting role actions is not allowed |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
