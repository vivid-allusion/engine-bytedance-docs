---
title: "Vocal Separation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/vocal-separation-d93f41dcef5cac84"
---

The Vocal Separation operator separates the first audio stream of an audio or video file into a vocal track and a non\-vocal residual track. Video input also produces an MP4 that retains the original picture with vocals\-only audio.

# Operator introduction

> Operator ID: `las_vocal_separation`

## Core capabilities

* **Two audio tracks**: Returns temporary download URLs, object\-storage paths, and file sizes for `vocals` and `no_vocals`.

* **Vocals\-only video**: Video input additionally returns `vocals_video.mp4`, containing the original picture and vocals\-only audio.

* **Common peak gain**: `normalize` applies the same safe gain to both tracks while preserving their relative levels. It is not LUFS normalization and does not improve separation quality.

* **Multiple output formats**: WAV for editing and downstream processing; MP3 or AAC for preview and distribution.

## Effect display

**Vocal and accompaniment separation from video**

* Input video

   [video](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/14435782-bdf9-43bb-8a71-165926234c74.mp4)

* Core parameter example

   ```json
   {
     "data": {
       "input_url": "tos://<your_bucket_name>/input.mp4",
       "output_tos_path": "tos://<your_bucket_name>/output/",
       "output_format": "wav",
       "normalize": false
     }
   }
   ```

* This example uses video as input and outputs two stereo WAV tracks at 44.1 kHz, each approximately 96 seconds long.

* `normalize=false` disables common peak gain. The operator may still apply the same safe attenuation to both tracks when needed to prevent clipping.

* Vocal track `vocals.wav`

   [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/4e32c396-f64e-432d-b34d-a8ff23224904.wav)

* Video retaining the original visuals with vocals only `vocals_video.mp4`

   [video](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/122bb5d7-c808-4436-a196-eaec261fef84.mp4)

* Accompaniment/background residual track `no_vocals.wav`

   [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/e0bf431e-7626-4c96-b53a-cb88e0fcce72.wav)

* `no_vocals` is the residual track obtained by subtracting the estimated vocals from the input. It can be used for accompaniment extraction or downstream mixing. It does not guarantee complete removal of vocals, so listen to or spot\-check the result before production use.

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

# Input and output requirements

## Input requirements

|**Breakdown item** |**Detailed requirements** |
|---|---|
|Supported input data modalities |* Audio<br><br>* Video |
|Input format: Audio/Video |* Format:<br><br>   * For video input, the video must contain a valid audio stream.<br><br>* Size: No larger than 1 GiB.<br><br>* Duration: Audio input must be 3–1800 seconds long; video input must be no longer than 1800 seconds.<br><br>* Source audio specifications: The source audio can contain 1–8 channels at a sample rate of 8000–192000 Hz.<br><br>* Audio streams: A maximum of 16 audio streams are supported. The first audio stream is always processed. For a multilingual or multitrack container, remux the target audio track as the first audio stream before submission.<br><br>* Other: The actual file must pass container and decoding validation. |
|Input path requirements |Provide input data to the operator through the `input_url` request parameter. Public URLs and TOS paths are supported.<br><br><br>* **Public URL**: A publicly accessible audio or video URL in `http://` or `https://` format.<br><br>* **TOS path**: Upload the input data to a TOS bucket under the same primary account and in the same region as the current LAS service. The calling account must have read permission for the object. Format: `tos://bucket/path/file`. |

## Output requirements

