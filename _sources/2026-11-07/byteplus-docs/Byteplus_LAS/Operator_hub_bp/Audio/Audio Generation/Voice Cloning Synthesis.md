---
title: "Voice Cloning Synthesis"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/voice-cloning-synthesis"
---

`las_voice_forge` is the Voice Cloning Synthesis operator. It synthesizes input text into speech and supports Voice Design, Controlled Voice Cloning, Material Library Voice Cloning, and High\-fidelity Continuation. It uses the asynchronous submit\-poll pattern: submit a synthesis task to obtain a `task_id`, then poll for the task status and audio result.

# Operator introduction

> Operator ID: `las_voice_forge`

## Application scenarios

* Narration, voiceover, broadcasting, and short\-video dubbing.

* Brand voices, virtual humans, and customer\-service voice reuse.

* High\-fidelity continuation when prompt audio and its exact transcript are available.

* Long\-form lectures, course content, and news\-broadcast audio generation.

## Core capabilities

* **Voice Design**: Use only `style_prompt` to describe and generate a target voice style without sample audio.

* **Controlled Voice Cloning**: Use `reference_audio_uri` to clone a voice, optionally with a style description.

* **Material Library Voice Cloning**: Reuse an available voice sample by material ID, optionally pin a revision, select it with label filters, or derive selection preferences from the synthesis text and style description.

* **High\-fidelity Continuation**: Provide `prompt_audio_uri` together with a `prompt_text` that matches the prompt audio, then synthesize new text using its voice, prosody, and delivery. This mode cannot be used together with `style_prompt`.

* **Long\-form Synthesis**: Split long text at natural boundaries, synthesize each segment, and concatenate the audio automatically.

* **Quality Self\-check and Regeneration**: Automatically regenerate results that appear to have low synthesis quality.

* **Multi\-format Audio Delivery**: Output multiple audio formats and return an audio URL, format, sample rate, duration, and character count. In `audio_uri` or `service` mode, a successful task returns a downloadable audio URL even when no output directory is specified.

## Effect display

* **Voice Design without reference audio**

   * **Scenario**: Generate a calm, professional narration voice from a text description without providing sample audio.

   * **Voice description**: `Calm and professional male voice, moderate speed`

   * **Core parameters**:

      ```json
      {
        "req_params": {
          "text": "LAS Voice Cloning Synthesis operator synthesizes input text into speech and supports Voice Design, Controlled Voice Cloning, and High-fidelity Continuation.",
          "audio_params": {
            "format": "wav",
            "sample_rate": 48000
          }
        },
        "engine_params": {
          "style_prompt": "Calm and professional male voice, moderate speed"
        },
        "service_params": {
          "response_mode": "audio_uri"
        }
      }
      ```

   * **Output**: WAV, mono, 16\-bit PCM, 48,000 Hz, 9.6 seconds

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/8a66d33b-7c74-47e4-80ce-fe36083d1a54.wav)

