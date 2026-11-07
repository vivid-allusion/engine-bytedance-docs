---
title: "ListVideoConvertTemplates"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/ListVideoConvertTemplates"
---

<span id="491e13c6"></span>
## Supported features

This API queries video transcoding templates.

<span id="8618e7da"></span>
## Notes

When using a sub\-account, grant the current bucket the `GetDataProcessTemplate` permission.

<span id="773c3b75"></span>
## Request syntax

```JSON
GET /?process_template&tag=Transcode&id={} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="f276449b"></span>
## Request parameters and headers


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Tag |String |Yes |Transcode |Video transcode template identifier. |
|Name |String |Yes<br><br> |name |Custom template name:<br><br><br>* Only supports `a-z`, `A-Z`, `0-9`, `_`, `-`, and `.`; length must not exceed 64 characters and must start and end with `a-z`, `A-Z`, or `0-9`.<br><br>* Multiple rules cannot be duplicated. |
|ID |String |No |34333938323062333934611901\*\*\*\*\*\*\*\*\*\* |Audio and video task ID. If no ID is specified, all audio and video tasks will be listed. |


<span id="97b53200"></span>
## Request body elements

No elements are used.

<span id="16987b05"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ffa34086"></span>
## Response body elements


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Tag |String |Yes |Transcode |Video transcode template identifier. |
|Name |String |Yes<br><br> |transcode\-template\-1 |Custom template name:<br><br><br>* Only supports `a-z`, `A-Z`, `0-9`, `_`, `-`, and `.`. Length must not exceed 64 characters and must start and end with `a-z`, `A-Z`, or `0-9`.<br><br>* Rules cannot be duplicated. |
|ID |String |No |34333938323062333934611901\*\*\*\*\*\*\*\*\*\* |Audio and video task ID. If no ID is specified, all audio and video tasks will be listed. |
|TranscodeConfig |Container |Yes |\- |Details of the audio and video transcoding template. |
|Transcode |Container |Yes |\- |Audio and video transcode template details.<br><br>Parent node: `TranscodeConfig`. |
|TimeInterval |Container |No |\- |Specify the transcoding duration.<br><br>Parent node: `Transcode`. |
|Start |Integer |No |0 |Start time in milliseconds, default is 0.<br><br>Parent node: `TimeInterval`. |
|Duration |Integer |No |100000 |Duration, in milliseconds, default 0 means video length.<br><br>Parent node: `TimeInterval`. |
|Container |Container |Yes |\- |Specify the transcode container format.<br><br>Parent node: `Transcode`. |
|Format |String<br><br> |Yes<br><br> |mp4 |Video file container format. Available values:<br><br><br>* `mp4`.<br><br>* `ts`.<br><br><br>Parent node: `Container`. |
|ClipConfig |Container |No |\- |Fragment configuration specifying `HLS` transcoding fragment duration.<br><br>Parent node: `Container`. |
|Duration |Integer |No |0 |Segment duration for `hls` transcoding, in milliseconds. Default is 5000, valid range is (0, 3600000).<br><br>Parent node: `ClipConfig`. |
|Video |Container |Yes |\- |Video encoding parameters.<br><br>Parent node: `Transcode`. |
|Codec |String |No |h264 |Video codec format:<br><br><br>* `h264`.<br><br>* `h265`.<br><br><br>Parent node: `Video`. |
|Width |Integer |No |0 |Video width in `px`, must be an even number, range [128, 4096].<br><br>Parent node: `Video`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If only <code>Width</code> is set and <code>Height</code> is not set, the video height will be calculated according to the original aspect ratio.</div><br> |
|Height |Integer |No |720 |Video height in `px`, must be even, within the range [128, 4096].<br><br>Parent node: `Video`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If only <code>Height</code> is set and <code>Width</code> is not, the video file's width will be calculated based on the original aspect ratio.</div><br> |
|Crf |Integer |No |23 |Bitrate control factor for the video file, range (0, 51], default 0 means not set.<br><br><br>* If the value of `Crf` is greater than 0, the `BitRate` parameter will be ignored.<br><br>* If `BitRate` is not set or empty, the encoder's default value will be used.<br><br><br>Parent node: `Video`. |
|PixFmt |String |No |yuv420p |Video pixel format.<br><br>Parent node: `Video`. |
|BitRate |Integer |No |0 |Video output file bitrate in `bps`, value range: [10000, 50000000]. Default 0 means not set.<br><br><br>* Parent node: `Video`. |
|Fps |Integer |No |0 |Video frame rate, in `fps`, range (0, 60], default 0 means not set.<br><br>Parent node: `Video`. |
|Remove |Bool |No |false |Whether to delete the source video stream, set to `true` or `false`.<br><br>Parent node: `Video`. |
|Audio |Container |No |\- |Specify audio stream parameters.<br><br>Parent node: `Transcode`. |
|Codec |String |No |aac<br><br> |Audio stream encoding format, value list as follows:<br><br><br>* `mp3`.<br><br>* `aac`.<br><br>* `flac`<br><br>* `Vorbis`.<br><br>* `ac3`.<br><br>* `opus`.<br><br>* `pcm_s16le`.<br><br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different container formats support different audio encoding formats. For details, see <a href="https://docs.byteplus.com/en/docs/tos/CreateTranscodeJob?lang=zh#cd717e7f">Audio encoding format support for different containers</a>.</div><br> |
|BitRate |Integer |No |0 |Audio bitrate, in bits per second (bps), value range: 1000~10000000. Use original audio bitrate when set to 0; some containers do not support specifying bitrate.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of supported channels varies by format; see<a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">support for different audio container parameters</a> for details.</div><br> |
|SampleFormat |String |No |\- |Audio sample format; the value range varies by container. The options are as follows:<br><br><br>* `fltp`.<br><br>* `s16`.<br><br>* `s16p`<br><br>* `s32`.<br><br>* `s32p`.<br><br><br>Parent node: `Audio`. |
|SampleRate |Integer |No |0 |Audio sample rate varies across containers.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported sample rates vary by format; see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">audio container sample rate support details</a> for more information...</div><br> |
|Channels |Integer |No |0 |Number of audio channels, default matches the specified source audio, range: 1~ 8, varies by container type.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of supported channels varies by format. For details, see <a href="https://docs.byteplus.com/en/docs/tos/AudioConcat?lang=zh#6b82ba91">supported channel numbers by audio container format</a>.</div><br> |
|Remove |Bool |No |false |Whether to delete the source audio stream, values are `true` or `false`.<br><br>Parent node: `Audio`. |
|Options |Container |No |\- |Specify optional transcoding parameters.<br><br>Parent node: `Transcode`. |


<span id="f6debea9"></span>
## Sample request

```JSON
GET /?process_template&tag=Transcode&id={} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="dda971a9"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Content-Type: application/json
Content-Length: <length>
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

{
    "Tag": "Transcode",
    "ID": "34333938323062333934611901**********",
    "Name": "transcode-template-1",
    "TranscodeConfig": {
        "TimeInterval": {
            "Start": 0,
            "Duration": 10000
        },
        "Container": {
            "Format": "mp4",
            "ClipConfig": {
                "Duration": 0
            }
        },
        "Video": {
            "Codec": "h264",
            "Width": 0,
            "Height": 720,
            "Crf": 23,
            "PixFmt": "yuv420p",
            "BitRate": 0,
            "Fps": 0,
            "Remove": false
        },
        "Audio": {
            "Codec": "aac",
            "SampleRate": 0,
            "BitRate": 0,
            "Channels": 0,
            "SampleFormat": "",
            "Remove": false
        },
        "Options": {}
    }
}
```
