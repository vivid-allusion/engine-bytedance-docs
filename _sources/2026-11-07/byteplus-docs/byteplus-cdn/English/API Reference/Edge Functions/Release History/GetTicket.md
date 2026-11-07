---
title: "GetTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-GetTicket-en"
---

Gets a release record.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=GetTicket&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `GetTicket`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|TicketId |Long |Yes |Release record ID. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|Ticket |Object |Release record details. | |
|Id |Long |Release record ID |`1` |
|FunctionId |String |Function ID. |`23455331245` |
|Content |String |Content of the release record. |`{&quot;current_traffics&quot;:[{&quot;version_tag&quot;:&quot;1.0.1&quot;}],&quot;origin_traffics&quot;:[]}` |
|Status |Integer |Release status.<br><br><br>* 100: Canary release successful<br><br>* 200: Full release successful |`100` |
|Description |String |Description |`this is a release` |
|Creator |String |Creator |`example` |
|CreateTime |Long |Creation time |`1638326159` |
|UpdateTime |Long |Update time |`1638326159` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=GetTicket&Version=2021-03-01&FunctionId=3gyz993****&TicketId=28
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "GetTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Ticket":
         {
            "Id": 133,
            "FunctionId": "3gyz993****",
            "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
            "Description": "test publish",
            "Creator": "****",
            "CreateTime": 1640077698,
            "UpdateTime": 1640077759
        }
    }
}
```
