---
title: "Viral clip generation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Viral_content_editing"
---

The Viral Clip Generation operator can automatically perform shot detection, semantic analysis, editing decision\-making, and video synthesis based on multiple episodes of short drama videos, generating multiple traffic\-attracting videos suitable for distribution on short video platforms in batches.

# Operator introduction

> Operator ID: las_viral_clip_gen

## Applicable scenarios

* **Short drama promotion**: Automatically edit multiple episodes of short dramas into traffic\-attracting content suitable for distribution on short video platforms, supporting batch production of multiple viral content videos in different styles.

   > **说明**

   > Currently, this is more suitable for hit material editing scenarios in vertical short drama videos. The editing effect for horizontal short drama videos is not as good as that for vertical videos.

## Core capabilities

* **Batch processing of multiple short drama episodes**: Input multiple episodes of short dramas at once to automatically complete all analysis and editing, and generate multiple viral content videos in batches.

* **Intelligent editing plan generation**: Automatically analyzes plot content and generates multiple editing plans (sequential editing/jump editing) to meet different delivery requirements.

* **Automatic removal of extraneous content**: Automatically detect and remove irrelevant frames, such as freeze frames and repeated content from previous or subsequent episodes.

* **Shot\-level semantic understanding**: Analyze the plot and rate the importance of each shot, outputting structured shot analysis results.

* **Script restoration**: Automatically reconstruct the complete script of multiple short drama episodes, including character relationships, scene structure, and plot development.

* **Rendering of the three key elements of short dramas**: Support adding drama titles, prompts, and corner labels to the content, adapting to vertical short drama scenarios.

* **Highlight frontloading**: Support placing highlight segments at the beginning of the content to quickly attract viewers' attention.

## Results demonstration

* Input video: EP01

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e472c17b08f4eb999cedc9ebdf331f3~tplv-goo7wpa0wc-image.image)

* Input video: EP02

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7c819aefc50a41f589d23eba5f61f2ad~tplv-goo7wpa0wc-image.image)

Example1:

* Output video: clip1

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e12c64aee1fb418c8cffc6ef23291cec~tplv-goo7wpa0wc-image.image)

* Output video: clip2

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cc49f600c3ba4ed9bc0d765aba36da45~tplv-goo7wpa0wc-image.image)

* Key Parameters

   ```Bash
   "mode": "sequential",
   "preset_intro": true,
           "drama_elements": {
               "template_name": "模板1",
               "title": "THE DASHWOOD FAMILY",
               "hint": "Film and television effects"
               }
   ```

Example2:

* Output video: clip1

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8fa1e5e03064afb8beaa6ca13109748~tplv-goo7wpa0wc-image.image)

* Output video: clip2

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e9d903973a11406b8afbc925b2ce0ab2~tplv-goo7wpa0wc-image.image)

* Key Parameters

   ```Bash
   "mode": "sequential",
   "preset_intro": false,
   ```

*

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Breakdown item |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Duration |Total duration depends on the length of each input material and the number of materials. The more inputs and the longer the duration, the longer the total processing time. |

# Input and output requirements

## Input requirements

|Breakdown |Detailed requirements |
|---|---|
|Supported input data modalities |Video |
|Input video: original video to be edited |* Format: `mp4`, `mov`, `avi`, `mkv`.<br><br>* Quantity: up to 100 videos can be input at a time.<br><br>* Size: each episode video must be at least 1 second and up to 10 minutes; the total duration of all episode videos input at one time must not exceed 2 hours, and the maximum total size is 10 GB.<br><br>* Resolution: all input videos must have the same resolution, and the video resolution must be between 360x640 (360 as the short side, 640 as the long side) and 1080x1920 (1080 as the short side, 1920 as the long side).<br><br>* Other requirements: ensure that the input videos contain subtitles. |
|Input video: preroll or postroll video |* Format: mp4, mov, avi, mkv.<br><br>* Preroll videos must contain a video stream with a duration greater than 0. Up to 20 preroll videos are supported.<br><br>* The resolution of the postroll video must be exactly the same as the resolution of the original video to be edited; otherwise, an error will occur. |
|Miniseries element length |* Miniseries title: maximum 200 characters by default.<br><br>* Miniseries hint text: maximum 100 characters by default. |
|Input path requirements |Provide input data to the operator via the request parameters `video_urls`, `preroll_urls`, and `postroll_url`. Currently, two methods are supported: public URL and TOS path.<br><br><br>* Public URL: A video URL accessible via the public network, with the format `http/https`.<br><br>   * Public URLs do not support addresses that require login status or additional header authentication; temporary URLs must remain valid during task execution.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide a TOS path in the format `tos://bucket_name/demo/`.<br><br>   * The TOS object must exist and have read permissions. |

