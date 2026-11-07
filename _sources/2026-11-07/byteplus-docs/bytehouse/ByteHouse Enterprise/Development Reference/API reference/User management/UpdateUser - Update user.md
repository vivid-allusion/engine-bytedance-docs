---
title: "UpdateUser - Update user"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/update-user"
---

Update a user.

<span id="5a4d6837"></span>
## Request parameter

The table below lists only the specific request parameters and some common parameters for this interface. For more details, refer to [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Param |Type |REQUIRED |Example Value |Description |
|---|---|---|---|---|
|Action |String |Yes |UpdateUser |The action to be performed, Value: UpdateUser. |
|Version |String |Yes |2024\-08\-31 |API version, Value: 2024\-08\-31. |
|Username |String |Yes |user1 |Username |
|Email |String |Yes |xxx@xxx.com |User E\-mail |
|Description |String |Yes |description |Description information |
|Readonly |Boolean |Yes |false |Is it readOnly User? |


<span id="7d4f3516"></span>
## Response parameters

The table below lists only the return parameters specific to this interface. For more details, refer to [request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Param | |Type |Example value |Description |
|---|---|---|---|---|
|Message | |String |None |Top response information |
|Data | |Object |{<br><br>"Message": "update user successfully"<br><br>} |Response Data |
| |Message |String |update user successfully |Response Message |


<span id="b7ee449e"></span>
## Request example

```text
POST /?Action=UpdateUser&Version=2024-08-31 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20240912T130647Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240912/ap-southeast-1/bytehouse_ce/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Username": "user1",
  "Email": "xxx@xxx.com",
  "Description": "description",
  "Readonly": true
}
```


<span id="debb2e7e"></span>
## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20240912210653198048077034DA31F8",
    "Action": "UpdateUser",
    "Version": "2024-08-31",
    "Service": "bytehouse_ce",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Message": "",
    "Data": {
      "Message": "update user successfully"
    }
  }
}
```


<span id="9def0600"></span>
## Error code

The following table lists the error codes related to this interface and business logic. For common error codes, refer to [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).


|Status Code |Error Code |Error Information |Description |
|---|---|---|---|
|400 |Bad Request |api service received invalid request format |Parameter error |
|401 |SignatureNotMatch |The request signature provided is incorrect. | |
|500 |InternalError |The request has failed due to an unknown error. | |
|503 |ServiceUnavailable |The request has failed due to a temporary failure of the server. | |
