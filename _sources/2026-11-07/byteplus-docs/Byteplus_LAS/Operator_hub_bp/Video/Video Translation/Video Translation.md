---
title: "Video Translation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Translation_operator"
---

The Video Translation operator efficiently and accurately converts video content from the source language to one or more target languages. The service scope includes not only subtitle translation, but also audio translation and facial translation, ultimately outputting the dubbed video and subtitle files in the corresponding languages.

# Operator introduction

> Operator ID: las_video_translate

## Applicable scenarios

|Scenarios |Description |
|---|---|
|Short drama internationalization |Provide multilingual translation and dubbing for short dramas to support overseas distribution |
|Course training |Multilingual localization of training videos to support global customer learning |
|Marketing materials |International dissemination of advertising videos, product introductions, and promotional films |

## Core capabilities

* **Multilingual support**: Supports translation in multiple languages. Input languages support video input in 25 languages, and output languages support audio dubbing in 31 languages, covering Chinese, English, Japanese, Indonesian, Spanish, Portuguese, Korean, French, German, and many other widely used languages. Leveraging the powerful translation capabilities of large models, it achieves extremely high translation accuracy and localized terminology, meeting the needs of global content dissemination.

* **Voice cloning**: Accurately extracts the speaker's voice from the video and recreates its vocal characteristics. This capability is enabled by default and requires no additional configuration.

* **High\-quality dubbing and fast mode**: The `high_quality` mode provides richer emotional expression, more faithful reproduction of the original speaker's voice timbre, and more accurate pronunciation. Its optional fast mode reduces processing time with a possible slight reduction in dubbing quality and is recommended together with dynamic duration.

* **Convenient result delivery**: Supports securely writing translated subtitles, dubbed voice audio, and video directly to your specified cloud storage (TOS), while generating a pre\-signed download link.

* **Subtitle burning and style control**: Supports burning translated subtitles into the corresponding dubbed video. You can freely configure parameters such as font, font size, color, bold, outline, shadow, opacity, line spacing, subtitle width, and position.

* **Facial translation**: Supports standard audiovisual matching and fuzzy matching through `lip_translate_param.lip_fuzzy_matching` to synchronize translated speech with the speaker's lip movements. Enabling this feature incurs an additional facial translation fee.

* **Lip sync to specified dubbed audio**: Supports generating a lip\-synced video directly from external dubbed audio or the video's own audio track, without subtitle translation or TTS.

* **Dynamic duration**: Slightly adjusts video duration to better match the rhythm of translated speech. Output duration may differ by target language.

* **Separate subtitle picture source**: Uses a timeline\-matched video, such as a version with original subtitles removed, as the picture source for final dubbed videos.

* **Video restoration**: Removes existing subtitles or watermarks through `las_video_inpaint_pro`. Poll returns the repaired source and its restoration task ID separately from the translated videos.

## Demo

---

**[Short drama for overseas markets]**

* Input video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc999aa66d714a8f862c6f812e361791~tplv-goo7wpa0wc-image.image)

* Output requirements:

   * Multiple languages: English, Japanese, Korean

   * Burn\-in subtitles

* Output video \- English

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ddd02fd300f4002988598834ab8fc9a~tplv-goo7wpa0wc-image.image)

* Output subtitle file

   [EP02_en-US_translated_caption_e7d674.srt](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b8368ca5b9b144fa8d3cfe3a313e576c~tplv-goo7wpa0wc-image.image)

* Output video \- Japanese

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb2fcd27ac0644f690d6d29633491006~tplv-goo7wpa0wc-image.image)

* Output subtitle file

   [EP02_ja-JP_translated_caption_4f58ed.srt](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ae7ab683cea541ca9dae231081a2ede2~tplv-goo7wpa0wc-image.image)

* Output video \- Korean

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cccfa7df332949ab8992e06e03a94301~tplv-goo7wpa0wc-image.image)

* Output subtitle file

   [EP02_ko-KR_translated_caption_41a857.srt](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e48420255eb4c00b45bef3b6175a9e7~tplv-goo7wpa0wc-image.image)

---

**[Marketing materials]**

* Input video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/89a92bbcd1cb4fa2bd411ca47e2cc9c0~tplv-goo7wpa0wc-image.image)

* Output video \- English \- lip\-sync translation not enabled

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be60b0c1b668474fa5a0570624a32c35~tplv-goo7wpa0wc-image.image)

——The output video directly contains English subtitles

* Output video \- English \- lip\-sync translation enabled

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e864771772a14e5b8e570f2ed1e64953~tplv-goo7wpa0wc-image.image)

——Lip movements and speech are more synchronized and natural

---

**[Training courses]**

* Input video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d9fc24b55919410ab74e593370d6d231~tplv-goo7wpa0wc-image.image)

* Output video \- English

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcf2fe1b5f7b4229b9a485fe9f1ef28a~tplv-goo7wpa0wc-image.image)

---

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Supported languages and fonts

