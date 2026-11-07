---
title: "GetGtm"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/CHmr_V"
---

Gets information of a GTM instance.

<span id="request"></span>
## Request


* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=GetGtm&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetGtm` |The name of the API. The value of this parameter is `GetGtm`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |
|GtmId |String |Yes |`GtmId` |The UUID of the BytePlus GTM instance. You can obtain the `GtmId` through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |


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


<span id="result-object"></span>
### Result Object


|Name |Type |Description |
|---|---|---|
|GtmId |String |The UUID of the BytePlus GTM instance. |
|Domain |String |The domain name of the BytePlus GTM instance. |
|Cname |String |The routing domain name of the BytePlus GTM instance. |
|PolicyType |String |The policy type. The value of this parameter can be:<br><br><br>* geo: Basic routing policy.<br><br>* perf: Intelligent routing policy. |
|Ttl |Integer |The expiration time of the DNS record. The unit is seconds. |
|Remark |String |The remark information of the BytePlus GTM instance. |
|AlarmId |String |The ID of the alarm rule bound to this BytePlus GTM instance. |
|AccessMode |String |The access mode of the BytePlus GTM instance.<br><br><br>* cname: BytePlus GTM automatically generates a routing domain name based on your domain name. According to your traffic scheduling configuration in BytePlus GTM, BytePlus GTM resolves this routing domain name to the IP or domain name of the target address. You need to create a CNAME record at your DNS service provider and then point your domain name to this routing domain name.<br><br>* domain: Resolve your domain name to the IP or domain name of the target address. You can only use this access mode when your domain name's DNS service provider is BytePlus DNS. |
|CreateTime |String |The creation time of the BytePlus GTM instance. Accurate to milliseconds. The format complies with the ISO 8601 standard. |
|UpdateTime |String |The most recent modification time of the BytePlus GTM instance. Accurate to milliseconds. The format complies with the ISO 8601 standard. |
|State |String |This parameter is invalid. Please ignore this parameter. |
|Owner |String |The BytePlus account of the user who created this BytePlus GTM instance. |
|LastOperator |String |The BytePlus account of the last user who operated on this BytePlus GTM instance. |
|SpecName |String |The edition of the BytePlus GTM instance. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
POST https://gtm.byteplusapi.com/?Action=GetGtm&Version=2023-01-01&GtmId=fd5277c1-74ea-4ff8-aa44-0020bc612e1c
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20240722073056855D411AF1C94D0DB0C0",
        "Action": "GetGtm",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "GtmId": "fd5277c1-74ea-4ff8-aa44-0020bc612e1c",
        "Domain": "test.example.com",
        "Cname": "",
        "PolicyType": "geo",
        "Ttl": 600,
        "Remark": "",
        "AlarmId": "",
        "AccessMode": "domain",
        "CreateTime": "2024-07-22T06:46:14.499Z",
        "UpdateTime": "2024-07-22T06:46:14.499Z",
        "State": "init",
        "Owner": "30*****32",
        "LastOperator": "30*****32",
        "SpecName": "ultimate"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
