---
title: "Intelligent Video Remix"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Intelligent-Video-Remix"
---

The Intelligent Video Remix operator leverages understanding of input materials, speech recognition, semantic retrieval, and large model orchestration capabilities to automatically match, sort, and edit talking head, b\-roll, or long real\-shot materials according to script, structured shot list, or natural language creative requirements, producing the final video.

# Operator introduction

> Operator ID: las_video_remix

## Applicable scenarios

## Core capabilities

* The operator first completes material understanding and shot matching, then generates an editing plan based on the configured editing scenario mode (`mode`). Supported editing scenario modes include:

   * **Talking head original audio match**: `mode=speech_match`. Enter the script text to be extracted and edited. The operator locates the corresponding segments in the video material ASR and outputs the original audio and video of the matched segments. In this scenario, both the video and audio of the input video material can be directly used for editing output.

   * **Visual semantic match**: `mode=visual_match`. Use natural language descriptions to specify the video material to be extracted and edited, such as descriptions of the video visuals or content script. In this scenario, the visuals of the input video material are typically used for editing output, but the audio is usually not usable. You may choose to input TTS narration to replace the original audio.

   * **Talking head marketing remix**: `mode=marketing_headtalk`. This mode intelligently performs rough editing of recorded talking head materials and selectively inserts b\-roll based on semantics. Currently, commonly used editing templates for automotive live talking head are preset and can be used directly.

   * **Long real\-shot process editing**: `mode=long_real_shot`. This mode is designed for long real\-shot materials such as price negotiation, vehicle delivery, maintenance, and store visits. It intelligently edits to organize a complete storyline using original audio and visuals, and supports bounding the output duration via `min_duration_sec` and `max_duration_sec`.

* For different editing scenario modes, the application scenarios of the input video materials can be flexibly configured.

   * By using the material role (`role`) parameter, input video materials can be marked as `speech` (talking head/main material), `voiceover` (audio only), or `broll` (visuals only).

* **Structured storyboard**: Supports using `speech`, `visual_description`, `duration`, and `video_id` to control each script unit.

* **Smart packaging**: Supports subtitle effects, sound effects, and BGM.

* **Plan and deliverables**: After the operator processing is completed, the final editing plan, SRT subtitles, video without subtitles, and video with subtitles are returned as deliverables. You can also use `data.match_scheme` to view the matching relationship between the input script units and video material segments in the generated editing plan and finished video.

## Effect demonstrations

* Input examples

   * [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13bce3be58224e3c88bbc6f718e01d5f~tplv-goo7wpa0wc-image.image)

   * [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bbd154c912f456ab47f556188b3cad7~tplv-goo7wpa0wc-image.image)

   * [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e63d541537b740109571d13df48ea25b~tplv-goo7wpa0wc-image.image)

* Task code example – core parameters

   ```Bash
   "data": {
     "video_urls": [
         {
       "url": "tos://las-doctest/las-ai/input/video/marketing_video/car/v2/headtalk_01.mp4",
       "role": "speech"
         },
         {
       "url": "tos://las-doctest/las-ai/input/video/marketing_video/car/v2/car_exterior_broll.mp4",
       "role": "broll"
         },
         {
       "url": "tos://las-doctest/las-ai/input/video/marketing_video/car/v2/car_interior_broll.mp4",
       "role": "broll"
         }
       ],
       "mode": "marketing_headtalk",
       "template": "automotive",
       "script": "Create a fast-paced, authentic vertical marketing video for a new-energy sedan. Retain the sales consultant's complete, non-repetitive core narration. The final video must use both b-roll clips: insert exterior showroom footage when discussing driving range and daily commuting; insert interior, storage, rear-seat, and charging footage when discussing the smart cockpit, passenger space, storage, and charging efficiency. Use each type of b-roll at least twice while continuing the consultant's original audio. End by cutting back to the consultant and retain the invitation to visit the store for a test drive. The input materials contain no subtitles; use only the operator-generated standard subtitles and dynamic captions, avoiding subtitle overlap. Enable sound effects and background music. Keep the visual packaging clean and professional, do not obscure faces or the vehicle, and do not emphasize any brand, model, or trim name.",
       "video_edit_mode": "lite",
       "smart_packaging": {
         "enabled": true,
         "enable_subtitle_effect": true,
         "enable_sound_effect": true,
         "enable_bgm": true
       },
       "output_tos_path": "${OUTPUT_TOS_PATH}"
     }
   ```

* Output examples

   * [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4719ca43c2db4c6681a5303f2663093b~tplv-goo7wpa0wc-image.image)

   * [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/52ef828d19354f12a6b385b5815a84c9~tplv-goo7wpa0wc-image.image)

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Sub\-items |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Duration |The overall duration depends on the number of materials, total duration of materials, cache hit rate, editing profile, and whether rendering is performed.<br><br><br>* `video_edit_mode=lite` skips large model evaluation and correction, prioritizing speed; `pro` enables evaluation and correction, prioritizing quality and requiring more time.<br><br>* When the same materials are called again, the material understanding process will not be repeated for materials that hit the cache. |

# Input and output requirements

## Input requirements

|Subdivision |Detailed requirements |
|---|---|
|Supported input data modalities |* Video<br><br>* Audio<br><br>* Text |
|Input modality: Video |* Format: `mp4`, `mov`, `m4v`, `webm`, `mkv`, `avi`.<br><br>* Quantity: Up to 100 videos can be input at a time.<br><br>* Size: Each episode video must be at least 1 second and no longer than 10 minutes; the total duration of all episode videos in a single input must not exceed 2 hours, and the total size must not exceed 10 GB.<br><br>* Resolution: All input videos must have consistent resolution. Video resolution must be between 360x640 (360 is the short side, 640 is the long side) and 1080x1920 (1080 is the short side, 1920 is the long side).<br><br>* Other requirements: Ensure that subtitles are included in the input videos. |
|Input modality: Audio |When input materials are used only for the final audio input (`role=voiceover`), the following audio formats are supported:<br><br>Format: `mp3`, `wav`, `m4a`, `aac`, `flac`, `ogg` |
|Input modality: Text |When refining and editing input material videos, you can use the `script` parameter to specify the refinement and editing requirements for each storyboard segment. |
|Input path requirements |Provide input data to the operator via the `video_urls` request parameter. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A video URL accessible via the public network, in the format `http/https`.<br><br>   * Public URLs do not support addresses requiring login status or additional header authentication; temporary URLs must be valid during task execution.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and in the Asia Pacific (Johor) region (`ap-southeast-1`) as the current LAS service, you can provide a TOS path in the format `tos://bucket_name/demo/`.<br><br>   * The TOS object must exist and have read permissions. |

