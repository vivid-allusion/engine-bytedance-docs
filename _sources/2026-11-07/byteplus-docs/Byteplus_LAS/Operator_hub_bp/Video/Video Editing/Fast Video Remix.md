---
title: "Fast Video Remix"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/fast-video-remix"
---

Combine video materials by act order into multiple short videos for product showcases, marketing campaigns, and promotions that require different visual versions of a defined content structure. You can manually arrange acts such as “attract attention → show benefits → call to action”, or use automatic or random act planning. Original visual\-source audio is discarded. Output can be silent or use synthesized/existing narration, with regular subtitles when a script is provided.

# Operator introduction

> Operator ID: `las_video_fast_remix`

## Applicable scenarios

|Scenario |Description |
|---|---|
|Product showcase |Generate multiple versions based on a fixed structure such as opening, selling points, and call to action. |
|Marketing campaign |Automatically or randomly combine visuals to quickly generate different editing plans. |
|Promotion |Use a script, TTS, or existing narration to generate short videos with subtitles. |

## Core capabilities

* **Three act\-planning modes**: Supports 2–10 manually defined acts, automatic act planning based on visual understanding, and random act planning without material understanding.

* **Audio and subtitles**: Discards original visual\-source audio and supports silent output, TTS narration, or one existing narration track. A script produces sentence\-level subtitles.

* **Multiple deliverables**: Generates up to 1,000 videos per task and delivers subtitled/clean videos, SRT, segment videos, editing plans, and complete result JSON.

* **Output specifications**: Supports target resolution, frame rate, and strict validation. When a nonblank script is provided, the operator generates sentence\-level subtitles using its built\-in style.

## Effect demonstrations

---

**[Input videos]**

* Input video 1

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d4eb54be82184dd2adf9efb19434c522~tplv-goo7wpa0wc-image.image)

* Input video 2

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8eba36d7f464a559dffa8804761ca51~tplv-goo7wpa0wc-image.image)

* Input video 3

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9645a38d86f419786f5e51b2e296bbf~tplv-goo7wpa0wc-image.image)

* Input video 4

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ba6059832c894054bc70f9d252a5d681~tplv-goo7wpa0wc-image.image)

* Input video 5

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f73a6a70478f45afb816909907e68981~tplv-goo7wpa0wc-image.image)

* Input video 6

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ea3dc53faf0f4757ac04982d217392ff~tplv-goo7wpa0wc-image.image)

* Input video 7

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ec68da48a94f48c58be63cc4da19b331~tplv-goo7wpa0wc-image.image)

* Input video 8

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/294a7b35a4d541ed8d9669f3a314a834~tplv-goo7wpa0wc-image.image)

---

**[Output videos]**

* Output example 1: Automatic act planning + silent output

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/406fab7bc3b345c0b5bb7782eb3919cd~tplv-goo7wpa0wc-image.image)

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38c9d74a142e462f8ae44c49b3a57464~tplv-goo7wpa0wc-image.image)

* Output example 2: Automatic act planning + TTS narration

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5f615cffeaf849949302e49bdf55ddc1~tplv-goo7wpa0wc-image.image)

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8645df9554c94f08a8e150640deb2acd~tplv-goo7wpa0wc-image.image)

---

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Sub\-item |Limit or description |
|---|---|
|Duration |Depends on the number and total duration of materials, act\-planning mode, output count, TTS, and target specifications. Automatic act planning adds visual\-understanding time. |

# Input and output requirements

## Input requirements