* **Controlled Voice Cloning with Standard narration**

   * **Scenario**: Clone the reference voice.

   * **Reference audio**: The source MP3 was converted to a mono, 24 kHz, 16\-bit WAV and uploaded to a readable TOS path.

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/c252cd91-164d-4c00-adba-dd0a2a853be8.mp3)

   * **Core parameters**:

      ```json
      {
        "req_params": {
          "text": "LAS Voice Cloning Synthesis operator synthesizes input text into speech and supports Voice Design, Controlled Voice Cloning, and High-fidelity Continuation.",
          "audio_params": {
            "format": "wav",
            "sample_rate": 48000
          }
        },
        "engine_params": {
          "reference_audio_uri": "tos://las-doctest-bp/las-ai/input/audio/las_voice_forge/529299c23994e1b1/standard_narration.wav"
        },
        "service_params": {
          "response_mode": "audio_uri"
        }
      }
      ```

   * **Output**: WAV, mono, 16\-bit PCM, 48,000 Hz, 10.08 seconds

      [audio](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/1f0b055d-53d5-482f-8670-2eea2a0032ee.wav)

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Breakdown item |Performance impact |
|---|---|
|Submit RPM |5 |
|Poll RPM |300 |

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Text<br><br>* Audio |
|Input format: Text |* Length: `req_params.text` is required and must contain 1 to 20,000 characters.<br><br>* SSML: Limited `<break>` pause tags are supported.<br><br>* Prompt text: When using prompt audio, provide an accurate `prompt_text` of no more than 1,000 characters. |
|Input format: Audio |* Format: Readable WAV files.<br><br>* Size: No larger than 50 MB.<br><br>* Duration: 0.1 to 300 seconds. A clear, low\-noise, single\-speaker recording of about 5 to 15 seconds is recommended. |
|Input path requirements |Provide reference or prompt audio through `reference_audio_uri` or `prompt_audio_uri`:<br><br><br>* **Public URL**: Use a service\-accessible `http://` or `https://` URL. Local paths are not supported.<br><br>* **TOS path**: Use a readable object in a TOS bucket under the same primary account and in the same region as the current LAS service. The calling account must have permission to read the object. Format: `tos://bucket/path/file.wav`.<br><br>   `prompt_audio_uri` must be used together with `prompt_text`. |
|Material Library voice |* `material_scope.voice` supports `EXACT` and `AUTO`.<br><br>* `EXACT` requires one material ID and accepts an optional positive\-integer `revision`; if omitted, the latest available revision selected for this request is fixed for the task.<br><br>* `AUTO` requires exactly one of non\-empty label `filters` or `infer_filters=true`.<br><br>* Material Library selection cannot be combined with `reference_audio_uri` or `prompt_audio_uri`, but it may be used with `style_prompt`. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |Audio |
|Output format: Audio |* Format: `wav`, `mp3`, `ogg_opus`, or `pcm`. PCM output is a raw mono `s16le` stream without a WAV header.<br><br>* Sample rate: 8,000, 16,000, 22,050, 24,000, 32,000, 44,100, or 48,000 Hz. |
|Output path requirements |Use `response_mode` to select the result form:<br><br><br>* **Base64**: `base64` returns Base64\-encoded audio in the Poll response.<br><br>* **Audio URI**: `audio_uri` returns a downloadable audio address; `service` returns both Base64 audio and an audio address. An output directory is not required for these modes.<br><br>* **TOS output directory**: When `output_object_storage_dir` is provided, it must be a writable TOS directory under the same primary account and in the same region as the current LAS service. The calling account must have permission to write to the directory. Format: `tos://bucket/output/`. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Unicode characters in the original decoded `req_params.text` for successful tasks. SSML tags, punctuation, spaces, and line breaks are included; audio duration is not billed. |
   |Billing type |Usage\-based billing in `USD/10K characters`. |
   |Unit price |1.5 USD/10K characters. |

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## API call instructions

* This operator uses asynchronous task APIs. Call the Submit interface to obtain a `task_id`, then call the Poll interface with that `task_id` to query the task status and retrieve the audio result after the task completes.

## Submit

### Interface description

Submit a `las_voice_forge` Voice Cloning Synthesis task. The API returns an asynchronous task ID. Use the Poll API to query the synthesis result. Set `material_scope.voice` to select a Material Library voice by material ID and optional revision, by label filters, or from preferences inferred from the synthesis text and `style_prompt`.

### Request parameters

**operator_id** string 必选 `Example value: las_voice_forge`

Operator ID, fixed to `las_voice_forge`.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed to `v1`.

**data** VoiceForgeUserReqParams 必选

Voice cloning / text\-to\-speech parameters. The request object is strictly validated; only the documented public fields are accepted, and undefined fields are rejected.

**material_scope** MaterialScope `Optional`

Material Library voice selection. Only `voice` is supported. Omit or set to `null` to preserve existing behavior. It cannot be combined with `engine_params.reference_audio_uri` or `engine_params.prompt_audio_uri`, but may be used with `style_prompt`.

