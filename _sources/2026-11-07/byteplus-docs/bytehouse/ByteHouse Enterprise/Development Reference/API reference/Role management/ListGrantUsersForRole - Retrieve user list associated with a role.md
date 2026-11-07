---
title: "ListGrantUsersForRole - Retrieve user list associated with a role"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/list-grant-users-for-role-retrieve-user-list-associated-with-a-role"
---

Retrieve the user list associated with a role.

<span id="请求参数"></span>
## Request parameters

The table below only lists the parameters specific to this interface and some common parameters. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |ListGrantUsersForRole |The action to be performed is: ListGrantUsersForRole. |
|Version |String |Yes |2024\-08\-31 |The version of the API is: 2024\-08\-31. |
|RoleID |Integer |Yes |12345 |Role ID |


<span id="返回参数"></span>
## Response parameters

The table below only lists the return parameters specific to this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | | |Type |Example Value |Description |
|---|---|---|---|---|---|
|Message | | |String |None |Top Response Information |
|Data | | |Object |{<br><br>"Grants": [<br><br>{<br><br>"Username": "user1",<br><br>"Admin_option": "false"<br><br>}<br><br>]<br><br>} |Return Data |
| |Grants | |Array of Object | |Information granted to the user |
| | |Username |String |user1 |Username |
| | |AdminOption |Boolean |false |Can be granted to other users |


<span id="请求示例"></span>
## Request example

```text
GET /?Action=ListGrantUsersForRole&Version=2024-08-31&RoleID=12345 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240926T121739Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240926/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id="返回示例"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409122216351342261631723656AC",
    "Action": "ListGrantUsersForRole",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Grants": [
        {
          "Username": "user1",
          "AdminOption": true
        }
      ]
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
|400 |FailedToGetRoleInMetadata |failed to get role in metadata |Error fetching Role metadata |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
