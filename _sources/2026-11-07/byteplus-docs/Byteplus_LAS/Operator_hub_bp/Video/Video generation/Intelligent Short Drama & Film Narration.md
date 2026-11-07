---
title: "Intelligent Short Drama & Film Narration"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/intelligent-short-drama-and-film-narration"
---

The Intelligent Short Drama & Film Narration operator processes multi\-episode short dramas or TV series, or a single film, understands the plot, discovers highlight clues, and generates a narrated highlight video. It supports Chinese and English narration, preset and custom writing styles, narration speed control, original\-audio segments, opening strategies, high\-quality preset voices, reference\-audio or Material Library voice cloning in the normal tier, Material Library BGM selection and mixing, and configurable subtitle styles.

# Operator introduction

> Operator ID: las_short_drama_highlight_narration

## Applicable scenarios

* **Short drama and TV series promotion**: Generate narrated highlight videos from multiple episodes for distribution on video platforms.

* **Film remixing**: Discover narrative clues in a film or long video and generate a short\-form narrated highlight.

## Core capabilities

* **Cross\-episode story understanding**: Analyze short drama or TV series episodes, or a film, to identify key events, character relationships, conflict progression, and visual highlights.

* **Clue discovery and selection**: Select candidate main storylines, character arcs, conflict arcs, and relationship arcs for narration.

* **Multilingual narration**: Generate Chinese or English narration.

* **Writing style and speed control**: Use one of six preset styles or a custom style description, with slow, normal, or fast narration.

* **Original\-audio and opening planning**: Insert qualifying original\-audio segments and independently configure the opening strategy.

* **TTS quality and voice control**: Use high\-quality preset voices or reference\-audio voice cloning in the normal tier.

* **Material Library voices and BGM**: Select reference voices and music by asset ID, labels, or context without supplying audio URLs. BGM selection considers style and video duration; music is looped or trimmed and faded in and out.

* **Subtitle styling**: Configure the subtitle background and position.

## Effect showcase

* Input video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9e3157eced74b3ea6c307ab574a6e80~tplv-goo7wpa0wc-image.image)

* Output video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/470a5aa76afe48679b96fe91b6d2da5e~tplv-goo7wpa0wc-image.image)

——From the input long video, extract plot clues to generate a commentary short video

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Breakdown item |Performance impact description |
|---|---|
|Submit RPM |5 |
|Poll RPM |300 |
|Duration |Processing time generally increases with the input duration and target output duration. |

# Input and output requirements

## Input requirements

|Breakdown |Detailed requirements |
|---|---|
|Supported input data modalities |Video, audio, and text |
|Input video |* URL scheme: `http`, `https`, or `tos://`.<br><br>* Format: `mp4`, `mov`, or `mkv`.<br><br>* Quantity: 1–160 videos by default. Film mode requires exactly one video.<br><br>* Short drama and TV series: provide episodes in story order. Each episode must be at least 30 seconds by default and no longer than 300 minutes. Each episode must not exceed 10 GiB.<br><br>* Combined input: total duration must not exceed 300 minutes, inclusive, and total size must not exceed 20 GiB. |
|Reference audio and Material Library assets |* `tts_clone_prompt_audio_url` supports `tos://`, `http://`, and `https://` URLs and `wav` or `mp3` files. Reference audio is available only when `tts_audio_quality=normal`.<br><br>* `material_scope` supports `voice` and `bgm`, with at least one role. A Material Library voice also requires `tts_audio_quality=normal` and cannot be combined with manual reference audio.<br><br>* `EXACT` selects one material ID and an optional positive\-integer `revision`; when omitted, the latest available revision selected for the request is fixed for the task. `AUTO` requires exactly one of non\-empty `filters` or `infer_filters=true`. |

## Output requirements

