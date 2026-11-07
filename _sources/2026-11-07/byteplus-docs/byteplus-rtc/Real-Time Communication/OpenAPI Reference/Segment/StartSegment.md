---
title: "StartSegment"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-155129"
---

In an audio & video application, you can segment audio streams in the room for processing later including moderating the content.

You can call the `StartSegment` OpenAPI to do this.

<span id="description"></span>
## Description

By calling the `StartSegment` interface, you can segment specified audio streams in a room under your `AppId`.

The result of snapshot will be uploaded to the storage platform you select.The [callback address](https://console.byteplus.com/rtc/cloudRTC?tab=callback) you set on the console will receive a metadata callback for each result. About details about callback, see [SegmentRealTimeData](https://docs.byteplus.com/en/docs/12/docs-75125#segmentrealtimedata)

<span id="prerequisites"></span>
## Prerequisites

Before using the function, you need to go to [console](https://console.byteplus.com/rtc) to enable Segment service.

<span id="make-a-call"></span>
## Make a call

For the service address, communication protocol, character encoding, and signature mechanism of the interface, see [Call OpenAPI](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828).

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StartSegment&Version=2022\-06\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StartSegment` |Interface name. The value of this interface: `StartSegment` |
|Version |String |Yes |`2022-06-01` |OpenAPI version. The value of this interface: `2022-06-01` |


<span id="body-parameters"></span>
### Body parameters


|Whether to enable mix\-streaming segment.<br><br>'Mixed' is a switch to enable mixing\-stream segment, whose default value is `False`.<br><br><br>* When `Mixed = False`, only the audio streams specified in `TargetStreams` will be segmented separately.<br><br>* When `Mixed = True`, the audio streams specified in `TargetStreams` will be segmented separately, and the specified audio streams will also be mixed to generate a file, and the username of the mixing\-stream file is `mixed`. After the task is created, callbacks for the mixed\-stream segment will continue to be triggered regardless of whether someone is on the mic or not.<br><br><br>For callbacks on different platforms, see:<br><br>&nbsp;<br><br> | | | | |
|---|---|---|---|---|
|IgnoreSilence |Boolean |No |`false` |Whether to ignore silent segmented file |
|RedundantDuration |Integer |No |`2` |Duration of redundant segment, in seconds.<br><br>&nbsp;<br><br>Redundant segment The server segments by the fixed `Duration`, so there may be cases where sensitive words are truncated or unrecognized. In such cases, you can add a redundant segment which is the end of the previous segment, and the duration of the segment will be `RedundantDuration`+ `Duration`.<br><br>&nbsp;<br><br>For example, when `Duration`= `20` and `RedundantDuration`= `3`, the duration of final output files are: [0\-20], [17\-40], [37\-60]. |
|VadConfig |Object |No | |VAD (Voice Activity Detection) configuration. |
|Enable |Boolean |No |`false` |Whether to enable VAD.<br><br><br>* `true`: Enabled. The system performs voice activity detection on each audio slice. Slices in which no human voice is detected are filtered out and will not be stored or delivered via callback, saving storage cost and downstream processing resources.<br><br>* `false` (default): Disabled. All audio slices are stored and delivered via callback normally, without any VAD\-based filtering. |
|Mode |Integer |No |`2` |Strictness level of VAD detection. Valid range: `[0, 3]`. A larger value indicates a stricter detection, which is more likely to classify ambiguous audio as non\-voice.<br><br><br>* `0`: Most lenient. Highest recall — human voice is rarely missed, but background noise may be misclassified as voice.<br><br>* `1`: Lenient.<br><br>* `2` (default): Balanced mode. A good trade\-off between recall and precision.<br><br>* `3`: Strictest. Highest precision — fewest false positives, but faint human voice may be missed.<br><br><br>warning<br><br>This field only takes effect when `Enable` is `true`. |
|SpeechRatioThreshold |Float |No |`0.15` |Speech\-frame ratio threshold. Defines the minimum proportion of speech duration required for an audio slice to be classified as "containing human voice". A slice is classified as containing voice only when the number of speech frames detected by VAD divided by the total number of frames is greater than or equal to this threshold.<br><br><br>* **Valid range**: `(0.0, 1.0]`.<br><br>* **Default**: `0.15`.<br><br>* A smaller value (e.g. `0.05`) makes detection more sensitive — slices are more easily classified as containing voice.<br><br>* A larger value (e.g. `0.5`) makes detection more conservative — more obvious speech activity is required for a slice to be classified as containing voice.<br><br><br>warning<br><br>This field only takes effect when `Enable` is `true`. |
|Identifier |String |No |`Your_Identifier` |Prefix of customized filename.<br><br>The filename consists of `Identifier` + `UserId` + `timestamp` + `sequence number`. By default, the `Identifier` is a randomly generated UUID . When customizing a filename, the naming rules of the Identifier refer to the [ID](https://docs.byteplus.com/docs/byteplus-rtc/docs-115995). |
|Handle |Boolean |No |`true` |Whether to start segmenting immediately when this function is turned on. `True` means to start segmenting immediately when this function is turned on; `False` means to start a task but not segmenting immediately when this function is turned on. The default value is `true`. |


<span id="response-parameters"></span>
## Response parameters

`Result` returns "ok" only when the request succeeds and null when it fails.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StartSegment&Version=2022-06-01
{
    "AppId": "Your_AppId",
    "BusinessId": "Your_BusinessId",
    "RoomId": "Your_RoomId",
    "TaskId": "Your_TaskId",
    "MaxIdleTime": 200,
    "TargetStreams": {
        "StreamList": [
            {
                "UserId": "user1", 
                "StreamType": 0
            },
            {
                "UserId": "user1", 
                "StreamType": 0
            }
        ]
    },
    "Duration": 20,
    "StorageConfig": {
        "Type": 2,
        "TosConfig": {
            "Vendor": 0,
            "Region": 0,
            "Bucket": "Your_Bucket",
            "AccessKey": "Your_AccessKey",   
            "SecretKey": "Your_SecretKey"
        }
    },
    "Control" : { 
        "Align" : true, 
        "Mixed" : true, 
        "RedundantDuration" : 2, 
        "IgnoreSilence" : true 
     }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StartSegment",
        "Version": "2022-06-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