|**Breakdown item** |**Detailed requirements** |
|---|---|
|Supported output data modalities |* Audio<br><br>* Video |
|Output format: Audio |* Format:<br><br>   * For video input, the fixed output formats are `MP4` and `aac`.<br><br>   * For audio input, `wav`, `mp3`, and `aac` are supported. Use the `output_format` request parameter to specify the output format.<br><br>   * `wav` uses PCM16. The target bitrate of `mp3` and `aac` is 192 kbps, and `aac` uses an ADTS container.<br><br>* The output always includes a `vocals` track and a `no_vocals` residual track. Both tracks are 44100 Hz stereo.<br><br>   * This operator separates vocals and accompaniment in music mixes. It does not distinguish between speakers and does not provide denoising, dereverberation, or a zero\-vocal guarantee.<br><br>   * `no_vocals` is the residual after the estimated vocals are subtracted from the input. Intelligible speech may remain in dialogue\-only, highly reverberant, or low\-bitrate media. Before using the result for automated dubbing replacement, perform residual\-speech detection and manual spot checks. |
|Output format: Video |* Format: `MP4`. If the input contains a valid video stream, `vocals_video.mp4` is generated automatically. Video fields are not returned for audio\-only input. Whether a video is generated depends on the presence of a valid video stream, not the file extension.<br><br>* The output video retains the first non\-cover video stream and replaces the original audio track with a 44100 Hz stereo AAC vocals track. Video codecs incompatible with MP4 are transcoded to H.264.<br><br>* The original audio track, subtitles, attachments, and other data streams are not retained. |
|Output path requirements |Use `output_tos_path` to specify where the operator stores its output. A TOS path is supported.<br><br><br>* **TOS path**: Specify a writable TOS bucket directory under the same primary account and in the same region as the current LAS service. The calling account must have write permission for the directory. Format: `tos://bucket/output/`. If `output_tos_path` is omitted or set to `null`, the service uses a platform\-assigned directory.<br><br>* **Temporary URL**: Poll also returns download URLs valid for 1 day (24 hours). Retain the returned object\-storage paths or copy the results for long\-term use. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Usage is calculated from the input audio duration, including the audio\-track duration of video input. |
   |Billing type |Usage\-based billing in `USD/media minute`, with charges generated hourly. Billing precision is minute\-level; usage shorter than one minute is billed as one minute. |
   |Unit price |0.010 USD/media minute. |

* Billing details

   Billing formula: `Total fee = Unit price × Usage`

# Cautions and prerequisites

