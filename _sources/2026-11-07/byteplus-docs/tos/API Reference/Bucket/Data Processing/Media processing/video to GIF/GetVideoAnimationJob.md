---
title: "GetVideoAnimationJob"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetVideoAnimationJob"
---

<span id="60a44605"></span>
## Description

This interface queries the asynchronous task status of video\-to\-animation conversion.

<span id="f2c564a8"></span>
## Notes


* When using a sub\-account, it must have the relevant permissions required for `GetDataProcessJob` data processing.

* Querying audio and video asynchronous tasks supports only synchronous processing (`x-tos-process` processing mode).


<span id="6601990a"></span>
## Request syntax

```HTTP
GET /?job_type=Transcode&job_id=183535129563a53bfa71000188********** HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="19d57b8d"></span>
## Request parameters and headers 

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|Name |  |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|job_type |Query |String |Yes |Transcode |Audio and video task types. Supported query types currently include:<br><br><br>* `Transcode`<br><br>* `Remux`<br><br>* `Animation` |
|job_id |Query |String |Yes |183535129563a53bfa71000188\*\*\*\*\*\*\*\*\*\* |Audio and video task ID. |


<span id="d0cb9a0c"></span>
## Request body elements

No elements are used.

<span id="bc88286b"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="e4935f21"></span>
## Response body elements

<span id="70025aa1"></span>
### Common elements


|Name |Type |Example value |Description |
|---|---|---|---|
|JobID |String |183535129563a53bfa71000188\*\*\*\*\*\*\*\*\*\* |Task ID. |
|CreateTime |String |2025\-11\-18T20:32:54+08:00 |Task creation time. |
|StartTime |String |2025\-11\-18T20:32:55+08:00 |Task start time. |
|EndTime |String |2025\-11\-18T20:32:55+08:00 |Task end time. |
|State |String |Success |Task status. |
|Code |Integer |0 |Task status code. |
|Message |String |Success |Task status message. |
|Input |Container |\- |Input file. |
|Object |String<br><br> |sample.mp4 |Enter the input file object name.<br><br>Parent node: `Input`. |
|Output |Container |\- |Output file. |
|Region |String |cn\-beijing |Region where the output file bucket is located.<br><br>Parent node: `Output`. |
|Bucket |String |testbkt |Output file bucket name.<br><br>Parent node: `Output`. |
|Object |String |output.gif |Name of the output file object.<br><br>Parent node: `Output`. |


<span id="32263365"></span>
### Additional elements returned when the task type is Animation


|Field name |Type |Example value |Description |
|---|---|---|---|
|Width |Integer |1024 |Output GIF width in px, range [32,4096].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If set to 0, it calculates automatically based on the source video's resolution ratio.</div><br> |
|Height |Integer |1024 |Height of the output animation in px, range [32,4096].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If set to 0, it calculates automatically based on the source video's resolution ratio.</div><br> |
|Fps |Integer |30 |Animated image frame rate. The default value is automatically calculated from the interval of the source video. Range: [0, 240].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter controls the playback speed of the animated image. The default value matches the source video's playback speed. Values higher than the default will speed up playback; values lower will slow it down.</div><br> |
|FrameInterval |Integer |1 |GIF frame extraction interval in milliseconds; by default, all video frames are extracted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this parameter is less than the source video's frame interval (the inverse of the frame rate), frame extraction follows the source video frame interval.</div><br> |
|FrameNum |Integer |100 |Number of animated frames, default is unlimited (frames extracted until the video ends).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the video length is insufficient, the actual number of extracted frames will be less than the set parameter.</div><br> |
|ScaleType |String |crop |Zoom mode. The options are as follows:<br><br><br>* `crop`: Scale and crop.<br><br>* `stretch` (Default): Stretch to fill.<br><br>* `fill`: Scale and maintain black borders.<br><br>* `fit`: Scale without preserving black borders, proportional scaling. |


<span id="e217ce0c"></span>
## Sample request

```Plain Text
GET /?job_type=Animation&job_id=183535129563a53bfa71000188********** HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="805b8204"></span>
## Sample response

```Plain Text
{
    "JobID": "183535129563a53bfa71000188**********",
    "CreateTime": "2026-03-26T10:28:19+08:00",
    "StartTime": "2026-03-26T10:28:19+08:00",
    "EndTime": "2026-03-26T10:28:19+08:00",
    "State": "Success",
    "Error": "",
    "Code": 0,
    "Message": "success",
    "Input": {
        "Object": "sample.mp4"
    },
    "AnimationConfig": {
        "TimeInterval": {
            "Start": 1000,
            "Duration": 0
        },
        "Container": {
            "Format": "gif"
        },
        "Animation": {
            "Width": 0,
            "Height": 0,
            "Fps": 10,
            "FrameInterval": 200,
            "FrameNum": 10,
            "ScaleType": ""
        }
    },
    "Output": {
        "Region": "cn-beijing",
        "Bucket": "testbkt",
        "Object": "output.gif"
    },
    "Tag": "Animation"
}
```
