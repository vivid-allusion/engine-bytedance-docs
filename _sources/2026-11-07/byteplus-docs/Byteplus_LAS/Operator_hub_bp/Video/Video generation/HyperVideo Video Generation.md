---
title: "HyperVideo Video Generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/hyperframes-video-generation"
---

`las_video_hypervideo` is a HyperFrames\-based video generation operator. It takes a natural\-language video creation request (`prompt`), image / audio / video reference media, and a rendering specification (`render_config`), lets LAS plan the video structure and generate renderable HyperFrames content, and hands it to the Render Server to render, mix audio, encode, and upload to object storage (TOS), finally returning an accessible video URL and the TOS object path. The operator uses the asynchronous submit\-poll pattern: submit a generation task to obtain a `task_id`, then poll by `task_id` to retrieve the status and video result.

# Operator introduction

> Operator ID: `las_video_hypervideo`

## Core capabilities

* **Request\-driven generation**: Describe the video request with a natural\-language `prompt` (style, subtitles, on\-screen text, etc.); the service plans the video structure and generates renderable content.

* **Structured reference media**: Supply image, audio, and video references through `reference_images`, `reference_audios`, and `reference_videos`, then address them precisely in `prompt` with `@imageN`, `@audioN`, and `@videoN`. Each list is numbered independently from 1. English reference names are case\-insensitive, and spaces before the number are allowed, for example `@Image 1`.

* **Controllable rendering specification**: Control target duration, frame rate, aspect ratio, and resolution through `render_config`.

* **TTS narration**: Generate a narration track with `audio.tts_voice` + `audio.narration_text`.

* **External BGM**: Provide a list of HTTP(S) background\-music URLs through `audio.bgm_urls`.

* **Audio\-reactive visuals**: With `audio.audio_reactive=true`, the visuals follow the audio rhythm (requires TTS narration or BGM).

* **Custom output delivery**: Specify the output path with `storage.output_uri` (`tos://`); otherwise the server default directory is used.

## Application scenarios

* Fast production of marketing short videos such as product feature explainers and selling\-point introductions.

* Generate consistently styled videos from existing product images, brand music, or live\-action footage.

* Vertical short videos, feed ads, and other `9:16` video generation scenarios.

* Explainer videos with narration and subtitles, such as poem readings and knowledge popularization.

* Rhythm\-driven videos whose visuals follow the music or narration rhythm.

## Effect display

* Example input

   ```text
   Generate a short English enlightenment teaching video for children aged 3-6 in Hong Kong on the most common basic English words in daily life, such as fruit (apple, banana, orange). The video uses colorful cartoon animation style, each word is matched with a corresponding cute illustration, and the words are displayed large and clear on the screen. At the same time, there are standard British English pronunciation demonstrations to encourage children to follow along.
   ```