**voice** MaterialVoiceSelector 必选

Required when `material_scope` is non\-null. No other role or unknown field is accepted.

**mode** string 必选 `Example value: EXACT`

Selection mode: `EXACT` or `AUTO`. `EXACT` requires one material ID and accepts an optional revision. `AUTO` requires exactly one of non\-empty `filters` or `infer_filters=true` and does not accept a material ID or revision.

**material_ids** list of string `Conditionally required` `Example value: ["mat-voice-example"]`

`EXACT` requires exactly one non\-empty Material Library voice ID. For `AUTO`, omit this field or pass an empty list.

**revision** integer `Optional` `Example value: 1`

Material revision, separate from operator version `v1`. For `EXACT`, an explicit positive integer takes precedence. If omitted or `null`, the latest available revision selected for this request is fixed for the task. For `AUTO`, omit this field or set it to `null`.

**filters** object `Optional` `Example value: {"gender":"FEMALE","language":["ZH","EN"]}`

Label filters for `AUTO`: at most 8 non\-empty keys, each with one non\-empty string or 1–20 non\-empty strings. Use current Material Library label keys and values. Cannot be combined with `infer_filters=true`.

**infer_filters** boolean `Optional` `Example value: true`

Default: `false`. With `AUTO`, set to `true` to derive selection preferences from `req_params.text` and `engine_params.style_prompt`. Do not provide non\-empty `filters`.

**req_params** ReqParams 必选

Text and audio output parameters.

**text** string 必选 `Example value: Welcome to the voice cloning operator.`

Text to synthesize. Raw length must be between 1 and 20000 characters. Limited SSML `<break>` pause tags are supported.

**audio_params** AudioParams `Optional`

Audio output parameters.

**format** string `Optional` `Example value: wav`

Output format. Supported values: `wav`, `mp3`, `ogg_opus`, `pcm`. Default: `wav`.

**sample_rate** integer `Optional` `Example value: 48000`

Output sample rate in Hz. Supported values: 8000, 16000, 22050, 24000, 32000, 44100, 48000. Default: 48000.

**bit_rate** integer `Optional` `Example value: 128000`

Compression bitrate from 64000 to 160000 bps. Effective only for `mp3` / `ogg_opus`. Default: 128000.

**additions** Additions `Optional`

Additional processing parameters.

**silence_duration** integer `Optional` `Example value: 0`

Tail silence duration in milliseconds, from 0 to 30000. Default: 0.

**engine_params** EngineParams `Optional`

Voice and generation parameters.

**style_prompt** string `Optional` `Example value: Calm and professional male voice, moderate speed`

Target voice\-style description, up to 300 characters. It cannot be configured together with `prompt_audio_uri`.

**reference_audio_uri** string `Optional` `Example value: tos://example-bucket/refs/speaker.wav`

Reference audio used to clone a voice. Supports only `tos://`, `http://`, and `https://`; local paths are not supported. The file must be a readable WAV file no larger than 50 MB and between 0.1 and 300 seconds long. A clear, low\-noise, single\-speaker recording of about 5 to 15 seconds is recommended. No transcript is required.

**prompt_audio_uri** string `Optional` `Example value: tos://example-bucket/refs/prompt.wav`

Prompt audio used for High\-fidelity Continuation. Supports the same URI schemes and file requirements as `reference_audio_uri`, must be paired with a matching `prompt_text`, and cannot be configured together with `style_prompt`.

**prompt_text** string `Optional` `Example value: This is the exact transcript of the prompt audio.`

Accurate transcript of the prompt audio, up to 1000 characters. Must be paired with `prompt_audio_uri`.

**guidance_scale** double `Optional` `Example value: 2.0`

Voice/style adherence strength, from 1.0 to 3.0. Default: 2.0.

**inference_steps** integer `Optional` `Example value: 10`

Generation steps, from 4 to 30. Default: 10. Higher values usually increase processing time.

**temperature** double `Optional` `Example value: 0.7`

