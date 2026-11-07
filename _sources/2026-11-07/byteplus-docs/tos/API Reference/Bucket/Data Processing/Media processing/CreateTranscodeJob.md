---
title: "CreateTranscodeJob"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/CreateTranscodeJob"
---

<span id="bb25dd0b"></span>
## Description

This interface creates audio and video transcoding jobs.

<span id="445b6ff1"></span>
## Notes

When using a sub\-account, you must grant the current bucket the `CreateMediaProcessJobs` permission.

<span id="e140c48f"></span>
## Request syntax

```Plain Text
POST /?job_type=Transcode&media_jobs HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
    "Input": {
        "Object": "sample.mp4"
    },
    "TranscodeConfig": {
        "Transcode": {
            "TimeInterval": {
              "Start": 0,
              "Duration": 10000
            },
            "Container": {
              "Format": "mp4",
              "ClipConfig": {
                "Duration": 0,
              }
            },
            "Video": {
              "Codec": "h264",
              "Width": 480,
              "Height": 480,
              "Crf": 1,
              "PixFmt": "yuv420p",
              "BitRate": 0,
              "Fps": 0,
              "Remove": false
            },
            "Audio": {
              "Codec": "mp3",
              "SampleRate": 44100,
              "BitRate": 0,
              "Channels": 2,
              "SampleFormat": "fltp",
              "Remove": false,
            }
        }
    },
    "Output": {
        "Region": "cn-beijing",
        "Bucket": "testbkt",
        "Object": "output.mp4"
    }
}    
```


<span id="5feb345a"></span>
## Request parameters and headers


|Field name | Location |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|media_jobs |Query |String |Yes |\- |Represents the unique identifier for the media task request. |
|job_type |Query |String |Yes |Transcode |Task type. For audio and video transcoding scenarios, the value is only `Transcode`. |


<span id="a69b7b2a"></span>
## Request body elements


