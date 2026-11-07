---
title: "ModifyChargeCode"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/ModifyChargeCode"
---

Call ModifyChargeCode to change the billing method of an instance from pay\-as\-you\-go to subscription.

<span id="36ca4c94"></span>
## Request Description


* Request method: POST

* Request URL: /?Action=ModifyChargeCode&Version=2023\-01\-01 HTTP/1.1


<span id="c2fec432"></span>
## Request parameters

<span id="eff4dc33"></span>
### Query


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`ModifyChargeCode` |The action that you want to perform. Value: `ModifyChargeCode`. |
|Version |String |Yes |`2023-01-01` |The version of the API. Value: `2023-01-01`. |


<span id="b66b8e2f"></span>
### Body


|**Name** |**Type** |**Required** |**Example** |**Description** |
|---|---|---|---|---|
|InstanceId |String |Yes |o\-00k\*\*\*718 |The ID of the instance whose billing method you want to change. |
|ToChargeType |String |Yes |PrePaid |The new billing method. Set the value to `PrePaid`. You can only change the billing method from pay\-as\-you\-go to subscription. |
|AutoRenew |Boolean |Yes |true |Whether to enable automatic renewal.<br><br><br>* true: enables automatic renewal.<br><br>* false: disables automatic renewal. |
|IncludeMonths |Int |Yes |5 |The subscription duration of the instance. Unit: `months`. |


<span id="3bdee48a"></span>
## Response parameters


|**Name** |**Type** |**Example** |**Description** |
|---|---|---|---|
|InstanceId |String |o\-00k\*\*\*718 |The instance ID returned after the billing method is changed. |


<span id="f9f4321e"></span>
## Sample request

```HTTP
POST https://open.ap-southeast-1.byteplusapi.com/?Action=ModifyChargeCode&Version=2023-01-01
Content-Type: application/json
X-Date: 20231003T104027Z
Authorization: HMAC-SHA256 
Credential=AKLTMjI2ODVlYzI3ZGY1NGU4ZjhjYWRjMTlmNTM5OTZ****/20231003/ap-southeast-1/ESCloud/request, SignedHeaders=content-type;host;x-date, Signature=88dd0a9ea555d8609ec83eb46054b52f6cd4f79b8d5094fa784c66fa3f2b****
{
    "AutoRenew": true,
    "IncludeMonths": 5,
    "InstanceId": "o-0080**iu98",
    "ToChargeType": "PrePaid"
}
```


<span id="f5b7871c"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20231116150829349***99926C7",
        "Action": "ModifyChargeCode",
        "Version": "2023-01-01",
        "Service": "escloud",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "o-008***u98"
    }
}
```