|Breakdown |Detailed requirements |
|---|---|
|Output data type |Video |
|Output path |`output_tos_path` is optional. If provided, it must be a writable `tos://` directory. If omitted, LAS stores results temporarily and returns presigned URLs valid for 3 days. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |Charges consist of two billing items: **original video understanding** and **narration video generation**. The charge for an operator task is the sum of these two items.<br><br><br>* **Original video understanding**: Billed based on the total duration of all input videos. Tiered pricing applies to the portion up to and including 60 minutes and the portion exceeding 60 minutes.<br><br>* **Narration video generation**: Billed based on the total duration of all generated narration videos. You can obtain the actual duration of each generated video from the `duration_s` field returned by Poll. |
   |Billing type |Usage\-based billing, in `USD/minute`. Usage is calculated with millisecond precision and rounded down to the nearest millisecond. Charges are generated hourly based on actual usage. |
   |Unit price |The unit prices vary by billing item and duration tier. See Billing details below. |

* Billing details

   Billing formula: `Total charge = Original video understanding charge + Narration video generation charge`

   |Billing item |Billing tier |Unit price |
   |---|---|---|
   |Original video understanding |Portion of total input video duration up to and including 60 minutes |0.04 USD/minute |
   |Original video understanding |Portion of total input video duration exceeding 60 minutes |0.05 USD/minute |
   |Narration video generation |Total generated narration video duration |0.20 USD/minute |

* Billing example

   * Scenario: A task processes 30 short drama videos, each 3 minutes long, and generates 20 minutes of narration video.

   * Usage:

      * Total input video duration: `30 × 3 minutes = 90 minutes`.

      * Total generated narration video duration: `20 minutes`.

   * Charge calculation:

      * Original video understanding charge: `60 minutes × 0.04 USD/minute + 30 minutes × 0.05 USD/minute = 3.90 USD`.

      * Narration video generation charge: `20 minutes × 0.20 USD/minute = 4.00 USD`.

      * Total charge: `3.90 USD + 4.00 USD = 7.90 USD`.

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## API usage instructions

* This operator uses an asynchronous Submit/Poll workflow. Submit a task, then poll with the returned `task_id` until it reaches a terminal state.

* The top\-level `callback` parameter is not supported.

* `pending_timeout_minutes` controls how long a task may remain in `PENDING`. If the limit is reached, the task becomes `EXPIRED`.

## Submit

### API description

Submit an Intelligent Short Drama & Film Narration task. A successful response returns a task ID.

### Request parameters

**operator_id** string 必选 `Example value: las_short_drama_highlight_narration`

Operator ID.

**operator_version** string 必选 `Example value: v1`

Operator version.

**data** ShortDramaHighlightNarrationReq 必选

Narration request parameters.

**input_videos** list of string 必选 `Example value: ["tos://bucket/drama/ep01.mp4", "tos://bucket/drama/ep02.mp4"]`

Input video URLs. Supports `tos://`, `http://`, and `https://`. Short drama and TV series episodes must be provided in episode order; array order is preserved. Film mode requires exactly one video.

**target_narration_duration** string `Example value: mid`

Approximate output duration: `short` (about 1 minute), `mid` (1 to 3 minutes), or `long` (3 minutes or longer). Default: `mid`. Poll returns the actual duration in `duration_s`.

**source_content_type** string `Example value: auto`

Source material type: `auto`, `short_drama`, `movie`, or `tv_series`. Default: `auto`. `movie` requires exactly one input video.

**narration_language** string `Example value: en`

Narration language: `en` or `zh`. Default: `zh`.

**narration_style** NarrationStyle

Narration writing style.

**type** string `Example value: custom`

Style type: `preset` or `custom`. Default: `preset`.

**name** string 必选 `Example value: Fast-paced and suspenseful`

For `type=preset`, supported values are `dramatic_reversal`, `calm_documentary`, `light_colloquial`, `roast_commentary`, `suspense_reasoning`, and `emotional_storytelling`. For `type=custom`, provide a non\-empty description of up to 1,000 characters.