## Output requirements

|Breakdown |Detailed requirements |
|---|---|
|Output data type |Video |
|Output path: TOS |Specify the storage path for the operator's output results via the request parameter `output_tos_path`. Currently, only TOS paths are supported.<br><br>TOS path: A directory in a TOS Bucket under the same primary account and region as the LAS service, with write permissions. Format: `tos://bucket/output/`. |

# Billing information

* Billing standards

   |Breakdown |Billing standards description |
   |---|---|
   |Billing items |Billing is calculated based on video duration. Billing items include two parts: **AI analysis fees for input videos** and **clip composition fees**. The total cost to be paid is the sum of all billing items. |
   |Billing type |Usage\-based billing, unit: `USD/minute`. Billing is generated hourly based on actual usage. Billing precision: millisecond\-level accuracy, rounded to the nearest millisecond |
   |Unit price |The unit price depends on the selected intelligent editing mode. Different editing modes have different unit prices. |

* Billing details

   Billing formula: `Total cost = AI analysis fees for all input videos + clip composition fees = ∑(unit price for input video analysis * input video duration) + unit price for clip composition * output video duration`

   |Billing items |Unit price |
   |---|---|
   |Input video analysis |* 0.25 USD/minute<br><br>* When multiple videos are input, each video incurs AI analysis fees. |
   |Output video from clip composition |0.01 USD/minute |

* Billing example

   * Example scenario: 10 short videos, each 3 minutes long, are input. After processing by the algorithm, a 1\-minute viral clip is generated. The cost is as follows:

   * Cost details:

      `Total cost = 10 * 3 minutes * 0.25 USD/minute + 1 minute * 0.01 USD/minute = 7.51 USD`

* Billing unit

   The current bill generated by invoking this operator displays the billing unit as "Video intelligent editing" in the bill details. Please note this difference when reviewing your bill.

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Usage recommendations

### Quick experience

You can use the sample code below, replacing `LAS_API_KEY`, `output_tos_path`, and the video URL to be processed, to quickly submit a viral content editing task. Poll the task status and obtain the edited result once processing is complete.

### Parameter configuration best practices

To help you efficiently generate high\-conversion\-rate materials for ad placement, we provide the following parameter configuration best practices based on industry experience in short drama advertising:

* **Input video**: It is recommended to select the **first 10–20 free episodes of the short drama** as the input source for highlight analysis. These episodes are key to attracting new users. Mixing segments with dramatic conflicts and high\-impact plot twists from these episodes can effectively increase click\-through and conversion rates for advertising materials.

* **Target generated duration**: Advertising materials typically have a fixed duration range. You can control the total duration of the generated highlight compilation using the min_clip_duration and max_clip_duration parameters:

   * **1–3 minute material**: Set min_clip_duration to 60 and max_clip_duration to 180.

   * **3–5 minute material**: Set min_clip_duration to 180 and max_clip_duration to 300.

   * **5–7 minute material**: Set min_clip_duration to 300 and max_clip_duration to 420.

* **Intelligent highlight pre\-roll**: It is recommended to enable the intelligent highlight pre\-roll feature and use the system default configuration. By default, the system will place the most exciting 5–15 second segments at the beginning of the material, and each placed segment will consist of sub\-clips no shorter than 5 seconds. This configuration is designed to quickly capture users' attention and is an effective means of increasing advertising conversion rates.