|Sub\-item |Detailed requirements |
|---|---|
|Supported data modalities |* Video<br><br>* Audio (existing narration)<br><br>* Text (script and act requirements)<br><br><br>Images, industry templates, BGM, sound effects, decorative captions, and covers are not supported. |
|Input modality: Video |* Formats: mp4, mov, m4v, webm, mkv, and avi.<br><br>* Quantity and size:<br><br>   * Up to 30 videos in total, each no longer than 10 minutes.<br><br>   * In automatic mode, each visual\-source video must be longer than 1 second.<br><br>   * Each manual/automatic act must be at least 1.2 seconds; each random shot must be at least 1 second. |
|Input modality: Audio |* Formats: mp3, wav, m4a, aac, flac, and ogg.<br><br>* Quantity: At most one existing narration track.<br><br>* Other requirements: Mutually exclusive with TTS and requires `script`. |
|Input modality: Text |* `script` supports up to 4,000 characters and is mutually exclusive with `target_duration_sec`, which supports 10–60 seconds.<br><br>* Each act `requirement` supports up to 200 characters. |
|Input path |* Public URL: Use an HTTP/HTTPS direct file URL accessible by LAS. Directories are not accepted. Signed URLs must remain valid throughout queuing and processing.<br><br>* TOS path: Use a concrete file address in `tos://bucket/key` format. The TOS bucket must belong to the same primary account and Asia Pacific (Johor) region as LAS, and LAS must have read permission for the object. |

## Output requirements

|Sub\-item |Detailed requirements |
|---|---|
|Supported data modalities |* Video<br><br>* Text (SRT, editing plans, and result JSON) |
|Output modality: Video |* Returns up to the requested `max_clips` value, from 1 to 1,000; actual successful output can be lower. Deliverables can include subtitled videos, clean videos, and segment videos.<br><br>* The default target is 1080×1920 at 60 FPS in non\-strict mode. |
|Output modality: Text |* Returns subtitle SRT, editing\-plan JSON, and complete result JSON. Actual artifacts are determined by Poll `data.artifacts`.<br><br>* Act count: 2–10 for manual/automatic mode; random mode generates 1–10 acts from the materials. |
|Output path |* TOS path:<br><br>   * Use `output_tos_path` to specify an output directory in `tos://bucket/prefix` format.<br><br>   * The TOS bucket must belong to the same primary account and Asia Pacific (Johor) region as LAS, and LAS must have write permission for the target directory.<br><br>* If `output_tos_path` is omitted, LAS assigns an output location.<br><br><br>Final TOS paths and temporary access URLs are returned in Poll `data.artifacts`. |

# Billing instructions

* Billing standards

   |Sub\-item |Billing description |
   |---|---|
   |Billing items |The following billing items apply:<br><br><br>* **Remix output fee**: Billed by the total actual duration of all successfully generated videos. Subtitled and clean versions of the same video are counted once.<br><br>* **Automatic act\-planning fee**: When `enable_auto_chaptering=true`, billed by the original duration of all visual\-source materials, counting each source once.<br><br>* **Narration (TTS) fee**: Billed by the number of characters actually synthesized. No fee is incurred when narration is not synthesized.<br><br><br>The total task fee is the sum of the preceding billing items. |
   |Billing type |Usage\-based billing. Duration is recorded in milliseconds and prorated without rounding up to a whole minute. Only successful tasks with `task_status=COMPLETED` and `business_code="0"` are billed. |
   |Unit price |Unit prices vary by billing item, as listed below. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Remix output |0.1 USD/minute |
   |Automatic act planning |0.1 USD/minute |
   |Narration (TTS) |0.075 USD/1,000 characters |

# Caution and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, understand the model invocation costs. For details, see [Large model invocation billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Generate an API Key for operator invocation and configure it as an environment variable. For details, see [Obtain and configure the API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|Base URL |The Base URL for Asia Pacific (Johor), `ap-southeast-1`, is `https://operator.las.ap-southeast-1.bytepluses.com`. For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |

# REST API calls

## API usage instructions

* This operator uses asynchronous task APIs. Call Submit to obtain a `task_id`, then call Poll with that `task_id` to query task status and retrieve results.

* A `task_id` remains valid for 3 days. After that, it can no longer be used to retrieve results.

## Submit

### Request parameters

**operator_id** string 必选 `Example value: las_video_fast_remix`

Always las_video_fast_remix.

**operator_version** string 必选 `Example value: v1`

Always v1.

**data** FastRemixReqParams 必选

Business configuration for this operator.

**acts** list of FastRemixAct `Conditionally required`

Manual candidate pools, 2–10 acts in playback order. Omitted/null selects automatic or random mode via enable_auto_chaptering.