## Output requirements

|Subdivision |Detailed requirements |
|---|---|
|Output data modalities |* Video<br><br>* Audio<br><br>* Text (such as editing scheme JSON) |
|Output modality: video |* Duration: The maximum length of the output video is 10 minutes.<br><br>   * For `long_real_shot`, `real_shot_headtalk`, and `live_slicing`, use `min_duration_sec` and `max_duration_sec` to bound the output duration. The supported overall range is 5–3,600 seconds, subject to the parameter\-specific limits.<br><br>   * The bounds do not pad insufficient source content; `live_slicing` applies them to each clip. |
|Output path: TOS |Specify the storage path for operator output results using the request parameters `output_tos_path`, `tts_audio_tos_path`. Currently, only TOS paths are supported.<br><br>TOS path: A TOS Bucket directory under the same primary account and in the Asia Pacific (Johor) region (`ap-southeast-1`) as the LAS service, with write permissions. Format: `tos://bucket/output/`. |

# Billing instructions

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing items |The following billing items are included:<br><br><br>* **Material understanding fee**: The material understanding fee for input video materials is billed based on the total duration of the input video materials.<br><br>   * When inputting video materials via TOS, the material understanding fee is incurred for the same material when the task is submitted for the first time.<br><br>   * If the material does not change in TOS (such as its path and file content), repeated tasks do not incur the material understanding fee again.<br><br>* **Intelligent editing fee**: The fee for invoking the model to edit the final video content when generating the final video output. Billed based on the total duration of the output video. No fee is incurred if the final video output is not generated.<br><br>* **Voice\-over (TTS) fee**: Billed based on the number of characters generated for the voice\-over. No fee is incurred if the voice\-over is not generated.<br><br>* **Intelligent subtitle fee**: Billed based on the number of characters generated for intelligent subtitles. No fee is incurred if intelligent subtitles are not generated.<br><br>* **Special effects text fee**: Billed based on the number of characters generated for special effects. No fee is incurred if special effects text is not generated.<br><br><br>The total task fee is the sum of the above billing items. |
   |Billing type |Usage\-based billing, invoiced hourly based on actual usage. Billing precision: millisecond\-level, proportional, no rounding up for durations less than one minute. |
   |Unit price |The unit price varies for different billing items. Details are as follows. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Material understanding |0.2 USD/minute |
   |Intelligent editing |* lite: 4 USD/minute<br><br>* pro: 6.5 USD/minute |
   |Voice\-over |0.15 USD/1,000 characters |
   |Intelligent subtitles |0.7 USD/1,000 characters |
   |Special effects text |0.1 USD/1,000 characters |

# Caution and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model invocation billing - BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |The BaseURL for the supported Asia Pacific (Johor) region (`ap-southeast-1`) is `https://operator.las.ap-southeast-1.bytepluses.com`. Use this value to configure the path for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |

# REST API calls

## API usage instructions

* The API for this operator is an asynchronous task interface. You need to submit a task via the `Submit` interface to obtain the `task_id`, then use the `Poll` interface to get the running status of the corresponding task (`task_id`) and obtain the operator processing result.

* Caution: After submitting the task, the `task_id` is valid for 3 days. After 3 days, you will not be able to use this `task_id` to obtain the operator processing result.

## Submit

### Interface descriptions

Submit an Intelligent Video Remix asynchronous task. The operator generates an editing plan based on the materials and script, and can further complete subtitles, smart packaging, video rendering, and TOS delivery.

### Request parameters

**operator_id** string 必选 `Example value: las_video_remix`

Operator ID, fixed as `las_video_remix`.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed as `v1`.

**data** VideoRemixReqParams 必选

Video remix business parameters.

**mode** string 必选 `Example value: marketing_headtalk`

Supported modes: `speech_match`, `visual_match`, `marketing_headtalk`, `long_real_shot`, `real_shot_headtalk`, `live_slicing`, and `repackage`. `repackage` re\-renders a previous `match_scheme.json` and rejects `video_urls` and `script`. Other values return `Parameter.Invalid`.

**video_urls** string / array `Conditionally required` `Example value: tos://bucket/remix/materials/`

Input materials. Required for every mode except `repackage`, which rejects this field. A string can be a TOS directory prefix or a single `tos://` or HTTP(S) video URL. An array must contain concrete files and consistently use URL strings or material objects. Material quotas vary by mode: `speech_match` and `visual_match` support up to 1,000 clips; `marketing_headtalk` supports up to 30 clips, each no longer than 10 minutes and totaling no more than 30 minutes; `long_real_shot` supports up to 100 clips, each no longer than 1 hour and totaling no more than 2 hours; `real_shot_headtalk` applies these limits to the corresponding sections; and `live_slicing` supports up to 12 recordings, each no longer than 5 hours and totaling no more than 8 hours.

**url** string 必选 `Example value: tos://bucket/remix/voiceover.mp3`

Specific material file address. Supports `tos://` or HTTP(S).

**role** string `Optional` `Example value: voiceover`

Material role, default is `speech`. `speech` keeps both picture and speech and is supported by every mode. `voiceover` uses audio only and is supported only by `speech_match`, `marketing_headtalk`, and `long_real_shot`; provide usable b\-roll to cover the picture. `broll` is used only as a candidate visual source.

**section** string `Conditionally required` `Example value: real_shot`

Composite section, used only by `real_shot_headtalk`. Values are `real_shot` and `headtalk`. Either specify it on every material object or omit it from all objects for automatic sectioning. A `real_shot` section rejects `role=broll`; other modes reject this field.

**image_urls** list of ImageUrlItem `Optional`