Generation diversity, from 0.1 to 2.0. If omitted, the engine default is used.

**text_normalize** boolean `Optional` `Example value: true`

Whether to normalize numbers, dates, monetary amounts, and similar text. Default: `true`.

**reference_denoise** boolean `Optional` `Example value: false`

Whether to denoise reference audio. Default: `false`.

**enable_quality_retry** boolean `Optional` `Example value: true`

Whether to regenerate automatically when quality does not meet the threshold. Default: `true`.

**quality_retry_max_times** integer `Optional` `Example value: 3`

Maximum quality\-regeneration attempts, from 0 to 5. Default: 3.

**seed** integer `Optional` `Example value: 1234`

Random seed. A fixed value makes result reproduction and comparison easier.

**service_params** ServiceParams `Optional`

Output and long\-text parameters.

**response_mode** string `Optional` `Example value: audio_uri`

Response mode: `base64` returns Base64 audio, `audio_uri` returns an audio location, and `service` returns both. Default: `audio_uri`.

**timeout_sec** integer `Optional` `Example value: 1800`

Total request timeout from 5 to 3600 seconds. Default: 1800. Covers voice selection, sample download, synthesis, transcoding, and audio persistence.

**long_text** LongText `Optional`

Long\-text segmentation parameters.

**enable** boolean `Optional` `Example value: true`

Whether to segment long text automatically. Default: `true`.

**target_segment_chars** integer `Optional` `Example value: 1000`

Target segment length and automatic segmentation threshold, from 100 to 2000. Default: 1000.

**max_segment_chars** integer `Optional` `Example value: 1000`

Maximum characters per segment, from 100 to 2000. Default: 1000. Must not be less than `target_segment_chars`.

**output_object_storage_dir** string `Optional` `Example value: tos://example-bucket/tts-output/`

Audio output directory. Supports only `tos://` paths. If omitted, a downloadable audio URL is returned after successful completion in `audio_uri` or `service` mode.

**callback** object `Optional` `Example value: {"url":"https://example.com/callback"}`

Optional terminal callback configuration. The callback address is `callback.url`; omit it to retrieve the result through Poll.

**pending_timeout_minutes** integer `Optional` `Example value: 60`

Maximum time a task may remain in PENDING, from 30 to 4320 minutes. The task becomes `EXPIRED` after the timeout.

`data` and its nested objects accept only the fields documented here. An incorrect field name or type returns `Parameter.Invalid`.

The text supports pauses in the forms `<break time="500ms"/>` and `<break time="2s"/>`; each pause is capped at 30000 milliseconds. The `<break>` tag is not spoken. Full SSML and other tags such as `<speak>`, `<prosody>`, and `<emphasis>` are not supported.

`pcm` output is a raw mono `s16le` stream without a WAV header and must be decoded with `sample_rate`. `bit_rate` has no effect on `wav` / `pcm`.

Reference and prompt audio must currently be readable WAV files no larger than 50 MB and between 0.1 and 300 seconds long. For production, a clear, low\-noise, single\-speaker recording of about 5 to 15 seconds is recommended. Inaccessible, damaged, or non\-compliant audio returns `Tts.ReferenceAudioInvalid`.

The synthesis mode is determined by the parameter combination:

|Synthesis mode |Parameter combination |
|---|---|
|Voice Design |`style_prompt` |
|Controlled Voice Cloning |`reference_audio_uri` |
|Material Library Voice Cloning |`material_scope.voice`, optionally with `style_prompt`; do not provide `reference_audio_uri` or `prompt_audio_uri` |
|High\-fidelity Continuation |`prompt_audio_uri` + `prompt_text`, without `style_prompt` |

### Response parameters

**metadata** Metadata

Request metadata.

**task_id** string `Example value: ffb57ea6450c894f354c`

Asynchronous task ID used by the Poll API.

**task_status** string `Example value: PENDING`

Task status. A successful submission usually returns `PENDING`.

**business_code** string `Example value: 0`

