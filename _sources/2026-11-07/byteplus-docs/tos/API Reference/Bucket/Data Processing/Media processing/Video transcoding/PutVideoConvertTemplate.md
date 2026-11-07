---
title: "PutVideoConvertTemplate"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/PutVideoConvertTemplate"
---

<span id="adddf010"></span>
## Description

This interface creates audio and video transcoding templates.

<span id="90f0a392"></span>
## Notes


* Each rule `body` must not exceed 20KB, and up to 100 custom templates can be configured.

* When using a sub\-account, grant the current bucket `PutDataProcessTemplate` permission.


<span id="4b78610f"></span>
## Request syntax

```JSON
PUT /?process_template&tag=Transcode HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "Transcode", // fixed identifier
  "Name": "my-template",
  "TranscodeConfig": {
    "TimeInterval": {
      "Start": 0,
      "Duration": 10000,
    },
    "Container": {
      "Format": "mp4"
    },
    "Video": {
      "Codec": "h264",
      "Width": 480,
      "Height": 480,
      "Crf": 1,
      "PixFmt": "yuv420p"
      "BitRate": 3000000,
      "Fps": 24,
      "Remove": false
    },
    "Audio": {
      "Codec": "aac",
      "BitRate": 128000,
      "SampleFormat": "fltp",
      "Channels": 2,
      "Remove": false
    },
    "Options": {
      "AIGCMetadata": {
        "Label": "1",
        "ContentProducer": "test_producer",
        "ProduceID": "12345",
        "ContentPropagator": "test_propagator",
        "PropagateID": "12345",
        "ReservedCode1": "ewogICAgIm****UiLAp9",
        "ReservedCode2": "ewogICAg*****UyIiwKfQ"
      }
    }
  }
}
```


<span id="6d7b5470"></span>
## Request parameters and headers 


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|process_template |String |Yes |\- |Video transcoding template identifier. |
|Tag |String |Yes |Transcode |Task type, Only `Transcode` is valid in audio and video transcoding scenarios. |