* [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9b07f0e48fc457c8b8b232a63d74a37~tplv-goo7wpa0wc-raw.image)

   * When invoking this operator, you can first use the [Video Script Planner](https://docs.byteplus.com/docs/Byteplus_LAS/video-script-planner) operator to generate a video production plan, and then invoke this operator.

   * When using this operator to generate videos, contact the LAS support team for assistance with output quality optimization.

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Breakdown item |Performance impact |
|---|---|
|Submit RPM |30 |
|Poll RPM |600 |
|Processing time |Generation and rendering time increases with the output duration and reference\-media complexity. Use backoff polling. |

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Text<br><br>* Image<br><br>* Audio<br><br>* Video |
|Input format: Text |* Prompt: `prompt` is required and must describe the video generation request.<br><br>* Narration: When `narration_text` is provided, `tts_voice` must also be provided. |
|Input format: Image |* Provide reference images through `reference_images`. Array order maps to `@imageN` in `prompt` and must be preserved.<br><br>* Each file must be decodable as an image. No common file\-extension whitelist or per\-file size limit is currently enforced. |
|Input format: Audio |* Reference audio: Provide it through `reference_audios`. Array order maps to `@audioN` in `prompt`, and each item is an independent track starting at 0 seconds and playing at most until the output video ends.<br><br>* Background music: `bgm_urls` accepts HTTP(S) URLs and follows the same requirements as reference audio.<br><br>* Each file must be decodable as audio. No common file\-extension whitelist, per\-file size limit, or source\-audio duration limit is currently enforced.<br><br>* Audio\-reactive generation: When `audio_reactive=true`, provide `tts_voice`, `bgm_urls`, or `reference_audios`. |
|Input format: Video |* Provide reference videos through `reference_videos`. Array order maps to `@videoN` in `prompt`, and videos are used as muted visual assets by default.<br><br>* Each file must be decodable as video. No common file\-extension whitelist, per\-file size limit, or source\-video duration limit is currently enforced. The 300\-second target\-output limit does not apply to reference videos. |
|Input path requirements |* Reference images, audio, videos, and background music must use directly accessible `http://` or `https://` URLs that do not require additional authentication headers.<br><br>* `tos://`, local paths, and Base64 Data URLs are not accepted.<br><br>* Presigned input URLs must remain valid until the task completes. Downloading, decoding, and rendering remain subject to execution timeouts and resource limits. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Video |
|Output format: Video |* Duration: `duration` accepts integers from 1 to 300 seconds inclusive and defaults to 10 seconds. The maximum requested target duration is 300 seconds (5 minutes); `0` and values outside the range return `Parameter.Invalid`. The actual output duration is returned in `output_video_duration_sec`.<br><br>* Frame rate: 1 to 60 FPS; the default is 30 FPS.<br><br>* Aspect ratio: `16:9`, `9:16`, `1:1`, `4:3`, or `3:4`; the default is `16:9`.<br><br>* Resolution: `720p` or `1080p`; the default is `1080p`.<br><br>* Configuration: `render_config` is required. Pass an empty object `{}` to use the default rendering settings. |
|Output path requirements |* Specify a `tos://` path through `storage.output_uri`. If omitted, the service uses its default storage. Poll returns the accessible video URL, TOS object path, and actual output duration after generation completes.<br><br>* The default signature lifetime of an output presigned URL is 7 days (604800 seconds). Temporary credentials may expire sooner. When Poll URL re\-signing is enabled, querying a successful result generates an 11\-hour (39600\-second) signature. Use `X-Tos-Date` and `X-Tos-Expires` in the returned URL to determine its expiry.<br><br>* After a URL expires, use `output_video_tos_uri` to obtain a new accessible URL. Polling again refreshes the URL when re\-signing is enabled.<br><br>* Video objects in the default service directory are retained for 30 days. Custom output directories follow the target bucket lifecycle rules. URL expiry does not immediately delete the object; download and save the result promptly. |

# Billing information

* Billing standard

   |Sub\-item |Billing standard description |
   |---|---|
   |Billing item |Usage is billed based on the duration of the output video. |
   |Billing type |Pay\-as\-you\-go. Unit: `USD/second`. Bills are generated hourly based on actual billable usage. Billing precision: millisecond\-level precision, with truncation. |
   |Unit price |0.075 USD/second |

* Billing details

   Billing formula: `Total fee = Unit price * Usage`

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Submit

### Interface description

Submit a `las_video_hypervideo` HyperFrames video generation task. The API returns an asynchronous task ID. Use the Poll API to query the video result once the task completes.

The default online quotas are 30 RPM for Submit and 600 RPM for Poll. Actual quotas follow the account service configuration. Authenticate with the `Authorization: Bearer <LAS_API_KEY>` request header.

### Request parameters

**operator_id** string 必选 `Example value: las_video_hypervideo`

Operator ID, fixed to `las_video_hypervideo`.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed to `v1`.

**data** VideoHypervideoUserReqParams 必选

Video generation business parameters. All nested objects enforce strict validation and reject undefined fields.

**prompt** string 必选 `Example value: Generate a 10-second product feature explainer video in a tech style.`

Video generation request; style, subtitles, and on\-screen text are all recommended here. An empty value returns `Parameter.Invalid`.

**reference_images** array of string `Optional` `Example value: ["https://example.com/images/product.png"]`

HTTP(S) URLs of reference images, default empty array. Array order maps to `@image1`, `@image2`, and so on in `prompt` and must be preserved. Files must be decodable images; no common file\-extension whitelist or per\-file size limit is currently enforced. See Input requirements for the common reference\-media and URL requirements.

**reference_audios** array of string `Optional` `Example value: ["https://example.com/audio/music.mp3"]`

HTTP(S) URLs of reference audio, default empty array. Array order maps to `@audio1`, `@audio2`, and so on in `prompt`. Each item is an independent track starting at 0 seconds and playing at most until the output video ends. No common file\-extension whitelist, per\-file size limit, or source\-audio duration limit is currently enforced.

**reference_videos** array of string `Optional` `Example value: ["https://example.com/videos/camera.mp4"]`

HTTP(S) URLs of reference videos, default empty array. Array order maps to `@video1`, `@video2`, and so on in `prompt`; reference videos are muted visual assets by default. Files must be decodable videos; no common file\-extension whitelist, per\-file size limit, or source\-video duration limit is currently enforced. The 300\-second limit applies to the requested output duration, not the reference video.

**render_config** RenderConfig 必选

Rendering specification. A missing value returns `Parameter.Invalid`; pass an empty object `{}` when no special settings are needed.

**duration** integer `Optional` `Example value: 10`

Target video duration in seconds. Accepts integers from 1 to 300 inclusive and defaults to 10; the maximum requested target duration per task is 300 seconds (5 minutes). A value of `0` or outside this range returns `Parameter.Invalid`. The actual output duration is returned in `output_video_duration_sec` by Poll.

**fps** integer `Optional` `Example value: 30`

Target frame rate, ranging from 1 to 60, default 30.

**ratio** string `Optional` `Example value: 16:9`

Aspect ratio, supports `16:9`, `9:16`, `1:1`, `4:3`, `3:4`, default `16:9`.

**resolution** string `Optional` `Example value: 1080p`

Resolution, supports `720p`, `1080p`, default `1080p`.

**storage** Storage `Optional`

Output storage configuration. The server default TOS directory is used when omitted.

**output_uri** string `Optional` `Example value: tos://example-bucket/hypervideo/demo-001`

Final video output path, must use the `tos://` prefix. When `storage` is omitted, the server default directory is used.

**region** string `Optional` `Example value: ap-southeast-1`

TOS region.

**tos_endpoint** string `Optional` `Example value: https://tos-ap-southeast-1.bytepluses.com`

TOS endpoint.

**audio** Audio `Optional`

Audio configuration.

**tts_voice** string `Optional` `Example value: zh_female_vv_uranus_bigtts`

TTS narration voice; generates a narration track when provided.

**narration_text** string `Optional` `Example value: Today we learn Li Bai's "Quiet Night Thoughts".`

Narration text; `tts_voice` must be provided together, otherwise `Parameter.Invalid` is returned.

**bgm_urls** array of string `Optional` `Example value: ["https://example.com/bgm/quiet-night.mp3"]`

Directly accessible HTTP(S) URLs of BGM audio files; other schemes return `Parameter.Invalid`. The same format, size, duration, and URL\-validity requirements as reference audio apply.

**audio_reactive** boolean `Optional` `Example value: true`

Whether the visuals follow the audio rhythm; when `true`, `tts_voice`, `bgm_urls`, or `reference_audios` must be provided, otherwise `Parameter.Invalid` is returned.

**callback** object `Optional`

Optional terminal callback configuration; `callback.url` is the callback address. If omitted, use Poll to retrieve the result.

**idempotent_id** string `Optional` `Example value: hypervideo-demo-001`

Idempotency ID, reserved by the protocol.

### Response parameters

**metadata** Metadata

Request metadata.

**task_id** string `Example value: fad4efcfd5022e012a3b`

Asynchronous task ID, used for Poll.

**task_status** string `Example value: PENDING`

Task status; a successful submit is usually `PENDING`.

**business_code** string `Example value: 0`

Business code; `0` means success.

**error_msg** string

Error description; empty on success.

**request_id** string `Example value: 9fed0e5f0659b128bad47e971aed3c81`

Request ID.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_video_hypervideo",
    "operator_version": "v1",
    "data": {
        "prompt": "Use @image1 and @video1 to create a 10-second product explainer whose visuals follow @audio1.",
        "reference_images": ["https://example.com/images/product.png"],
        "reference_audios": ["https://example.com/audio/music.mp3"],
        "reference_videos": ["https://example.com/videos/camera.mp4"],
        "render_config": {
            "duration": 10,
            "fps": 30,
            "ratio": "16:9",
            "resolution": "1080p"
        },
        "audio": {
            "audio_reactive": true
        }
    }
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "fad4efcfd5022e012a3b",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Parameter validation failed (missing prompt / render_config, non\-HTTP(S) reference media or BGM, invalid enum, out\-of\-range value, non\-`tos://` `output_uri`, `narration_text` without `tts_voice`, `audio_reactive` without an audio source, unknown fields, etc.). |
|400 |Operator.InvalidId |The operator is invalid. |The operator ID is invalid or unregistered. |
|400 |Operator.InvalidVersion |The operator version is invalid. |The operator version is invalid. |
|401 |Authorization.Missing |The authorization header is missing. |Missing authentication information. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|429 |Server.Busy |Server is Busy, please try again later. |Server busy or rate limited. |
|500 |Server.InternalError |General Internal Error |Server internal error (e.g. failed to obtain STS credentials or submit the task). |

## Poll

### Interface description

Query the status and result of a `las_video_hypervideo` HyperFrames video generation task by task ID. Video generation and rendering take time, so use a backoff polling strategy. Once the task completes, the accessible video URL, TOS object path, and actual output duration are returned.

The default signature lifetime of an output presigned URL is 7 days (604800 seconds). Temporary credentials may expire sooner. When Poll URL re\-signing is enabled, querying a successful result generates an 11\-hour (39600\-second) signature. Use `X-Tos-Date` and `X-Tos-Expires` in the returned URL to determine its expiry. After expiry, use `output_video_tos_uri` to obtain a new accessible URL; polling again refreshes the URL when re\-signing is enabled.

Video objects in the default service directory are retained for 30 days. Custom output directories follow the target bucket lifecycle rules. URL expiry does not immediately delete the object; download and save the result promptly. The default online Poll quota is 600 RPM, subject to the account service configuration.

### Request parameters

**operator_id** string 必选 `Example value: las_video_hypervideo`

Operator ID, fixed to `las_video_hypervideo`.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed to `v1`.

**task_id** string 必选 `Example value: fad4efcfd5022e012a3b`

The asynchronous task ID returned by the Submit API. An empty value returns `TaskId.Invalid`.

### Response parameters

**metadata** Metadata

Request metadata and task status.

**task_id** string `Example value: fad4efcfd5022e012a3b`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Task status; one of `PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, `TIMEOUT`, `UNKNOWN`.

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.

**business_code** string `Example value: 0`

Business code; `0` means success, non\-`0` indicates a specific error.

**error_msg** string

Error or status description.

**request_id** string `Example value: 9fed0e5f0659b128bad47e971aed3c81`

Request ID.

**data** VideoHypervideoUserResp

Video generation result after the task completes; non\-empty only on success.

**output_video_url** string `Example value: https://example.com/video.mp4`

Final accessible video URL. The default presigned signature lifetime is 7 days; temporary credentials may expire sooner. Poll re\-signing, when enabled, uses 11 hours. See the interface description for expiry and renewal rules.

**output_video_tos_uri** string `Example value: tos://example-bucket/hypervideo/demo-001/video.mp4`

The TOS object path of the final video.

**output_video_duration_sec** double `Example value: 8`

Actual output video duration in seconds, used for duration billing; it may differ from the requested target duration.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_video_hypervideo",
    "operator_version": "v1",
    "task_id": "fad4efcfd5022e012a3b"
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "fad4efcfd5022e012a3b",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "output_video_url": "https://example.com/video.mp4",
    "output_video_tos_uri": "tos://example-bucket/hypervideo/demo-001/video.mp4",
    "output_video_duration_sec": 8
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |TaskId.Invalid |The task id is invalid. |The task ID is empty, does not exist, or the result is missing. |
|400 |Parameter.Invalid |The parameter is invalid. |Parameter validation failed or task result parsing failed. |
|401 |Authorization.Missing |The authorization header is missing. |Missing authentication information. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|429 |Server.Busy |Server is Busy, please try again later. |Server busy or rate limited. |
|500 |Server.InternalError |General Internal Error |Server internal error. |

> Task\-level failures (e.g. the downstream Render Server failing to render or upload) are returned with `metadata.task_status=FAILED`, and `business_code` / `error_msg` carry the specific reason passed through from the execution side (such as `Hypervideo.RenderFailed`).