**video_urls** list of string 必选

At least one concrete video for this act. At most 30 entries across all acts; mp4, mov, m4v, webm, mkv and avi, up to 10 minutes each.

**requirement** string `Optional`

Visual localization requirement, up to 200 characters. First/last acts default to opening/CTA localization; middle acts without a requirement are not localized.

**duration_sec** float `Optional` `Example value: 6`

Fixed act duration, at least 1.2 seconds; omitted acts share remaining time. Fixed durations must fit the timeline and leave at least 1.2 seconds for each other act.

**enable_auto_chaptering** boolean `Optional` `Example value: false`

Default false. Without acts, false selects random planning and true selects AI planning from visual understanding. true cannot be combined with acts.

**video_urls** list of MaterialItem `Conditionally required`

Without acts, at least one picture source, up to 30, as strings or MaterialItem objects. For automatic acts, each picture\-source video must be longer than 1 second. With manual acts, pictures belong in acts and this array accepts only one voiceover.

**url** string 必选 `Example value: tos://your-bucket/product.mp4`

Concrete video path; voiceover also accepts mp3, wav, m4a, aac, flac and ogg audio.

**role** string `Optional` `Example value: broll`

Default speech. speech: visuals only; broll: visuals only; voiceover: audio only, at most one and requires script.

**script** string `Conditionally required`

Finished\-video copy, up to 4000 characters; mutually exclusive with target_duration_sec, not a storyboard array. Nonblank copy produces sentence subtitles.

**target_duration_sec** integer `Conditionally required` `Example value: 30`

Required without copy, [10, 60] seconds; omit when copy is provided.

**max_clips** integer `Optional` `Example value: 5`

Rendered video count limit, [1, 1000], default 5; actual successful count may be lower.

**tts** TtsParams `Optional`

TTS is disabled when omitted; enable with script, mutually exclusive with voiceover.

**enable** boolean `Optional` `Example value: true`

Default false. true synthesizes narration from script; false does not. Requires script.

**language** string `Optional` `Example value: en`

Narration language, inferred from copy when omitted. Supports zh Chinese, en English, id Indonesian, ar Arabic, es Spanish, ja Japanese and ko Korean. Invalid or unrecognized languages produce a parameter error.

**voice** string `Optional`

TTS speaker ID, selected by language when omitted. Must support the target language and requested emotion.

**speed** float `Optional` `Example value: 1.25`

Narration speed multiplier, default 1.25; explicit speech_rate takes priority.

**speech_rate** integer `Optional` `Example value: 0`

Native speech\-rate setting, [\-50, 100]: \-50 is 0.5×, 0 is 1×, 100 is 2×. Derived from speed when omitted.

**loudness_rate** float `Optional` `Example value: 0`

Source synthesis loudness setting, [\-50, 100]; omission uses the TTS service default. This is not final video loudness.

**emotion** string `Optional`

Speaker emotion; omission uses the speaker default. Supported values depend on the speaker.

**emotion_scale** float `Optional` `Example value: 3`

Emotion intensity, [1, 5], applicable when the speaker supports emotion; omission follows the TTS service default.

**video_spec** VideoSpecParams `Optional`

Default target is 1080×1920 at 60 fps, non\-strict; lower\-quality sources reduce delivery specifications as described below.

**width** integer `Optional` `Example value: 1080`

Target width in pixels, [64, 7680], default 1080; provide together with height.

**height** integer `Optional` `Example value: 1920`

Target height in pixels, [64, 7680], default 1920; provide together with width.

**fps** integer `Optional` `Example value: 60`

Target frame rate in frames/second, [1, 240], default 60.

**strict** boolean `Optional` `Example value: false`

Default false: reduce delivery specifications as needed, without upsampling. true rejects any source requiring upsampling or with insufficient frame rate. Scaling down a landscape source and adding padding is not upsampling.

**output_tos_path** string `Optional` `Example value: tos://your-bucket/fast-remix/results/`

Writable TOS output directory; omitted uses the platform default.

### Response parameters

**metadata** Metadata

