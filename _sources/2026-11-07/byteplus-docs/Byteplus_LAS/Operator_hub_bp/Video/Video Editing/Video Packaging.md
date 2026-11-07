---
title: "Video Packaging"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/video-packaging"
---

The Video Packaging operator adds subtitles, emphasis, music, and visual packaging to edited portrait videos and delivers a complete video, a clean version, SRT, and a packaging plan.

# Operator introduction

> Operator ID: `las_video_packaging`

## Applicable scenarios

|Scenario |Description |
|---|---|
|Product presentation |Recognize or import subtitles and add keyword highlights, information cards, BGM, and sound effects. |
|Marketing material |Apply a consistent packaging style, transitions, and pacing to multiple portrait videos. |
|Life\-service and documentary content |Preserve original audio and automatically plan subtitle effects, BGM, and visual elements. |

## Core capabilities

* **Multiple subtitle sources**: Uses ASR, an external SRT file, or a transcript to correct recognized text for each video.

* **Content emphasis**: Supports regular subtitles, decorative captions, keyword highlights, and information cards, with independent subtitle and card styles.

* **Visual and audio packaging**: Supports transitions, 1–2× playback speed, BGM, and sound effects while preserving original video audio.

* **Asset constraints**: Supports candidate pools for sound effects, BGM, fonts, subtitle effects, and transitions, as well as user\-provided TOS music.

## Supported regions

* Asia Pacific (Johor): `ap-southeast-1`

## Operator performance

|Sub\-item |Limit or description |
|---|---|
|Duration |Depends on total input duration, material count, subtitle source, visual understanding, enabled packaging items, and target specifications. |

# Input and output requirements

## Input requirements

|Sub\-item |Detailed requirements |
|---|---|
|Supported data modalities |* Video<br><br>* Text (SRT, transcript, and packaging instructions)<br><br>* Audio (user\-provided BGM) |
|Input modality: Video |* Formats: mp4, mov, m4v, webm, mkv, and avi.<br><br>* Quantity and size: 1–20 portrait videos whose height exceeds width; each at least 1 second, with a total original duration no longer than 30 minutes. |
|Input modality: Text |* SRT:<br><br>   * Each video accepts one local\-timeline SRT file, mutually exclusive with `script`.<br><br>   * Maximum 2 MiB; UTF\-8 (including BOM) and GB18030 are supported.<br><br>* `instruction` supports up to 2,000 characters.<br><br>* Each video `script` supports up to 10,000 characters. |
|Input modality: Audio |* Formats: mp3, wav, m4a, aac, flac, and ogg.<br><br>* Quantity: Up to 20 tracks. |
|Input path |* Public URL: Videos and SRT files can use HTTP/HTTPS direct file URLs accessible by LAS. Directories are not accepted. Signed URLs must remain valid throughout queuing and processing.<br><br>* TOS path: Use a concrete file address in `tos://bucket/key` format. The TOS bucket must belong to the same primary account and Asia Pacific (Johor) region as LAS, and LAS must have read permission for the object. User\-provided BGM supports TOS files only. |

## Output requirements

|Sub\-item |Detailed requirements |
|---|---|
|Supported data modalities |* Video<br><br>* Text (SRT, packaging plan, and result JSON) |
|Output modality: Video |* Returns a complete subtitled video and a clean video. Without newly added subtitles, they can be the same artifact.<br><br>* The default target is 1080×1920 at 60 FPS in non\-strict mode. Width must be less than height. Actual delivery is determined by Poll. |
|Output modality: Text |Returns a complete\-timeline SRT, packaging\-plan JSON, result JSON, statistics, and warnings. |
|Output path |* TOS path: Use `output_tos_path` to specify an output directory in `tos://bucket/prefix` format.<br><br>   * The TOS bucket must belong to the same primary account and Asia Pacific (Johor) region as LAS, and LAS must have write permission for the target directory.<br><br>* If `output_tos_path` is omitted, LAS assigns an output location.<br><br><br>Final TOS paths and temporary access URLs are returned in Poll `data.artifacts`. |

# Billing instructions