**narration_speed** string `Example value: normal`

Narration speed: `slow`, `normal`, or `fast`. Default: `normal`.

**enable_original_audio_windows** boolean `Example value: false`

Whether to insert original\-audio segments into the main narration. Default: `false`. A qualifying segment is not guaranteed.

**opening_hook_mode** string `Example value: auto`

Opening strategy: `auto`, `original_audio`, `narrated`, or `off`. Default: `auto`. With `original_audio`, the task fails if no qualifying segment is found.

**tts_audio_quality** string `Example value: high-quality`

TTS tier: `high-quality` or `normal`. Default: `normal`. Reference audio and Material Library voices are not supported in the high\-quality tier.

**tts_voice** string `Example value: 青年男声`

Preset voice for the high\-quality tier. Supported values are `young_female`, `sweet_female`, `young_male`, and `teenage_male`. Default in this tier: `young_male`.

**subtitle_blur_mode** string `Example value: gaussian`

Subtitle background: `gaussian`, `white`, or `black`. Default: `gaussian`.

**subtitle_position** string `Example value: bottom`

Subtitle position: `auto`, `top`, or `bottom`. Default: `auto`.

**tts_clone_prompt_audio_url** string `Example value: tos://bucket/audio/voice.wav`

Reference audio for voice cloning in the normal tier. Supports `tos://`, `http://`, and `https://`, with `wav` or `mp3` files. Mutually exclusive with `material_scope.voice`. If no Material Library voice is selected, omission or a blank value uses the execution service default voice.

**material_scope** MaterialScope `Optional`

Material Library voice and BGM selection. Omit or set to `null` to keep the existing behavior. A non\-null object must contain at least one non\-null role.

**voice** MaterialSelector `Optional`

Selects a `VOICE` asset. Requires `tts_audio_quality=normal` and cannot be combined with `tts_clone_prompt_audio_url` or the high\-quality preset voice parameter `tts_voice`.

**mode** string 必选 `Example value: EXACT`

Selection mode. Supported values: `EXACT` and `AUTO`.

**material_ids** list of string `Conditionally required` `Example value: ["mat-voice-example"]`

`EXACT` requires exactly one non\-empty material ID. For `AUTO`, omit this field or pass an empty list.

**revision** integer `Optional` `Example value: 1`

Optional material revision for `EXACT`. An explicit positive integer takes precedence. If omitted or `null`, the latest available revision selected for this request is fixed for the task. For `AUTO`, omit this field or set it to `null`.

**filters** object `Optional` `Example value: {"gender":"FEMALE","language":["ZH","EN"]}`

Label filters for `AUTO`: at most 8 non\-empty keys, each mapped to a non\-empty string or 1–20 non\-empty strings. Use current Material Library value codes. Cannot be combined with `infer_filters=true`; omit or use an empty object for `EXACT`.

**infer_filters** boolean `Optional` `Example value: true`

Default: `false`. For `AUTO`, set to `true` to infer preferences from content type, narration style, language, and other context. Cannot be combined with non\-empty `filters`.

**bgm** MaterialSelector `Optional`

Selects a `BGM` asset. AUTO selection can use labels or infer preferences from context and final\-video duration. One BGM track is used for each output video.

**mode** string 必选 `Example value: EXACT`

Selection mode. Supported values: `EXACT` and `AUTO`.

**material_ids** list of string `Conditionally required` `Example value: ["mat-voice-example"]`

`EXACT` requires exactly one non\-empty material ID. For `AUTO`, omit this field or pass an empty list.

**revision** integer `Optional` `Example value: 1`

Optional material revision for `EXACT`. An explicit positive integer takes precedence. If omitted or `null`, the latest available revision selected for this request is fixed for the task. For `AUTO`, omit this field or set it to `null`.

**filters** object `Optional` `Example value: {"gender":"FEMALE","language":["ZH","EN"]}`

