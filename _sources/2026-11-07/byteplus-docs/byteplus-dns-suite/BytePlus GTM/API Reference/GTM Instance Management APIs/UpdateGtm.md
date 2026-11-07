---
title: "UpdateGtm"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/SYFqCs"
---

Updates a GTM instance.

<span id="request"></span>
## Request


* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=UpdateGtm&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateGtm` |The name of the API. The value of this parameter is `UpdateGtm`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|GtmId |String |Yes |`2a8f91c4-aa07-4ae4-9ebc-68750d611822` |The UUID of the BytePlus GTM instance. You can obtain the `GtmId` through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |
|Ttl |Integer |No |`60` |The expiration time of the DNS record cache in the BytePlus GTM instance. |
|Remark |String |No |`Remark` |The remark for the BytePlus GTM instance. UTF\-8 format. The maximum length is 128 UTF\-8 characters. |
|AlarmId |String |No |`157284163494346****` |The ID of the alarm rule bound to the BytePlus GTM instance. |
|PolicyType |String |No |`geo` |The policy in effect in the BytePlus GTM instance.<br><br><br>* **geo**: Basic routing.<br><br>* **perf**: Intelligent routing. |


<span id="response-parameters"></span>
## Response Parameters

<span id="responsemetadata-object"></span>
### ResponseMetadata Object


|Name |Type |Description |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The API version. |
|Service |String |The service type. |
|Region |String |The region where the service is located. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=UpdateGtm&Version=2023-01-01
{
    "GtmId":"fd5277c1-74ea-4ff8-aa44-0020bc612e1c",
  "Remark": "test"
}
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2024072207544336CB2B2F6A39290EC031",
        "Action": "UpdateGtm",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