|Field name |Type |Required |Example value |Description |
|---|---|---|---|---|
|Input |Container |Yes |\- |Source file. |
|Object |String |Yes |data.mp4 |Name of the source audio and video file to be transcoded.<br><br>Parent node: `Input`. |
|TranscodeConfig |Container |No |\- |Specific configuration for audio and video transcoding. |
|Transcode |Container |No |\- |Specific configuration for audio and video transcoding.<br><br>Parent node: `TranscodeConfig`. |
|Callback |String |No |https://myapp.com/callback |Asynchronous task HTTP POST callback URL. The callback request `body` structure matches the response message body of [QueryMediaJob](https://docs.byteplus.com/docs/tos/QueryMediaJob). |
|TimeInterval |Container |No |\- |Specify the time period for audio and video to be transcoded.<br><br>Parent node: `Transcode`. |
|Start |Integer |No |0 |Audio and video start time in milliseconds.<br><br>Parent node: `TimeInterval`. |
|Duration |Integer |No |1000 |Audio and video duration in milliseconds.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If <code>Start</code> and <code>Duration</code> are not set, the entire video will be transcoded.</div><br><br><br>Parent node: `TimeInterval`. |
|Container |Container |Yes |\- |Audio and video container format.<br><br>Parent node: `Transcode`. |
|Format |String |Yes |ts |Packaging format of the transcoded audio and video files. The options are as follows:<br><br><br>* `mp4`.<br><br>* `ts`.<br><br>* `hls`.<br><br>* `mp3`.<br><br>* `aac`.<br><br>* `flac`.<br><br>* `m4a`.<br><br>* `oga`.<br><br>* `wav`.<br><br>* `ac3`.<br><br>* `opus`.<br><br><br>Parent node: `Container`. |
|ClipConfig |Container |No |\- |Segment configuration, effective when `Format` is `hls`.<br><br>Parent node: `Container`. |
|Duration |Integer |No |5000 |Segment duration in milliseconds.<br><br>Parent node: `ClipConfig`. |
|Video |Container |No |\- |Video encoding parameters.<br><br>Parent node: `Transcode`. |
|Codec |String |No |h264 |Video stream encoding format, with the following values:<br><br><br>* `h264`.<br><br>* `h265`.<br><br><br>Parent node: `Video`. |
|Width |Integer |No |4096 |video file width must be an even number, unit `px`, range [128, 4096].<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If <code>Width</code> is set but <code>Height</code> is not, the video file height will be calculated according to the original video aspect ratio.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If <code>Height</code> is set but <code>Width</code> is not, the video file width will be calculated according to the original video aspect ratio.</div><br><br><br><br>Parent node: `Video`. |
|Height |Integer |No |1024 |The height of the video file must be an even number in `px`, with a range of [128, 4096].<br><br>Parent node: `Video`. |
|Crf |Integer |No |25 |Bitrate control factor for video files, with a value range of (0, 51].<br><br><br>* Default 0 means not set.<br><br>* If `Crf` is set, the `Bitrate` setting is ignored.<br><br>* When Bitrate is empty, the encoder default value applies.<br><br><br>Parent node: `Video`. |
|PixFmt |String |No |yuv420p |Video pixel format.<br><br>Parent node: `Video`. |
|BitRate |Integer |No |10000 |Video output file bitrate, unit `bps`, range [10000, 50000000], default 0 means not set.<br><br>Parent node: `Video`. |
|Fps |Integer |No |24 |Video frame rate in `fps`, value range (0, 60], default 0 means not set.<br><br>Parent node: `Video`. |
|Remove |Boolean |No |false |Whether to delete the video stream. Possible values are:<br><br><br>*  `true` .<br><br>*  `false`.<br><br><br>Parent node: `Video`. |
|Audio |Container |No |\- |Audio encoding parameters.<br><br>Parent node: `Transcode`. |
|Codec |String |No |mp3 |Audio stream encoding format, with possible values as follows:<br><br><br>* `mp3`.<br><br>* `aac`.<br><br>* `flac`.<br><br>* `Vorbis`.<br><br>* `ac3`.<br><br>* `opus`.<br><br>* `pcm_s16le`.<br><br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Different container formats support various audio encoding formats. For details, see <a href="https://docs.byteplus.com/docs/tos/CreateTranscodeJob#cd717e7f">Audio encoding format support for different containers</a>.</div><br> |
|SampleRate |Integer |No |44100 |Audio sampling rate. Defaults to match the specified source audio. Possible values are:<br><br><br>* `8000`.<br><br>* `11025`.<br><br>* `12000`.<br><br>* `16000`.<br><br>* `22050`.<br><br>* `24000`.<br><br>* `32000`.<br><br>* `44100`.<br><br>* `48000`.<br><br>* `64000`.<br><br>* `88200`.<br><br>* `96000`.<br><br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The supported sampling rates vary by format. For details, see <a href="https://docs.byteplus.com/docs/tos/AudioConcat#9a1124e1">Sampling rate support for different audio containers</a>..</div><br> |
|BitRate |Integer |No |8000 |Audio bit rate, in bits per second (bps). Valid range: 1000 to 10000000. Use the original audio bitrate when set to 0; some containers do not support specifying bitrate.<br><br>Parent node: `Audio`. |
|Channels |Integer |No |2 |Number of audio channels. Defaults to the source audio specified, with a range of 1 to 8.<br><br>Parent node: `Audio`.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The number of supported channels varies by format. See <a href="https://docs.byteplus.com/docs/tos/AudioConcat#6b82ba91">Audio container parameter support</a> for details.</div><br> |
|SampleFormat |String |No |fltp |Audio sample format; the range varies by container.<br><br>The options are as follows:<br><br><br>* `fltp`.<br><br>* `s16`.<br><br>* `s16p`.<br><br>* `s32`<br><br>* `s32p`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Supported sampling formats vary by different formats. See <a href="https://docs.byteplus.com/docs/tos/AudioConcat#6b82ba91">audio container parameter support details</a> for more information.</div><br> |
|Remove |Boolean |No |false |Whether to delete the audio stream. The value can be `true` or `false`.<br><br>Parent node: `Audio`. |
|Output |Container |Yes |\- |Storage configuration for transcoded video files. |
|Region |String |Yes |cn\-beijing |Storage region for the transcoded video file.<br><br>Parent node: `Output`. |
|Bucket |String |Yes |test |Storage bucket for transcoded video files.<br><br>Parent node: `Output`. |
|Object |String |Yes |data.ts |Name of the transcoded video file.<br><br>Parent node: `Output`. |


<span id="cd717e7f"></span>
### Audio codec support for different containers


|**Container format** |**Supported audio codec formats** |
|---|---|
|mp4 |mp3/aac |
|ts |mp3/aac |
|hls |mp3/aac |
|mp3 |mp3 |
|aac |aac |
|flac |flac |
|oga |Vorbis |
|ac3 |ac3 |
|opus |opus |
|wav |pcm_s16le |


&nbsp;

<span id="f0a74848"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="dfad2b08"></span>
## Response body elements


|**Field name** |**Type** |**Example value** |**Description** |
|---|---|---|---|
|Code |String |OK |Status code. |
|Message |String |Success |Request status information. |
|JobId |String |1852a9645b553232cdf10001fd35952a4b08 |Video transcoding task ID. |


<span id="84108137"></span>
## Sample request

```JSON
POST /?job_type=Transcode&media_jobs HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Content-Type: application/json
Content-Length: <length>
Authorization: authorization string

{
    "Input": {
        "Object": "sample.mp4"
    },
    "TranscodeConfig": {
        "Transcode": {
            "TimeInterval": {
              "Start": 0,
              "Duration": 10000
            },
            "Container": {
              "Format": "mp4"
            },
            "Video": {
              "Codec": "h264",
              "Width": 480,
              "Height": 480,
              "Crf": 1
            }
        }
    },
    "Output": {
        "Region": "cn-beijing",
        "Bucket": "testbkt",
        "Object": "output.mp4"
    }
}    
```


<span id="59163e07"></span>
## Sample response

```Plain Text
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0

{
    "Code": "OK",
    "Message": "Success",
    "JobId": "1852a9645b553232cdf10001fd35952a4b08"
}
```
