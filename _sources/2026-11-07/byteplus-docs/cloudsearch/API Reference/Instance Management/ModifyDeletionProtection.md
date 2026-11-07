---
title: "ModifyDeletionProtection"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ModifyDeletionProtection"
---

Call ModifyDeletionProtection to enable or disable the deletion protection feature for an instance.

<span id="369d4796"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ModifyDeletionProtection&Version=2023\-01\-01 HTTP/1.1


<span id="f95117d5"></span>
## Request parameters

<span id="d3376760"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ModifyDeletionProtection` |The action that you want to perform. Value: `ModifyDeletionProtection`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="98fb9bcc"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*o718 |The ID of the instance for which you want to enable or disable the deletion protection feature. |
|DeletionProtection |Boolean |No |true |Whether to enable the deletion protection feature for the instance.<br><br><br>* true: enables deletion protection.<br><br>* false: disables deletion protection. This is the default value.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Once deletion protection is enabled for an instance, the instance cannot be deleted using the API or through the console.</div><br> |


<span id="3abc786e"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Status |String |SUCCESSFUL |Whether the request is successful or failed. |
|Message |String | |The message returned. |


<span id="a1bf9ed2"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyDeletionProtection&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "DeletionProtection": true,
    "InstanceId": "o-00k***o718"
}
```


<span id="ec1738e7"></span>
## Response parameters

```json
{
    "ResponseMetadata": {
        "RequestId": "202310201***7B426409B8CC",
        "Action": "ModifyDeletionProtection",
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