Label filters for `AUTO`: at most 8 non\-empty keys, each mapped to a non\-empty string or 1–20 non\-empty strings. Use current Material Library value codes. Cannot be combined with `infer_filters=true`; omit or use an empty object for `EXACT`.

**infer_filters** boolean `Optional` `Example value: true`

Default: `false`. For `AUTO`, set to `true` to infer preferences from content type, narration style, language, and other context. BGM selection also considers the narration summary and final\-video duration. Cannot be combined with non\-empty `filters`.

**output_tos_path** string `Example value: tos://bucket/output/highlight/`

Optional TOS output directory. If omitted, results are returned as presigned URLs valid for 3 days.

**pending_timeout_minutes** integer `Example value: 120`

Maximum time that the task may remain in `PENDING`, from 30 to 4320 minutes. If omitted, pending expiration is disabled.

Submit validates the request structure, video count, URL scheme prefix, enum and numeric values, and cross\-field rules. Video accessibility, media format, duration and size, reference audio, and TOS read/write behavior are validated asynchronously. Read asynchronous failures from Poll metadata.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-20260715120000-abc123`

Task ID used by Poll.

**task_status** string `Example value: PENDING`

Always `PENDING` after a successful submission.

**business_code** string `Example value: 0`

Business code. `0` indicates successful submission.

**error_msg** string

Error message. Empty when submission succeeds.

**request_id** string `Example value: 20260819120000ABCDEF`

Request ID for tracing and troubleshooting.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_highlight_narration",
    "operator_version": "v1",
    "pending_timeout_minutes": 120,
    "data": {
        "input_videos": [
            "https://example.com/episode_01.mp4",
            "https://example.com/episode_02.mp4"
        ],
        "target_narration_duration": "short",
        "source_content_type": "short_drama",
        "narration_language": "en",
        "narration_style": {
            "type": "custom",
            "name": "Fast-paced and suspenseful"
        },
        "narration_speed": "normal",
        "enable_original_audio_windows": false,
        "opening_hook_mode": "auto",
        "tts_audio_quality": "high-quality",
        "tts_voice": "青年男声",
        "subtitle_blur_mode": "gaussian",
        "subtitle_position": "bottom",
        "output_tos_path": "tos://bucket/output/highlight_narration/"
    }
}'
```

Use a specific Material Library voice and let the operator infer BGM preferences:

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_highlight_narration",
    "operator_version": "v1",
    "data": {
        "input_videos": ["https://example.com/episode_01.mp4"],
        "tts_audio_quality": "normal",
        "material_scope": {
            "voice": {
                "mode": "EXACT",
                "material_ids": ["mat-voice-example"]
            },
            "bgm": {
                "mode": "AUTO",
                "infer_filters": true
            }
        }
    }
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20260715120000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": "",
    "request_id": "20260819120000ABCDEF"
  }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |A required value is missing or a value, enum, cross\-field combination, URL scheme, video count, or `pending_timeout_minutes` is invalid. This includes an empty `material_scope`, invalid selection constraints, a Material Library voice used with the high\-quality tier or manual reference audio, and the unsupported `callback` field. |
|400 |Body.Invalid |The body is invalid. |The request body is invalid or cannot be deserialized. |
|400 |Operator.InvalidId |The operator is invalid. |The operator ID does not exist or is unavailable. |
|400 |Operator.InvalidVersion |The operator version is invalid. |The operator version does not exist or is unavailable. |
|401 |Authorization.Missing |The authorization header is missing. |Authentication information is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|429 |OperatorConcurrencyExceeded |Concurrency limit of the operator is exceeded. |The operator concurrency limit for the current account has been reached. |
|429 |OperatorPendingQueueLimitExceeded |Pending queue limit of the operator is exceeded. |The pending\-task limit for the current account has been reached. |
|429 |APIAccountRpmRateLimitExceeded |The RPM limit for the API on your account has been exceeded. |The API request rate exceeds the account limit. |
|500 |Server.InternalError |General Internal Error |Internal server error. |

