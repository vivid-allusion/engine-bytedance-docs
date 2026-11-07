---
title: "DeleteUser - Delete user"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/delete-user"
---

Delete a user.

<span id="df6cb2e9"></span>
## Request parameters

This table only lists the specific request parameters and some common parameters for this interface. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |DeleteUser |The action to be executed, value: Delete User. |
|Version |String |Yes |2024\-08\-31 |The version of the API, value: 2024\-08\-31. |
|UserID |Integer |Yes |12345 |User ID |


<span id="7f6bdab9"></span>
## Response parameters

This table only lists the specific return parameters for this interface. For more information, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example value |Description |
|---|---|---|---|---|
|Message | |String |None |Top response information |
|Data | |Object |{<br><br>"Message": "delete user successfully"<br><br>} |Response Data |
| |Message |String |delete user successfully |Response Message |


<span id="cc598755"></span>
## Request example

```text
POST /?Action=DeleteUser&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T131140Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "UserID": 12345
}
```


<span id="c4ae4755"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "202409122111462530431551715843EF",
    "Action": "DeleteUser",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "delete user successfully"
    }
  }
}
```


<span id="1a3341d7"></span>
## Error code

The following table lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