* Billing standards

   |Sub\-item |Billing description |
   |---|---|
   |Billing items |Billed by the total original duration of all input videos before playback\-speed adjustment. Subtitles, ASR, and TTS do not incur separate fees. Increasing `playback_speed` does not reduce measured input usage. |
   |Billing type |Usage\-based billing. Duration is recorded in milliseconds and prorated without rounding up to a whole minute. Only successful tasks with `task_status=COMPLETED` and `business_code="0"` are billed. |
   |Unit price |Two mutually exclusive tiers are available:<br><br><br>* With visual understanding (`usage.visual_understanding_duration_ms>0`): 0.15 USD/minute<br><br>* Standard packaging (`usage.visual_understanding_duration_ms=0`): 0.075 USD/minute |

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

**operator_id** string 必选 `Example value: las_video_packaging`

Always las_video_packaging.

**operator_version** string 必选 `Example value: v1`

Always v1.

**data** VideoPackagingReqParams 必选

Business configuration for this operator.

**video_urls** string / list of PackagingVideoItem 必选

Required: one URL or 1–20 URLs/video objects, which may be mixed; output follows input order.

**url** string 必选 `Example value: tos://your-bucket/edited.mp4`

Concrete portrait video whose height exceeds width. Each video must be at least 1 second, and the total duration must not exceed 30 minutes. TOS supports mp4, mov, m4v, webm, mkv, and avi.

**subtitle_srt** string `Optional` `Example value: tos://your-bucket/edited.srt`

Local\-timeline SRT file provided through TOS or HTTP(S), up to 2 MiB and mutually exclusive with `script`. Out\-of\-range cues are trimmed or dropped, overlaps are adjusted with warnings, and unparseable SRT is rejected.

**script** string `Optional`

Transcript of up to 10,000 characters, mutually exclusive with `subtitle_srt`. It corrects recognized text while retaining ASR timing.

**transition_in** string `Optional` `Example value: feature_flash_white`

Transition into the current video. It cannot be set on the first item. If omitted, LAS selects a transition automatically. Supported values are `none`, `feature_flash_white`, `feature_flash_gold`, `feature_soft_reveal`, `feature_accel_left`, `feature_accel_right`, `feature_accel_up`, `feature_accel_down`, `feature_accel_upleft`, `feature_accel_upright`, `feature_accel_downleft`, `feature_accel_downright`, `feature_zoom_punch`, `feature_zoom_pull`, `seam_punch_in`, `feature_spin_cut`, `feature_blur_dip`, and `feature_glitch_burst`.

**smart_packaging** PackagingSmartParams `Optional`

Subtitle effect, sound effect and BGM switches and candidate pools; all three enabled by default.

**enabled** boolean `Optional`

true forces all three on and ignores individual switches; false enables only explicitly true items; omitted defaults all on with explicit item overrides.

**enable_subtitle_effect** boolean `Optional`

Default true; controls subtitle effects, not regular subtitles; enabled takes priority.

**enable_sound_effect** boolean `Optional`

Default true; controls sound effects; enabled takes priority.

**enable_bgm** boolean `Optional`

Default true; controls background music; enabled takes priority.

**subtitle_effect_density** string `Optional` `Example value: low`

low / medium / high; density is automatic when omitted.

**bgm_volume** float `Optional` `Example value: 0.3`

[0.2, 0.8], automatically selected when omitted; explicit value sets music volume.

**bgm_segmentation** string `Optional` `Example value: auto`

Default auto follows content; single uses one track; per_video uses a section per input video. One input is treated as a whole video.

**assets** SmartPackagingAssets `Optional`

Optional allowlists for five asset groups. Omitted or {} uses default pools; a supplied group restricts selection to its candidates.

**sound_effect** SoundEffectAssetPool `Optional`

Sound\-effect allowlist; omission uses the default pool.

**asset_ids** list of string 必选

1–20 valid sound effects IDs, deduplicated in input order; not empty. Must start with sfx_.

**selection** string `Optional` `Example value: director`

director: default, select by content within the pool; random: choose randomly within the pool. Does not relax allowlist restrictions.

**bgm** BgmAssetPool `Optional`

Built\-in allowlist and/or user TOS tracks; omission uses the default music pool.

**asset_ids** list of string `Conditionally required`

Built\-in bgm_ IDs, up to 20 distinct entries, default []. At least one of asset_ids or urls must be nonempty.

**urls** list of string `Conditionally required`

User TOS audio files: mp3, wav, m4a, aac, flac, ogg. Up to 20 distinct files, default []; at least one of urls or asset_ids must be nonempty. Initial track analysis can add latency.

**source** string `Optional` `Example value: user`

With urls, defaults to user: user tracks only; full: user plus built\-in pool. Explicit source requires urls. With only asset_ids, select from the built\-in allowlist.

