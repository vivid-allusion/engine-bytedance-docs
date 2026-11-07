---
title: "ResumeLiveStreamAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-resumelivestreamapi"
---

Call this API to resume forbidden streams from specific live sources in a live room.

If you want to re\-forbid a stream after resuming it, ensure you call [ForbidLiveStreamAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-forbidlivestreamapi) at least 30 seconds after calling this API operation.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ResumeLiveStreamAPI&Version=2020-06-01`

* Method: POST


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ResumeLiveStreamAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="body"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Integer |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|LineId |Array of Integer |No |`[356218,356219]` |The IDs of live sources whose streams you want to resume. If not specified, streams in all sources of the live room are resumed.<br><br>A live room can have multiple sources, each with its own stream. You can get the source IDs of the live room by calling [GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi). |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Status |Boolean |`true` |Indicates whether the specified streams were resumed.<br><br><br>* `true`: All specified streams were resumed.<br><br>* `false`: At least one specified stream was not resumed. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=ResumeLiveStreamAPI&Version=2020-06-01
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
        "Action": "ResumeLiveStreamAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1662570420
    },
    "Result": {
        "Status": true
    }
}
```


<span id="error-codes"></span>
## Error codes

The following table lists error codes specific to this API operation. For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |200027 |You cannot resume streams that are forbidden because of enabling the live stream start time or end time feature. To resume such streams, you must disable these features. |Disable the 'live stream start time' and 'end time' features on the BytePlus Live console or by calling [UpdateActivityBasicConfigAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateactivitybasicconfigapi). |
