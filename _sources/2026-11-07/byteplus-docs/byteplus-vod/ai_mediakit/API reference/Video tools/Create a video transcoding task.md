---
title: "Create a video transcoding task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-transcoding-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-video`

This API submits an asynchronous video transcoding task. Video transcoding is the process of converting one video bitstream into another, typically involving changes to the encoding format (such as H.264), encoding parameters (such as resolution, bitrate, and GOP), and container format (such as MP4 or TS), to adapt to different business scenarios, playback devices, and network environments.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For a complete usage flow and application examples, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-transcoding">Video transcoding</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example-video.com/input.mov` |The URL of the video to be transcoded.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|`container_format` |String |Yes |`MP4` |The container format of the output video. Supported values:<br><br><br>* `MP4` (Default)<br><br>* `FLV`<br><br>* `MPEGTS` |
|`video` |Object |Yes |`-` |Video transcoding parameter configuration. See [The video object (video transcoding parameters)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-transcoding-task#video-structure-video-transcoding-parameters) below. |
|`audio` |Object |No |`-` |Audio transcoding parameter configuration. If this object is not provided, audio is transcoded with default parameters (codec `aac`, other parameters match those of the source file). See [The audio object (audio transcoding parameters)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-transcoding-task#audio-structure-audio-transcoding-parameters) below. |
|`metadata_keep_tags` |Array of Strings |No |`["title", "artist"]` |The list of metadata tags to keep from the source video. By default, transcoding discards most metadata (such as title and artist). Use this parameter to specify the tag keys to keep. This parameter does not take effect when the `container_format` is set to `MPEGTS`. |
|`metadata_add_tags` |Array of Objects |No |`[{"key": "album", "value": "2024 Remaster"}]` |The list of metadata tags to add to the output video. Each tag consists of a `key` and a `value`. If an added tag has the same name as a kept tag, the setting here **overrides** the source file's value. This parameter does not take effect when the `container_format` is set to `MPEGTS`. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/uchbv7an/yf0irz3g). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |


<span id="video-structure-video-transcoding-parameters"></span>
#### The video object (video transcoding parameters)


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`codec` |String |No |`h264` |The video codec. Defaults to `h264`. Supported values: `h264`, `h265`. |
|`scale_type` |Integer |No |`2` |The video scaling mode. Defaults to `0`.<br><br><br>* `0`: **Follow\-source mode**. No scaling is performed; `scale_mode`, `scale_width`, `scale_height`, `scale_short`, and `scale_long` are all ignored. This mode supports up to 8K resolution.<br><br>* `1`: **Long/short\-side limit mode**. Activates `scale_short` and `scale_long`. You can set the long or short side of the output; the other side scales proportionally. This mode supports up to 4K resolution.<br><br>* `2`: **Width/height limit mode**. Activates `scale_width` and `scale_height`. You can set the width or height of the output; the other side scales proportionally. This mode supports up to 4K resolution. |
|`scale_mode` |Integer |No |`2` |The fill and stretch strategy. Effective only when `scale_type` is `1` or `2`, used to handle mismatches between your target dimensions and the source aspect ratio. Defaults to `0`.<br><br><br>* `0`: No upsampling; the video is shrunk if the source is larger than the target, and the original size is kept if it is smaller.<br><br>* `1`: Stretch upsampling; force\-stretch to the target width and height, which may distort the picture.<br><br>* `2`: Letterbox upsampling; scale proportionally to fit within the target frame and pad the rest with black bars.<br><br><br>For example, to force a 16:9 video to output as 1:1 with `scale_mode` = `1`, the system squeezes or stretches the picture to fill the entire 1:1 canvas; with `scale_mode` = `2`, the system keeps the original ratio, places it fully within the 1:1 canvas, and pads the top/bottom or left/right with black bars. |
|`scale_width` |Integer |No |`1920` |The target width, in px. The value range is `[0, 4320]`. Effective only when `scale_type` is `2` (width/height limit mode). If only one of `scale_width` or `scale_height` is provided, the other side scales proportionally. |
|`scale_height` |Integer |No |`1080` |The target height, in px. The value range is `[0, 4320]`. Effective only when `scale_type` is `2` (width/height limit mode). If only one of `scale_width` or `scale_height` is provided, the other side scales proportionally. |
|`scale_short` |Integer |No |`720` |The target short side, in px. The value range is `[0, 4320]`. Effective only when `scale_type` is `1` (long/short\-side limit mode). If only one of `scale_short` or `scale_long` is provided, the other side scales proportionally. |
|`scale_long` |Integer |No |`1280` |The target long side, in px. The value range is `[0, 4320]`. Effective only when `scale_type` is `1` (long/short\-side limit mode). If only one of `scale_short` or `scale_long` is provided, the other side scales proportionally. |
|`bitrate_mode` |String |No |`crf` |The bitrate control mode. Defaults to `crf`.<br><br><br>* `crf`: **Constant Rate Factor** mode. The system tries to keep the overall visual quality at the level set by `bitrate_crf` (the smaller the value, the higher the quality), while ensuring the instantaneous bitrate does not exceed the `bitrate_kbps` limit. This is the best choice for balancing quality and file size and is recommended for most scenarios.<br><br>* `abr`: **Average Bitrate** mode. The encoder adjusts the bitrate so that the overall average bitrate of the output approaches the value set by `bitrate_kbps`. Suitable for scenarios that need to control file size within a specific range.<br><br>* `cbr`: **Constant Bitrate** mode. The encoder tries to keep every second of the stream strictly at the bitrate set by `bitrate_kbps`. Quality fluctuates with scene complexity, but the bitrate is very stable. Suitable for streaming scenarios with extremely high requirements for network transmission stability. |
|`bitrate_crf` |Number |No |`23` |The CRF (Constant Rate Factor) parameter, which is effective only when `bitrate_mode` is `crf`, is the primary quality controller in `crf` mode. The value range is `[0, 51]`, with a default of `25`. The smaller the value, the higher the quality and the larger the file. `0` means lossless. |
|`bitrate_kbps` |Integer |No |`2500` |The target video bitrate, in Kbps. The value range is `[10, 50000]`, with a default of `2000`. Its exact effect depends on `bitrate_mode`:<br><br><br>* In `crf` mode: the maximum bitrate limit.<br><br>* In `abr` mode: the average bitrate target.<br><br>* In `cbr` mode: the constant bitrate target. |
|`fps_mode` |String |No |`vfr` |The frame\-rate control mode. `fps_mode` takes effect only after you set the `fps` parameter. If you do not provide `fps`, the system uses the source's frame rate and `fps_mode` is ignored. Defaults to `vfr`.<br><br><br>* `vfr`: Variable frame\-rate mode. The `fps` value acts as the maximum frame\-rate limit. If the source frame rate is lower than your `fps` value, the source rate is kept; if higher, it is reduced to the `fps` value. This helps avoid unnecessary frame\-rate increases.<br><br>* `cfr`: Constant frame\-rate mode. The `fps` value is the forced output frame rate. Regardless of the source frame rate, the output is forced to the constant frame rate set by `fps`. |
|`fps` |Integer |No |`30` |The target frame rate. The value range is `[1, 240]`. Setting this parameter activates the `fps_mode` logic. In `vfr` mode it represents the maximum frame rate; in `cfr` mode it represents the constant frame rate. If not set, the source's frame rate is used. |
|`is_hdr_to_sdr` |Boolean |No |`true` |Whether to convert HDR (High Dynamic Range) video to SDR (Standard Dynamic Range) video. Defaults to `true`. Set to `false` to keep HDR. |


<span id="audio-structure-audio-transcoding-parameters"></span>
#### The audio object (audio transcoding parameters)


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`codec` |String |No |`aac` |The audio codec. Defaults to `aac`. Currently only `aac` is supported. |
|`sample_rate` |Integer |No |`44100` |The audio sample rate, in Hz. Defaults to `44100`. The sample rates currently supported by `aac` are: `8000`, `11025`, `12000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`, `64000`, `88200`, `96000`. |
|`bitrate_mode` |String |No |`cbr` |The audio bitrate control mode. Supported values:<br><br><br>* `cbr`: (Default) Constant bitrate mode. Supported only when `video.codec` is `h264`. The encoder tries to keep every second of the audio stream strictly at the bitrate set by `bitrate_kbps`, making the file size precisely predictable—suitable for streaming scenarios with high bandwidth\-stability requirements.<br><br>* `cae`: Adaptive bitrate mode (supported only when `audio.codec` is `aac`). The encoder dynamically adjusts the instantaneous bitrate based on content complexity but ensures the overall **average bitrate** of the file approaches the target set by `bitrate_kbps`. |
|`bitrate_kbps` |Integer |No |`192` |The audio bitrate, in Kbps. The value range is `[10, 500]`, with a default of `128`. If this parameter is not set, the output audio bitrate matches the source audio. |
|`channels` |Integer |No |`2` |The number of audio channels. Supported values:<br><br><br>* `1`: Mono<br><br>* `2`: (Default) Stereo |
|`volume_method` |String |No |`2Pass` |Controls loudness normalization. Set to `2Pass` to enable two\-pass loudness analysis and processing, in which case `volume_integrated_loudness`, `volume_true_peak`, and `volume_loudness_range` take effect. If not set, the volume is not processed. |
|`volume_integrated_loudness` |Number |No |`-14` |Specifies the target integrated loudness in LUFS, which is used to set the overall perceived volume of the audio. The value range is `[-70, -5]`, with a default of `-12`. Required when `volume_method` is `2Pass`. |
|`volume_true_peak` |Number |No |`-1.5` |Specifies the true peak level in dBTP, which is used to set the maximum limit of the audio signal to prevent clipping distortion. The value range is `[-9, 0]`, with a default of `0`. Required when `volume_method` is `2Pass`. |
|`volume_loudness_range` |Number |No |`7` |Specifies the loudness range (dynamic range) in LU, which is used to adjust the difference between the loudest and quietest parts of the audio. The value range is `[1, 20]`, with a default of `7`. Effective when `volume_method` is `2Pass`. |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a video transcoding task: convert a video to `MP4` format, use `h264` video encoding, scale the resolution to `1920x1080`, use `abr` bitrate mode at `2500 Kbps`, and encode audio as `aac` at `192 Kbps`.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "video_url": "https://example-video.com/input.mov",
    "container_format": "MP4",
    "video": {
        "codec": "h264",
        "scale_type": 2,
        "scale_width": 1920,
        "scale_height": 1080,
        "bitrate_mode": "abr",
        "bitrate_kbps": 2500,
        "fps": 30
    },
    "audio": {
        "codec": "aac",
        "sample_rate": 48000,
        "bitrate_mode": "cbr",
        "bitrate_kbps": 192,
        "channels": 2
    }
}'
```


<span id="response-description"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="3248d691"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="b68d6121"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="c6579c6d"></span>
### Response example

<span id="1845fc6f"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-transcode-video-123456789",
  "request_id": "20240522180000ABCDEFG12345"
}
```


<span id="f58bd7a0"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240522180500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter 'video' is required.",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Video transcoding is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`"https://..."` |The download URL of the output video. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |`125.5` |The duration of the output video, in seconds. |
|`resolution` |String |`"1080p"` |The resolution specification of the transcoded video. Possible values include `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, `4k`, and so on. |
|`video_codec` |String |`"h264"` |The codec of the transcoded video. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-transcode-video-123456789",
    "request_id": "20240522180000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/transcoded_video.mp4?auth_key=...",
        "duration": 125.5,
        "resolution": "1080p",
        "video_codec": "h264"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```