Supplementary images for `speech_match`, `visual_match`, and `marketing_headtalk`. Up to 20 images remain after trimming and deduplicating complete URLs. Selection, placement, and presentation are system\-decided; not every image is guaranteed to be used. Not supported with `initialize_only=true`.

**url** string 必选 `Example value: tos://your-bucket/remix/images/product.png`

Concrete `tos://`, `http://`, or `https://` image URL. Supports JPG, JPEG, PNG, and WebP.

**caption** string `Optional` `Example value: Product fabric details`

Optional semantic description, up to 200 characters. It assists content matching but does not become overlay text or force a layout.

**script** string / array `Conditionally required` `Example value: Organize a complete product introduction and highlight the selling points at the beginning.`

Editing script. `speech_match` and `visual_match` accept fixed copy or a `ScriptShot` object array, with at most 1,000 characters across all `speech` values. `marketing_headtalk`, `long_real_shot`, and `real_shot_headtalk` require a natural\-language instruction of at most 4,000 characters. `live_slicing` accepts an optional natural\-language instruction of at most 4,000 characters. `repackage` rejects this field.

**speech** string `Conditionally required` `Example value: Introducing this new product today.`

Voiceover or narration text to be matched.

**visual_description** string `Conditionally required` `Example value: Product close-up and unboxing scenes`

Visual semantic matching description.

**duration** float `Conditionally required` `Example value: 3.5`

Target shot duration in seconds and must be greater than 0. Required when only `visual_description` is set, optional when both `speech` and `visual_description` are set, and must not be set when only `speech` is provided.

**video_id** string `Optional` `Example value: tos://bucket/remix/materials/clip-01.mp4`

Restricts the shot to one material. It must exactly match a value in `video_urls`; otherwise, the request returns a parameter error.

**video_edit_mode** string `Optional` `Example value: lite`

Editing mode: `lite` skips large model evaluation and correction, prioritizing speed; `pro` enables evaluation and correction, prioritizing quality. Default `lite`.

**template** string `Optional` `Example value: automotive`

Industry template. Values are `automotive` and `life_service` (food, store visits, entertainment, and lifestyle). It applies only to the three auto\-planning modes and `live_slicing`; omit it to use a cross\-industry neutral profile.

**max_duration_sec** integer `Optional` `Example value: 300`

Upper output\-duration bound in seconds, supported only by `long_real_shot`, `real_shot_headtalk`, and `live_slicing`. Range: 10–3,600. It caps but does not pad the result. `long_real_shot` defaults to 210 seconds; for `live_slicing`, it applies to each clip and defaults to 40 seconds.

**min_duration_sec** integer `Optional` `Example value: 20`

Lower output\-duration bound in seconds, supported only by `long_real_shot`, `real_shot_headtalk`, and `live_slicing`. Range: 5–3,600 and must be lower than `max_duration_sec`. The service does not pad insufficient source material. For `live_slicing`, it applies to each clip and defaults to 20 seconds.

**max_clips** integer `Optional` `Example value: 5`

Maximum number of clips to produce for `live_slicing`, from 1 to 10 and defaulting to 5. The service can return fewer clips rather than padding similar content.

**opening_setting** OpeningSettingParams `Optional`

Opening settings for the real\-shot section of `long_real_shot` and `real_shot_headtalk`.

**enable_cold_open** boolean `Optional` `Example value: true`

Whether to lift a suspenseful segment to the opening. Default is `true`; if no suitable segment exists, the cold open is skipped.

**render_video** boolean `Optional` `Example value: true`

Whether to render the video. Default is `true`. When `false`, the editing scheme and related files are still produced, and synthesized TTS audio is still returned. The resulting scheme can be used with `repackage`.

**material_rotation** boolean `Optional` `Example value: false`

Whether to down\-weight visual materials used more often by the current account in recent tasks. Default is `false`. It applies only to visual or b\-roll candidates in `speech_match` and `visual_match`; ASR\-matched speech and `voiceover` visuals are not rotated.

**initialize_only** boolean `Optional` `Example value: false`

Whether to warm the material index without matching or rendering. Default is `false`; supported only by `speech_match` and `visual_match`. When enabled, only the initialization snapshot is returned in `artifacts`.

**smart_packaging** SmartPackagingParams `Optional`

Subtitle effects, sound effects, and BGM switches. LAS provides a variety of preset subtitle effects, sound effects, and BGM. When the switches are enabled, the model will automatically select suitable special effect subtitles, sound effects, or BGM based on the requirements for generating the final video. `marketing_headtalk` and `long_real_shot`, if not provided, all three items are enabled by default; for `speech_match` and `visual_match`, if not provided, all are disabled by default. This switch only controls whether special effect subtitles are enabled; regular sentence\-by\-sentence subtitles are not affected by this switch.

**enabled** boolean `Optional` `Example value: true`

When `true`, all subtitle effects, sound effects, and BGM are enabled and detailed items are ignored; when `false`, only the detailed items explicitly set to `true` are enabled. If not provided, defaults to the mode.

**enable_subtitle_effect** boolean `Optional` `Example value: true`

Whether to enable dynamic subtitle effects. Default is `false`. Only takes effect independently when `enabled` is not `true`.

**enable_sound_effect** boolean `Optional` `Example value: true`

Whether to enable sound effects. Default is `false`. Only takes effect independently when `enabled` is not `true`.

**enable_bgm** boolean `Optional` `Example value: true`

Whether to enable BGM. Default is `false`. Only takes effect independently when `enabled` is not `true`.

**subtitle_effect_density** string `Optional` `Example value: medium`

Dynamic subtitle\-effect density: `low` (about 4 per minute, at most one per sentence), `medium` (about 10 per minute), or `high` (system\-selected without a fixed cap). It overrides mode and template defaults and has no effect when subtitle effects are disabled.

**audio** AudioParams `Optional`

Per\-track fixed gain in dB relative to source audio. Omitted fields remain automatic and do not enable BGM or TTS. For `repackage`, edit audio in the scheme instead.

**bgm_gain_db** float `Optional` `Example value: -12`

Fixed BGM gain in `[-60,20]` dB. Explicit `0` keeps source level and bypasses automatic adjustment; it does not mute the track.

**tts_gain_db** float `Optional` `Example value: 3`

