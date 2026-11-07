---
title: "GetStreamsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getstreamsapi"
---

Call this API to get the information required for pushing a stream to a live room, or pulling a stream from a third\-party platform to a live room in specific live channels of the live room.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetStreamsAPI&Version=2020-06-01`

* Method: GET


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetStreamsAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|LineDetails |Array of [LineDetails](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |`-` |The live channel information. |


<span id="linedetails"></span>
### LineDetails


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|LineId |Long |`3606624` |The channel ID. |
|LineName |String |`Default` |The channel name. |
|MainPushInfo |Array of [MainPushInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |`-` |Information for pushing the primary stream to the live room. |
|BackPushInfo |Array of [BackPushInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |`-` |The backup stream information used to push a stream to the live room. |
|Ratio |String |`1280x720` |The resolution of the channel. |
|ForwardInfo |Array of [ForwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |`-` |Information for pulling the primary stream from a third\-party platform to the live room.<br><br>The pull stream task is valid for 48 hours after it starts. |
|BackupForwardInfo |Array of [BackupForwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi) |`-` |The backup stream information used to pull a stream from a third\-party platform to the live room.<br><br>The pull stream task is valid for 48 hours after it starts. |
|ExpireTime |Long |`1697167355` |The expiration time of the push stream address in Unix timestamp format. The unit is seconds. |


<span id="mainpushinfo"></span>
### MainPushInfo


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PushPath |String |`rtmps://push-rtmp-l1-act.****.com/live/` |The server URL. |
|PushUrl |String |`rtmps://push-rtmp-l1-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |The push stream address. |
|StreamingCode |String |`stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |The stream key. |


<span id="backpushinfo"></span>
### BackPushInfo


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PushPath |String |`rtmps://push-rtmp-f5-act.****.com/live/` |The server URL. |
|PushUrl |String |`rtmps://push-rtmp-f5-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |The push stream address. |
|StreamingCode |String |`stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334` |The stream key. |


<span id="forwardinfo"></span>
### ForwardInfo


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PullStreamUrl |String |`https://example/livesaas?key=example` |The primary stream URL. |
|PullStreamStatus |String |`0` |The status of the pull stream task. The status changes once you call [UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi) to start or stop pulling the stream.<br><br><br>* `0`: Initializing.<br><br>* `1`: In progress.<br><br>* `2`: Complete. |
|PullStreamCheckStatus |String |`0` |The status of the stream pull check.<br><br><br>* `0`: Checking.<br><br>* `1`: Source stream not pushing.<br><br>* `2`: Stream is being pulled successfully.<br><br>* `3`: Stream pulling ended.<br><br>* `4`: Error in stream pulling. |


<span id="backupforwardinfo"></span>
### BackupForwardInfo


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PullStreamUrl |String |`https://example/livesaas?key=example` |The backup stream URL. |
|PullStreamStatus |String |`0` |The status of the pull stream task. The status changes once you call [UpdatePullToPushAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatepulltopushapi) to start or stop pulling the stream.<br><br><br>* `0`: Initializing.<br><br>* `1`: In progress.<br><br>* `2`: Complete. |
|PullStreamCheckStatus |String |`0` |The status of the stream pull check.<br><br><br>* `0`: Checking.<br><br>* `1`: Source stream not pushing.<br><br>* `2`: Stream is being pulled successfully.<br><br>* `3`: Stream pulling ended.<br><br>* `4`: Error in stream pulling. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetStreamsAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="sample-response"></span>
### Sample response

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetStreamsAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1",
        "SystemTime":1697163541        
   },
  "Result": {
    "LineDetails": [
      {
        "LineId": 3606624,
        "ExpireTime": 1697167355,
        "MainPushInfo": {
          "PushUrl": "rtmps://push-rtmp-l1-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334",
          "PushPath": "rtmps://push-rtmp-l1-act.****.com/live/",
          "StreamingCode": "stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334"
        },
        "BackPushInfo": {
          "PushPath": "rtmps://push-rtmp-f5-act.****.com/live/",
          "StreamingCode": "stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334",
          "PushUrl": "rtmps://push-rtmp-f5-act.****.com/live/stream-2421148009386476461?keeptime=00093a80&wsSecret=7c23ee8c864b672d4f****2d30c1a94b&wsTime=66695334"
        },
        "ForwardInfo": {
          "PullStreamUrl": "https://example/livesaas?key=example",
          "PullStreamStatus": 0,
          "PullStreamCheckStatus": 0
        },
        "LineName": "Default",
        "BackupForwardInfo": {
          "PullStreamUrl": "https://example/livesaas?key=example",
          "PullStreamStatus": 0,
          "PullStreamCheckStatus": 0
        },
        "Ratio": "1280x720"
      }
    ]
  }
}
```
