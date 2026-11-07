---
title: "UnassignRoles - Revoke roles"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/unassign-roles"
---

Revoke a user's role.

<span id="请求参数"></span>
## Request parameters

The table below lists only the specific request parameters and some common parameters for this interface. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter | |Type |Required |Example Value |Description |
|---|---|---|---|---|---|
|Action | |String |Yes |UnassignRole |Action to be performed: Value: UnassignRole. |
|Version | |String |Yes |2024\-08\-31 |API version, value: 2024\-08\-31. |
|RoleID | |Integer |Yes |12345 |Role id |
|Users | |Array of Object |No |[<br><br>{<br><br>"Username": "user1",<br><br>"Admin_option": "false"<br><br>}<br><br>] |Authorized User Information |
| |Username |String |No |user1 |Username |
| |AdminOption |Boolean |No |false |Whether it can be granted to other users |


<span id="返回参数"></span>
## Response parameters

The table below lists only the specific response parameters for this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example value |Description |
|---|---|---|---|---|
|Message | |String |None |Top response information |
|Data | |Object |{<br><br>"Message": "successfully update users for role role1"<br><br>} |Return Data |
| |Message |String |successfully update users for role role1 |Response Information |


<span id="请求示例"></span>
## Request example

```text
POST /?Action=UnassignRole&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T141030Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
{
  "RoleID": 12345,
  "Users": [
    {
      "Username": "user1",
      "AdminOption": true
    }
  ]
}
```


<span id="返回示例"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "2024091222103619617120409949EFCC",
    "Action": "UnassignRole",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "successfully update users for role role1"
    }
  }
}
```


<span id="错误码"></span>
## Error code

The table below lists the error codes related to this interface and business logic. For common error codes, refer to the [common error code](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Error Information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