Business code. `0` indicates success.

**error_msg** string

Error message. Empty on success.

**request_id** string `Example value: 9fed0e5f0659b128bad47e971aed3c81`

Request ID.

### Examples

#### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_voice_forge",
    "operator_version": "v1",
    "data": {
        "req_params": {
            "text": "Welcome to the voice cloning operator. This is a text-to-speech example.",
            "audio_params": {
                "format": "wav",
                "sample_rate": 48000
            }
        },
        "engine_params": {
            "style_prompt": "Calm and professional male voice, moderate speed"
        },
        "service_params": {
            "response_mode": "audio_uri"
        }
    },
    "pending_timeout_minutes": 60
}'
```

Select a specific Material Library voice. Omit `revision` to use and lock the latest available revision selected for this request:

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_voice_forge",
    "operator_version": "v1",
    "data": {
        "req_params": {"text": "Welcome to our product introduction."},
        "material_scope": {
            "voice": {
                "mode": "EXACT",
                "material_ids": ["mat-voice-example"]
            }
        }
    }
}'
```

Let the operator infer Material Library voice preferences from the text and style:

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_voice_forge",
    "operator_version": "v1",
    "data": {
        "req_params": {"text": "Welcome to our product introduction."},
        "engine_params": {"style_prompt": "Warm, clear, and reassuring delivery"},
        "material_scope": {
            "voice": {"mode": "AUTO", "infer_filters": true}
        }
    }
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "ffb57ea6450c894f354c",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Incorrect field type, enum, numeric range, or parameter dependency, including an invalid `material_scope.voice` selection or conflicting audio sources. |
|400 |Operator.InvalidId |The operator id is invalid. |Incorrect or unavailable `operator_id`. |
|400 |Operator.InvalidVersion |The operator version is invalid. |Incorrect `operator_version`. |
|400 |Tts.InvalidText |The synthesis text is empty after cleaning. |The text is empty or becomes empty after processing. |
|400 |Tts.TextTooLong |The synthesis text exceeds the maximum length. |The text exceeds the allowed length. |
|400 |Tts.TooManySegments |The synthesis text has too many segments. |Long\-text segmentation produces too many segments. |
|400 |Tts.ReferenceAudioInvalid |The reference audio is invalid. |The reference or prompt audio URI, format, or content does not meet the requirements. |
|400 |Tts.ReferenceAudioRequired |Reference audio is required. |The selected synthesis mode requires reference audio. |
|400 |Tts.InvalidRequest |The TTS request is invalid. |Invalid parameter combination, such as `prompt_audio_uri` and `prompt_text` not provided as a pair. |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication information. |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API Key. |
|429 |Server.Busy |Server is Busy, please try again later. |Server busy or rate limited. |
|500 |Tts.InternalError |TTS Internal Error |Speech synthesis service error. |
|500 |Tts.AudioSaveFailed |Failed to transcode or persist the audio. |Failed to transcode or persist audio. |
|500 |Tts.EngineLoadFailed |The synthesis engine failed to load. |The synthesis service is temporarily unavailable. |
|500 |Tts.EngineGpuOom |The synthesis engine ran out of GPU memory. |Insufficient synthesis resources. |
|500 |Tts.RequestTimeout |The synthesis request timed out. |Synthesis task timed out. |

## Poll

### Interface description

Query the status and result of a `las_voice_forge` Voice Cloning Synthesis task by task ID. A completed task returns the audio, character count, format, sample rate, duration, and other result information. If voice\-material selection or access fails after submission, the task returns `FAILED`; inspect `metadata.business_code` and `metadata.error_msg`.

### Request parameters

**operator_id** string 必选 `Example value: las_voice_forge`

Operator ID, fixed to `las_voice_forge`.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed to `v1`.

**task_id** string 必选 `Example value: ffb57ea6450c894f354c`

Asynchronous task ID returned by the Submit API.

### Response parameters

**metadata** Metadata

Request metadata and task status.

