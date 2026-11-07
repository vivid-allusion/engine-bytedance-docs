---
title: "GetAudioConvertJob"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetAudioConvertJob"
---

<span id="362aa1f1"></span>
## Description

This interface is used to query audio transcoding tasks.

<span id="fbf6766f"></span>
## Notes

When using a sub\-account, it must have the relevant permissions required for `GetDataProcessJob` data processing.

<span id="11f568c6"></span>
## Request syntax

```Plain Text
GET /?job_type=AudioConvert&job_id=183535129563a53bfa71000188********** HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="9f8d8fa8"></span>
## Request parameters and headers 


|Field name |  |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|job_id |Query |String |Yes |183535129563a53bfa71000188\*\*\*\*\*\*\*\*\*\* |Audio transcoding task ID. |
|job_type |Query |String |Yes |AudioConvert |Task type, for audio transcoding scenarios, the value is only `AudioConvert`. |


<span id="88d3f2b1"></span>
## Request body elements

No elements are used.

<span id="0a377092"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="3e29219d"></span>
## Response body elements


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|JobID |String |fa81ef2a00a2211f08a9aa5\*\*\*\*\*\*\*\*\*\* |Task ID. |
|CreateTime |String |2025\-03\-26T17:14:01+0800 |Time when the task is created. |
|StartTime |String |2025\-03\-26T17:14:02+0800 |Task start time. |
|EndTime |String |2025\-03\-26T17:14:02+0800 |Task end time. |
|State |String |Success |Task status. |
|Code |Integer |0 |Task status code. |
|Message |String |Success |Task status message. |
|Input |Container |\- |Input file. |
|Object |String<br><br> |sample.mp4 |Name of the input file object.<br><br>Parent node: `Input`. |
|AudioConvertConfig |Container |\- |Audio transcoding task details. |
|ContainerFormat |String |mp3 |Specify the transcoding container format, the value list is as follows:<br><br><br>* `wav`<br><br>* `mp3`<br><br>* `aac`<br><br>* `flac`<br><br>* `oga`<br><br>* `ac3`<br><br>* `opus`<br><br><br>Parent node: `AudioConvertConfig`. |
|TimeInterval |Container |\- |Specify the transcoding duration.<br><br>Parent node: `AudioConvertConfig`. |
|Start |Integer |0 |Start time in milliseconds, default is 0.<br><br>Parent node: `TimeInterval`. |
|Duration |Integer |1000 |Duration in milliseconds. The default value of 0 means the video length.<br><br>Parent node: `TimeInterval`. |
|BitRate |Integer |8000 |Audio bitrate, range [8000, 1000000]. If set to 0, the original audio bitrate is used. Some containers do not support specifying bitrate.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of supported audio channels varies by format. See <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Support for different audio container parameters</a> for details.</div><br><br><br>Parent node: `AudioConvertConfig`. |
|BitRateOpt |Integer |0 |Audio bitrate options. The options are as follows:<br><br><br>* 0 (default): always use the target audio bitrate.<br><br>* 1: use the source audio bitrate if it is lower than `BitRate`.<br><br>* 2: fail if the source audio bitrate is lower than `BitRate`.<br><br><br>Parent node: `AudioConvertConfig`. |
|SampleFormat |Integer |\- |Audio sample format, with different ranges depending on the container.<br><br>Parent node: `AudioConvertConfig`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported sample rates vary by format. See <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#9a1124e1">Sample Rate Support for Different Audio Containers</a> for details.</div><br> |
|SampleRate |Integer |48000 |Audio sampling rate, with different value ranges depending on the container.<br><br>parent node: `AudioConvertConfig`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">sampling rates supported vary by format; see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#9a1124e1">sampling rate support for different audio containers</a> for details.</div><br> |
|Channels |Integer |2 |Number of audio channels varies by container type.<br><br>Parent node: `AudioConvertConfig`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The supported number of channels varies by format; see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Supported audio container parameters</a> for details.</div><br> |
|Output |Container |\- |Output file. |
|Region |String |cn\-beijing |Region where the output file bucket is located `Region`.<br><br>Parent node: `Output`. |
|Bucket |String |testbkt |Output file bucket name.<br><br>Parent node: `Output`. |
|Object |String |output.mp4 |Output file object name.<br><br>Parent node: `Output`. |


<span id="654dd03b"></span>
## Sample request

```JavaScript
GET /?job_type=AudioConvert&job_id=183535129563a53bfa71000188********** HTTP/1.1
Host: <bucket_name>.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: <authorization_string>
```


<span id="66f386ab"></span>
## Sample response

```JavaScript
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

{
    "JobID": "fa81ef2a00a2211f08a9aa5**********",
    "CreateTime": "2025-03-26T17:14:01+0800",
    "StartTime": "2025-03-26T17:14:02+0800",
    "EndTime": "2025-03-26T17:14:02+0800",
    "State": "Success",
    "Code": 0,
    "Message": "success",
    "Input" : {                     // Source file
        "Object" : "sample.wav"     
    },
    "AudioConvertConfig": {
        "ContainerFormat": "mp3",
        "TimeInterval": {
            "Start": 0,
            "Duration": 1000
        },
        "BitRate": 8000,
        "BitRateOpt": 0,
        "SampleFormat": "",
        "SampleRate": 48000,
        "Channels": 2
    },
    "Output" : {                    // Output file
        "Region" : "cn-beijing",    
        "Bucket" : "testbkt",
        "Object" : "output.mp3"
    }
}
```
