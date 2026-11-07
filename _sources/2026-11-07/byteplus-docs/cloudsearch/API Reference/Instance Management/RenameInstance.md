---
title: "RenameInstance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/RenameInstance"
---

Call RenameInstance to rename an instance.

<span id="2776e54e"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=RenameInstance&Version=2023\-01\-01 HTTP/1.1


<span id="1941f03b"></span>
## Request parameters

<span id="56ef12a5"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`RenameInstance` |The action that you want to perform. Value: `RenameInstance`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="b30922c0"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k0\*\*\*o718 |The ID of the instance that you want to rename. |
|NewName |String |Yes |doc\-test\-1 |The new custom name of the instance.<br><br><br>* It can contain only letters, digits, Chinese characters, hyphens ( \- ), and underscores ( _ ), and it cannot start or end with a digit or a hyphen ( \- ).<br><br>* It must be 1–128 characters in length. |


<span id="6b1821f9"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Status |String |SUCCESSFUL |Whether the request is successful or failed. |
|Message |String | |The message returned. |


<span id="860a62f8"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=RenameInstance&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k0***o718",
    "NewName": "doc-test-1"
}
```


<span id="48e7ccb9"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202310201407***2CF35308FA73",
        "Action": "RenameInstance",
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