**selection** string `Optional` `Example value: director`

director: default, select by content within the pool; random: choose randomly within the pool. Does not relax allowlist restrictions.

**font** FontAssetPool `Optional`

Font allowlist; omission uses default candidates.

**font_ids** list of string 必选

1–20 valid fonts IDs, deduplicated in input order; not empty.

**selection** string `Optional` `Example value: director`

director: default, select by content within the pool; random: choose randomly within the pool. Does not relax allowlist restrictions.

**subtitle_effect** SubtitleEffectAssetPool `Optional`

Caption/highlight allowlist; omission uses default presets.

**effect_ids** list of string 必选

1–20 valid caption/highlight presets IDs, deduplicated in input order; not empty.

**selection** string `Optional` `Example value: director`

director: default, select by content within the pool; random: choose randomly within the pool. Does not relax allowlist restrictions.

**transition** TransitionAssetPool `Optional`

Inter\-video transition allowlist.

**preset_ids** list of string 必选

1–20 valid between\-video transition IDs, deduplicated in input order and nonempty; allowed values are listed under PackagingVideoItem.transition_in.

**selection** string `Optional` `Example value: director`

director: default, select by content within the pool; random: choose randomly within the pool. Does not relax allowlist restrictions.

**instruction** string `Optional`

Packaging preferences, up to 2000 characters; affects expression, not subtitle wording.

**srt_line_break** string `Optional` `Example value: reflow`

External SRT only: default reflow wraps to picture width with shared cue times; keep preserves cues and joins internal line breaks with spaces.

**subtitle_style** SubtitleStyleParams `Optional`

Regular subtitle font, size, colors, outline, shadow and position; omitted items use defaults, independently of card styles.

**font_id** string `Optional`

Valid font ID; automatically selected when omitted. Other omitted style values use defaults.

**font_size** integer `Optional` `Example value: 50`

Body font size, [24, 120] px at a 720×1280 reference; omission uses the default.

**keyword_font_size** integer `Optional` `Example value: 60`

Keyword font size, [24, 120] px; omission uses the default.

**text_color** string `Optional` `Example value: #FFFFFF`

Text color, #RRGGBB or #RRGGBBAA. AA is opacity: 00 transparent, FF opaque. Omission uses the default.

**outline_color** string `Optional` `Example value: #101010`

Outline color, same format as text_color; omission uses the default.

**outline_width** integer `Optional` `Example value: 40`

Outline width, [0, 100]. 0 disables the outline; omission uses the default.

**shadow_color** string `Optional` `Example value: #000000`

Shadow color, same format as text_color; omission uses the default.

**shadow_size** integer `Optional` `Example value: 0`

Shadow offset, [0, 100]; omission uses the default.

**position_ratio** float `Optional` `Example value: 0.87`

Subtitle\-line vertical center as a fraction of frame height, [0.05, 0.95], measured down from the top; omission uses the position default.

**background_color** string `Optional` `Example value: #00000080`

Subtitle background color, same format as text_color; omission uses the default background style.

**info_card** InfoCardParams `Optional`

Information\-card content, position and styles; prompt required when provided.

**prompt** string 必选 `Example value: Show the product name at the start and a learn-more prompt at the end`

Card content and placement instructions, 1–4000 characters after trimming.

**position** string `Optional` `Example value: top_left`

top_left, top_center, top_right, bottom_left, bottom_center or bottom_right. Omission leaves placement to card planning.

**style** CardTextStyleParams `Optional`

Body style; omission uses card defaults without inheriting subtitle_style.

**font_id** string `Optional`

Valid font ID; omission uses the card default.

**font_size** integer `Optional` `Example value: 36`

Font size, [24, 60] px; omission uses the relevant card title/body default.

**text_color** string `Optional` `Example value: #FFFFFF`

Text color, #RRGGBB or #RRGGBBAA, with AA opacity; omission uses card defaults.

**outline_color** string `Optional` `Example value: #101010`

Outline color, same format as text_color; omission uses card defaults.

**outline_width** integer `Optional` `Example value: 40`

Outline width [0, 100]; 0 disables the outline. Omission uses card defaults.

**shadow_color** string `Optional` `Example value: #000000`

Shadow color, same format as text_color; omission uses card defaults.

**shadow_size** integer `Optional` `Example value: 0`

Shadow offset [0, 100]; omission uses card defaults.

**background_color** string `Optional` `Example value: #00000080`

Background color, same format as text_color; omission uses card defaults.

