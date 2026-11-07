---
title: "DeleteZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-deletezone"
---

Deletes a domain.

You can only delete domains belonging to the free edition. You cannot delete domains belonging to other editions.

<span id="usage"></span>
## Usage


* Rate limit: 5 calls per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=DeleteZone?Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`DeleteZone` |The name of the API. The value of this parameter is `DeleteZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZID |Integer |Yes |`1234` |The ID of the domain to be deleted. You can get the domain ID by [CreateZone API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-createzone) or [ListZones API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listzones). |


<span id="response-body"></span>
## Response body

<span id="responsemetadata-object"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="80d026c6"></span>
## Example

<span id="598f3d44"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=DeleteZone
{
  "ZID": 1234
}
```


<span id="ec726bcd"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202112151945020102251331430333B652",
        "Action": "DeleteZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
