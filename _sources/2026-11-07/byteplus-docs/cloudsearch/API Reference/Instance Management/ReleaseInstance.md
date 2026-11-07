---
title: "ReleaseInstance"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ReleaseInstance"
---

Call ReleaseInstance to delete or release an instance.

<span id="90a4ce23"></span>
## Precautions


* When you call the ReleaseInstance action, the specified instance is released without secondary confirmation immediately after the request is sent. Once the delete operation starts, it cannot be paused or revoked. After deletion, all configurations and data of the instance are permanently destroyed and cannot be recovered. Exercise caution when you call this action.

* If a subscription instance is released, refunds are handled according to the unsubscription and refund rules. For more information, refer to [Unsubscription management](https://docs.byteplus.com/en/docs/cloudsearch/Costs-of-unsubscription).

* If your instance has deletion protection enabled, it cannot be deleted directly by calling this action. To delete such an instance, call [ModifyDeletionProtection](https://docs.byteplus.com/docs/cloudsearch/ModifyDeletionProtection) to disable the deletion protection feature and then call this action.


<span id="16e64a5c"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ReleaseInstance&Version=2023\-01\-01 HTTP/1.1


<span id="1c7bca6b"></span>
## Request parameters

<span id="ba2c43ea"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ReleaseInstance` |The action that you want to perform. Value: `ReleaseInstance`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="0b1d4667"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*o718 |The ID of the instance that you want to release. |


<span id="cef45d0f"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|Status |String |SUCCESSFUL |Whether the request is successful or failed. |
|Message |String | |The message returned. |


<span id="b170abf5"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ReleaseInstance&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "InstanceId": "o-00k***o718"
}
```


<span id="ac83809b"></span>
## Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20231020******30C5380B5810",
        "Action": "ReleaseInstance",
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