|Language code |Language name |Input support status |Output support status |Subtitle font IDs supported by output video |
|---|---|---|---|---|
|ar\-SA |Arabic |✅ |✅ |`NotoSansArabic-Regular`, `Cairo-Regular`, `FiraGO-Regular` |
|bn\-BD |Bengali |✅ |❌ |Not applicable |
|da\-DK |Danish |❌ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|de\-DE |German |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|el\-GR |Greek |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|en\-US |English |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular`, `AtkinsonHyperlegible-Regular` |
|es\-MX |Spanish |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|fi\-FI |Finnish |❌ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|fil\-PH |Filipino |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|fr\-FR |French |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|he\-IL |Hebrew |❌ |✅ |`NotoSansHebrew-Regular`, `Heebo-Regular`, `FiraGO-Regular` |
|hi\-IN |Hindi |❌ |✅ |`NotoSansDevanagari-Regular`, `AnekDevanagari[wdth,wght]`, `FiraGO-Regular` |
|id\-ID |Indonesian |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|it\-IT |Italian |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|ja\-JP |Japanese |✅ |✅ |`NotoSansJP-Regular`, `MPLUS1-Regular` |
|km\-KH |Khmer |❌ |✅ |`NotoSansKhmer-Regular`, `KantumruyPro[wght]` |
|ko\-KR |Korean |✅ |✅ |`NotoSansKR-Regular`, `Pretendard-Regular` |
|lo\-LA |Lao |❌ |✅ |`NotoSansLao-Regular`, `BoonBaan-Regular` |
|ms\-MY |Malay |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|my\-MM |Burmese |❌ |✅ |`NotoSansMyanmar-Regular` |
|ne\-NP |Nepali |✅ |❌ |Not applicable |
|nl\-NL |Dutch |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|no\-NO |Norwegian |❌ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|pl\-PL |Polish |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|pt\-BR |Portuguese |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|ro\-RO |Romanian |✅ |❌ |Not applicable |
|ru\-RU |Russian |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|sv\-SE |Swedish |❌ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|sw\-KE |Swahili |❌ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|th\-TH |Thai |✅ |✅ |`NotoSansThai-Regular`, `Sarabun-Regular`, `BoonBaan-Regular`, `FiraGO-Regular` |
|tr\-TR |Turkish |✅ |✅ |`NotoSans-Regular`, `FiraGO-Regular` |
|uk\-UA |Ukrainian |✅ |❌ |Not applicable |
|vi\-VN |Vietnamese |✅ |✅ |`NotoSans-Regular`, `BeVietnamPro-Regular`, `FiraGO-Regular` |
|yue\-CN |Cantonese |✅ |✅ |`NotoSansHK-Regular`, `NotoSansTC-Regular`, `ChironHeiHK-Text-R` |
|zh\-CN |Chinese (Simplified) |✅ |✅ |`NotoSansSC-Regular` |

## Operator performance

|Sub\-item |Performance impact |
|---|---|
|Submit/Poll RPM |Submit: 600 RPM; Poll: 600 RPM |
|Maximum concurrency |10 |
|Duration |Processing time depends on input duration, subtitle density, output\-language count, content complexity, and service load.<br><br><br>* Speech translation, per target language: in standard mode, a roughly 1\-minute video typically takes about 6 minutes; 2–3\-minute videos typically take about 4 times the input duration. In high\-quality fast mode, a roughly 1\-minute video typically takes about 4 minutes. Multiply the estimate by the number of output languages.<br><br>* Video Translation + face translation: Estimated processing time ≈ output video duration × 30 × number of output languages.<br><br>* Enabling video restoration may increase the total processing time.<br><br><br>The actual processing time may fluctuate depending on the complexity of the video content, output languages, and service load. |

# Input and output requirements

## Input requirements

|Breakdown |Detailed requirements |
|---|---|
|Supported input data modalities |Video |
|Input format: Video |* Formats: `mp4`, `mov`, `avi`, `mkv`, `flv`, `webm`.<br><br>* Size: Maximum 10 GB.<br><br>* Duration:<br><br>   * Facial translation not enabled: Minimum 2 seconds, maximum 4 hours;<br><br>   * Facial translation enabled: Minimum 2 seconds, maximum 10 minutes, and no more than 30 fps.<br><br>* Other:<br><br>   * For standard video translation and lip sync using the video's own audio track, the video must contain an audio track. Multiple\-language audio tracks are not supported, and the primary audio track language must match `audio_language`.<br><br>   * If the original audio and lip movements do not match, set `lip_translate_param.lip_fuzzy_matching=true` to use visual\-only active speaker detection for face matching.<br><br>   * When using external dubbed audio for lip sync, its language can be detected automatically, and the difference between the video and dubbed audio durations must not exceed 1 second. |
|Input path requirements |Provide input data to the operator via the `video_url` request parameter. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A video URL accessible via the public network, in the format `http/https`.<br><br>   * Public URLs do not support addresses that require login status or additional header authentication. Temporary URLs must remain valid during task execution.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide a TOS path in the format `tos://bucket_name/demo`.<br><br>   * The TOS object must exist and have read permissions. |

