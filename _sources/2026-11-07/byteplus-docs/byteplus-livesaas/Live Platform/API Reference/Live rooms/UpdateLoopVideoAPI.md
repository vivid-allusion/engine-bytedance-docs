---
title: "UpdateLoopVideoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateloopvideoapi"
---

Call this API to edit the configuration of a looped video for a specified live\-streaming activity.

<span id="request"></span>
## Request

<span id="details"></span>
### Details


* API operation: `UpdateLoopVideoAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="query-string-parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |


<span id="body-parameters"></span>
### Body parameters


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|ActivityId |Yes |Integer |ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|LineId |Yes |Integer |ID of the live stream. You can get the ID by calling [GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi). |
|LoopNumber |Yes |Integer |The number of times the video is played. Currently, you can only set it to `1`. |
|LoopVideo |Yes |Array of [LoopVideo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideoapi) |Configuration for looped playback. |


<span id="loopvideo"></span>
#### LoopVideo


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Index |Yes |Integer |Video index, starting from `1`, increasing sequentially. |
|VideoCoverImage |No |Integer |Cover image of the video. This parameter is deprecated. |
|VideoName |Yes |String |Video name. |
|VideoVid |Yes |String |The unique ID of the video. You can get the ID by calling [ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi). |


<span id="sample-request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "LineId":1234,
    "LoopNumber":1,
    "LoopVideo":[
        {
            "Index":1,
            "VideoName":"video.mp4",
            "VideoVid":"v02a49370000b****gbiokkno91"
        }
    ]
}
```


<span id="response"></span>
## Response

<span id="response-schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Id |Integer |The ID of the looped playback configuration. |


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata":{
    "RequestId":"201806041104200100100232280022D30",
    "Action":"UpdateLoopVideoAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
  "Result":{
   "Id": 123
}
}
```
