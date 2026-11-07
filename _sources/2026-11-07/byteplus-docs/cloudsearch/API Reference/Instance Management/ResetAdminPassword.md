---
title: "ResetAdminPassword"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ResetAdminPassword"
---

Call ResetAdminPassword to reset the password of the administrator account (admin) for an instance.

<span id="26e824d3"></span>
## Precautions


* Resetting the admin password restarts the instance, which may lead to brief service unavailability. We recommend that you call this action during off\-peak hours.

* If an exception occurs during the reset and your password is not updated as a result, the instance continues to use the previous password. You can keep using the original password or try the reset operation again.


<span id="7ad70cd6"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ResetAdminPassword&Version=2023\-01\-01 HTTP/1.1


<span id="eea2368a"></span>
## Request parameters

<span id="f666d585"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ResetAdminPassword` |The action that you want to perform. Value: `ResetAdminPassword`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="33736bd0"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*o718 |The ID of the instance for which you want to reset the password. |
|UserName |String |No |admin |The user whose password you want to reset. Only the password of the `admin` user can be reset. |
|NewPassword |String |Yes |Password\*\*\*\* |The new password. The password must meet the following requirements:<br><br><br>* It must contain at least three of the following character types: uppercase letters, lowercase letters, digits, and special characters. It must be 8–32 characters in length.<br><br>* Supported special characters are `_ # ! @ $ % ^ & * () + = -`, and spaces and Chinese characters are not allowed. |


<span id="874a0ac5"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Status |String |SUCCESSFUL |Whether the request is successful or failed. |
|Message |String | |The message returned. |


<span id="0c9abfb5"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ResetAdminPassword&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k***o718",
    "NewPassword": "Password****",
    "Force": false,
    "UserName": "admin"
}
```


<span id="491f21f3"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202310201********EB17D663",
        "Action": "ResetAdminPassword",
        "Version": "2023-01-01",
        "Service": "ESCloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Status": "SUCCESSFUL",
        "Message": ""
    }
}
```