## Output requirements

|Breakdown |Detailed requirements |
|---|---|
|Output data types |* Video<br><br>* Text (subtitle file)<br><br>* Audio (optional output) |
|Output format: video |Format: Fixed as `mp4` |
|Output format: text |Format: Supports `.ass`, `.txt`, `.srt`, `.xml`, `.vtt`. Specify the output subtitle file format via the request parameter `caption_formats`. |
|Output format: audio |Format: Fixed as `wav` |
|Output path: TOS |Specify the storage path for the operator's output results via the `output_tos_path` request parameter. Currently, only TOS paths are supported.<br><br>TOS path: A directory in a TOS Bucket under the same primary account and region as the LAS service, with write permissions. Format: `tos://bucket/output/`. |

# Billing instructions

* Billing standards

   |Breakdown |Billing standard description |
   |---|---|
   |Billing item |Billing is based on the input video duration. Each time a new language video is generated through translation, it is billed separately. For each language translation task, the cost consists of two parts:<br><br><br>* Video Translation fee: A fixed billing item for invoking this operator.<br><br>* (Fee charged if enabled) Face translation fee: If the face translation feature is enabled when invoking the operator, an additional face translation fee will be charged. |
   |Billing type |Usage\-based billing, unit: `USD /minute`. Charges are billed hourly based on actual usage. Billing precision: rounded to the nearest integer |
   |Unit price |The Video Translation unit price depends on the dubbing mode. Face translation is billed separately when enabled.<br><br><br>* Video Translation with `dubbing_mode=high_quality`: 0.68 USD /minute<br><br>* Video Translation with any other dubbing mode: 0.32 USD /minute<br><br>* Face translation: 0.68 USD /minute |

* Billing details

   Billing formula: `Total cost = (Video Translation unit price * input video duration + face translation unit price * face translation duration) * number of new language videos generated by translation`

   Enabling video restoration (`enable_video_inpaint=true`) incurs additional charges based on `video_inpaint_params` and the billing rules of `las_video_inpaint_pro`. These charges are not included in the video translation prices above.

* Billing example

   * Example scenario: A 10\-minute Chinese video is used as input, and new videos are generated in English, Japanese, and Korean through translation using a dubbing mode other than `high_quality`, with no face translation required.

   * Cost details:

      `Total cost = 0.32 USD /minute × 10 minutes × 3 = 9.6 USD`

# Caution and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## API usage instructions

* The API for this operator is an asynchronous task interface. You need to submit a task through the `Submit` interface to obtain the task's `task_id`, then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After submitting a task, the task's `task_id` is valid for three days. After three days, you will not be able to retrieve the operator's processing result using this `task_id`.

## Submit

### API description

Submit a video translation task using the las_video_translate operator. Upon completion, you can obtain subtitles in the target language, the dubbed video, and optionally, pure dubbed audio.

### Request parameters

**operator_id** string 必选 `Example value: las_video_translate`

The operator ID for this service is `las_video_translate`.

**operator_version** string 必选 `Example value: v1`

Currently, only `v1` is supported.

**data** VideoTranslateReqParams 必选

Operator parameters.

**video_url** string 必选 `Example value: tos://xxx/video.mp4`

Input video URL. Supports `http/https` and TOS `tos://bucket/key`. Supported formats: `.mp4`, `.mov`, `.avi`, `.mkv`, `.flv`, `.webm`. Duration must be from 2 seconds to 4 hours, or up to 10 minutes when face translation is enabled. File size must not exceed 10 GB.

**audio_language** string `Conditionally required` `Example value: zh-CN`

