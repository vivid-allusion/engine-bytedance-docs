---
title: "Create an audio transcoding task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-audio-transcoding-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-audio`

This API submits an asynchronous audio transcoding task. Audio transcoding is the process of converting one audio bitstream into another, typically involving changes to the encoding format (such as AAC), encoding parameters (such as sample rate and bitrate), and container format (such as MP3), to adapt to different business scenarios, playback devices, and network environments.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-transcoding">Audio transcoding</a>.</div>


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
|`audio_url` |String |Yes |`https://example.com/source.wav` |The URL of the audio to be transcoded.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream audio formats such as `mp3`, `m4a`, `wav`, `wma`, `amr`, `aac`, `ogg`, and `flac`. |
|`container_format` |String |No |`MP3` |The target container format. Recommended to specify. The system automatically selects the corresponding encoder based on the container format:<br><br><br>* `MP3`: (Default) Encoder is MP3.<br><br>* `M4A`: Encoder is AAC.<br><br>* `OGG`: Encoder is Opus. |
|`audio` |Object |No |`-` |Audio parameter configuration. See [audio structure (audio transcoding parameters)](https://docs.byteplus.com/en/docs/25/115138#audio-structure-audio-transcoding-parameters) below. |
|`metadata_keep_tags` |Array of Strings |No |`["title", "artist"]` |The list of metadata tags to keep from the source audio. By default, transcoding discards most metadata (such as title and artist). Use this parameter to specify the tag keys to keep. |
|`metadata_add_tags` |Array of Objects |No |`[{"key": "album", "value": "Remastered 2024"}]` |The list of metadata tags to add to the output audio. Each tag consists of a `key` and a `value`. If an added tag has the same name as a kept tag, the setting here **overrides** the source file's value. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/uchbv7an/n1ltw7a7). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/uchbv7an/yf0irz3g). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |


<span id="audio-structure-audio-transcoding-parameters"></span>
#### The audio object (audio transcoding parameters)


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`sample_rate` |Integer |No |`44100` |The audio sample rate, in Hz. Defaults to `48000`. Recommended to fill in according to your target encoder. Different encoders support different sample rates:<br><br><br>* **MP3 supports**: `8000`, `11025`, `12000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`<br><br>* **AAC supports**: `8000`, `11025`, `12000`, `16000`, `22050`, `24000`, `32000`, `44100`, `48000`, `64000`, `88200`, `96000`<br><br>* **Opus supports**: `48000` |
|`bitrate_mode` |String |No |`cbr` |The audio bitrate control mode. Supported values:<br><br><br>* `cbr`: (Default) Constant bitrate mode. The encoder tries to keep every second of the audio stream strictly at the bitrate set by `bitrate_kbps`, making the file size precisely predictable—suitable for streaming scenarios with high bandwidth\-stability requirements.<br><br>* `cae`: Adaptive bitrate mode (supported only when `container_format` is `M4A`). The encoder dynamically adjusts the instantaneous bitrate based on content complexity but ensures the overall **average bitrate** of the file approaches the target set by `bitrate_kbps`. |
|`bitrate_kbps` |Integer |No |`192` |The audio bitrate, in Kbps. The value range is `[10, 500]`, with a default of `128`. If left empty, the output audio bitrate matches the source audio. |
|`channels` |Integer |No |`2` |The number of audio channels. Supported values:<br><br><br>* `1`: Mono<br><br>* `2`: (Default) Stereo |
|`volume_method` |String |No |`2Pass` |The loudness normalization switch. Set to `2Pass` to enable two\-pass loudness analysis and processing, in which case `volume_integrated_loudness`, `volume_true_peak`, and `volume_loudness_range` take effect. If not set, the volume is not processed. |
|`volume_integrated_loudness` |Number |No |`-14` |The target integrated loudness, used to set the overall perceived volume of the audio, in LUFS. The value range is `[-70, -5]`, with a default of `-12`. Effective and required when `volume_method` is `2Pass`. |
|`volume_true_peak` |Number |No |`-1.5` |The true peak level, used to set the maximum limit of the audio signal to prevent clipping distortion, in dBTP. The value range is `[-9, 0]`, with a default of `0`. Effective and required when `volume_method` is `2Pass`. |
|`volume_loudness_range` |Number |No |`7` |The loudness range (dynamic range), used to adjust the difference between the loudest and quietest parts of the audio, in LU. The value range is `[1, 20]`, with a default of `7`. Effective when `volume_method` is `2Pass`. |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit an audio transcoding task that converts the source audio to `MP3` format at `192` Kbps with loudness normalization enabled.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/transcode-audio' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "audio_url": "https://example.com/source_audio.wav",
    "container_format": "MP3",
    "audio": {
        "sample_rate": 44100,
        "bitrate_mode": "cbr",
        "bitrate_kbps": 192,
        "channels": 2,
        "volume_method": "2Pass",
        "volume_integrated_loudness": -14,
        "volume_true_peak": -1.5
    }
}'
```


<span id="response-description"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="6c9a33e9"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="96720cab"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="d62a3e9a"></span>
### Response example

<span id="1ba169c0"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-transcode-audio-123456789",
    "request_id": "20240522200000ABCDEFG12345"
}
```


<span id="225b9c82"></span>
#### Failure

```JSON
{
    "success": false,
    "task_id": "",
    "request_id": "20240522200500XYZW54321",
    "error": {
        "code": "InvalidParameter",
        "message": "The sample rate '64000' is not supported for container format 'MP3'.",
        "type": "BadRequest"
    }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Audio transcoding is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`audio_url` |String |The download URL of the output video. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |The duration of the output audio, in seconds. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-transcode-audio-123456789",
    "request_id": "20240522200000ABCDEFG12345",
    "result": {
        "audio_url": "https://example.byteplus.com/transcode_output.mp3?auth_key=...",
        "duration": 240.8
    },
    "expires_at": 1777473600,
    "created_at": 1777296000,
    "finished_at": 1777296030
}
```