Fixed synthesized\-TTS gain in `[-60,20]` dB. It applies only when TTS is generated.

**speech_gain_db** float `Optional` `Example value: 2`

Fixed original\-speech and supplied\-voiceover gain in `[-60,20]` dB.

**subtitle_style** SubtitleStyleParams `Optional`

Styling for normal line\-by\-line subtitles. `repackage` rejects this field; edit `subtitle.style` in the scheme instead.

**text_color** string `Optional` `Example value: #FFFFFF`

Text color in `#RRGGBB` or `#RRGGBBAA` format. Default is `#FFFFFF`.

**outline_color** string `Optional` `Example value: #101010`

Outline color in the same format as `text_color`. Default is `#101010`.

**outline_width** integer `Optional` `Example value: 40`

Outline\-thickness slider from 0 to 100; internally divided by 10 to obtain pixel width. `0` disables the outline. Default is 40.

**shadow_color** string `Optional` `Example value: #000000`

Shadow color in the same format as `text_color`; ignored when `shadow_size=0`. Default is `#000000`.

**shadow_size** integer `Optional` `Example value: 0`

Shadow\-distance slider from 0 to 100. `0` disables the shadow and is the default.

**font_size** integer `Optional` `Example value: 68`

Main font size from 24 to 120 at a 720×1,280 base. Default is 68, or 50 for `long_real_shot`.

**keyword_font_size** integer `Optional` `Example value: 80`

Inline keyword font size from 24 to 120 in the same unit as `font_size`.

**position_ratio** float `Optional` `Example value: 0.67`

Subtitle vertical\-center position as a ratio from the top of the frame, from 0.05 to 0.95. Default is 0.67; `long_real_shot` and `life_service` use 0.75.

**video_spec** VideoSpecParams `Optional`

Delivery resolution, frame rate, and strictness. The default is 1,080×1,920 at 60 fps in non\-strict mode.

**width** integer `Optional` `Example value: 1080`

Width from 64 to 7,680. Must be set together with `height`.

**height** integer `Optional` `Example value: 1920`

Height from 64 to 7,680. Must be set together with `width`.

**fps** integer `Optional` `Example value: 60`

Frame rate from 1 to 240.

**strict** boolean `Optional` `Example value: false`

Whether to reject source material below the target resolution or frame rate. Default is `false`; non\-strict mode does not upscale lower\-spec material.

**output_tos_path** string `Optional` `Example value: tos://bucket/remix/results/`

Output directory, must be a `tos://bucket/prefix/` writable by the current identity. If not provided, the server assigns a default directory for the task.

**tts** TtsParams `Optional`

TTS configuration. Full\-length narration is synthesized only by `visual_match`. `speech_match` can synthesize unmatched sentences when both `enable` and `fill_missing_speech` are true; other modes do not synthesize TTS.

**enable** boolean `Optional` `Example value: true`

Whether to synthesize continuous narration for `visual_match` `speech` text. Default is `false`.

**language** string `Optional` `Example value: zh`

Narration language options: `zh` (Chinese), `en` (English), `id` (Indonesian), `ar` (Arabic), `es` (Spanish), `ja` (Japanese), `ko` (Korean); if not provided, the language is recognized based on the actual synthesized text.

**fill_missing_speech** boolean `Optional` `Example value: true`

For `speech_match`, synthesize sentences not found in source ASR and match them by visual semantics. Requires `enable=true`; default is `false`.

**voice** string `Optional` `Example value: zh_female_vv_uranus_bigtts`

seed\-tts\-2.0 voice ID. When omitted, the service selects a voice from the language and visual persona.

**speed** float `Optional` `Example value: 1.25`

Speech\-rate multiplier, default 1.25. `speech_rate` takes precedence when set.

**speech_rate** integer `Optional` `Example value: 0`

Speech\-rate slider from \-50 to 100, where \-50 is 0.5×, 0 is 1.0×, and 100 is 2.0×.

**loudness_rate** float `Optional` `Example value: 0`

Synthesis\-source loudness setting from \-50 to 100. `audio.tts_gain_db` separately controls the final\-video TTS track.

**emotion** string `Optional` `Example value: happy`

Emotion style supported by the underlying TTS service.

**emotion_scale** float `Optional` `Example value: 3`

Emotion intensity from 1 to 5.

**format** string `Optional` `Example value: mp3`

Audio format: `mp3`, `ogg_opus`, `pcm`, or `wav`. Default is `mp3`.

**sample_rate** integer `Optional` `Example value: 24000`

Sample rate. Default is 24,000.

**bit_rate** integer `Optional`

Bitrate for the synthesized audio.

**match_scheme** string `Conditionally required` `Example value: tos://bucket/remix/results/match_scheme.json`

TOS path of a previously produced editing plan. Required for `mode=repackage` and rejected for other modes.

### Response parameters

**metadata** Metadata

Asynchronous task metadata.

**task_id** string `Example value: task-20261008143000-abc123`

Asynchronous task ID, used for Poll queries.

**task_status** string `Example value: PENDING`

Task status: `PENDING` (queued), `RUNNING` (processing), `COMPLETED` (finished; check `business_code`), `FAILED`, `TIMEOUT`, `EXPIRED`, or `CANCELLED`. After a successful Submit, the status is usually `PENDING`.

**business_code** string `Example value: 0`

Business code. `0` indicates successful submission; when not `0`, troubleshoot with `error_msg`.

**error_msg** string

Error message, empty when successful.

### Examples

#### Request examples