<span id="e1fe25d7"></span>
## Request body elements


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Name |String |Yes<br><br> |name |Custom template name:<br><br><br>* Only supports `a-z`, `A-Z`, `0-9`, `_`, `-`, and `.`; length cannot exceed 64 characters. Must start and end with `a-z`, `A-Z`, or `0-9`.<br><br>* Multiple rules cannot be duplicated. |
|TranscodeConfig |Container |Yes |\- |Audio and video transcoding template details. |
|Transcode |Container |Yes |\- |Audio and video transcoding template details.<br><br>Parent node: `TranscodeConfig`. |
|TimeInterval |Container |No |\- |Specify the transcoding duration.<br><br>Parent node: `Transcode`. |
|Start |Integer |No |0 |Start time in milliseconds, default is 0.<br><br>Parent node: `TimeInterval`. |
|Duration |Integer |No |10000 |Duration in milliseconds, default 0 means video length.<br><br>Parent node: `TimeInterval`. |
|Container |Container |Yes |\- |Specify the transcoding container format.<br><br>Parent node: `Transcode`. |
|Format |String<br><br> |Yes<br><br> |mp4 |Video file container formats, with the following values:<br><br><br>* `mp4`.<br><br>* `ts`.<br><br>* `hls`.<br><br>* `mp3`.<br><br>* `aac`.<br><br>* `flac`.<br><br>* `m4a`.<br><br>* `oga`.<br><br>* `wav`.<br><br>* `ac3`.<br><br>* `opus`.<br><br><br>Parent node: `Container`. |
|ClipConfig |Container |Not supported |\- |Fragment configuration specifying `hls` transcoding fragment duration.<br><br>Parent node: `Container`. |
|Duration |Integer |No |5000 |The fragment duration for `hls` transcoding, in milliseconds. The default value is 5000. Valid range is (0, 3600000).<br><br>Parent node: `ClipConfig`. |
|Video |Container |Yes |\- |Video encoding parameters.<br><br>Parent node: `Transcode`. |
|Codec |String |No |H.264 |Video codec format, with the following values:<br><br><br>* `h264`.<br><br>* `h265`.<br><br><br>Parent node: `Video`. |
|Width |Integer |No |4096 |Video width in `px`, must be even, range [128, 4096].<br><br>Parent node: `Video`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If only <code>Width</code> is set and <code>Height</code> is not set, the video height will be calculated based on the original aspect ratio.</div><br> |
|Height |Integer |No |1024 |Video height in `px`, must be even, range [128, 4096].<br><br>Parent node: `Video`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If only <code>Height</code> is set and <code>Width</code> is not, the video width will be calculated based on the original aspect ratio.</div><br> |
|Crf |Integer |No |25 |Bitrate control factor for video files, with a value range of (0, 51].<br><br><br>* default 0 means not set.<br><br>* If `Crf` is set, the `Bitrate` setting becomes invalid.<br><br>* If Bitrate is empty, the encoder default value is used.<br><br><br>Parent node: `Video`. |
|PixFmt |String |No |yuv420p |Video pixel format.<br><br>Parent node: `Video`. |
|BitRate |Integer |No |0 |Video output file bitrate in `bps`, range [10000, 50000000]. Default 0 means unset.<br><br>Parent node: `Video`. |
|Fps |Integer |No |0 |Video frame rate, in `fps`, value range (0, 60], default 0 means unset.<br><br>Parent node: `Video`. |
|Remove |Bool |No |false |Whether to remove the source video stream; values are `true` or `false`.<br><br>Parent node: `Video`. |
|Audio |Container |No |\- |Specify audio stream parameters.<br><br>Parent node: `Transcode`. |
|Codec |String |No |aac<br><br> |Audio stream encoding formats, values are as follows:<br><br><br>* `mp3`.<br><br>* `aac`.<br><br>* `flac`.<br><br>* `Vorbis`.<br><br>* `ac3`.<br><br>* `opus`.<br><br>* `pcm_s16le`.<br><br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different container formats support different audio codec formats. See <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Audio codec format support in different containers</a> for details.</div><br> |
|BitRate |Integer |No |128000 |Audio bitrate, in bits per second (bps), range: 1000~10000000. Use the original audio bitrate if set to 0. Some containers do not support specifying bitrate.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of channels supported varies by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">audio container parameter support</a>.</div><br> |
|SampleFormat |String |No |fltp |Audio sampling format, with varying value ranges across different containers. The options are as follows:<br><br><br>* `fltp`.<br><br>* `s16`.<br><br>* `s16p`.<br><br>* `s32`.<br><br>* `s32p`.<br><br><br>Parent node: `Audio`. |
|SampleRate |Integer |No |48000 |Audio sample rate, with different ranges depending on the container.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The supported sampling rates vary by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">Support for sampling rates in different audio containers</a>.</div><br> |
|Channels |Integer |No |2 |Number of audio channels, default consistent with the specified source audio. Range: 1 – 8, varies by container.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The supported number of channels varies by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">support for parameters in different audio containers</a>.</div><br> |
|Remove |Bool |Not supported |false |Whether to delete the source audio stream, value `true` or `false`<br><br>Parent node: `Audio`. |
|Options |Container |No |\- |Optional parameters for specified transcoding.<br><br>Parent node: `Transcode`. |
|AIGCMetadata |Container |No |\- |Video AIGC metadata, see below `AIGCMetaddata`.<br><br>Parent node: `Options`. |
|Label |String |Yes |1 |Generate composite tag elements used to identify target videos as AI\-generated, potentially AI\-generated, or suspected AI\-generated content.<br><br>Parent node: `AIGCMetadata`. |
|ContentProducer |String |Yes |tes_producer |Generate the element for the synthesis service provider, containing the name or code of the video synthesis service provider.<br><br>Parent node: `AIGCMetadata`. |
|ProduceID |String |Yes |123456 |The content creation identifier element uniquely identifies the content provided by the video generation synthesis service provider.<br><br>Parent node: `AIGCMetadata`. |
|ContentPropagator |String |No |test_propagator |The content distribution service provider element contains the name or code of the video distribution service provider.<br><br>Parent node: `AIGCMetadata`. |
|PropagateID |String |No |123456 |Content distribution identification element, containing the unique ID assigned to the video by the video distribution service provider.<br><br>Parent node: `AIGCMetadata`. |
|ReservedCode1 |String |No |ewogICAgIm\*\*\*\*UiLAp9 |Reserved field 1, used for users to independently implement security protection and safeguard content and identification integrity. Must be passed in after base64 encoding.<br><br>Parent node: `AIGCMetadata`. |
|ReservedCode2 |String |No |ewogICAg\*\*\*\*\*UyIiwKfQ |Reserved field 2, containing user\-initiated security protection information to safeguard content and identity integrity. Must be passed in after base64 encoding.<br><br>Parent node: `AIGCMetadata`. |


<span id="6d013080"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="a0e36bcd"></span>
## Response body elements


|Name |Type |Example value |Description |
|---|---|---|---|
|template_id |String |393161343761366633396119012ee2450b08 |Create the unique ID for the audio transcoding template. |


<span id="99bf4d28"></span>
## **Sample request**

```JSON
PUT /?process_template&tag=Transcode HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
  "Tag": "Transcode", // fixed identifier
  "Name": "my-template",
  "TranscodeConfig": {
    "TimeInterval": {
      "Start": 0,
      "Duration": 10000,
    },
    "Container": {
      "Format": "mp4"
    },
    "Video": {
      "Codec": "h264",
      "Width": 480,
      "Height": 480,
      "Crf": 1,
      "PixFmt": "yuv420p"
      "BitRate": 3000000,
      "Fps": 24,
      "Remove": false
    },
    "Audio": {
      "Codec": "aac",
      "BitRate": 128000,
      "SampleFormat": "fltp",
      "Channels": 2,
      "Remove": false
    },
    "Options": {
      "AIGCMetadata": {
        "Label": "1",
        "ContentProducer": "test_producer",
        "ProduceID": "12345",
        "ContentPropagator": "test_propagator",
        "PropagateID": "12345",
        "ReservedCode1": "ewogICAgIm****UiLAp9",
        "ReservedCode2": "ewogICAg*****UyIiwKfQ"
      }
    }
  }
}
```


<span id="7e38339b"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Content-Type:  text/plain
Content-Length: <length>
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

393161343761366633396119012ee2450b08
```