Source language code of the input video audio track. It must match the actual primary spoken language in the video. Required for standard video translation and when `lip_translate_param.dubbing_audio.source=video`. Optional when an external dubbed audio URL is specified, in which case it serves as the fallback language for the dubbed audio. For supported languages, see [Supported languages and fonts](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator#supported-languages-and-fonts).

**output_languages** list of string `Conditionally required` `Example value: [en-US]`

List of target output languages. Required for standard video translation and not required when lip syncing to specified dubbed audio. Empty and duplicate values are removed. The target languages cannot contain `audio_language`. For supported languages, see [Supported languages and fonts](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator#supported-languages-and-fonts).

**caption_formats** list of string `Optional` `Example value: [.srt, .ass]`

List of output subtitle formats. Supported values are `.ass`, `.txt`, `.srt`, `.xml`, and `.vtt`. Default: `.srt`. `.ass` subtitles use the font, color, outline, dynamic background, shadow, opacity, background padding, line spacing, width, position, and other subtitle control parameters from the current request; any omitted parameter uses its default value.

**output_tos_path** string 必选 `Example value: tos://xxx/output`

Result output directory. It must be a writable TOS directory for the request credentials, in the format `tos://bucket/prefix`. Translated assets are written here. When restoration is enabled, this is also the default repaired\-video directory unless `video_inpaint_params.output_tos_path` is set.

**dubbing_mode** string `Optional` `Example value: emotion`

Dubbing mode. Supported values: `emotion`, `timbre`, and `high_quality`. Default: `emotion`. `emotion` prioritizes reproducing the original emotion; `timbre` prioritizes voice\-timbre consistency with the original speaker; `high_quality` provides richer emotional expression, more faithful reproduction of the original speaker's voice timbre, and more accurate pronunciation. Has no effect when lip syncing to specified dubbed audio.

**enable_fast_mode** boolean `Optional` `Example value: false`

Fast mode. Default: `false`. It can be enabled only when `dubbing_mode=high_quality`. It reduces processing time but may slightly reduce dubbing quality. We recommend enabling it together with dynamic duration (`enable_dynamic_duration=true`).

**enable_dynamic_duration** boolean `Optional` `Example value: false`

Whether to slightly adjust video duration to match translated\-speech rhythm. Default: `false`. Output duration may differ by target language. Cannot be combined with `lip_translate=true`.

**subtitle_video_url** string `Optional` `Example value: https://example.com/clean-video.mp4`

Optional picture source for subtitle burn\-in. Its video\-stream duration must differ from `video_url` by at most 1 second. Requires `burn_translated_subtitles=true` and cannot be combined with restoration or specified dubbed\-audio lip sync.

**enable_video_inpaint** boolean `Optional` `Example value: false`

Whether to enable restoration through `las_video_inpaint_pro`, such as removing existing subtitles or watermarks. Default: `false`. Cannot be combined with `subtitle_video_url` or specified dubbed\-audio lip sync. Additional restoration charges apply.

**video_inpaint_params** VideoInpaintParams `Optional`

Restoration options. Omit or pass an empty object to use defaults.

**output_tos_path** string `Optional` `Example value: tos://xxx/repair/`

Repaired\-video output directory; defaults to the top\-level `output_tos_path`.

**model_level** string `Optional` `Example value: pro`

Restoration tier. Default: `pro`.

**detection_mode** string `Optional` `Example value: standard_subtitle`

Detection and erasure mode. Default: `standard_subtitle`.

**targets** list of string `Optional` `Example value: [subtitle]`

Target types for precise detection.

**fixed_bboxes** list of list of integer `Optional` `Example value: [[0,700,1000,950]]`

Fixed restoration regions in normalized 1000×1000 coordinates.

**return_subtitle_bbox** boolean `Optional` `Example value: true`

Whether the restoration task returns subtitle boxes. Video Translation Poll does not expose those boxes.

**max_process_frames** integer `Optional` `Example value: -1`

Maximum frames to process. Keep the default `-1` to process the complete video and pass duration validation.

**maximum_output_fps** integer `Optional` `Example value: 30`

Maximum output frame rate. Default: `30`.

**maximum_resolution** string `Optional` `Example value: 1080p`

Maximum output resolution. Default: `1080p`.

**output_video_mode** string `Optional` `Example value: balanced`

Output mode. Default: `balanced`.

**output_codec** string `Optional` `Example value: h264`

Output codec. Omitted by default, in which case the restoration service default is used.

**output_bitrate** integer `Optional` `Example value: 4000000`

Output bitrate in bps. Omitted by default.

**subtitle_persistent** boolean `Optional` `Example value: false`

Whether to treat subtitles as persistent. Default: `false`.

**output_dubbing_audio** boolean `Optional` `Example value: false`

Whether to additionally output clean dubbed speech audio. Default: `false`. When `true`, each target language returns a `translated_audio` asset in addition to the translated video.

**lip_translate** boolean `Optional` `Example value: false`

Whether to perform face translation / lip sync. Default: `false`. When set to `true`, use `lip_translate_param` to configure face matching or lip sync to specified dubbed audio. When enabled, an additional fee is charged.

**lip_translate_param** LipTranslateParam `Optional`

Face translation parameters. This field can be provided only when `lip_translate=true`. When omitted, standard face translation is performed.

**lip_fuzzy_matching** boolean `Optional` `Example value: false`

Whether to use visual\-only active speaker detection for face matching. Default: `false`. When set to `true`, the service no longer verifies consistency between the original audio and lip movements. This is suitable when the source video's audio and visuals are out of sync but translated dubbing and synchronized lip movements are still required. This field cannot be used together with `dubbing_audio`.

**dubbing_audio** LipTranslateDubbingAudio `Optional`

Specifies the dubbed audio to use for lip sync. When provided, the task enters specified dubbed audio lip\-sync mode: subtitle translation and TTS are skipped, and no translated subtitles are generated. The difference between the video and dubbed audio durations must not exceed 1 second. The result contains only one lip\-synced video.

**source** string 必选 `Example value: url`

Dubbed audio source. Supported values: `url` and `video`. `url` uses the dubbed audio specified by `url`; `video` extracts the input video's own audio track as the dubbed audio.

**url** string `Conditionally required` `Example value: tos://xxx/dubbing.wav`

Dubbed audio URL. Supports `http/https` and TOS `tos://bucket/key`. Required and non\-empty when `source=url`; must not be provided when `source=video`.

**language** string `Optional` `Example value: en-US`

Language code of the dubbed audio, used for ASR. This field takes precedence over the top\-level `audio_language`. When `source=url` and neither field is provided, the dubbed audio language is detected automatically. Language codes are case\-sensitive, and the supported languages are the same as those for input languages.

**ignore_audio_video_duration_mismatch** boolean `Optional` `Example value: false`

Whether to ignore the duration difference between the video and dubbed audio. Default: `false`. When `false`, a difference greater than 1 second causes an error. When `true`, the video is aligned to the dubbed audio duration: if the dubbed audio is longer, the video loops from the beginning; if the video is longer, its tail is trimmed.

**burn_translated_subtitles** boolean `Optional` `Example value: true`

Whether to burn each translated subtitle track into its corresponding dubbed video. Default: `false`. When enabled, the `translated_video` assets in `translated_videos` contain burned\-in subtitles; when disabled, they are dubbed videos without burned\-in subtitles.

**subtitle_font_by_language** list of string `Optional` `Example value: [NotoSans-Regular]`

Fonts for subtitles, mapped one\-to\-one to `output_languages` in the same order. If the whole field is omitted or `null`, every language uses its automatic default font. A `null` or empty item selects the default font for that language. When provided, the list length must match `output_languages`, which must not contain empty or duplicate items. Each selector must be a supported font ID for the corresponding language; external paths are not supported. For supported fonts, see [Supported languages and fonts](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator#supported-languages-and-fonts).

**subtitle_font_size** integer `Optional` `Example value: 40`

Subtitle font size in output\-video pixel ASS units. Range: `[8, 128]`. Default: `40`.

**subtitle_font_color** string `Optional` `Example value: #FFFFFF`

Subtitle fill color in `#RRGGBB` or `#RRGGBBAA` format. The optional `AA` component is opacity: `FF` is opaque and `00` is transparent. Default: `#FFFFFF`.

**subtitle_bold** boolean `Optional` `Example value: false`

Whether the subtitle text is bold. Default: `false`.

**subtitle_outline_color** string `Optional` `Example value: #000000`

Subtitle outline color in `#RRGGBB` or `#RRGGBBAA` format. Default: `#000000`.

**subtitle_outline_width** float `Optional` `Example value: 0.0`

Outline width of the main subtitle text in output\-video pixel ASS units. Range: `[0, 16]`. Default: `0`. This parameter applies only to the main subtitle text and does not affect the separate shadow layer.

**subtitle_background_color** string `Optional` `Example value: #00000080`

Dynamic subtitle background fill color in `#RRGGBB` or `#RRGGBBAA` format. The optional `AA` component controls only the background opacity; `subtitle_opacity` does not affect the background. Default: `#00000000`, which is fully transparent.

**subtitle_background_padding_x** float `Optional` `Example value: 12.0`

Horizontal padding added on each side of the dynamic subtitle background in output\-video pixel ASS units. Range: `[0, 128]`. Default: `0`. This parameter expands only the background and does not change the subtitle text layout.

**subtitle_background_padding_y** float `Optional` `Example value: 6.0`

Vertical padding added to the top and bottom of the dynamic subtitle background in output\-video pixel ASS units. Range: `[0, 128]`. Default: `0`. This parameter expands only the background and does not change the subtitle text layout.

**subtitle_shadow_color** string `Optional` `Example value: #00000000`

Subtitle shadow color in `#RRGGBB` or `#RRGGBBAA` format. Default: `#00000000`.

**subtitle_opacity** float `Optional` `Example value: 1.0`

Global opacity of the main subtitle text and shadow, multiplied by the alpha values of the text fill, main outline, and shadow colors. Range: `[0, 1]`. Default: `1`. This parameter does not affect `subtitle_background_color`.

**subtitle_shadow_offset_x** float `Optional` `Example value: 0.0`

Horizontal subtitle shadow offset in output\-video pixel ASS units. Range: `[-32, 32]`. Default: `0`.

**subtitle_shadow_offset_y** float `Optional` `Example value: 0.0`

Vertical subtitle shadow offset in output\-video pixel ASS units. Range: `[-32, 32]`. Default: `0`.

**subtitle_shadow_blur** float `Optional` `Example value: 0.0`

Gaussian blur strength applied to the entire separate shadow layer, including the glyph fill. It does not affect the main subtitle text or its outline. Range: `[0, 10]`. Default: `0`.

**subtitle_line_spacing** float `Optional` `Example value: 0.0`

Extra spacing between subtitle lines in output\-video pixel ASS units. Range: `[0, 64]`. Default: `0`.

**subtitle_width_ratio** float `Optional` `Example value: 0.88`

Maximum visual width of the subtitle text layout, including the text, main outline, and shadow, divided by the video width. Range: `[0.1, 1]`. Default: `0.88`. Background padding is applied after text layout, so the background may extend beyond this width without changing text wrapping.

**subtitle_top_margin_ratio** float `Optional` `Example value: 0.77`

Distance from the nominal top edge of the subtitle block to the top edge of the video, divided by the video height. Range: `[0, 1)`. Default: `0.77`. A value that is too large places the subtitle block too close to the bottom of the video and may cause subtitles to be partially clipped or not fully visible.

**callback** Callback `Optional`

Task\-status callback configuration. After `callback.url` is configured, a POST request is sent to this address when the task status changes. If omitted, use Poll to query the task status and result.

**url** string 必选 `Example value: https://example.com/callback`

Callback URL. By default, only publicly accessible HTTPS URLs are supported.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-xxx`

Async task ID used to query task status and results.

**task_status** string `Example value: PENDING`

Task status. Possible values: `PENDING`, `RUNNING`, `COMPLETED`, `FAILED`, `TIMEOUT`.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

Error message returned when an exception occurs.

### Example

**Request example:**

example1: Dynamic duration with original subtitle removal

```Bash
# Dynamic duration with original subtitle removal

# Please set INPUT_PATH to the TOS path of a video file stored under your account
export INPUT_PATH="tos://xxxx/sample.mp4"
# Please set OUTPUT_PATH_TEMPLATE to a writable TOS path under your account
export OUTPUT_PATH_TEMPLATE="tos://xxxx/output/"
# Submit the operator service request
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_translate",
    "operator_version": "v1",
    "callback": {
        "url": "https://example.com/callback"
    },
    "data": {
        "video_url": "$INPUT_PATH",
        "audio_language": "zh-CN",
        "output_languages": ["en-US"],
        "caption_formats": [".srt", ".ass"],
        "dubbing_mode": "high_quality",
        "enable_fast_mode": true,
        "enable_dynamic_duration": true,
        "enable_video_inpaint": true,
        "video_inpaint_params": {
            "model_level": "pro",
            "detection_mode": "standard_subtitle",
            "max_process_frames": -1,
            "output_video_mode": "balanced"
        },
        "output_dubbing_audio": false,
        "lip_translate": false,
        "burn_translated_subtitles": true,
        "subtitle_font_by_language": ["NotoSans-Regular"],
        "subtitle_font_size": 40,
        "subtitle_font_color": "#FFFFFF",
        "subtitle_outline_color": "#000000",
        "subtitle_outline_width": 2,
        "subtitle_top_margin_ratio": 0.77,
        "output_tos_path": "$OUTPUT_PATH_TEMPLATE"
    }
}'
```

example2: Use a Separate Picture Source for Subtitle Burn\-In

The picture source must match the original visual timeline, and its video\-stream duration must differ from the original by no more than 1 second. Set `burn_translated_subtitles` to `true`. Do not combine this mode with video restoration or specified dubbed\-audio lip sync.

```JSON
{
  "operator_id": "las_video_translate",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://xxxx/sample.mp4",
    "subtitle_video_url": "https://example.com/clean-video.mp4",
    "burn_translated_subtitles": true,
    "audio_language": "zh-CN",
    "output_languages": ["en-US"],
    "output_tos_path": "tos://xxxx/output/",
    "enable_dynamic_duration": true
  }
}
```

example3: Face Translation

```Bash
# Face Translation

{
  "operator_id": "las_video_translate",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://xxxx/sample.mp4",
    "audio_language": "zh-CN",
    "output_languages": ["en-US"],
    "output_tos_path": "tos://xxxx/output/",
    "lip_translate": true
  }
}
```

example4:Face Translation \- Fuzzy Speech\-Lip Matching

```Bash
# Face Translation - Fuzzy Speech-Lip Matching