**task_id** string `Example value: ffb57ea6450c894f354c`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Task status: `PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, `EXPIRED`, or `CANCELLED`.

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time in ISO 8601 format.

**end_time** string `Example value: 2026-07-21T16:04:09+08:00`

Task end time in ISO 8601 format. It may be empty before the task reaches a terminal state.

**business_code** string `Example value: 0`

Business code. `0` indicates success; a non\-zero value identifies an error. For a failed material\-selection task, this may be `NotFound.Material` or `Material.Unavailable`; use `error_msg` for details.

**error_msg** string

Error or status message. Empty on success.

**request_id** string `Example value: 9fed0e5f0659b128bad47e971aed3c81`

Request ID.

**data** VoiceForgeUserResp

Speech synthesis result returned after task completion.

**data** string

Base64 audio, which may be returned in `base64` / `service` mode.

**audio_uri** string `Example value: https://example-bucket.tos-ap-southeast-1.bytepluses.com/voice_forge/demo.wav`

Audio access location returned in `audio_uri` / `service` mode as a TOS presigned HTTPS URL valid for 3 days.

**audio_format** string `Example value: wav`

Actual output audio format.

**sample_rate** integer `Example value: 48000`

Actual output sample rate in Hz.

**duration_sec** double `Example value: 3.04`

Output audio duration in seconds. This is result metadata and is not used for billing.

**text_chars** integer `Example value: 38`

Number of Unicode characters in the original `req_params.text`; this is the Voice Forge usage and billing metric.

**segment_count** integer `Example value: 1`

Number of text segments. Single\-segment synthesis returns 1.

**reference_audio_used** boolean `Example value: true`

Whether a voice reference was used for this synthesis, including a sample selected through `material_scope.voice`.

### Examples

#### Request example

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_voice_forge",
    "operator_version": "v1",
    "task_id": "ffb57ea6450c894f354c"
}'
```

#### Response example

```json
{
  "metadata": {
    "task_id": "ffb57ea6450c894f354c",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:09+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "data": "",
    "audio_uri": "https://example-bucket.tos-ap-southeast-1.bytepluses.com/voice_forge/tts/demo.wav?X-Tos-Signature=...",
    "audio_format": "wav",
    "sample_rate": 48000,
    "duration_sec": 3.04,
    "text_chars": 38,
    "segment_count": 1,
    "reference_audio_used": true
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |TaskId.Invalid |The task id is invalid. |The task ID is empty, does not exist, or is not accessible. |
|400 |Parameter.Invalid |The parameter is invalid. |Parameter validation or task\-result parsing failed. |
|400 |Tts.InvalidText |The synthesis text is empty after cleaning. |The text is empty or becomes empty after processing. |
|400 |Tts.TextTooLong |The synthesis text exceeds the maximum length. |The text exceeds the allowed length. |
|400 |Tts.TooManySegments |The synthesis text has too many segments. |Long\-text segmentation produces too many segments. |
|400 |Tts.InvalidRequest |The TTS request is invalid. |Invalid request parameter combination. |
|400 |Tts.ReferenceAudioInvalid |The reference audio is invalid. |The reference or prompt audio does not meet the requirements. |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication information. |
|401 |ApiKey.Invalid |The api key is invalid. |Invalid API Key. |
|429 |Server.Busy |Server is Busy, please try again later. |Server busy or rate limited. |
|500 |Server.InternalError |General Internal Error |Internal server error. |
|500 |Tts.InternalError |TTS Internal Error |Speech synthesis service error. |
|500 |Tts.AudioSaveFailed |Failed to transcode or persist the audio. |Failed to transcode or persist audio. |
|500 |Tts.EngineLoadFailed |The synthesis engine failed to load. |The synthesis service is temporarily unavailable. |
|500 |Tts.EngineGpuOom |The synthesis engine ran out of GPU memory. |Insufficient synthesis resources. |
|500 |Tts.RequestTimeout |The synthesis request timed out. |Synthesis task timed out. |
