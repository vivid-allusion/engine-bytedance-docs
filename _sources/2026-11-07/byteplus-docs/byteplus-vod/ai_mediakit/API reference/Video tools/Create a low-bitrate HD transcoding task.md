---
title: "Create a low-bitrate HD transcoding task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-low-bitrate-HD-transcoding-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/martencode-video`

This API submits an asynchronous low\-bitrate HD transcoding task. Based on the characteristics of the human visual system, low\-bitrate HD transcoding intelligently analyzes the scenes, motion, content, and textures of a video during transcoding and selects the optimal encoding parameters, so that it outputs a video with better perceived quality at a relatively lower bitrate. This reduces bandwidth costs while delivering a better viewing experience for your users.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-low-bitrate-hd-transcoding">Low\-bitrate HD transcoding</a>.</div>


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
|`video_url` |String |Yes |`https://example.com/input.mov` |The URL of the video to be transcoded.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|`container_format` |String |Yes |`MP4` |The output container format. Supported values:<br><br><br>* `MP4` (default)<br><br>* `FLV`<br><br>* `MPEGTS` |
|`video` |Object |Yes |`-` |Video transcoding parameters. See [The video object](https://docs.byteplus.com/docs/byteplus-vod/117668#video-object) below for the detailed structure. |
|`audio` |Object |No |`-` |Audio transcoding parameters. If this object is omitted, the audio is transcoded with default parameters (codec `aac`, other parameters following the source file). See [The audio object](https://docs.byteplus.com/docs/byteplus-vod/117668#audio-object) below for the detailed structure. |
|`metadata_keep_tags` |Array of Strings |No |`["title", "artist"]` |The list of metadata tags to keep from the source video. By default, transcoding discards most metadata (such as title and artist). Use this parameter to specify the tag keys to keep. This parameter does not take effect when the `container_format` is set to `MPEGTS`. |
|`metadata_add_tags` |Array of Objects |No |`[{"key": "album", "value": "2024 Remaster"}]` |The list of metadata tags to add to the output video. Each tag consists of a `key` and a `value`. If an added tag has the same name as a kept tag, the setting here **overrides** the source file's value. This parameter does not take effect when the `container_format` is set to `MPEGTS`. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/uchbv7an/yf0irz3g). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |


<span id="video-object"></span>
#### The video object

The `video` object defines the video transcoding parameters and is required.


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`codec` |String |Yes |`h264` |The video codec. Defaults to `h264`. Supported values: `h264`, `h265`. |
|`scale_type` |Integer |No |`2` |The scaling mode of the video frame. Defaults to `0`.<br><br><br>* `0`: **Follow\-source mode**. No scaling is performed, and `scale_mode`, `scale_width`, `scale_height`, `scale_short`, and `scale_long` are all ignored. This mode supports up to 8K resolution.<br><br>* `1`: **Long/short edge mode**. Activates `scale_short` and `scale_long`. You can set the long or short edge of the output frame; the other edge scales proportionally. This mode supports up to 4K resolution.<br><br>* `2`: **Width/height mode**. Activates `scale_width` and `scale_height`. You can set the width or height of the output frame; the other edge scales proportionally. This mode supports up to 4K resolution. |
|`scale_mode` |Integer |No |`2` |The fill/stretch strategy, used when the target size you set differs in aspect ratio from the source. Takes effect only when `scale_type` is `1` or `2`. Defaults to `0`.<br><br><br>* `0`: No upscaling. Downscale when the source is larger than the target; keep the original size when smaller.<br><br>* `1`: Stretch upscaling. Force\-stretch to the target width and height, which may distort the frame.<br><br>* `2`: Letterbox upscaling. Scale proportionally to fit within the target box and pad the remaining area with black bars. |
|`scale_width` |Integer |No |`1920` |The target width, in px. Value range `[0, 4320]`. Takes effect only when `scale_type` is `2` (width/height mode). If you provide only one of `scale_width` or `scale_height`, the other edge scales proportionally. |
|`scale_height` |Integer |No |`1080` |The target height, in px. Value range `[0, 4320]`. Takes effect only when `scale_type` is `2` (width/height mode). If you provide only one of `scale_width` or `scale_height`, the other edge scales proportionally. |
|`scale_short` |Integer |No |`720` |The target short edge, in px. Value range `[0, 4320]`. Takes effect only when `scale_type` is `1` (long/short edge mode). If you provide only one of `scale_short` or `scale_long`, the other edge scales proportionally. |
|`scale_long` |Integer |No |`1280` |The target long edge, in px. Value range `[0, 4320]`. Takes effect only when `scale_type` is `1` (long/short edge mode). If you provide only one of `scale_short` or `scale_long`, the other edge scales proportionally. |
|`bitrate_mode` |String |Yes |`crf` |The bitrate control mode. Defaults to `crf`.<br><br><br>* `crf`: **Constant Rate Factor** mode. The system keeps the overall visual quality at the level set by `bitrate_crf` (the smaller the value, the higher the quality) while ensuring the instantaneous bitrate does not exceed the `bitrate_kbps` limit. This is the best balance between quality and file size and is recommended for most scenarios.<br><br>* `abr`: **Average Bitrate** mode. The encoder adjusts the bitrate so that the overall average bitrate of the output approaches the value set by `bitrate_kbps`. Suitable when the file size must stay within a specific range.<br><br>* `cbr`: **Constant Bitrate** mode. The encoder tries to keep every second of the stream strictly at the bitrate set by `bitrate_kbps`. Quality fluctuates with scene complexity, but the bitrate is very stable. Suitable for streaming scenarios with strict transmission\-stability requirements. |
|`bitrate_crf` |Number |No |`23` |The CRF (Constant Rate Factor) value, effective only when `bitrate_mode` is `crf`; it is the main quality controller in `crf` mode. Value range `[0, 51]`, default `25`. A smaller value means higher quality and a larger file. `0` means lossless. |
|`bitrate_kbps` |Integer |Yes |`2500` |The target video bitrate, in Kbps. Value range `[10, 50000]`, default `2000`. Its exact effect depends on `bitrate_mode`:<br><br><br>* In `crf` mode: the maximum bitrate limit.<br><br>* In `abr` mode: the average bitrate target.<br><br>* In `cbr` mode: the constant bitrate target. |
|`fps_mode` |String |No |`vfr` |The frame\-rate control mode. It takes effect only when `fps` is set; if you omit `fps`, the system follows the source frame rate and `fps_mode` is ignored. Defaults to `vfr`.<br><br><br>* `vfr`: Variable frame rate. `fps` is the maximum frame\-rate limit. If the source frame rate is below `fps`, it is preserved; if above, it is reduced to `fps`.<br><br>* `cfr`: Constant frame rate. The output is force\-converted to the constant frame rate set by `fps`, regardless of the source frame rate. |
|`fps` |Integer |No |`30` |The target frame rate. Value range `[1, 240]`. Setting this activates the `fps_mode` logic. In `vfr` mode it is the maximum frame rate; in `cfr` mode it is the constant frame rate. If omitted, the source frame rate is fully followed. |
|`is_hdr_to_sdr` |Boolean |No |`true` |Whether to convert an HDR (High Dynamic Range) video to SDR (Standard Dynamic Range). Defaults to `true`. Set to `false` to preserve HDR. |


<span id="audio-object"></span>
#### The audio object

The `audio` object defines the audio transcoding parameters. If omitted, the audio is encoded as `aac` following the source.


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`codec` |String |Yes |`aac` |The audio codec. Defaults to `aac`. Currently only `aac` is supported. |
|`sample_rate` |Integer |Yes |`44100` |The audio sample rate, in Hz. Defaults to `44100`. Supported `aac` sample rates: `8000`, `11025`, `12000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`, `64000`, `88200`, `96000`. |
|`bitrate_mode` |String |Yes |`cbr` |The audio bitrate control mode. Supported values:<br><br><br>* `cbr`: (default) Constant bitrate mode. Supported only when `video.codec` is `h264`. The encoder tries to keep every second of the audio stream strictly at the bitrate set by `bitrate_kbps`, making the file size predictable—suitable for streaming with strict bandwidth\-stability requirements.<br><br>* `cae`: Content\-adaptive bitrate mode (supported only when `audio.codec` is `aac`). The encoder dynamically adjusts the instantaneous bitrate based on content complexity while ensuring the **average bitrate** of the whole file approaches the target set by `bitrate_kbps`. |
|`bitrate_kbps` |Integer |No |`192` |The audio bitrate, in Kbps. Value range `[10, 500]`, default `128`. If omitted, the output audio bitrate matches the source audio. |
|`channels` |Integer |No |`2` |The number of audio channels. Supported values:<br><br><br>* `1`: Mono<br><br>* `2`: (default) Stereo |
|`volume_method` |String |No |`2Pass` |The loudness\-normalization switch. Set to `2Pass` to enable two\-pass loudness analysis and processing, in which case `volume_integrated_loudness`, `volume_true_peak`, and `volume_loudness_range` take effect. If omitted, volume is not processed. |
|`volume_integrated_loudness` |Number |No |`-14` |The target integrated loudness, setting the overall perceived volume, in LUFS. Value range `[-70, -5]`, default `-12`. Required when `volume_method` is `2Pass`. |
|`volume_true_peak` |Number |No |`-1.5` |The true\-peak level, setting the maximum limit of the audio signal to prevent clipping distortion, in dBTP. Value range `[-9, 0]`, default `0`. Required when `volume_method` is `2Pass`. |
|`volume_loudness_range` |Number |No |`7` |The loudness range (dynamic range), adjusting the difference between the loudest and quietest parts, in LU. Value range `[1, 20]`, default `7`. Takes effect when `volume_method` is `2Pass`. |


<span id="request-example"></span>
## Request example

The following example submits a low\-bitrate HD transcoding task that:


* Packages the video in the `MP4` container format.

* Encodes video with `h265`, using `crf` mode with a CRF value of `23`, and limits the long edge to `1920` px.

* Sets the audio bitrate to `192` Kbps.


```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/martencode-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "video_url": "https://example.com/your_video.mp4",
    "container_format": "MP4",
    "video": {
        "codec": "h265",
        "scale_type": 1,
        "scale_long": 1920,
        "bitrate_mode": "crf",
        "bitrate_crf": 23,
        "bitrate_kbps": 4000
    },
    "audio": {
        "bitrate_kbps": 192
    }
}'
```


<span id="response-description"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="7171ea93"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="ef078b27"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="1c71267b"></span>
### Response example

<span id="597479c5"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-martencode-video-123456789",
    "request_id": "20240522180000ABCDEFG12345"
}
```


<span id="f8a07331"></span>
#### Failure

```JSON
{
    "success": false,
    "task_id": "",
    "request_id": "20240522180500XYZW12345",
    "error": {
        "code": "InvalidParameter",
        "message": "The parameter 'video_url' is missing or invalid.",
        "type": "BadRequest"
    }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Low\-bitrate HD transcoding is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/108405) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`video_url` |String |The download URL of the output video. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |The duration of the output video, in seconds. |
|`resolution` |String |The resolution of the transcoded video. Possible values: `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, `4k`. |
|`video_codec` |String |The video codec, for example `h264` or `h265`. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-martencode-video-123456789",
    "request_id": "20240522180000ABCDEFG12345",
    "result": {
        "video_url": "https://example.byteplus.com/martencode_output.mp4?auth_key=...",
        "duration": 125.5,
        "resolution": "1080p",
        "video_codec": "h265"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```
