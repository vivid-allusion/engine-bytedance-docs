---
title: "PutAudioConvertTemplate"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutAudioConvertTemplate"
---

<span id="ef79b2a5"></span>
## Description

This api creates an audio transcoding template.

<span id="ad477af2"></span>
## Notes


* Each rule body must not exceed 20KB, and up to 100 custom templates can be configured.

* When using a sub\-account, the `PutDataProcessTemplate` permission for the current bucket must be granted.


<span id="bf59853a"></span>
## Request syntax

```Python
PUT /?process_template&tag=AudioConvert HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "AudioConvert", //Fixed sign
  "Name": "my-template",
  "AudioConvertConfig": {
    "TimeInterval": {
      "Start": 0,
      "Duration": 10000,
    },
    "ContainerFormat": "mp3",
    "Bitrate": 16000,
    "SampleRate": 24000,
    "Channels": 2
  }
}
```


<span id="d488dc2d"></span>
## Request parameters and headers 


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|process_template |String |Yes |\- |Create audio transcoding template identifier. |
|Tag |String |Yes |Watermark |Task type, for audio transcoding scenarios, only `AudioConvert` is valid. |


<span id="78f7f455"></span>
## Request body elements


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Name |String |Yes<br><br> |name |Custom template name:<br><br><br>* Only supports `a-z`, `A-Z`, `0-9`, `_`, `-`, and `.`. Length cannot exceed 64 characters and must start and end with `a-z`, `A-Z`, or `0-9`.<br><br>* Duplicate rules are not allowed. |
|AudioConvertConfig |Container |Yes |\- |Audio transcoding template details. |
|TimeInterval |Container |No |\- |Specify the transcoding duration.<br><br>Parent node: `AudioConvertConfig`. |
|ContainerFormat |String |Yes |wav<br><br> |Specify the transcoding container format. Available values are as follows:<br><br><br>* `wav`<br><br>* `mp3`<br><br>* `aac`<br><br>* `flac`<br><br>* `oga`<br><br>* `ac3`<br><br>* `opus`<br><br><br>Parent node: `AudioConvertConfig`. |
|BitRate |Integer |No |128000 |Audio bitrate, range [8000, 1000000]. Use 0 to keep the original audio bitrate. Some containers do not support setting bitrate.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of supported channels varies by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Audio container parameter support</a>.</div><br><br><br>Parent node: `AudioConvertConfig`. |
|BitRateOpt |Integer |No |0 |Audio bitrate options. The options are as follows:<br><br><br>* `0` (default): Always use the target audio bitrate.<br><br>* `1`: Use the source audio bitrate when it is lower than `BitRate`.<br><br>* `2`: Fail if the source audio bitrate is lower than `BitRate`.<br><br><br>Parent node: `AudioConvertConfig`. |
|SampleFormat |String |No |fltp |Audio sampling format; value ranges vary across different containers.<br><br>Parent node: `AudioConvertConfig`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported sample rates vary by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#9a1124e1">Support for sample rates in different audio containers</a>.</div><br> |
|SampleRate |Integer |No |48000 |Audio sample rate; the range varies between containers.<br><br>Parent node: `AudioConvertConfig`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Sample rate support varies by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#9a1124e1">sample rate support for different audio containers</a>.</div><br> |
|Channels |Integer |No |2 |Number of audio channels, the range varies by container.<br><br>Parent node: `AudioConvertConfig`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different formats support different numbers of channels. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Audio container parameter support</a>.</div><br> |
|Start |Integer |No |0 |Start time in milliseconds, default value is 0.<br><br>Parent node: `TimeInterval`. |
|Duration |Integer |No |10000 |Duration in milliseconds. The default value 0 means video length.<br><br>Parent node: `TimeInterval`. |


<span id="038ad961"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="1167cdd4"></span>
## Response body elements


|**Name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|template_id |String |39316134376136663339611901\*\*\*\*\*\*\*\*\*\* |Creating unique ID for the audio transcoding template. |


<span id="93fa3c5b"></span>
## Sample request

```Python
PUT /?process_template&tag=AudioConvert HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "AudioConvert", // Fixed sign
  "Name": "my-template",
  "AudioConvertConfig": {
    "TimeInterval": {
      "Start": 0,
      "Duration": 10000,
    },
    "ContainerFormat": "mp3",
    "Bitrate": 16000,
    "SampleRate": 24000,
    "Channels": 2
  }
}
```


<span id="7df5ea12"></span>
## Sample response

```Python
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Content-Type: application/json
Content-Length: <length>
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

39316134376136663339611901**********
```