No matching assets, an unavailable revision, reference\-audio download failure, or BGM processing failure causes the asynchronous task to fail. The operator does not silently substitute a default voice or deliver a video without the selected BGM. Inspect Poll `metadata.task_status`, `metadata.business_code`, and `metadata.error_msg`.

## Poll

### API description

Query the status and result of an Intelligent Short Drama & Film Narration task.

### Request parameters

**operator_id** string 必选 `Example value: las_short_drama_highlight_narration`

Operator ID.

**operator_version** string 必选 `Example value: v1`

Operator version.

**task_id** string 必选 `Example value: task-20260715120000-abc123`

Task ID returned by Submit.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string

Task ID.

**task_status** string `Example value: COMPLETED`

Valid values: `ACCEPTED`, `PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, `EXPIRED`, `CANCELLED`, `TIMEOUT`, and `UNKNOWN`. Only `ACCEPTED`, `PENDING`, `RUNNING`, and `UNKNOWN` are non\-terminal.

**business_code** string `Example value: 0`

Business code. Interpret it together with `task_status` and `error_msg`.

**error_msg** string

Status or error information.

**request_id** string

Request ID of the current Poll call.

**submit_time** string

Submission time in ISO 8601 format, when available.

**end_time** string

Completion time in ISO 8601 format, when available.

**data** ShortDramaHighlightNarrationResp

Task result. Treat `videos` as complete only when `task_status=COMPLETED`.

**videos** list of Video

Generated videos.

**video_id** string `Example value: v_main_storyline_01`

Generated video ID.

**duration_s** float `Example value: 95.1`

Actual video duration in seconds.

**final_video_path** string

TOS path of the final video.

**final_video_url** string

Temporary accessible URL of the final video.

`COMPLETED`, `FAILED`, `EXPIRED`, `CANCELLED`, and `TIMEOUT` are terminal states. Executor status `partial_success` is normalized to `FAILED`. Do not determine task success from the Poll HTTP status alone.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_short_drama_highlight_narration",
    "operator_version": "v1",
    "task_id": "task-20260715120000-abc123"
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20260715120000-abc123",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": "",
    "request_id": "20260819120500ABCDEF",
    "submit_time": "2026-08-19T12:00:00+08:00",
    "end_time": "2026-08-19T12:05:00+08:00"
  },
  "data": {
    "videos": [
      {
        "video_id": "v_main_storyline_01",
        "duration_s": 95.1,
        "final_video_path": "tos://bucket/output/highlight_narration/main_storyline/v_main_storyline_01/final.mp4",
        "final_video_url": "https://example.com/final_01.mp4"
      }
    ]
  }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Body.Invalid |The body is invalid. |The Poll request body is invalid or cannot be deserialized. |
|400 |TaskId.Missing |The task id is missing. |`task_id` is missing or empty. |
|400 |Operator.InvalidId |The operator is invalid. |The operator ID does not exist or is unavailable. |
|400 |Operator.InvalidVersion |The operator version is invalid. |The operator version does not exist or is unavailable. |
|401 |Authorization.Missing |The authorization header is missing. |Authentication information is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|429 |APIAccountRpmRateLimitExceeded |The RPM limit for the API on your account has been exceeded. |The Poll request rate exceeds the account limit. |
|200 |TaskId.Invalid |The task id is invalid. |The task does not exist, has no result, or is temporarily unavailable. Metadata returns `task_status=FAILED`. |
|200 |Server.InternalError |General Internal Error |The query or task result could not be parsed. Metadata returns `task_status=FAILED`. |

Asynchronous execution failures are returned in an HTTP 200 Poll response. Read `metadata.task_status`, `metadata.business_code`, and `metadata.error_msg` to determine the result.