**title_style** CardTextStyleParams `Optional`

Title style; omission uses title defaults independently of body styling.

**font_id** string `Optional`

Valid font ID; omission uses the card default.

**font_size** integer `Optional` `Example value: 36`

Font size, [24, 60] px; omission uses the relevant card title/body default.

**text_color** string `Optional` `Example value: #FFFFFF`

Text color, #RRGGBB or #RRGGBBAA, with AA opacity; omission uses card defaults.

**outline_color** string `Optional` `Example value: #101010`

Outline color, same format as text_color; omission uses card defaults.

**outline_width** integer `Optional` `Example value: 40`

Outline width [0, 100]; 0 disables the outline. Omission uses card defaults.

**shadow_color** string `Optional` `Example value: #000000`

Shadow color, same format as text_color; omission uses card defaults.

**shadow_size** integer `Optional` `Example value: 0`

Shadow offset [0, 100]; omission uses card defaults.

**background_color** string `Optional` `Example value: #00000080`

Background color, same format as text_color; omission uses card defaults.

**visual_understanding** boolean `Optional` `Example value: false`

Default false, planning primarily from subtitles; true adds visual understanding to assist decisions. Successful tasks select the standard or visual\-understanding pricing tier based on actual understanding usage; see specifications.

**video_spec** VideoSpecParams `Optional`

Target resolution/frame rate, default 1080×1920@60fps, strict=false; width must be less than height.

**width** integer `Optional` `Example value: 1080`

Target width in pixels, [64, 7680], default 1080; provide together with height.

**height** integer `Optional` `Example value: 1920`

Target height in pixels, [64, 7680], default 1920; provide together with width.

**fps** integer `Optional` `Example value: 60`

Target frame rate in frames/second, [1, 240], default 60.

**strict** boolean `Optional` `Example value: false`

Default false: reduce delivery specifications as needed, without upsampling. true rejects any source requiring upsampling or with insufficient frame rate. Scaling down a landscape source and adding padding is not upsampling.

**playback_speed** float `Optional` `Example value: 1.0`

[1.0, 2.0], default 1.0; video, subtitles and duration_sec use final\-speed timing; source_duration_sec is original duration.

**output_tos_path** string `Optional` `Example value: tos://your-bucket/packaging/results/`

