---
title: "QueryMediaJob"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/QueryMediaJob"
---

<span id="a180eac4"></span>
## Description

This interface queries the processing status of asynchronous audio and video tasks.

<span id="4fa4202b"></span>
## Notes


* Querying asynchronous audio and video tasks only supports synchronous processing (x\-tos\-process method).

* You must have the relevant permissions required for `GetDataProcessJob` data processing.


<span id="ab3b6e8f"></span>
## Request syntax

```HTTP
GET /?job_type=Transcode&job_id=183535129563a53bfa71000188********** HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="0f91f283"></span>
## Request parameters and headers 

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** | ** ** Location |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|job_type |Query |String |Yes |Transcode |Audio\-video task type. The currently supported query task types are:<br><br><br>* `Transcode`<br><br>* `Remux`<br><br>* `Animation` |
|job_id |Query |String |Yes |183535129563a53bfa71000188\*\*\*\*\*\*\*\*\*\* |Audio and video task ID. |


<span id="2a64f58c"></span>
## Request body elements

No elements are used.

<span id="45de9113"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements

<span id="0c204390"></span>
### Common elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|JobID |String |fa81ef2a00a2211f08a9aa5\*\*\*\*\*\*\*\*\*\* |Task ID. |
|CreateTime |String |2025\-11\-18T20:32:54+08:00 |Task creation time. |
|StartTime |String |2025\-11\-18T20:32:55+08:00 |Task start time. |
|EndTime |String |2025\-11\-18T20:32:55+08:00 |Task end time. |
|State |String |Success |Task status. |
|Code |Integer |0 |Task status code. |
|Message |String |Success |Task status message. |
|Input |Container |\- |Input file. |
|Object |String<br><br> |sample.mp4 |Input file object name.<br><br>Parent node: `Input`. |
|Output |Container |\- |Output file. |
|Region |String |cn\-beijing |The region where the output file bucket is located.<br><br>Parent node: `Output`. |
|Bucket |String |testbkt |Output file bucket name.<br><br>Parent node: `Output`. |
|Object |String |output.mp4 |Output file object name.<br><br>Parent node: `Output`. |


<span id="e7b59a5c"></span>
### Additional elements returned when the task type is Transcode


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|TranscodeConfig |Container |\- |Specific configuration for video transcoding. |
|Transcode |Container |\- |Specific configuration for video transcoding.<br><br>Parent node: `TranscodeConfig`. |
|TimeInterval |Container |\- |Specify the time segment for video transcoding.<br><br>Parent node: `Transcode`. |
|Start |Integer |0 |Video start time in milliseconds.<br><br>Parent node: `TimeInterval`. |
|Duration |Integer |1000 |Video duration in milliseconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If <code>Start</code> and <code>Duration</code> are not set, the entire video will be transcoded.</div><br><br><br>Parent node: `TimeInterval`. |
|Container |Container |\- |Video container format.<br><br>Parent node: `Transcode`. |
|Format |String |ts |The container format of the transcoded video file. The options are as follows:<br><br><br>* `mp4`.<br><br>* `ts`.<br><br><br>Parent node: `Container`. |
|Video |Container |\- |Video encoding.<br><br>Parent node: `Transcode`. |
|Codec |String |H.264 |Video codec format, possible values are:<br><br><br>* `H.264`<br><br>* `H.265`<br><br><br>Parent node: `Video`. |
|Width |Integer |4096 |Video file width, must be an even number, unit px, value range is [128, 4096].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If only <code>Width</code> is set without <code>Height</code>, the video file height will be calculated based on the original aspect ratio.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If only <code>Height</code> is set and <code>Width</code> is not set, the video file width will be calculated based on the original video aspect ratio.</div><br><br><br><br>Parent node: Video |
|Height |Integer |1024 |Video file height, must be an even number, in px, range [128, 4096].<br><br>Parent node: `Video`. |
|Crf |Integer |25 |Video file bitrate.<br><br>Parent node: `Video`. |
|PixFmt |String |yuv420p |Video pixel format, value is `yuv420p`.<br><br>Parent node: `Video`. |


<span id="8406e289"></span>
### Additional elements returned when the task type is Remux


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|RemuxConfig |Container |\- |Specific configuration for audio and video transmuxing. |
|Format |String |MP4 |Audio and video container formats.<br><br>Supported:<br><br><br>* `mp4`<br><br>* `mkv`<br><br>* `avi`<br><br>* `mkv`<br><br>* `ts`<br><br>* `mp3`<br><br>* `aac`<br><br>* `flac`<br><br><br>Parent node: `RemuxConfig`. |
|TranscodeIndex |String |0 |Specify the stream index to process; only the specified audio and video streams will be retained in the output file.<br><br>All streams are processed by default.<br><br>Parent Node: `RemuxConfig`. |
|AIGCMetadata |Container |\- |Identifier for AIGC metadata content.<br><br><br>* The encapsulation format supports only `mp4` when not `nil`;<br><br>* All fields under AIGCMetadata have a length limit of 22048 UTF\-8 characters, restricted to characters within the GB18030\-2022 (ASCII) code range 0x21 \- 0x7E.<br><br><br>Parent node: `RemuxConfig`. |
|Label |String |test_label |Generate synthetic tag elements to indicate whether the video is, may be, or is suspected to be AI\-generated content.<br><br>Parent node: `AIGCMetadata`. |
|ContentProducer |String |test_content_producer |Generate the synth service provider element, containing the name or code of the video synthesis service provider.<br><br>Parent node: `AIGCMetadata`. |
|ProduceID |String |test_produce_id |Content production identification element, which is the unique identifier assigned by the video generation and synthesis service provider for this content.<br><br>Parent node: `AIGCMetadata`. |
|ContentPropagator |String |test_content_propagator |Content distribution service provider element, which is the name or code of the video distribution service provider.<br><br>Parent node: `AIGCMetadata`. |
|PropagateID |String |test_propagate_id |The content distribution identifier is a unique number assigned by the video distribution service provider to this video.<br><br>Parent node: `AIGCMetadata`. |
|ReservedCode1 |String |dGVzdF9yZXNlcnZlZF9jb2RlXzE= |Reserved field 1, contains user\-initiated security protection information to safeguard content and identity integrity. Must be encoded in base64 before transmission.<br><br>Parent node: `AIGCMetadata`. |
|ReservedCode2 |String |dGVzdF9yZXNlcnZlZF9jb2RlXzI= |Reserved field 2 for user\-initiated security measures, protecting content and identity integrity. Must be passed in after base64 encoding.<br><br>Parent node: `AIGCMetadata`. |


<span id="b498570b"></span>
### Additional elements returned when the task type is Animation


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|AnimationConfig |Container |\- |Specific configuration for video to GIF conversion. |
|TimeInterval |Container |\- |Time range configuration for video GIF.<br><br>Parent node: `AnimationConfig` |
|Start |Integer |0 |Start time of video\-to\-GIF conversion, in milliseconds. Values:<br><br><br>* `0 (default)`: Start from the beginning.<br><br>* `Greater than 0`: Start from **ss** milliseconds.<br><br><br>Parent node: `TimeInterval`. |
|Duration |Integer |0 |Duration of video\-to\-animation conversion, in milliseconds. The options are as follows:<br><br><br>* `0 (default)`: to the end of the video.<br><br>* `greater than 0`: **ss** milliseconds after the start time.<br><br><br>Parent node: `TimeInterval`. |
|Container |Container |\- |Output container format for video\-to\-animated image conversion.<br><br>Parent node: `AnimationConfig`. |
|Format |String |gif |Output animation format, values: `gif`.<br><br>Parent node: `Container`. |
|Animation |Container |\- |Detailed configuration for video to GIF conversion.<br><br>Parent node: `AnimationConfig`. |
|FrameNum |Integer |100 |Number of animated frames, unlimited by default (extract frames until the video ends).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If the video is shorter, the actual number of extracted frames will be less than the set value.</div><br><br><br>Parent node: `Animation`. |
|FrameInterval |Integer |1 |Frame extraction interval for animated images, in milliseconds. By default, all video frames are extracted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If this value is less than the source video's frame interval (the inverse of the frame rate), frames are extracted according to the source video's frame interval instead.</div><br><br><br>Parent node: `Animation`. |
|Fps |Integer |30 |Animated frame rate, default is **inter ** countdown. Value range is [0, 240].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter controls the playback speed of the animation. When set to the default value, it matches the source video's playback speed. Values higher than the default create a speeding\-up effect; values lower produce a slowing\-down effect.</div><br><br><br>Parent node: `Animation`. |
|Width |Integer |1024 |Set the output GIF width in pixels, with a range of [32,4096].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If set to 0, the width will be calculated automatically based on the source video’s resolution ratio.</div><br><br><br>Parent node: `Animation`. |
|Height |Integer |1024 |Output GIF height in px, range [32,4096].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If set to 0, it calculates automatically based on the source video's resolution ratio.</div><br><br><br>Parent node: `Animation`. |
|ScaleType |String |crop |Scaling mode. The options are as follows:<br><br><br>* `crop`: scale and crop.<br><br>* `stretch` (default): stretch to fill.<br><br>* `fill`: scale and keep black borders.<br><br>* `fit`: scale proportionally without black borders.<br><br><br>Parent: `Animation`. |


<span id="dce26f64"></span>
## Sample request

```HTTP
GET /?job_type=Segment&job_id=183535129563a53bfa71000188********** HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="7a0748ba"></span>
## Sample response

```HTTP
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

{
    "JobID": "fa81ef2a00a2211f08a9aa5**********",
    "CreateTime": "2025-11-18T20:32:54+08:00",
    "StartTime": "2025-11-18T20:32:55+08:00",
    "EndTime": "2025-11-18T20:32:55+08:00",
    "State": "Success",
    "Code": 0,
    "Message": "success",
    "Input" : {                     // Source file
        "Object" : "sample.mp4"     
    },
    "RemuxConfig": {
        "Format": "mp4",
        "TranscodeIndex": 0,
        "StartTime": 1000,
        "EndTime": 20000,
        "Duration": 5,
        "AIGCMetadata": {
            "Label": "",
            "ContentProducer": "",
            "ProduceID": "",
            "ContentPropagator": "",
            "PropagateID": "",
            "ReservedCode1": "",
            "ReservedCode2": ""
        }
    },
    "Output" : {                    // Output file
        "Region" : "cn-beijing",    
        "Bucket" : "testbkt",
        "Object" : "output.mp4"
    }
}
```
