---
title: "GetLiveStreamForbidStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi"
---

Call this API to check whether the stream of a specific live source in a live room is forbidden.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetLiveStreamForbidStatusAPI&Version=2020-06-01`

* Method: POST


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetLiveStreamForbidStatusAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="body"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Integer |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|LineId |Array of Integer |No |`[356218,356219]` |The IDs of live sources. If this parameter is omitted, the API returns the stream statuses for all sources in the live room.<br><br>A live room can have multiple live sources and each source has its own stream. You can get the source IDs of the live room by calling [GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi). |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|StreamForbidStatus |Array of [ForbidStatus](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getlivestreamforbidstatusapi) |`-` |The stream statuses for the specified sources. |


<span id="forbidstatus"></span>
### ForbidStatus


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|StreamStatus |Integer |`0` |The status of the stream.<br><br><br>* `0`: Not forbidden.<br><br>* `1`: Forbidden. |
|ForbidTime |String |`2024-07-13T02:59:50Z` |The time (UTC+0) until which the stream is forbidden.<br><br>A value of `"0"` indicates that the stream is not forbidden. |
|LineId |Integer |`356218` |The live source ID. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetLiveStreamForbidStatusAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "LineId": [356218,356219]
}
```


<span id="sample-response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "GetLiveStreamForbidStatusAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1718161649
    },
    "Result": {
        "StreamForbidStatus": [
            {
                "StreamStatus": 0,
                "ForbidTime": "0",
                "LineId": 356218
            },
            {
                "StreamStatus": 1,
                "ForbidTime": "2024-07-13T02:59:50Z",
                "LineId": 356219
            }
        ]
    }
}
```
