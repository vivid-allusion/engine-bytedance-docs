---
title: "GetUserInitialPassword - Retrieve user initial password"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/get-user-initial-password-retrieve-user-initial-password"
---

Get user's initial password.

<span id="6fce6ec4"></span>
## Request parameters

The table below only lists the request parameters specific to this interface and some common parameters. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |GetUserInitialPassword |The actions to be performed, value: GetUserInitialPassword. |
|Version |String |Yes |2024\-08\-31 |The version of the API, value: 2024\-08\-31. |
|Username |String |Yes |user1 |Username |


<span id="c1c10044"></span>
## Response parameters

The table below only lists the return parameters specific to this interface. For more details, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example |Description |
|---|---|---|---|---|
|Message | |String |None |top gateway response message |
|Data | |Object |{<br><br>"user": {<br><br>"id": 123,<br><br>"userID": 12345678,<br><br>"accountID": 12345678,<br><br>"username": "user1",<br><br>"cloudName": "cloudname",<br><br>"userType": "MAIN",<br><br>"status": "ACTIVE",<br><br>"emaill": "xxx@xxx.com",<br><br>"description": "description",<br><br>"readonly": true,<br><br>"isSystemAdmin": true,<br><br>"lastLoginAt": 0,<br><br>"createdAt": 1716264720906,<br><br>"updatedAt": 1716264720906,<br><br>"clusters": [<br><br>"MZ"<br><br>]<br><br>}<br><br>} |Back to Data |
| |Password |String |xxxx |Base64 encrypted password |
| |PasswordIsDefault |Boolean | |Is it the default password? |
| |Message |String |Failed to get password, it has been modified | |


<span id="97b5d1ff"></span>
## Request example

```text
GET /?Action=GetUserInitialPassword&Version=2024-08-31&Username=user1 HTTP/1.1
Host: open.byteplusapi.com
X-Date: 20240912T090355Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

```


<span id="6d5c72ae"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240912170402120144117204C0807E",
    "Action": "GetUserInitialPassword",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Password": "xxxx",
      "PasswordIsDefault": false,
      "Message": "Failed to get password, it has been modified"
    }
  }
}
```


<span id="7abc30a1"></span>
## Error code

The table below lists the error codes related to this interface and its business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status code |Error code |Error information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