Writable TOS output directory; automatically allocated when omitted.

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
--data '{"operator_id":"las_video_packaging","operator_version":"v1","data":{"video_urls":[{"url":"tos://your-bucket/edited.mp4","script":"Welcome to this product introduction."}],"visual_understanding":false,"output_tos_path":"tos://your-bucket/results/"}}'
```

Detailed request example:

```json
{
  "operator_version": "v1",
  "data": {
    "video_urls": [
      {
        "url": "tos://your-bucket/input/opening.mp4",
        "subtitle_srt": "tos://your-bucket/input/opening.srt"
      },
      {
        "url": "tos://your-bucket/input/product.mp4",
        "script": "This product is lightweight and portable for everyday use.",
        "transition_in": "feature_soft_reveal"
      }
    ],
    "smart_packaging": {
      "enable_sound_effect": false,
      "bgm_segmentation": "single"
    },
    "instruction": "Keep subtitles concise, emphasize portability, and avoid excessive density.",
    "subtitle_style": {
      "font_size": 48,
      "text_color": "#FFFFFF"
    },
    "output_tos_path": "tos://your-bucket/output/packaging/"
  },
  "operator_id": "las_video_packaging"
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

**operator_id** string 必选 `Example value: las_video_packaging`

Fixed operator ID.

**operator_version** string 必选 `Example value: v1`

Always v1.

**task_id** string 必选 `Example value: task-example`

Task ID from Submit; query using the same caller identity.

### Response parameters

**metadata** Metadata

Task state and errors.

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

**data** VideoPackagingResponse

Successful video packaging result.

**clazz** string `Example value: las_video_packaging`

Always las_video_packaging.

**source_duration_sec** float `Example value: 30`

Total original input\-video duration in seconds, before speed adjustment; both standard and visual\-understanding tiers prorate this value to minutes.

**duration_sec** float `Example value: 30`

Delivered video duration in seconds, adjusted for playback_speed.

**playback_speed** float `Optional` `Example value: 1.2`

Delivery speed multiplier, present only above 1.0.

**video_count** integer `Example value: 1`

Number of videos included in the finished video.

**subtitle_srt** string

Full SRT text relative to delivered\-video start, speed\-adjusted; empty without subtitles.

**packaging_scheme** object

Packaging scheme corresponding to packaging_scheme_\* files.

**summary** PackagingSummary

Actual packaging statistics.

**subtitle_sources** list of string

In video order: asr (recognition), srt (supplied subtitles), asr_script (transcript correction). Describes the strategy, not a guarantee that speech was recognized.

**subtitle_cue_count** integer `Example value: 2`

Regular subtitle cue count; 0 without subtitles.

**subtitle_effect_count** integer `Example value: 0`

Decorative caption count in the scheme; 0 when disabled or unselected.

**keyword_highlight_count** integer `Example value: 1`

Keyword\-highlight count; 0 when disabled or unselected.

**sound_effect_count** integer `Example value: 0`

Number of planned sound\-effect entries, not distinct assets.

**bgm_track_count** integer `Example value: 1`

Number of BGM sections, not necessarily distinct tracks.

**transition_count** integer `Example value: 0`

Non\-hard\-cut transition count; 0 for one video or all hard cuts.

**info_card_count** integer `Example value: 0`

Card count; 0 when none are generated.

**warnings** list of string

Degradation, omitted content or material warnings, up to 50; inspect even on success.

**usage** PackagingUsage

Usage protocol v1; visual\-understanding duration selects one of two mutually exclusive tiers, both using source_duration_sec. ASR/output durations have no separate charge.

**version** string `Example value: v1`

Usage schema version.

**asr_duration_ms** integer `Example value: 0`

ASR duration in milliseconds; reference only, no separate charge.

**visual_understanding_duration_ms** integer `Example value: 0`

Actual visual\-understanding duration in milliseconds; positive selects the visual tier, 0 selects standard packaging. Both tiers bill total source_duration_sec; this field is not an additional duration charge.

**output_duration_ms** integer `Example value: 30000`

Delivered duration in milliseconds; reference only, no separate charge.

**artifacts** Artifacts

Artifact TOS paths and access URLs; missing artifacts generally omit their keys.

**result_json_tos_path** string

TOS path to the complete result JSON.

**result_json_url** string

Temporary result\-JSON download URL.

**video_subtitled_tos_path** string

Full video TOS path; identical to clean output without subtitles, null on subtitle\-burning degradation.

**video_subtitled_url** string

Temporary URL corresponding to video_subtitled_tos_path.

**video_clean_tos_path** string

TOS path to video without newly added text layers, retaining source text/audio and planned sound effects, BGM and transitions.

**video_clean_url** string

Temporary clean\-video download URL.

**subtitle_srt_tos_path** string

TOS path to separate SRT, returned when subtitles exist. Timestamps start at the beginning of this delivered video.

**subtitle_srt_url** string

Temporary SRT URL; null or absent without subtitles.

**packaging_scheme_tos_path** string

TOS path to the packaging scheme JSON.

**packaging_scheme_url** string

Temporary scheme\-JSON download URL.

### Examples

```bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{"operator_id":"las_video_packaging","operator_version":"v1","task_id":"task-example"}'
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
    "clazz": "las_video_packaging",
    "source_duration_sec": 30.0,
    "duration_sec": 30.0,
    "video_count": 1,
    "subtitle_srt": "1\n00:00:00,000 --> 00:00:02,000\nDiscover the details.\n\n2\n00:00:02,000 --> 00:00:04,000\nExplore the benefits.\n",
    "summary": {
      "subtitle_sources": [
        "srt"
      ],
      "subtitle_cue_count": 2,
      "subtitle_effect_count": 0,
      "keyword_highlight_count": 1,
      "sound_effect_count": 0,
      "bgm_track_count": 1,
      "transition_count": 0,
      "info_card_count": 0
    },
    "warnings": [],
    "usage": {
      "version": "v1",
      "asr_duration_ms": 0,
      "visual_understanding_duration_ms": 0,
      "output_duration_ms": 30000
    },
    "artifacts": {
      "video_subtitled_tos_path": "tos://your-bucket/packaging/results/subtitled.mp4",
      "video_clean_tos_path": "tos://your-bucket/packaging/results/clean.mp4",
      "subtitle_srt_tos_path": "tos://your-bucket/packaging/results/subtitle.srt",
      "packaging_scheme_tos_path": "tos://your-bucket/packaging/results/packaging_scheme.json",
      "result_json_tos_path": "tos://your-bucket/packaging/results/result.json"
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
