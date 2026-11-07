---
title: "ListTicket"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListTicket-en"
---

Gets the list of function release records.

<span id="limits"></span>
## Limits

Request rate limit: Maximum 20 requests per second.

<span id="usage"></span>
## Usage


* Request Method: GET

* Request URL: https://cdn.byteplusapi.com?Action=ListTicket&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request parameters

<span id="query"></span>
### Query


|Parameter |Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |API name. The name of the current API is `ListTicket`. |
|Version |String |Yes |API version. The version of the current API is `2021-03-01`. |
|FunctionId |String |Yes |Function ID. You can call [ListFunction](https://docs.byteplus.com/en/docs/byteplus-cdn/edge-functions-api-ref-ListFunction-en) to get the function ID. |
|Page |Integer |No |Page number. |
|Limit |Integer |No |Number of records per page. Default is 50. Maximum is 50. |
|OrderBy |Integer |No |Data order.<br><br><br>* 1 indicates descending order<br><br>* 2 indicates ascending order<br><br><br>Default is ascending order by function ID. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Type |Description |Example value |
|---|---|---|---|
|Tickets |Object[] |List of release records. | |
|Id |Long |Release record ID. |`1` |
|FunctionId |String |Function ID. |`23455331245` |
|Content |String |Content of the release record. |`{&quot;current_traffics&quot;:[{&quot;version_tag&quot;:&quot;1.0.1&quot;}],&quot;origin_traffics&quot;:[]}` |
|Status |Integer |Release status.<br><br><br>* 100: Canary release successful<br><br>* 200: Full release successful |`100` |
|Description |String |Description of the release record. |`this is a release` |
|Creator |String |Creator of the release record. |`example` |
|CreateTime |Long |Creation time. The format is Unix timestamp (seconds). |`1638326159` |
|UpdateTime |Long |Update time. The format is Unix timestamp (seconds). |`1638326159` |
|TotalCount |Long |Number of release records. |`1` |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```HTTP
GET  https://cdn.byteplusapi.com?Action=ListTicket&Version=2021-03-01&FunctionId=23455331245&Page=1&Limit=10&OrderBy=2
```


<span id="response-example"></span>
### Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "2022011310531001022511001100*****",
        "Action": "ListTicket",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tickets": [
            {
                "Id": 133,
                "FunctionId": "23455331245",
                "Content": "{\"current_traffics\":[{\"version_tag\":\"1.0.1\"}],\"origin_traffics\":[]}",
                "Description": "test publish",
                "Creator": "****",
                "CreateTime": 1640077698,
                "UpdateTime": 1640077759
            }
        ],
        "TotalCount": 1
    }
}
```