Task acceptance result. Videos are obtained by polling, not from this response.

**task_id** string `Example value: task-example`

Asynchronous task ID; use this value for subsequent Poll requests.

**task_status** string `Example value: PENDING`

Task state: keep polling for `PENDING` (queued) or `RUNNING` (processing). `COMPLETED` means execution finished; check business_code for success. `FAILED`, `TIMEOUT`, `EXPIRED` and `CANCELLED` are terminal failure, timeout, expiry and cancellation states.

**business_code** string `Example value: 0`

Business result code. The string "0" indicates success; inspect task_status and error_msg on failure.

**error_msg** string

Error details, empty on success; use them to diagnose execution failures.

### Examples

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{"operator_id":"las_video_fast_remix","operator_version":"v1","data":{"video_urls":["tos://your-bucket/a.mp4","tos://your-bucket/b.mp4"],"target_duration_sec":30,"max_clips":3,"output_tos_path":"tos://your-bucket/results/"}}'
```

Detailed request example:

```json
{
  "operator_version": "v1",
  "data": {
    "acts": [
      {
        "video_urls": [
          "tos://example-bucket/opening-a.mp4",
          "tos://example-bucket/opening-b.mp4"
        ],
        "requirement": "Use a product-results comparison to attract attention"
      },
      {
        "video_urls": [
          "tos://example-bucket/demo-a.mp4",
          "tos://example-bucket/demo-b.mp4"
        ],
        "requirement": "Show how the product is used"
      },
      {
        "video_urls": [
          "tos://example-bucket/cta.mp4"
        ],
        "requirement": "Show the promotion and purchase entry point"
      }
    ],
    "script": "Daily cleaning takes too much effort. This product makes it easier. Order now to enjoy the promotion.",
    "max_clips": 3,
    "tts": {
      "enable": true,
      "language": "zh",
      "speed": 1.0
    },
    "video_spec": {
      "width": 1080,
      "height": 1920,
      "fps": 30,
      "strict": false
    },
    "output_tos_path": "tos://example-bucket/remix-results/campaign-001/"
  },
  "operator_id": "las_video_fast_remix"
}
```

Automatic act\-planning request example:

```json
{
  "operator_id": "las_video_fast_remix",
  "operator_version": "v1",
  "data": {
    "video_urls": ["tos://example-bucket/product-demo.mp4", "tos://example-bucket/product-details.mp4"],
    "enable_auto_chaptering": true,
    "target_duration_sec": 30,
    "max_clips": 2
  }
}
```

Successful Submit response example:

```json
{
  "metadata": {
    "task_id": "task-example",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameter types, enums, ranges, or combinations. |
|401 |Authorization.Missing |Missing Authorization. |Authorization information is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|500 |Server.InternalError |General Internal Error |An internal service error occurred. |

The table lists request errors. After a task is accepted, determine execution failures from Poll `metadata.task_status`, `business_code`, and `error_msg`.

## Poll

### Request parameters

**operator_id** string 必选 `Example value: las_video_fast_remix`

Fixed operator ID.

**operator_version** string 必选 `Example value: v1`

Always v1.

**task_id** string 必选 `Example value: task-example`

Task ID from Submit; query using the same caller identity.

### Response parameters

**metadata** Metadata

Task state and error details.

**task_id** string `Example value: task-example`

Asynchronous task ID; use this value for subsequent Poll requests.

**task_status** string `Example value: COMPLETED`

Task state: keep polling for `PENDING` (queued) or `RUNNING` (processing). `COMPLETED` means execution finished; check business_code for success. `FAILED`, `TIMEOUT`, `EXPIRED` and `CANCELLED` are terminal failure, timeout, expiry and cancellation states.

**business_code** string `Example value: 0`

Business result code. The string "0" indicates success; inspect task_status and error_msg on failure.

**error_msg** string

Error details, empty on success; use them to diagnose execution failures.

**submit_time** string

Submission time in ISO 8601 format.

**end_time** string

End time in ISO 8601 format; may be empty before termination.

**data** FastRemixResponse

Read only on successful completion, not while pending or failed.

**clazz** string `Example value: las_video_fast_remix`

Always las_video_fast_remix.

**act_mode** string `Optional` `Example value: random`

random: default random acts; auto: AI acts with enable_auto_chaptering=true. Absent for manual acts.

**audio_source** string `Example value: silent`

silent, tts or voiceover; silent output with script still includes subtitles.

**acts** list of object

Global acts for manual/AI modes; empty for random mode, where acts are returned per variant.

**materials** list of object

Usable picture sources. Random mode uses act=0; inspect each variant’s acts[].video_ids for grouping.

**narration** Narration

Script and per\-video planned timeline; without script, line_count=0 and lines=[].

**line_count** integer `Example value: 0`

Copy sentence count; 0 without script.

**duration_sec** float `Example value: 15`

Planned duration per output in seconds, shared by variants.

**lines** list of string

Copy sentences in narration order; empty without script.

**requested_outputs** integer `Example value: 1`

Effective max_clips, the maximum number of successful renders.

**variant_count** integer `Example value: 1`

Planned scheme count, equal to plan.variants length; may exceed rendered count.

**output_count** integer `Example value: 1`

Successfully delivered video count, for checking delivery quantity.

**duration_sec** float `Example value: 15`

Total actual duration of successful videos, in seconds; output charges prorate this value to minutes, counting clean/subtitled versions of one video once.

**outputs** list of FastRemixOutput

Delivered videos with durations, picture order, acts, subtitles, schemes and file addresses.

**variant_id** string `Example value: v01`

Variant identifier; do not infer rendering order from it.

**batch_index** integer `Example value: 1`

One\-based index after shuffling; identifies this variant’s artifact directory.

**order** list of FastRemixShot

Ordered shots with source references and per\-shot durations.

**video_id** string

Source identifier for this shot.

**name** string `Example value: product.mp4`

Source filename.

**act** integer `Example value: 1`

Act index containing this shot.

**slot** string `Example value: opening`

Narrative slot: opening, content or ending.

**duration_sec** float `Example value: 5`

Shot duration in the output, in seconds.

**acts** list of FastRemixActDuration

Act indices and durations for this variant, plus source pools in random mode.

**act** integer `Example value: 1`

One\-based act index.

**duration_sec** float `Example value: 5`

Duration allocated to this act in this variant, in seconds.

**video_ids** list of string `Optional`

Candidate source identifiers for this act, returned only in random mode; may differ between variants.

**planned_duration_sec** float `Example value: 15`

Planned duration of one output in seconds, determined by narration.duration_sec.

**duration_sec** float `Example value: 15`

Actual duration of this delivered video in seconds.

**subtitle_srt** string

SRT text for this output; empty without script.

**match_scheme** object

Full scheme object for this output, corresponding to artifacts.match_scheme_\* files.

**artifacts** Artifacts

Paths for this variant’s video, SRT and scheme; unrendered plans have only match_scheme_\*.

**result_json_tos_path** string

TOS path to the complete result JSON for saving the successful task result.

**result_json_url** string

Temporary result\-JSON download URL.

**video_subtitled_tos_path** string

Subtitled video TOS path; may be empty when no subtitles exist or generation did not succeed.

**video_subtitled_url** string

Temporary subtitled video URL; fall back to video_clean_url if empty.

**video_clean_tos_path** string

TOS path to video without the new subtitle layer, including selected audio.

**video_clean_url** string

Temporary clean\-video download URL.

**subtitle_srt_tos_path** string

TOS path to separate SRT, returned when subtitles exist. Timestamps start at the beginning of this delivered video.

**subtitle_srt_url** string

Temporary SRT URL; null or absent without subtitles.

**match_scheme_tos_path** string

TOS path to the JSON editing scheme; retain for later repackaging.

**match_scheme_url** string

Temporary scheme\-JSON download URL.

**video_clip_tos_paths** list of string

Segment video TOS paths.

**video_clip_urls** list of string

Segment video URLs.

**plan** FastRemixPlan

All planned variants, including rendered, unrendered and individually failed plans.

**variants** list of FastRemixVariant

Variant plans, with length equal to variant_count.

**variant_id** string `Example value: v01`

Variant identifier; do not infer rendering order from it.

**batch_index** integer `Example value: 1`

One\-based index after shuffling; identifies this variant’s artifact directory.

**order** list of FastRemixShot

Ordered shots with source references and per\-shot durations.

**video_id** string

Source identifier for this shot.

**name** string `Example value: product.mp4`

Source filename.

**act** integer `Example value: 1`

Act index containing this shot.

**slot** string `Example value: opening`

Narrative slot: opening, content or ending.

**duration_sec** float `Example value: 5`

Shot duration in the output, in seconds.

**acts** list of FastRemixActDuration

Act indices and durations for this variant, plus source pools in random mode.

**act** integer `Example value: 1`

One\-based act index.

**duration_sec** float `Example value: 5`

Duration allocated to this act in this variant, in seconds.

**video_ids** list of string

Candidate source identifiers for this act, returned only in random mode; may differ between variants.

**planned_duration_sec** float `Example value: 15`

Planned duration of one output in seconds, determined by narration.duration_sec.

**rendered** boolean `Example value: false`

true means a successful render with a matching variant_id in outputs; false means unrendered or failed.

**artifacts** Artifacts

Paths for this variant’s video, SRT and scheme; unrendered plans have only match_scheme_\*.

**result_json_tos_path** string

TOS path to the complete result JSON for saving the successful task result.

**result_json_url** string

Temporary result\-JSON download URL.

**video_subtitled_tos_path** string

Subtitled video TOS path; may be empty when no subtitles exist or generation did not succeed.

**video_subtitled_url** string

Temporary subtitled video URL; fall back to video_clean_url if empty.

**video_clean_tos_path** string

TOS path to video without the new subtitle layer, including selected audio.

**video_clean_url** string

Temporary clean\-video download URL.

**subtitle_srt_tos_path** string

TOS path to separate SRT, returned when subtitles exist. Timestamps start at the beginning of this delivered video.

**subtitle_srt_url** string

Temporary SRT URL; null or absent without subtitles.

**match_scheme_tos_path** string

TOS path to the JSON editing scheme; retain for later repackaging.

**match_scheme_url** string

Temporary scheme\-JSON download URL.

**video_clip_tos_paths** list of string

Segment video TOS paths.

**video_clip_urls** list of string

Segment video URLs.

**failed_variants** list of VariantFailure `Optional`

Returned when individual variants fail rendering; absent when none fail.

**variant_id** string `Example value: v01`

Failed variant ID.

**reason** string

Failure summary identifying the affected variant; other outputs may still be delivered.

**skipped_materials** list of SkippedMaterial `Optional`

Returned for skipped sources, such as unrecognized durations or sources shorter than 1 second in random mode.

**video_id** string

Identifier of the skipped source.

**reason** string

Skip reason; resubmit with readable sources meeting duration requirements.

**usage** FastRemixUsage

Executed usage. Some fields are shared diagnostics; billing dimensions are defined in specifications.

**version** string `Example value: v1`

Usage schema version.

**input_duration_ms** integer `Example value: 0`

Billing field: original picture\-input duration in milliseconds for automatic acts, counting each source once and excluding voiceover; 0 in manual/random modes.

**material_duration_ms** integer `Example value: 0`

Material\-understanding duration in milliseconds; reference only, no separate charge.

**director_output_duration_ms** integer `Example value: 15000`

Total successful output duration statistic in milliseconds; output charges use top\-level data.duration_sec, without charging this field again.

**tts_chars** integer `Example value: 0`

Billing field: actually synthesized narration characters; 0 for existing narration or silent output.

**subtitle_chars** integer `Example value: 0`

Cumulative rendered subtitle characters; no separate charge.

**effect_chars** integer `Example value: 0`

Effect\-text characters; this API does not provide decorative\-caption packaging.

**artifacts** Artifacts

Task\-level complete result\-JSON paths.

**result_json_tos_path** string

TOS path to the complete result JSON for saving the successful task result.

**result_json_url** string

Temporary result\-JSON download URL.

**video_subtitled_tos_path** string

Subtitled video TOS path; may be empty when no subtitles exist or generation did not succeed.

**video_subtitled_url** string

Temporary subtitled video URL; fall back to video_clean_url if empty.

**video_clean_tos_path** string

TOS path to video without the new subtitle layer, including selected audio.

**video_clean_url** string

Temporary clean\-video download URL.

**subtitle_srt_tos_path** string

TOS path to separate SRT, returned when subtitles exist. Timestamps start at the beginning of this delivered video.

**subtitle_srt_url** string

Temporary SRT URL; null or absent without subtitles.

**match_scheme_tos_path** string

TOS path to the JSON editing scheme; retain for later repackaging.

**match_scheme_url** string

Temporary scheme\-JSON download URL.

**video_clip_tos_paths** list of string

Segment video TOS paths.

**video_clip_urls** list of string

Segment video URLs.

### Examples

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{"operator_id":"las_video_fast_remix","operator_version":"v1","task_id":"task-example"}'
```

```json
{
  "metadata": {
    "task_id": "task-example",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "clazz": "las_video_fast_remix",
    "act_mode": "random",
    "audio_source": "silent",
    "acts": [],
    "narration": {
      "line_count": 0,
      "duration_sec": 15.0,
      "lines": []
    },
    "requested_outputs": 1,
    "variant_count": 1,
    "output_count": 1,
    "duration_sec": 15.0,
    "outputs": [
      {
        "variant_id": "v01",
        "batch_index": 1,
        "order": [
          {
            "video_id": "tos://your-bucket/product.mp4",
            "name": "product.mp4",
            "act": 1,
            "slot": "opening",
            "duration_sec": 15.0
          }
        ],
        "acts": [
          {
            "act": 1,
            "duration_sec": 15.0,
            "video_ids": [
              "tos://your-bucket/product.mp4"
            ]
          }
        ],
        "planned_duration_sec": 15.0,
        "artifacts": {
          "video_clean_tos_path": "tos://your-bucket/fast-remix/results/batch_001/clean.mp4",
          "video_clean_url": "https://example.com/clean.mp4",
          "match_scheme_tos_path": "tos://your-bucket/fast-remix/results/batch_001/match_scheme.json"
        },
        "duration_sec": 15.0,
        "subtitle_srt": ""
      }
    ],
    "plan": {
      "variants": [
        {
          "variant_id": "v01",
          "batch_index": 1,
          "order": [
            {
              "video_id": "tos://your-bucket/product.mp4",
              "name": "product.mp4",
              "act": 1,
              "slot": "opening",
              "duration_sec": 15.0
            }
          ],
          "acts": [
            {
              "act": 1,
              "duration_sec": 15.0,
              "video_ids": [
                "tos://your-bucket/product.mp4"
              ]
            }
          ],
          "planned_duration_sec": 15.0,
          "rendered": true,
          "artifacts": {
            "video_clean_tos_path": "tos://your-bucket/fast-remix/results/batch_001/clean.mp4",
            "video_clean_url": "https://example.com/clean.mp4",
            "match_scheme_tos_path": "tos://your-bucket/fast-remix/results/batch_001/match_scheme.json"
          }
        }
      ]
    },
    "artifacts": {
      "result_json_tos_path": "tos://your-bucket/fast-remix/results/result.json"
    },
    "usage": {
      "version": "v1",
      "input_duration_ms": 0,
      "material_duration_ms": 0,
      "director_output_duration_ms": 15000,
      "tts_chars": 0,
      "subtitle_chars": 0,
      "effect_chars": 0
    }
  }
}
```

### Error codes

|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameter types, enums, ranges, or combinations. |
|400 |Task.NotFound |Task not found |The task does not exist, has expired, or is not visible to the caller. |
|401 |Authorization.Missing |Missing Authorization. |Authorization information is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|500 |Server.InternalError |General Internal Error |An internal service error occurred. |

The table lists request errors. After a task is accepted, determine execution failures from Poll `metadata.task_status`, `business_code`, and `error_msg`.
