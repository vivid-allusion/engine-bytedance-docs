---
title: "DeleteGtm"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/DeleteGtm"
---

Deletes a GTM instance.

<span id="request"></span>
## Request


* Method: POST

* URL: https://gtm.byteplusapi.com/?Action=DeleteGtm&Version=2023\-01\-01


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If you want BytePlus GTM to stop billing for a GTM instance, you need to delete that GTM instance.</div>


* <div data-tips="true" data-tips-type="tip">After deleting a GTM instance, the DNS resolution from the routing domain to the addresses will also be deleted.</div>



<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Please consider carefully before deleting a GTM instance. A deleted GTM instance cannot be recovered and can only be recreated. If you only want to temporarily disable the failover of the GTM instance while retaining the DNS resolution from the routing domain to the target addresses, you can call the <a href="https://docs.byteplus.com/docs/byteplus-dns-suite/StopRouting">StopRouting API</a> to stop automatic traffic routing.</div>


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you need to [authenticate the request](https://docs.byteplus.com/docs/byteplus-dns-suite/FvV-sD).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DeleteGtm` |The name of the API. The value of this parameter is `DeleteGtm`. |
|Version |String |Yes |`2023-01-01` |The version of the API. The value of this parameter is `2023-01-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|GtmId |String |Yes |`e93cb374-2b33-4202-842f-c066a4462c03` |The UUID of the GTM instance. You can obtain the `GtmId` through the [ListGtms API](https://docs.byteplus.com/docs/byteplus-dns-suite/CrGpNh). |


<span id="response-parameters"></span>
## Response parameters

<span id="responsemetadata-object"></span>
### ResponseMetadata object


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

```JSON
POST https://gtm.byteplusapi.com/?Action=DeleteGtm&Version=2023-01-01
{
    "GtmId":"fd5277c1-74ea-4ff8-aa44-0020bc612e1c"
}
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2024072207544336CB2B2F6A39290EC031",
        "Action": "DeleteGtm",
        "Version": "2023-01-01",
        "Service": "gtm",
        "Region": "ap-southeast-1"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/PujiSz).