The following example uses `marketing_headtalk` to perform marketing remix on spoken material and b\-roll material. Replace the TOS path with a readable and writable path in the Asia Pacific (Johor) region (`ap-southeast-1`) for the current account.

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_remix",
  "operator_version": "v1",
  "data": {
    "video_urls": [
      {
        "url": "tos://your-bucket/remix/materials/headtalk_01.mp4",
        "role": "speech"
      },
      {
        "url": "tos://your-bucket/remix/materials/product_broll.mp4",
        "role": "broll"
      }
    ],
    "mode": "marketing_headtalk",
    "template": "automotive",
    "script": "Create a fast-paced product introduction that highlights the key selling point at the beginning and ends with a call to learn more.",
    "video_edit_mode": "lite",
    "smart_packaging": {
      "enabled": true
    },
    "output_tos_path": "tos://your-bucket/remix/results/"
  }
}'
```

#### Core input parameters for other modes

```JSON
{
  "speech_match": {
    "mode": "speech_match",
    "script": "First presenter sentence. Second presenter sentence."
  },
  "visual_match": {
    "mode": "visual_match",
    "script": [
      {
        "speech": "Today, we are introducing this new product.",
        "visual_description": "Close-up of the product exterior"
      },
      {
        "visual_description": "Outdoor usage scenario",
        "duration": 3
      }
    ],
    "tts": {
      "enable": true,
      "language": "zh"
    }
  },
  "long_real_shot": {
    "mode": "long_real_shot",
    "template": "automotive",
    "script": "Edit a complete price-negotiation process that ends with the final deal.",
    "max_duration_sec": 180,
    "opening_setting": {
      "enable_cold_open": true
    }
  },
  "real_shot_headtalk": {
    "mode": "real_shot_headtalk",
    "template": "automotive",
    "max_duration_sec": 120,
    "video_urls": [
      {"url": "tos://bucket/handover-01.mp4", "role": "speech", "section": "real_shot"},
      {"url": "tos://bucket/sales-talk.mp4", "role": "speech", "section": "headtalk"},
      {"url": "tos://bucket/product-broll.mp4", "role": "broll", "section": "headtalk"}
    ],
    "script": "Use real vehicle-delivery footage in the first half, followed by a sales consultant's spoken summary in the second half."
  },
  "live_slicing": {
    "mode": "live_slicing",
    "template": "life_service",
    "max_clips": 6,
    "min_duration_sec": 25,
    "max_duration_sec": 45,
    "script": "Make each clip focus on one product, open with the host announcing the price or making a clear comparison, and end with a purchase call to action."
  },
  "repackage": {
    "mode": "repackage",
    "match_scheme": "tos://your-bucket/remix/results/match_scheme.json"
  }
}
```

#### Custom delivery specification and subtitle style

```JSON
{
  "video_spec": {"width": 1080, "height": 1920, "fps": 30, "strict": false},
  "subtitle_style": {
    "text_color": "#FFF589",
    "outline_color": "#101010",
    "outline_width": 55,
    "shadow_size": 20,
    "font_size": 60,
    "position_ratio": 0.8
  }
}
```

#### Supplementary images and track gains

```JSON
{
  "operator_id": "las_video_remix",
  "operator_version": "v1",
  "data": {
    "mode": "marketing_headtalk",
    "video_urls": [
      {"url": "tos://your-bucket/remix/materials/host.mp4", "role": "speech"}
    ],
    "script": "Introduce the jacket fabric and wearing experience, emphasizing softness and comfort.",
    "image_urls": [
      {"url": "tos://your-bucket/remix/images/fabric.png", "caption": "Close-up of the fabric texture"},
      "tos://your-bucket/remix/images/reaction.webp"
    ],
    "smart_packaging": {"enabled": false, "enable_bgm": true},
    "audio": {"bgm_gain_db": -12, "speech_gain_db": 2},
    "output_tos_path": "tos://your-bucket/remix/results/"
  }
}
```

#### Response examples

```JSON
{
  "metadata": {
    "task_id": "task-20261008143000-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |The parameter type, mode, enumeration, range, material role, or parameter combination is invalid. |
|400 |Material.Empty |no material video found |No video found under the TOS prefix, or no available material found. |
|400 |Shot.Empty |initialization produced no shots |Material initialization did not produce any matching shots. |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |The TOS input/output address is invalid, the object does not exist, or the current identity does not have read/write permissions. |
|401 |Authorization.Missing |Missing Authorization. |Authorization information is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |API Key is invalid. |
|429 |Server.Busy |Server is Busy, please try again later. |The service is busy or rate limiting has been triggered. |
|500 |Server.InternalError |General Internal Error |Internal service error, such as sub\-operator, matching, or rendering failure. |

The table above lists errors that may be returned during request validation or task creation. Asynchronous errors in material understanding, matching, rendering, and uploading are returned via Poll's `metadata.business_code` and `metadata.error_msg`.

## Poll

### Interface descriptions

Query the execution status and result of an Intelligent Video Remix asynchronous task. Only when `task_status=COMPLETED` and `business_code=0` will the complete `data` be returned; in other statuses, `data` is usually not returned.

### Request parameters

**operator_id** string 必选 `Example value: las_video_remix`

Operator ID, fixed as `las_video_remix`.

**operator_version** string 必选 `Example value: v1`

Operator version, fixed as `v1`.

**task_id** string 必选 `Example value: task-20261008143000-abc123`

`metadata.task_id` returned by Submit.

### Response parameters

**metadata** Metadata

Task metadata.

**task_id** string `Example value: task-20261008143000-abc123`

Asynchronous task ID.

**task_status** string `Example value: COMPLETED`

Task status: `PENDING` or `RUNNING` while unfinished; `COMPLETED`, `FAILED`, `TIMEOUT`, `EXPIRED`, and `CANCELLED` are terminal. Read `data` only for `COMPLETED` with `business_code=0`.

**submit_time** string `Example value: 2026-10-08T14:30:00+08:00`

Task submission time, ISO 8601 format.

**end_time** string `Example value: 2026-10-08T14:33:10+08:00`

Task end time, ISO 8601 format; may be empty if the task has not ended.

**business_code** string `Example value: 0`

Business code. `0` indicates success; when not `0`, check `error_msg`.

**error_msg** string

Error message, empty when successful.

**data** VideoRemixResponse

Remix result for a successful terminal state; usually absent or empty for other statuses. Single\-clip modes return `VideoRemixResponse`, while `live_slicing` returns `LiveSlicingResponse`.

**clazz** string `Example value: las_video_remix`

Response parameters type, fixed as `las_video_remix`.

**mode** string `Example value: marketing_headtalk`

The actual mode executed this time.

**template** string `Example value: automotive`

The industry template actually used, such as `automotive` or `life_service`; returned only when a template is configured.

**duration_sec** float `Example value: 58.6`

Total duration of the finished video, in seconds; equal to the sum of all segment durations in the final editing scheme (match_scheme) timeline.

**shot_count** integer `Example value: 126`

Number of material shots available for matching.

**unit_count** integer `Example value: 12`

Number of script/narrative units.

**match_scheme** MatchScheme

Final editing scheme, including audio mode, material segments for each unit, time intervals, audio\-video binding, candidates, and remarks.

**audio_mode** string `Example value: asr`

Audio mode used by the editing scheme.

**delivery_spec** object

Delivered `width`, `height`, and `fps`.

**playback_speed** float `Example value: 1.1`

Delivery playback speed. `speech_match`, `marketing_headtalk`, and `long_real_shot` use fixed 1.10× playback; other modes are not sped up.

**audio** AudioGainParams

Final scheme audio configuration, including per\-track gain when explicitly set.

**bgm_gain_db** float `Example value: -12`

Explicit fixed BGM gain in dB; absent or null means automatic mixing.

**tts_gain_db** float `Example value: 3`

Explicit final\-video TTS gain in dB; absent or null means automatic normalization.

**speech_gain_db** float `Example value: 2`

Explicit original\-speech or supplied\-voiceover gain in dB; absent or null means automatic adjustment.

**image_sticker_placement** ImageStickerPlacement

Sticker\-placement diagnostics. Its absence does not mean all supplementary images were unused because images can also fill all or part of the frame.

**requested** integer `Example value: 1`

Number of video\-sticker placement\-planning requests, not the number of `image_urls`.

**placed** integer `Example value: 1`

Number of successfully placed stickers.

**skipped** integer `Example value: 0`

Number of skipped stickers, for example because no suitable placement was available.

**units** list of MatchUnit

Ordered editing units.

**index** integer `Example value: 0`

Scheme\-unit index.

**unit_id** string

Stable unit ID for automatic planning; may be absent.

**text** string

Copy or content description for the unit.

**duration** float `Example value: 3.4`

Unit duration in seconds on the scheme timeline.

**video_id** string

Primary source identifier; detailed visuals may instead be in the source lists.

**start_time** string `Example value: 00:00:01.200`

Primary source start within the source video.

**end_time** string `Example value: 00:00:04.600`

Primary source end within the source video.

**media_binding** string `Example value: lock_av`

`lock_av` keeps original audio and video, `audio_capture_only` keeps source audio only, and `visual_only` keeps visuals only.

**visual_sources** list of MatchVisualSource

Visual source segments; each segment can contain `image_overlays`.

**video_id** string

Visual\-source identifier for the original video or image material.

**video_name** string

Source name.

**start_time** string `Example value: 00:00:01.200`

Video\-segment start within the source.

**end_time** string `Example value: 00:00:04.600`

Video\-segment end within the source.

**cover_media** string `Example value: image`

Can be `image` for an image\-supplied visual segment and can be absent for video segments.

**image_layout** ImageLayout

Image\-fill, composite, partial\-frame, or sticker layout.

**kind** string `Example value: video_sticker`

`full`, `stack`, `panel`, or `video_sticker`; selected by the service.

**canvas** list of integer `Example value: [1080,1920]`

Layout canvas `[width,height]` in pixels.

**tiles** list of ImageTile

Image tiles and their geometry.

**image_id** string

Source identifier for the image tile.

**src_crop** list of integer `Example value: [0,0,600,600]`

Source crop `[x,y,width,height]` in original\-image pixels.

**dest** list of integer `Example value: [760,180,240,240]`

Destination `[x,y,width,height]` in canvas pixels.

**rotation_deg** float `Example value: 5`

Tile rotation in degrees.

**radius_px** integer `Example value: 0`

Corner radius in canvas pixels.

**shadow** boolean `Example value: false`

Whether a shadow is applied.

**enter** ImageAnimation

Optional entrance animation.

**kind** string `Example value: fade`

`fade`, `slide_left`, `slide_right`, or `slide_up`.

**delay_ms** integer `Example value: 0`

Animation delay in milliseconds, at least 0.

**duration_ms** integer `Example value: 250`

Animation duration in milliseconds, at least 0.

**exit** ImageAnimation

Optional exit animation with the same fields as `enter`.

**backdrop** string

`black`, `blur`, or null when no backdrop is applied.

**motion** ImageMotion

Optional image motion.

**kind** string `Example value: push_in`

Image\-motion type; currently `push_in`.

**zoom_from** float `Example value: 1.0`

Starting zoom multiplier.

**zoom_to** float `Example value: 1.05`

Ending zoom multiplier.

**total_ms** integer `Example value: 3000`

Total motion duration in milliseconds; 0 uses the containing\-segment duration.

**image_overlays** list of ImageOverlay

Stickers over a playing host video.

**image_id** string

Sticker\-image identifier.

**offset_ms** integer `Example value: 500`

Offset from the host\-segment start in milliseconds.

**duration_ms** integer `Example value: 1800`

Positive sticker duration in milliseconds; it must fit within the host segment.

**layout** ImageLayout

Planned `video_sticker` layout using the structure above.

**locked_segments** list of MatchVisualSource

Locked source segments, which can also contain image overlays.

**picture** list of MatchVisualSource

Picture sources, including image layouts and stickers where applicable.

**audio_source** object

Audio\-source description and references.

**candidates** list of object

Candidate matches, with the selected item first when present.

**cover_candidates** list of object

Alternative visual candidates for `speech_match`; can be absent for other units.

**notes** list of string

Scheme notes.

**subtitle** object

Subtitle style and per\-sentence cues.

**transition_plan** list of object

Per\-boundary transition decisions.

**audio_direction_plan** object

BGM and sound\-effect plan when the corresponding packaging switches are enabled.

**video_filter_decision** object

Full\-video main\-filter decision.

**subtitle_srt** string `Example value: 1<br>00:00:00,000 --> 00:00:03,400<br>Core selling points.`

Generated SRT subtitle content.

**artifacts** Artifacts

Output artifacts. The returned fields vary depending on the mode, switches, and degradation scenarios.

**result_json_tos_path** string `Example value: tos://bucket/remix/results/result.json`

TOS address of the complete result JSON.

**result_json_url** string `Example value: https://example.com/result.json`

Temporary pre\-signed link for the complete result JSON, valid for 72 hours.

**initialization_jsonl_tos_path** string `Example value: tos://bucket/remix/results/initialization_results.jsonl`

Snapshot of the understanding results for each input material; returned after initialization is complete.

**initialization_jsonl_url** string `Example value: https://example.com/initialization_results.jsonl`

Temporary pre\-signed link for the snapshot of material understanding results, valid for 72 hours.

**video_subtitled_tos_path** string `Example value: tos://bucket/remix/results/subtitled.mp4`

TOS address of the subtitled final video. If subtitle burning fails and degrades to a non\-subtitled final video, it may be `null`.

**video_subtitled_url** string `Example value: https://example.com/subtitled.mp4`

Temporary pre\-signed link for the subtitled final video, valid for 72 hours; may be `null`.

**video_clean_tos_path** string `Example value: tos://bucket/remix/results/clean.mp4`

TOS address of the final video without subtitles.

**video_clean_url** string `Example value: https://example.com/clean.mp4`

Temporary pre\-signed link for the final video without subtitles, valid for 72 hours.

**video_speech_only_tos_path** string

TOS path of the speech\-only video before BGM and sound\-effect mixing, when produced.

**video_speech_only_url** string

Temporary URL for the speech\-only video.

**video_audio_directed_tos_path** string

TOS path of the video after BGM and sound\-effect mixing, when produced.

**video_audio_directed_url** string

Temporary URL for the audio\-directed video.

**video_clip_tos_paths** list of string `Example value: ["tos://bucket/remix/results/clips/clip_000.mp4"]`

List of TOS addresses for rendered intermediate clips.

**video_clip_urls** list of string `Example value: ["https://example.com/clip_000.mp4"]`

List of temporary pre\-signed links for rendered intermediate clips, valid for 72 hours.

**subtitle_srt_tos_path** string `Example value: tos://bucket/remix/results/subtitle.srt`

TOS address of the SRT subtitle file.

**subtitle_srt_url** string `Example value: https://example.com/subtitle.srt`

Temporary pre\-signed link for the SRT subtitle file, valid for 72 hours.

**subtitle_effect_ass_tos_path** string `Example value: tos://bucket/remix/results/subtitle_effect.ass`

TOS path of the ASS subtitle\-effect file, returned when generated and saved.

**subtitle_effect_ass_url** string `Example value: https://example.com/subtitle_effect.ass`

Temporary pre\-signed URL for the ASS subtitle\-effect file.

**subtitle_effect_timeline_tos_path** string `Example value: tos://bucket/remix/results/subtitle_effect_timeline.json`

TOS path of the subtitle\-effect timeline JSON.

**subtitle_effect_timeline_url** string `Example value: https://example.com/subtitle_effect_timeline.json`

Temporary pre\-signed URL for the subtitle\-effect timeline JSON.

**custom_subtitle_timeline_tos_path** string `Example value: tos://bucket/remix/results/custom_subtitle_timeline.json`

TOS path of the custom on\-screen caption and information\-card timeline JSON.

**custom_subtitle_timeline_url** string `Example value: https://example.com/custom_subtitle_timeline.json`

Temporary pre\-signed URL for the custom subtitle timeline JSON.

**video_filter_decision_tos_path** string `Example value: tos://bucket/remix/results/video_filter_decision.json`

TOS path of the video\-filter decision JSON.

**video_filter_decision_url** string `Example value: https://example.com/video_filter_decision.json`

Temporary pre\-signed URL for the video\-filter decision JSON.

**match_scheme_tos_path** string `Example value: tos://bucket/remix/results/match_scheme.json`

TOS address of the editing scheme JSON.

**match_scheme_url** string `Example value: https://example.com/match_scheme.json`

Temporary pre\-signed link for the editing scheme JSON, valid for 72 hours.

**tts_audio_tos_path** string `Example value: tos://bucket/remix/results/tts.mp3`

`visual_match` TOS address of the narration audio when TTS is enabled; if not generated, it is `null`.

**tts_audio_url** string `Example value: https://example.com/tts.mp3`

Temporary pre\-signed link for TTS narration, valid for 72 hours; if not generated, it is `null`.

**tts_audio_duration_sec** float `Example value: 58.6`

Duration of TTS narration in seconds; if not generated, it is `null`.

**video_cover_tos_path** string `Example value: tos://bucket/remix/results/cover.jpg`

TOS path of the generated video cover image.

**video_cover_url** string `Example value: https://example.com/cover.jpg`

Temporary pre\-signed URL for the video cover image.

**coarse_script_tos_path** string `Example value: tos://bucket/remix/results/coarse_script.json`

TOS path of the rough\-cut script JSON.

**coarse_script_url** string `Example value: https://example.com/coarse_script.json`

Temporary pre\-signed URL for the rough\-cut script JSON.

**audio_direction_plan_tos_path** string `Example value: tos://bucket/remix/results/audio_direction_plan.json`

TOS path of the BGM and sound\-effect arrangement plan JSON.

**audio_direction_plan_url** string `Example value: https://example.com/audio_direction_plan.json`

Temporary pre\-signed URL for the audio\-direction plan JSON.

**audio_library_tos_path** string `Example value: tos://bucket/remix/results/audio_library.json`

TOS path of the audio\-material catalog JSON.

**audio_library_url** string `Example value: https://example.com/audio_library.json`

Temporary pre\-signed URL for the audio\-material catalog JSON.

**live_session_digest_tos_path** string `Example value: tos://bucket/remix/results/live_session_digest.json`

TOS path of the `live_slicing` session digest JSON, returned in task\-level artifacts.

**live_session_digest_url** string `Example value: https://example.com/live_session_digest.json`

Temporary pre\-signed URL for the live\-session digest.

For `mode=live_slicing`, `data` uses the following `LiveSlicingResponse` fields instead of `VideoRemixResponse`:

**mode** string `Example value: live_slicing`

Fixed as `live_slicing`.

**clip_count** integer `Example value: 5`

Number of clips actually produced.

**requested_clips** integer `Example value: 6`

Requested clip\-count upper bound after applying the `max_clips` default.

**clip_duration_band_sec** list of integer `Example value: [25,45]`

Applied per\-clip duration band `[min,max]` in seconds.

**duration_sec** float `Example value: 182.0`

Sum of all produced clip durations in seconds.

**outputs** list of LiveSlicingClip

Produced clips.

**clip_id** string `Example value: clip_001`

Clip ID.

**batch_index** integer `Example value: 1`

One\-based clip index mapped to the `batch_NNN` artifact directory.

**product** string `Example value: Portable Fan`

Product covered by the clip.

**angle** string `Example value: Battery life comparison`

Selling\-point angle.

**audience** string `Example value: Outdoor users`

Target audience.

**hook_type** string `Example value: pricing_hook`

Hook type; can be empty.

**hook_text** string `Example value: This price is 20 lower than last week.`

Hook line.

**cta_text** string `Example value: Tap the yellow cart below to order.`

Call\-to\-action line.

**planned_duration_sec** float `Example value: 32.0`

Planned narration duration in seconds.

**planned_rows** list of string `Example value: ["row_12","row_17"]`

Narration rows selected during planning.

**source_windows** list of object

Source windows carved from the recording, containing `video`, `video_name`, `start_ms`, `end_ms`, `contains_hook`, and `derived_uri`.

**duration_sec** float `Example value: 32.0`

Delivered clip duration in seconds.

**match_scheme** MatchScheme

Editing scheme for this clip.

**subtitle_srt** string

SRT content for this clip.

**artifacts** Artifacts

Output artifacts for this clip.

**clips_shortfall** object

Returned only when fewer clips are produced than requested. It contains `requested`, `produced`, and dropped or failed clip entries with reasons.

**session_digest** object

Session\-planning digest for debugging.

**artifacts** Artifacts

Task\-level artifacts containing the session digest and result JSON; per\-clip video artifacts are under `outputs[].artifacts`.

**usage** RemixUsage

Task\-level actual usage summed across all clips.

**usage** RemixUsage

Actual business usage for this successful task; only records capabilities that were truly executed successfully, and price is not calculated.

**version** string `Example value: v1`

Usage protocol version, currently `v1`.

**material_duration_ms** integer `Example value: 180000`

Actual duration of material understanding executed this time, in milliseconds; materials that hit the cache are not counted repeatedly.

**director_tier** string `Example value: lite`

Director tier actually executed for the video, `lite` or `pro`; if no final video is produced, it is an empty string.

**director_output_duration_ms** integer `Example value: 58600`

Total duration of successfully produced final videos, in milliseconds; the subtitle and non\-subtitle versions of the same final video are not counted repeatedly.

**tts_chars** integer `Example value: 0`

Number of TTS billing characters successfully synthesized; 0 if TTS is not used.

**subtitle_chars** integer `Example value: 320`

Number of regular subtitle characters actually burned into the final video; not counted if subtitle burning fails.

**effect_chars** integer `Example value: 86`

Number of dynamic effect characters actually burned into the final video.

### Examples

#### Request examples

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
  --header "Content-Type: application/json" \
  --header "Authorization: Bearer $LAS_API_KEY" \
  --data '{
    "operator_id": "las_video_remix",
    "operator_version": "v1",
    "task_id": "task-20261008143000-abc123"
  }'
```

#### Response examples

The following is a successful terminal state example for `marketing_headtalk`. The validity period of a temporary pre\-signed link is subject to the actual response from the server; for long\-term storage, use the TOS address.

```JSON
{
  "metadata": {
    "task_id": "task-20261008143000-abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-10-08T14:30:00+08:00",
    "end_time": "2026-10-08T14:33:10+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "clazz": "las_video_remix",
    "mode": "marketing_headtalk",
    "duration_sec": 58.6,
    "shot_count": 126,
    "unit_count": 12,
    "match_scheme": {
      "audio_mode": "asr",
      "units": [
        {
          "index": 0,
          "text": "Lead with the product's key selling point.",
          "video_name": "headtalk_01.mp4",
          "start_time": "00:00:01.200",
          "end_time": "00:00:04.600",
          "duration": 3.4,
          "media_binding": "lock_av"
        }
      ],
      "notes": []
    },
    "subtitle_srt": "1\n00:00:00,000 --> 00:00:03,400\nLead with the product's key selling point.",
    "artifacts": {
      "video_subtitled_tos_path": "tos://your-bucket/remix/results/subtitled.mp4",
      "video_subtitled_url": "https://example.com/subtitled.mp4",
      "video_clean_tos_path": "tos://your-bucket/remix/results/clean.mp4",
      "video_clean_url": "https://example.com/clean.mp4",
      "subtitle_srt_tos_path": "tos://your-bucket/remix/results/subtitle.srt",
      "subtitle_srt_url": "https://example.com/subtitle.srt",
      "match_scheme_tos_path": "tos://your-bucket/remix/results/match_scheme.json",
      "match_scheme_url": "https://example.com/match_scheme.json",
      "result_json_tos_path": "tos://your-bucket/remix/results/result.json",
      "result_json_url": "https://example.com/result.json"
    },
    "usage": {
      "version": "v1",
      "material_duration_ms": 180000,
      "director_tier": "lite",
      "director_output_duration_ms": 58600,
      "tts_chars": 0,
      "subtitle_chars": 320,
      "effect_chars": 86
    }
  }
}
```

**Polling and error handling**

* `PENDING` and `RUNNING` are non\-terminal states, and polling should continue.

* `COMPLETED`, `FAILED`, `TIMEOUT`, `EXPIRED`, and `CANCELLED` are terminal states. Only `COMPLETED` with `business_code=0` indicates success.

* For any terminal state other than a successful `COMPLETED`, use `metadata.business_code` and `metadata.error_msg` for troubleshooting. Do not read empty `data` as the business result.

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |The Poll request parameters are invalid. |
|400 |Task.NotFound |Task not found |The task does not exist, has expired, or the current identity does not have permission to query. |
|401 |Authorization.Missing |Missing Authorization. |Authorization information is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |API Key is invalid. |
|500 |Server.InternalError |General Internal Error |Internal server error. |

When task execution fails, `metadata.business_code` may also return `Parameter.Invalid`, `Material.Empty`, `Shot.Empty`, `Tos.AccessFailed`, or internal service errors. For specific reasons, refer to `error_msg`.