### Stability guarantee

* It is recommended to add a retry mechanism on the client side to handle occasional network fluctuations or service rate limiting.

## API usage instructions

* The API for this operator is an asynchronous task interface. You need to submit a task via the submit interface, then use the Poll interface to check the task status and obtain the operator processing result. Meanwhile, this operator supports asynchronous callback capability (Callback). You can set the callback parameter `callback.url` when initiating the operator task. LAS will send an HTTP POST notification to this URL. For guidance on using asynchronous callbacks, refer to [Asynchronous callback API](https://docs.byteplus.com/docs/Byteplus_LAS/Asynchronous_callback_API).

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, the `task_id` cannot be used to retrieve the operator's processing result.

## Submit

### API description

Submit a Viral Clip Generation task. After successful submission, a task ID is returned, and the processing result can be obtained through the query interface.

### Request parameters

**operator_id** string 必选 `Example value: las_viral_clip_gen`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**data** ViralClipGenReqParams 必选

Video editing request parameters

**video_urls** list of string 必选 `Example value: ["tos://xxx/ep1.mp4"]`

List of short drama video URLs. TOS and HTTPS URLs are supported.

The operator will strictly determine the episode number according to the order in the list (that is, the first URL is regarded as episode 1, and so on). Please ensure the list is correctly sorted by episode order before submitting. Please ensure that the input videos contain subtitles. The video resolution must be between 360x640 (360 is the short side, 640 is the long side) and 1080x1920 (1080 is the short side, 1920 is the long side), and all video resolutions must be consistent.

* A maximum of 100 videos can be input at once.

* Each episode must be at least 1 second and no longer than 10 minutes.

* The total duration of all videos can be up to 2 hours; the total size can be up to 10 GB.

* Supported formats: mp4, mov, avi, mkv.

**output_tos_path** string 必选 `Example value: tos://bucket/output/`

TOS directory for output results.

**min_clip_duration** integer `Example value: 180`

Minimum material duration (seconds), default is 180, range is [5, 2400]. If set too high, suitable segments may not be found.

**max_clip_duration** integer `Example value: 300`

Maximum material duration (seconds), default is 300, range is [5, 2400]. Must be greater than or equal to min_clip_duration. It is recommended to set an appropriate range, as setting it too large or too small may result in not finding suitable segments.

**playback_speed** integer `Example value: 1.0`

Maximum number of edited materials, default is 10, range is [1, 300]. The actual number of generated materials depends on the duration and content of the input video. The larger the number set, the higher the probability of content duplication among materials.

**playback_speed** float `Example value: 1.0`

Playback speed multiplier for output materials, default is 1.0 (normal speed), range is [0.5, 2.0]. Speed adjustment is performed before editing, and the actual playback duration of the output material is still controlled by min_clip_duration and max_clip_duration. For example, if speed=2.0 and min_clip_duration=30, a 30\-second 2x speed material will be output (covering approximately 60 seconds of original content).

**mode** string `Example value: sequential`

Editing mode. Optional values:

* **sequential (sequential editing)** : Selects consecutive segments in chronological order to ensure narrative completeness.

* **jump_cut (jump cut)** : Selects consecutive segments in chronological order to ensure narrative completeness, skips dull segments, retains highlights, and creates a more compact rhythm. Default is sequential.

**preset_intro** boolean `Example value: false`

reset intro switch:

* **true**: Enable for all output clips

* **false**: Disabled (default).Cannot be specified together with preset_intro_ratio.

**preset_intro_ratio** float `Example value: false`

Preset intro ratio. Range: [0.0, 1.0]. Adds preset intros proportionally. For example, 0.5 means that 50% of the output clips will have a highlight preset intro at the beginning. Cannot be specified together with preset_intro.

**drama_elements** DramaElements

Drama element configuration for short drama, suitable for vertical screen scenarios. Rendering effects include title, prompt text, and corner mark. By default, drama elements are not added. Drama elements are added only if drama_elements is specified in the request.

**title** string `Example value: 《Attack LAS operator》`

Drama title. Leave blank to not add. Maximum 200 characters by default.

If the drama title is too long, it will automatically wrap to the next line.

Supports adding \n to control line breaks. For example, "This is a title with a line break\n" will be split into two lines at the \n position.

**hint** string `Example value: Film effect. Do not imitate. Does not promote negative values.`

Hint text. Leave blank to omit. Maximum 100 characters by default.

**include_badge** boolean `Example value: true`

Whether to add a badge.

**template_name** string `Example value: 模板1`

Template name. Optional values:

* 模板1 (Title centered at the top + hint text vertically on the left + badge "Popular Short Drama" in the upper right corner)

* 模板2 (Title centered at the top + hint text vertically on the right + badge "Currently Trending" in the upper right corner)

* 模板3 (Title centered at the top + hint text vertically on the left + badge "Recommended Hit" in the upper right corner).

**title_font_size** integer `Example value: 50`

Title font size, default is 50, range is [20, 150]. It is recommended to use font size 50 to avoid the font being too large and blocking the screen, which affects viewing.

**title_opacity** float `Example value: 1.0`

Title opacity, default is 1.0 (fully opaque), range is [0.3, 1.0].

**title_position** string `Example value: top_center`

Title position, optional values:

* top_left: Top left corner.

* top_center: Top center.

* top_right: Top right corner.

* bottom_left: Bottom left corner.

* bottom_center: Bottom center.

* bottom_right: Bottom right corner. Default: top_center.

**use_subdir** boolean `Example value: false`

Whether to automatically create subdirectories under output_tos_path. Default is false; output files are written directly to output_tos_path. When enabled, a subdirectory in the format `{ task_id}_{ timestamp}` will be created under output_tos_path to prevent results from multiple requests from overwriting each other.

**postroll_url** string `Example value: tos://bucket/postroll.mp4`

Postroll video URL (supports tos and https addresses). When specified, the postroll video will be automatically appended to the end of each output material.

Requirement: The resolution of the postroll video must be exactly the same as the input short drama video, otherwise an error will occur. Supports mp4, mov, avi, mkv formats.

**preroll_urls** list of string `Example value: ["tos://bucket/preroll1.mp4", "tos://bucket/preroll2.mp4"]`

List of preroll video URLs. TOS and HTTPS URLs are supported, with a maximum of 20 URLs. When specified, one video from the list is randomly selected and prepended to each output clip. The output clip duration includes the preroll. Supported formats are mp4, mov, avi, and mkv. Each preroll file must contain a video stream with a duration greater than 0.

**aspect_ratio** string `Example value: 9:16`

Output aspect ratio. Currently, only `9:16` is supported. When specified, all output clips are normalized to portrait 9:16. Landscape input is scaled proportionally and padded with black bars at the top and bottom without cropping. When omitted, the output aspect ratio follows the input.

**callback** Callback

Task status callback configuration. After configuring callback.url, a POST request will be sent to this address when the task status changes; if not configured, you can query the task status and result through Poll.

**url** string 必选 `Example value: https://example.com/callback`

Callback address. By default, only HTTPS addresses accessible from the public network are supported.

### Response parameters

**metadata** metadata

Request metadata.

**task_id** string `Example value: task-xxx`

Task ID in asynchronous mode, used for job status queries.

**task_status** string `Example value: PENDING`

Task status in asynchronous mode. PENDING: request received, RUNNING: running, COMPLETED: completed, FAILED: failed, TIMEOUT: timed out.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

If an exception occurs, detailed exception information will be returned.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_viral_clip_gen",
    "operator_version": "v1",
    "data": {
        "video_urls": ["tos://xxx/episode1.mp4", "tos://xxx/episode2.mp4"],
        "output_tos_path": "tos://bucket/output/",
        "mode": "sequential",
        "min_clip_duration": 120,
        "max_clip_duration": 240,
        "max_clip_count": 50,
        "aspect_ratio": "9:16",
        "preroll_urls": [
            "tos://bucket/preroll1.mp4",
            "tos://bucket/preroll2.mp4"
        ],
        "drama_elements": {
            "title": "《Attack LAS operator》",
            "hint": "Film and television effects, please do not imitate, no bad values guide",
            "include_badge": true,
"template_name": "模板1",
            "title_font_size": 50,
            "title_opacity": 1.0,
            "title_position": "top_center"
        },
        "preset_intro": true
    }
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "20250108_150000_abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |invalid parameter |Invalid parameter (for example, video count exceeds 100, inconsistent resolution, resolution lower than 640x360, drama_elements.template_name is invalid, and so on) |
|400 |Parameter.Missing |Missing required parameter |Missing required parameter |
|400 |Url.Invalid |invalid url |The video URL is inaccessible or does not exist |
|400 |Video.Invalid |invalid video file |The video file is invalid (no video stream, resolution too low, and so on) |
|400 |Video.DownloadFailed |Video download failed |Video download error or access failure |
|400 |Video.FormatUnsupported |Video format not supported |Video format not supported (only mp4, mov, avi, mkv are supported) |
|400 |Video.DurationTooShort |Video duration is too short |Video duration is too short (single episode < 1s) |
|400 |Video.DurationExceeded |Video duration exceeds maximum limit |Video duration exceeds limit (single episode \> 600s or total duration \> 7200s) |
|400 |Video.FileTooLarge |Video file is too large |Video file is too large (total size \> 10GB) |
|400 |Video.Timeout |Video processing timeout |Video processing timed out |
|400 |Video.UploadFailed |Video upload failed |Video upload failed |
|400 |Video.ClipFailed |Video clip extraction failed |Video clip extraction failed |
|400 |Video.VLMFailed |VLM call failed |VLM model invocation failed |
|400 |Video.ModelFailed |VLM call failed |VLM model invocation failed |
|400 |Video.FrameExtractionFailed |Video frame extraction failed |Video frame extraction failed |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |Failed to access TOS path |
|400 |Connection.TooMany |Too many connections |Too many concurrent requests, triggering rate limiting. |
|400 |ViralClipGen.AsrFailed |ASR generation failed |Speech recognition failed |
|400 |ViralClipGen.SceneFailed |scene detection failed |Scene detection failed |
|400 |ViralClipGen.ScriptFailed |script generation failed |Script generation failed |
|400 |ViralClipGen.BoundaryFailed |boundary detection failed |Episode boundary detection failed (freeze frame, next episode preview, previous recap, cross\-episode repetition, and so on) |
|400 |ViralClipGen.SubtitleFailed |embedded subtitle OCR failed |Embedded subtitle OCR failed |
|400 |ViralClipGen.ReviewFailed |review generation failed |Segment review/scoring failed |
|400 |ViralClipGen.JumpcutFailed |jumpcut generation failed |Jumpcut scheme generation failed |
|400 |ViralClipGen.RenderFailed |clip rendering failed |Clip rendering/upload failed |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.InValid |The api key is invalid. |API is invalid |
|500 |InternalError |Internal error |Internal service error |

## Poll

### API description

Query the execution status and result of a Viral Clip Generation task.

### Request parameters

**operator_id** string 必选 `Example value: las_viral_clip_gen`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**task_id** string 必选 `Example value: task-xxx`

Task ID

### Response parameters

**metadata** metadata

Requested metadata

**task_id** string `Example value: task-xxx`

Task ID

**task_status** string `Example value: COMPLETED`

Task status. ACCEPTED: Request received, RUNNING: In progress, COMPLETED: Finished, FAILED: Failed, TIMEOUT: Timed out.

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.

**business_code** string `Example value: 0`

Business code.

**error_msg** string

If there is an exception, detailed exception information will be returned.

**data** ViralClipGenResponse

Returned data

**total_clips** integer `Example value: 8`

Total number of segments meeting requirements.

**videos** list of SourceVideoInfo

List of original video information.

**episode** integer `Example value: 1`

Numbered according to the input order of the original videos.

**video_url** string `Example value: https://path/to/8.mp4`

Access method for the original video.

**file_size** integer `Example value: 132415150`

Original video byte size.

**duration** float `Example value: 65.0`

Original video duration (seconds).

**resolution** string `Example value: 360x640`

Video resolution.

**storyboard** list of SegmentInfo

Semantic storyboard list.

**id** string `Example value: ep8_seg24`

Original video storyboard segment ID.

**episode** integer `Example value: 8`

The original video number corresponding to the storyboard segment.

**start_sec** float `Example value: 86.72`

Start time (seconds) of the storyboard segment in the original video.

**end_sec** float `Example value: 103.04`

End time (seconds) of the storyboard segment in the original video.

**rating** string `Example value: S`

Storyboard segment importance rating, classified as S, A, B, or C. Importance decreases from S to C.

**highlight_score** integer `Example value: 95`

Storyboard segment highlight score.

**function_tags** list of string

The role of the current segment in the original video.

**content_desc** string `Example value: Xu Zhiyi delivers a tearful monologue, realizing that their family has moved their nephew's belongings into their own room...`

Description of the current segment's plot.

**asr** string `Example value: Why me`

ASR recognition result for the current segment.

**duration** float `Example value: 16.32`

Duration of the current segment (seconds).

**clips** list of ClipInfo

Clip list. Each element is a clip.

**id** string `Example value: clip_001`

Clip ID.

**url** string `Example value: tos://path/to/dir/clip_001.mp4`

Clip access address. If output_tos_path is not specified, this value is empty.

**preview_url** string `Example value: https://xxx/clip_001.mp4`

Temporary HTTPS link for the clip (valid for 3 days).

**duration** float `Example value: 160.04`

Clip duration (seconds).

**segment_count** integer `Example value: 31`

Number of original storyboard segments contained in the clip.

**timeline** list of SegmentRef

Details of original storyboard segments contained in the clip, in playback order within the clip.

**ref** string `Example value: ep8_seg24`

Referenced segment ID. When preroll or postroll is enabled, the prepended or appended segment uses `preroll` or `postroll`, respectively.

**clip_start_sec** float `Example value: 0.00`

Start time of the corresponding storyboard segment (ref) in the current clip.

**clip_end_sec** float `Example value: 16.32`

End time of the corresponding storyboard segment (ref) in the current clip.

**is_intro_dup** boolean `Example value: true`

Whether the current storyboard segment is a highlight introduction for the current clip.

**source_url** string `Example value: tos://bucket/preroll.mp4`

Returned when `ref` is `preroll` or `postroll`. The value is the user\-provided preroll or postroll video URL.

**script** ScriptInfo

Script reconstruction result.

**script_path** string `Example value: tos://bucket/xxx`

Script folder path.

**character_table_path** string `Example value: tos://bucket/xxx`

Global character table path.

**storyboard_json_path** string `Example value: tos://bucket/output/storyboard.json`

Storyboard result JSON file path (TOS address), containing complete structured storyboard data.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
    "operator_id": "las_viral_clip_gen",
    "operator_version": "v1",
    "task_id": "20250108_150000_abc123"
}'
```

#### Response example

```JSON
{
    "metadata": {
        "task_id": "20250108_150000_abc123",
        "task_status": "COMPLETED",
        "submit_time": "2026-07-21T16:04:06+08:00",
        "end_time": "2026-07-21T16:04:06+08:00",
        "business_code": "0",
        "error_msg": ""
    },
    "data": {
        "total_clips": 10,
        "storyboard_json_path": "tos://bucket/output/storyboard.json",
        "videos": [
            {
                "episode": 8,
                "video_url": "https://path/to/8.mp4",
                "file_size": 132415150,
                "duration": 65.0
            },
            {
                "episode": 9,
                "video_url": "https://path/to/9.mp4",
                "file_size": 123416235,
                "duration": 76.3
            }
        ],
        "storyboard": [
            {
                "id": "ep8_seg24",
                "episode": 8,
                "start_sec": 86.72,
                "end_sec": 103.04,
                "rating": "S",
                "highlight_score": 95,
                "function_tags": [
                    "钩子-情绪共鸣",
                    "冲突-原生家庭矛盾"
                ],
                "content_desc": "Xu Zhiyi delivers a tearful monologue, realizing that their family has moved their nephew's belongings into their own room..."
            },
            {
                "id": "ep9_seg3",
                "episode": 9,
                "start_sec": 10.76,
                "end_sec": 21.08,
                "rating": "S",
                "highlight_score": 95,
                "function_tags": [
                    "钩子-强冲突",
                    "爽点-直球出击"
                ],
                "content_desc": "Xu Zhiyi, wearing an off-white sweater, is writing. After hearing the phone ring, they answer it..."
            }
        ],
        "clips": [
            {
                "id": "clip_001",
                "url": "tos://path/to/dir/clip_001.mp4",
                "preview_url": "https://xxx/clip_001.mp4",
                "duration": 160.04,
                "segment_count": 31,
                "timeline": [
                    {
                        "ref": "preroll",
                        "clip_start_sec": 0.0,
                        "clip_end_sec": 5.06,
                        "source_url": "tos://bucket/preroll1.mp4"
                    },
                    {
                        "ref": "ep8_seg24",
                        "clip_start_sec": 5.06,
                        "clip_end_sec": 21.38
                    },
                    {
                        "ref": "ep8_seg19",
                        "clip_start_sec": 21.38,
                        "clip_end_sec": 31.42
                    },
                    {
                        "ref": "ep9_seg3",
                        "clip_start_sec": 31.42,
                        "clip_end_sec": 41.74,
                        "is_intro_dup": true
                    }
                ]
            }
        ]
    }
}
```

### Error code

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Invalid |invalid parameter |Invalid parameter |
|400 |Parameter.Missing |Missing required parameter |Missing required parameter |
|400 |Url.Invalid |invalid url |The video URL is inaccessible or does not exist |
|400 |Video.Invalid |invalid video file |The video file is invalid (no video stream, resolution too low, and so on) |
|400 |Video.DownloadFailed |Video download failed |Video download error or access failure |
|400 |Video.FormatUnsupported |Video format not supported |Video format is not supported |
|400 |Video.DurationTooShort |Video duration is too short |Video duration is too short |
|400 |Video.DurationExceeded |Video duration exceeds maximum limit |Video duration exceeds the limit |
|400 |Video.FileTooLarge |Video file is too large |Video file is too large |
|400 |Video.Timeout |Video processing timeout |Video processing timed out |
|400 |Video.UploadFailed |Video upload failed |Video upload failed |
|400 |Video.ClipFailed |Video clip extraction failed |Video clip extraction failed |
|400 |Video.ModelFailed |VLM call failed |VLM model invocation failed |
|400 |Video.FrameExtractionFailed |Video frame extraction failed |Video frame extraction failed |
|400 |Tos.AccessFailed |Failed to access TOS path with provided credentials |Failed to access TOS path |
|400 |Connection.TooMany |Too many connections |Too many concurrent requests, triggering rate limiting. |
|400 |ViralClipGen.AsrFailed |ASR generation failed |Speech recognition failed |
|400 |ViralClipGen.SceneFailed |scene detection failed |Scene detection failed |
|400 |ViralClipGen.ScriptFailed |script generation failed |Script generation failed |
|400 |ViralClipGen.BoundaryFailed |boundary detection failed |Episode boundary detection failed |
|400 |ViralClipGen.SubtitleFailed |embedded subtitle OCR failed |Embedded subtitle OCR failed |
|400 |ViralClipGen.ReviewFailed |review generation failed |Clip review failed |
|400 |ViralClipGen.JumpcutFailed |jumpcut generation failed |Clip scheme generation failed |
|400 |ViralClipGen.RenderFailed |clip rendering failed |Clip rendering/upload failed |
|401 |Authorization.Missing |Missing Authorization. |Missing authentication |
|401 |ApiKey.InValid |The api key is invalid. |API is invalid |
|500 |InternalError |Internal error |Internal service error |