# The following example still performs subtitle translation and TTS, but uses fuzzy speech-lip matching. This is suitable when the input video's speech and lip movements are out of sync:

{
  "operator_id": "las_video_translate",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://xxxx/sample.mp4",
    "audio_language": "zh-CN",
    "output_languages": ["en-US"],
    "output_tos_path": "tos://xxxx/output/",
    "lip_translate": true,
    "lip_translate_param": {
      "lip_fuzzy_matching": true
    }
  }
}
```

example5: Face Translation \- Lip Sync to External Dubbed Audio

```Bash
# Face Translation - Lip Sync to External Dubbed Audio

# The following example replaces the input video's audio track with the specified audio and generates a video with lip movements synchronized to that audio:

{
  "operator_id": "las_video_translate",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://xxxx/sample.mp4",
    "output_tos_path": "tos://xxxx/output/",
    "lip_translate": true,
    "lip_translate_param": {
      "dubbing_audio": {
        "source": "url",
        "url": "tos://xxxx/dubbing.wav",
        "language": "en-US"
      }
    }
  }
}
```

example6:Face Translation \- Lip Sync to the Video's Own Audio Track

```Bash
# Face Translation - Lip Sync to the Video's Own Audio Track

{
  "operator_id": "las_video_translate",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://xxxx/sample.mp4",
    "audio_language": "zh-CN",
    "output_tos_path": "tos://xxxx/output/",
    "lip_translate": true,
    "lip_translate_param": {
      "dubbing_audio": {
        "source": "video"
      }
    }
  }
}
```

**Response example:**

```JSON
{
  "metadata": {
    "task_id": "task-20251125163544-abc123",
    "task_status": "PENDING",
     "business_code": "0",
    "error_msg": ""
  }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |The parameter is invalid. |Invalid parameter |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.InValid |The api key is invalid. |API is invalid |

## Poll

### API description

Query the execution status and result of the video translation task.

### Request parameters

**operator_id** string 必选 `Example value: las_video_translate`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**task_id** string 必选 `Example value: task-xxx`

Task ID

### Response parameters

**metadata** metadata

Request metadata.

**task_status** string `Example value: COMPLETED`

Task status.

* PENDING, task queued after submission

* RUNNING, in progress

* COMPLETED, completed

* FAILED, failed

* TIMEOUT, timed out

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.

**business_code** string `Example value: ApiKey.InValid`

Business code.

**error_msg** string `Example value: The api key is invalid.`

Detailed error message returned when an exception occurs.

**task_id** string `Example value: task-xxx`

Task ID in async mode.

**data** VideoTranslateResponse

Response data.

**video_url** string `Example value: tos://xxx/video.mp4`

Input video URL.

**video_duration** float `Example value: 72.3`

Input video duration. In dynamic duration mode, read each final output duration from the corresponding video file. In specified dubbed\-audio lip\-sync mode with duration mismatch ignored, this is the looped or trimmed duration used for billing.

**translated_captions** list of AssetSummary

Returned subtitle assets. In specified dubbed audio lip\-sync mode, subtitle translation is not performed and this field returns an empty list.

**language** string `Example value: en-US`

Output language of the asset. In specified dubbed audio lip\-sync mode, this field returns `lip_translate_param.dubbing_audio.language`.

**type** string `Example value: translated_caption`

Asset type. `translated_caption` indicates a subtitle file, `translated_video` indicates a dubbed video, and `translated_audio` indicates clean dubbed speech audio, which is returned only when `output_dubbing_audio=true`.

**format** string `Example value: .srt`

Subtitle file format. Returned only when `type=translated_caption`; supported values are `.ass`, `.txt`, `.srt`, `.xml`, and `.vtt`. The font and style in `.ass` match the subtitle control parameters in the Submit request; omitted parameters use their defaults. For `translated_video` and `translated_audio`, this field is empty.

**tos_path** string `Example value: tos://xxx/output/xxx.mp4`

Full TOS path after the asset is written, for example `tos://bucket/prefix/video_translate_demo_en-US.mp4`.

**presigned_url** string `Example value: https://...`

Temporary presigned URL with a 3\-day validity period. After it expires, use `tos_path` to generate a new link or access the target TOS path directly.

**translated_videos** list of AssetSummary

Returned translated assets, including `translated_video` and, when requested, `translated_audio`.

**language** string `Example value: en-US`

Output language of the asset. In specified dubbed audio lip\-sync mode, this field returns `lip_translate_param.dubbing_audio.language`.

**type** string `Example value: translated_caption`

Asset type. `translated_caption` indicates a subtitle file, `translated_video` indicates a dubbed video, and `translated_audio` indicates clean dubbed speech audio, which is returned only when `output_dubbing_audio=true`.

**format** string `Example value: .srt`

Subtitle file format. Returned only when `type=translated_caption`; supported values are `.ass`, `.txt`, `.srt`, `.xml`, and `.vtt`. The font and style in `.ass` match the subtitle control parameters in the Submit request; omitted parameters use their defaults. For `translated_video` and `translated_audio`, this field is empty.

**tos_path** string `Example value: tos://xxx/output/xxx.mp4`

Full TOS path after the asset is written, for example `tos://bucket/prefix/video_translate_demo_en-US.mp4`.

**presigned_url** string `Example value: https://...`

Temporary presigned URL with a 3\-day validity period. After it expires, use `tos_path` to generate a new link or access the target TOS path directly.

**repaired_videos** list of RepairedVideo

Returned when restoration is enabled. On translation success, contains one repaired source video shared by all target languages and its restoration task ID. If translation fails after a restoration task ID is obtained, it contains only `task_id`. Omitted when restoration is disabled or no restoration task ID exists.

**task_id** string `Example value: repair-task-xxx`

ID of the `las_video_inpaint_pro` restoration task. This differs from the Video Translation task ID in `metadata.task_id`.

**language** string `Example value: null`

Always `null`; the repaired source is not language\-specific.

**type** string `Example value: repaired_video`

Always `repaired_video`.

**format** string `Example value: mp4`

Repaired video format.

**tos_path** string `Example value: tos://xxx/output/repaired_video.mp4`

Original repaired\-video TOS path returned by the restoration operator.

**presigned_url** string `Example value: https://example.com/repaired.mp4`

Temporary repaired\-video download URL.

**video_duration** float `Example value: 12.05`

Repaired video\-stream duration. Its absolute difference from the original must not exceed 1 second.

### Example

**Request example:**

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_video_translate",
    "operator_version": "v1",
    "task_id": "task-20251125163544-abc123"
}'
```

**Response example:**

```JSON
{
  "metadata": {
    "task_id": "task-20251125163544-abc123",
    "task_status": "COMPLETED",
    "submit_time": "2026-07-21T16:04:06+08:00",
    "end_time": "2026-07-21T16:04:06+08:00",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "video_url": "tos://path/to/video_translate_demo.mp4",
    "video_duration": 12.05,
    "translated_captions": [],
    "translated_videos": [
      {
        "language": "en-US",
        "type": "translated_video",
        "tos_path": "tos://xxx/output/video_translate_demo_en-US.mp4",
        "presigned_url": "https://xxx/output/video_translate_demo_en-US.mp4"
      }
    ],
    "repaired_videos": [
      {
        "task_id": "repair-task-xxx",
        "language": null,
        "type": "repaired_video",
        "format": "mp4",
        "tos_path": "tos://xxx/output/repaired_video.mp4",
        "presigned_url": "https://xxx/output/repaired_video.mp4",
        "video_duration": 12.05
      }
    ]
  }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Operator.VersionInvalid |the operator version is invalid |The operator version is not supported. |
|400 |Connection.TooMany |Exceed max connections. |Rate limiting triggered due to excessive concurrency. |
|400 |Parameter.Missing |Missing required parameter. |Missing required parameters, such as `video_url`, `audio_language` or `output_languages` required for standard video translation, `audio_language` required when using the video's own audio track for lip sync, `output_tos_path`, or complete access credentials for the output TOS path. |
|400 |Parameter.Invalid |Invalid parameter. |Invalid parameter, including incompatible face translation/dynamic duration/restoration options, restoration combined with a separate picture source, invalid restoration options, or a picture/repaired\-video duration difference greater than 1 second. |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |Failed to verify access or write permissions for TOS path. |
|400 |Video.DownloadFailed |Video download failed. |Failed to download input video, which may be caused by unreachable URL, authentication failure, expired signature, network timeout, or storage service exception. |
|400 |Video.Invalid |Invalid video file. |Video file is corrupted, incomplete download, or unable to read video information. |
|400 |Video.FormatUnsupported |Video format not supported |Video format is not supported; only `.mp4`, `.mov`, `.avi`, `.mkv`, `.flv`, and `.webm` are supported. |
|400 |Video.FileTooLarge |Video file is too large. |Video file size exceeds 10 GB. |
|400 |Video.DurationTooShort |Video duration is too short |Video duration is less than 2 seconds. |
|400 |Video.DurationTooLong |Video duration is too long |Video duration exceeds 4 hours. |
|400 |Video.AudioMissing |Video has no audio track |The video has no audio track, so captions and dubbing cannot be generated. |
|400 |Video.AudioSeparationFailed |Audio separation failed |Failed to separate vocals from background music. |
|400 |Video.AsrFailed |ASR processing failed |ASR invocation or processing failed. |
|400 |Video.AsrNoSpeech |No recognizable speech in audio |No transcribable speech detected in the audio. |
|400 |Video.FrameExtractionFailed |Video frame extraction failed |Failed to extract video frames. |
|400 |Video.RefineFailed |Refine VLM call failed |Multimodal caption refinement call or parsing failed. |
|400 |Video.TranslateFailed |Translate VLM call failed |Translation to the target language or rewriting of dubbing text failed. |
|400 |Video.CaptionUploadFailed |Caption file upload failed |Failed to upload caption file. |
|400 |Video.DubbingInitFailed |Dubbing initialization failed |Failed to initialize dubbing model, timbre verification model, or related dependencies. |
|400 |Video.DubbingFailed |Dubbing processing failed |Failed to generate dubbing, verify timbre, align duration, or adjust speed. |
|400 |Video.ComposeFailed |Video composition failed |Failed to compose dubbed audio with the video, match faces, perform lip sync, or complete video restoration. In specified dubbed audio lip\-sync mode, this is also returned when no matching face is found for any speech segment. |
|400 |Video.Timeout |Video processing timed out |Face translation, dubbed audio speech recognition, or result download timed out. |
|400 |Video.OutputUploadFailed |Output upload failed |Failed to upload audio, video, or other output files. |
|400 |Video.ResourceInsufficient |Video processing resources are temporarily insufficient |Processing resources are temporarily insufficient. Please try again later. |
|400 |Task.NotFound |Task not found. |The task does not exist. |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication. |
|401 |ApiKey.InValid |The api key is invalid. |API Key is invalid. |
|500 |InternalError |Internal error |Internal service error. |