|Details |Cautions and prerequisites |
|---|---|
|Authentication |Generate an LAS API Key and configure it as an environment variable. See [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Select the LAS BaseURL for the region in which the service is deployed. See [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |
|Residual speech |`no_vocals` is the input minus estimated vocals and may retain intelligible speech in dialogue\-only, reverberant, or low\-bitrate material. Automated dubbing replacement requires residual\-speech detection and manual checks. |

# Rest API call

The operator uses asynchronous Submit and Poll APIs. Submit a task to obtain a `task_id`, then query Poll until the task reaches a terminal state.

## Submit

### Interface description

Submit a `las_vocal_separation` task. A successful request returns `PENDING` and a task ID. Request validation failures use HTTP errors; media validation and execution failures after acceptance are reported by Poll.

### Request parameters

**operator_id** string 必选 `Example value: las_vocal_separation`

Fixed to `las_vocal_separation`.

**operator_version** string 必选 `Example value: v1`

Fixed to `v1`.

**data** VocalSeparationRequest 必选

Vocal\-separation parameters.

**input_url** string 必选 `Example value: https://example.com/media/demo.mp4`

Audio or video address, 1–4096 characters. Supports `tos://`, `http://`, and `https://`. The first audio stream is selected. A valid video stream automatically produces vocals\-only video.

**output_tos_path** string `Optional` `Example value: tos://example-bucket/vocal-separation`

TOS output\-directory prefix, up to 2048 characters. Omission or `null` uses a platform\-assigned directory. An explicit value must be a non\-empty `tos://bucket/prefix` accessible to the calling account.

**output_format** string `Optional` `Example value: wav`

Audio output format: `wav`, `mp3`, or `aac`. Default: `wav`. Values are case\-sensitive. This does not control the vocals\-only video, which always uses MP4/AAC.

**normalize** boolean `Optional` `Example value: false`

Apply the same safe peak gain to both tracks. Default: `false`. Necessary anti\-clipping attenuation still applies when disabled.

**callback** Callback `Optional`

Optional terminal callback configuration. Omit it to retrieve the result through Poll.

**url** string 必选 `Example value: https://example.com/callback`

Callback URL receiving terminal task notifications.

### Response parameters

**metadata** Metadata

Request metadata.

**task_id** string

Accepted asynchronous task ID.

**task_status** string `Example value: PENDING`

A successful submission returns `PENDING`.

**business_code** string `Example value: 0`

`0` for a successful submission.

**error_msg** string

Error description; empty on success.

**request_id** string

API request ID.

### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_vocal_separation",
  "operator_version": "v1",
  "data": {
    "input_url": "https://example.com/media/demo.mp4",
    "output_tos_path": "tos://example-bucket/vocal-separation",
    "output_format": "wav",
    "normalize": false
  }
}'
```

### Error codes

|HttpStatusCode |Error code |Description |
|---|---|---|
|400 |VocalSeparation.InvalidRequest |Missing input, invalid type or enum, invalid URI, or unsupported field. |
|400 |Operator.InvalidId |Invalid or unavailable operator ID. |
|400 |Operator.InvalidVersion |Invalid operator version. |
|401 |Authorization.Missing |Authorization is missing. |
|401 |ApiKey.Invalid |API key is invalid. |
|429 |Server.Busy |Service is busy or rate\-limited. |
|500 |Server.InternalError |Submission or platform configuration failed; no task was accepted. |

## Poll

### Interface description

Query the status and results of a task. `COMPLETED` returns both audio tracks and, for video input, the vocals\-only video. Other states return an empty `data` object. Check both `metadata.task_status` and `metadata.business_code`.

### Request parameters

**operator_id** string 必选 `Example value: las_vocal_separation`

Fixed to `las_vocal_separation`.

**operator_version** string 必选 `Example value: v1`

Fixed to `v1`.

**task_id** string 必选

Task ID returned by Submit.

### Response parameters

**metadata** Metadata

Task metadata.

**task_id** string

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

`PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, `EXPIRED`, `CANCELLED`, or `UNKNOWN`. Only `COMPLETED` returns usable results.

**business_code** string `Example value: 0`

Business code; also check `task_status`.

**error_msg** string

Error description.

**request_id** string

API request ID.

**submit_time** string

Submission time in ISO 8601 format.

**end_time** string

End time in ISO 8601 format when available.

**data** VocalSeparationResult

Media results after successful completion.

**request_id** string

Processing request identifier.

**vocals_url** string

Temporary vocal\-track URL, valid for 24 hours.

**vocals_object_storage_path** string

Vocal\-track object\-storage path.

**vocals_size_bytes** integer

Vocal\-track size in bytes.

**no_vocals_url** string

Temporary residual\-track URL, valid for 24 hours.

**no_vocals_object_storage_path** string

Residual\-track object\-storage path.

**no_vocals_size_bytes** integer

Residual\-track size in bytes.

**vocals_video_url** string

Temporary vocals\-only video URL. Returned only when the input has a valid video stream.

**vocals_video_object_storage_path** string

Vocals\-only video object\-storage path. The filename is `vocals_video.mp4`.

**vocals_video_size_bytes** integer

Vocals\-only video size in bytes.

**audio** AudioResult

Standardized audio details.

**duration_sec** double

Validated audio duration in seconds.

**frames** integer

PCM frame count per internal track.

**sample_rate** integer `Example value: 44100`

Fixed to 44100 Hz.

**channels** integer `Example value: 2`

Fixed to 2.

**sample_format** string `Example value: s16`

Internal PCM format.

**output_format** string `Example value: wav`

`wav`, `mp3`, or `aac`, matching Submit.

### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
  "operator_id": "las_vocal_separation",
  "operator_version": "v1",
  "task_id": "ffb57ea6450c894f354c"
}'
```

### Response example

```json
{
  "metadata": {
    "task_id": "ffb57ea6450c894f354c",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "vocals_url": "https://example.com/results/vocals.wav",
    "vocals_object_storage_path": "tos://example-bucket/task/vocals.wav",
    "vocals_size_bytes": 21168044,
    "no_vocals_url": "https://example.com/results/no_vocals.wav",
    "no_vocals_object_storage_path": "tos://example-bucket/task/no_vocals.wav",
    "no_vocals_size_bytes": 21168044,
    "vocals_video_url": "https://example.com/results/vocals_video.mp4",
    "vocals_video_object_storage_path": "tos://example-bucket/task/vocals_video.mp4",
    "vocals_video_size_bytes": 48211390,
    "audio": {
      "duration_sec": 120.0,
      "frames": 5292000,
      "sample_rate": 44100,
      "channels": 2,
      "sample_format": "s16",
      "output_format": "wav"
    }
  }
}
```

### Common task error codes

|Error code |Description |
|---|---|
|VocalSeparation.DownloadRejected |Input rejected by access policy or download validation. |
|VocalSeparation.FileTooLarge |Input exceeds the size limit. |
|VocalSeparation.DurationTooShort |Audio is shorter than the minimum duration. |
|VocalSeparation.DurationExceeded |Audio or video exceeds the duration limit. |
|VocalSeparation.AudioStreamMissing |Input has no audio stream. |
|VocalSeparation.FormatUnsupported |Unsupported container, codec, stream count, channel count, or sample rate. |
|VocalSeparation.MediaInvalid |Media is damaged, incomplete, or undecodable. |
|VocalSeparation.ProcessingFailed |Separation, transcoding, video composition, or output validation failed. |
|VocalSeparation.Timeout |Task execution timed out. |
