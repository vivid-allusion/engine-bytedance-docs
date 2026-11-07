---
title: "Video scene segmentation"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_scene_segmentation"
---

The video scene segmentation operator uses a multimodal large model to perform shot/scene segmentation, global character recognition, scene\-level character association, and character image extraction on the input video. The operator outputs scene summary results, a character registry, sliced videos for each scene, and image files archived by character, facilitating subsequent retrieval, editing, and content understanding.

# Operator introduction

> Operator ID: las_video_scene_seg

## Core capabilities

* Supports scene segmentation based on VLM, and also supports equal\-duration segmentation when `min_segment_duration == max_segment_duration`.

* Equal\-duration segmentation merges a short tail into the preceding segment. The source ending is preserved without padding or discarded frames, so only the final segment may exceed the configured maximum.

* Supports global character extraction and deduplication aggregation, generating a character registry.

* Supports character association within scenes with character IDs, display names, and available bounding boxes. Appearance intervals and candidate\-keyframe fields are not returned by this API.

* Supports automatic extraction of independent video files for each scene.

* Supports extracting and filtering representative images for each character, outputting them archived by character.

## Effect demonstration

---

**[Input video and output segmented video]**

* [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e472c17b08f4eb999cedc9ebdf331f3~tplv-goo7wpa0wc-image.image)

* [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8341c643d74846ff9aa7339fac6f4173~tplv-goo7wpa0wc-raw.image)

* [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc7048b850004c4f8fb39610bcb018c2~tplv-goo7wpa0wc-raw.image)

* [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e1788da3e4a3489785fc4325a2db6eff~tplv-goo7wpa0wc-raw.image)

---

**[Output character images]**

* Character 1

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b952134e930c49cab12cf0b1b4f52663~tplv-goo7wpa0wc-topic.webp)

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c1bed482146414cb5904c977c1065ac~tplv-goo7wpa0wc-topic.webp)

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b370516f6d54beeaabb8b77201d551a~tplv-goo7wpa0wc-topic.webp)

* Character 2

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1406cd1511fb4bbab3e347a41afd6bc7~tplv-goo7wpa0wc-topic.webp)

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da4aeb15a7964e5ab5c70db5bcbd18fa~tplv-goo7wpa0wc-topic.webp)

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d249cf46fe414aba88d68789f0967129~tplv-goo7wpa0wc-topic.webp)

* Scene storyboard image

   * Manor Hall

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24bfcc7929ff4941837a9297de3f14d2~tplv-goo7wpa0wc-topic.webp)

   * mansion corridor

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/25d8e0dfa62b463fbf9cd2bd74ac52c3~tplv-goo7wpa0wc-topic.webp)

* Prop image

   * Tapestry

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/968ddb3f852847b69cca317886a9273b~tplv-goo7wpa0wc-topic.webp)

   * Folding fan

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f91553eff8084d128b0c2b2211d005b7~tplv-goo7wpa0wc-topic.webp)

   * candlestick

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e0b6c437333849209ad734fc2b97a8c9~tplv-goo7wpa0wc-topic.webp)

The above are sample results for some outputs.

---

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Sub\-item |Performance impact description |
|---|---|
|Maximum RPM |600 |
|Maximum concurrency |10 |
|Processing time |* Total processing time is mainly affected by video duration, frame extraction rate, number of characters, number of scenes, and number of VLM calls.<br><br>* The operator relies on VLM calls; the longer the video, the more characters, and the more complex the scenes, the higher the overall processing time. |

# Input and output requirements

## Input requirements

|Subdivision |Detailed requirements |
|---|---|
|Supported input data modalities |Video |
|Input format: Video |Size: The current version limits video duration to within 20 minutes. |
|Input path requirements |Provide operator input data via the request parameter `video_url`. Currently, public URL and TOS path are supported.<br><br><br>* Public URL: A publicly accessible URL, in the format `http/https`.<br><br>   * Public URLs that require login status or additional header authentication are not supported; temporary URLs must be valid during task execution.<br><br>* TOS path: After uploading the data to be processed to a TOS Bucket under the same primary account and region as the current LAS service, you can provide the TOS path in the format `tos://bucket_name/demo`.<br><br>   * The TOS object must exist and have read permissions. |

## Output requirements

|Subdivision |Detailed requirements |
|---|---|
|Output data modalities |* Video (segmented video clips)<br><br>* Text (character registry<br><br>* Image (segmentation screenshots, character representative images |
|Output path: TOS |Specify the storage path for the operator output results via the request parameter `output_tos_path`. It must be a writable TOS directory owned by the current account and in the same region as the task.<br><br>TOS path: Under the same primary account and region as the LAS service, a TOS Bucket directory with write permissions. Format: `tos://bucket/output/`. |

# Billing information

* Billing standard

   |Breakdown |Billing standard description |
   |---|---|
   |Billing item |Usage is calculated based on **the duration of the input video**. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual usage. Billing accuracy: millisecond\-level accuracy, rounded to the nearest millisecond |
   |Unit price |0.25 USD/minute |

* Billing details

   Billing formula: `Total cost = unit price * usage`

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## API usage instructions

* The API for this operator is an asynchronous task interface. You need to submit a task via the submit interface, then use the Poll interface to check the task status and obtain the operator processing result. Meanwhile, this operator supports asynchronous callback capability (Callback). You can set the callback parameter `callback.url` when initiating the operator task. LAS will send an HTTP POST notification to this URL. For guidance on using asynchronous callbacks, refer to [Asynchronous callback API](https://docs.byteplus.com/docs/Byteplus_LAS/Asynchronous_callback_API).

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, the `task_id` cannot be used to retrieve the operator's processing result.

## Submit

### Interface description

Submitting an asynchronous task using the video scene segmentation operator supports scene segmentation, character extraction, scene slicing, and result upload. A successful response with `task_status=PENDING` means the task has been accepted; use Poll to determine whether video processing succeeds.

### Request parameters

**operator_id** string 必选 `Example value: las_video_scene_seg`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**data** VideoSceneSegUserReqParams 必选

Request parameters for video scene segmentation and character localization

**video_url** string/list of string 必选 `Example value: tos://example/sample_video.mp4`

A single video URL or a non\-empty list of video URLs. Supports `http/https` and `tos://bucket/key`. Multi\-video results preserve an independent source timeline for each video.

**output_tos_path** string 必选 `Example value: tos://bucket/output/`

Root output directory. It must be a writable TOS directory owned by the current account and in the same region as the task. The operator appends a task\-specific subdirectory and uploads JSON, scene videos, and asset images.

**min_segment_duration** float `Optional` `Example value: 4.0`

Minimum duration per scene in seconds. Default: `4.0`; range: `1.0–100.0`. The effective bounds must satisfy `min_segment_duration <= max_segment_duration`. A video shorter than the minimum, or bounds that cannot be satisfied on the source frame grid, fails with `Parameter.Invalid`.

**max_segment_duration** float `Optional` `Example value: 10.0`

Maximum duration per scene in seconds. Default: `10.0`; range: `1.0–100.0`. Equal minimum and maximum values select uniform splitting. A short tail is merged into the preceding segment, so only the final segment may exceed the maximum.

**seg_mode** string `Optional` `Example value: precise`

Scene segmentation mode: `precise` or `rough`. Default: `precise`. Both modes use 4–10 seconds as the default duration range and do not guarantee a segment count.

**output_language** string `Optional` `Example value: en`

Language for generated descriptions and asset display names: `zh` (default) or `en`. IDs, times, URLs, and source dialogue remain unchanged.

**callback** Callback `Optional`

Task status callback configuration. After configuring callback.url, a POST request will be sent to this address when the task status changes; if not configured, you can query the task status and result through Poll.

**url** string 必选 `Example value: https://example.com/callback`

Callback address. By default, only HTTPS addresses accessible from the public network are supported.

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Task ID in asynchronous mode, used for job status queries.

**task_status** string `Example value: PENDING`

Task status in asynchronous mode.

* PENDING, request received

* RUNNING, running

* COMPLETED, completed

* FAILED, failed

* TIMEOUT, timed out

**business_code** string `Example value: 0`

Business code. When nonzero, read `error_msg`; use `task_status` to determine whether the task is complete.

**error_msg** string

If an exception occurs, detailed error information will be returned.

### Example

#### Request example

```Bash
# Set OUTPUT_TOS_PATH to a writable TOS path in the same region as the task
export OUTPUT_TOS_PATH="tos://path/to/scene_seg_results"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" --header "Content-Type: application/json" --header "Authorization: Bearer $LAS_API_KEY" --data '{
    "operator_id": "las_video_scene_seg",
    "operator_version": "v1",
    "callback": {
        "url": "https://example.com/callback"
    },
    "data": {
        "video_url": "https://example.com/sample_video.mp4",
        "output_tos_path": "$OUTPUT_TOS_PATH",
        "min_segment_duration": 4.0,
        "max_segment_duration": 10.0,
        "seg_mode": "precise"
    }
}'
```

#### Response example

```JSON
{
    "metadata": {
        "task_id": "task-20260323153012-abc123",
        "task_status": "PENDING",
        "business_code": "0",
        "error_msg": ""
    }
}
```

## Poll

### Interface description

Query the execution status and result of a Video Scene Segmentation task. HTTP 200 means the query succeeded, not that video processing succeeded. Read result data only when `task_status=COMPLETED` and `business_code="0"`; missing qualified character reference images alone do not fail the task.

### Request parameters

**operator_id** string 必选 `Example value: las_video_scene_seg`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**task_id** string 必选 `Example value: task-xxx`

Task ID

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Task ID in asynchronous mode.

**task_status** string `Example value: COMPLETED`

Task status in asynchronous mode.

* PENDING, task submitted and queued

* RUNNING, in progress

* COMPLETED, task completed

* FAILED, failed

* TIMEOUT, timed out

**submit_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task submission time, in ISO 8601 timestamp format.

**end_time** string `Example value: 2026-07-21T16:04:06+08:00`

Task end time, in ISO 8601 timestamp format.

**business_code** string `Example value: 0`

Business code. When nonzero, read `error_msg`; use `task_status` to determine whether the task is complete.

**error_msg** string

If an exception occurs, detailed error information will be returned.

**data** VideoSceneSegResponse

Summary and result\-file URLs when completed. Before completion or on failure, this object may be absent or contain zero\-valued summary fields.

**video_duration** float `Example value: 98.4`

Total duration (seconds) of the input video.

**segment_count** integer `Example value: 12`

Number of segmented scenes.

**character_count** integer `Example value: 5`

Number of globally recognized characters.

**segments_url** string `Example value: tos://bucket/output/<run_id>/segments.json`

Scene result JSON URL. A single video produces a segment array; multiple videos produce an object with `episodes`, each containing its source `video_url` and local timeline.

**characters_registry_url** string `Example value: tos://bucket/output/<run_id>/characters_registry.json`

Character registry JSON URL. It may be absent when no characters are identified. Characters without a qualified reference image remain in the registry and are marked as requiring a new image.

**prop_registry_url** string `Example value: tos://bucket/output/<run_id>/prop_registry.json`

Prop registry JSON URL; may be absent or null when no corresponding assets have usable reference images.

**scene_registry_url** string `Example value: tos://bucket/output/<run_id>/scene_registry.json`

Scene registry JSON URL; may be absent or null when no corresponding assets have usable reference images.

**shot_registry_url** string `Example value: tos://bucket/output/<run_id>/shot_registry.json`

Shot registry JSON URL. Multi\-video results are grouped by episode; use `global_segment_id` to distinguish identical local segment IDs from different videos.

**storyboard_bundle_url** string `Example value: tos://bucket/output/<run_id>/storyboard_bundle_manifest.json`

Standard `storyboard_bundle_v2` manifest URL with `storage_mode=split`; read optional registries only when present.

**resolution** string `Example value: 1920x1080`

Measured source\-video resolution; may be absent when unavailable.

#### segments.json

**segment_id** string `Example value: scene_001`

Local scene ID; it may repeat across videos.

**global_segment_id** string `Example value: ep_001_scene_001`

Globally unique multi\-video segment ID used to correlate results across videos.

**episode_id** string `Example value: ep_001`

Source episode identifier.

**episode_index** integer `Example value: 1`

Source episode order, starting at 1.

**start_time** float `Example value: 0`

Start time in the source video, in seconds; includes the corresponding frame.

**end_time** float `Example value: 7`

End time in the source video, in seconds; excludes the corresponding frame.

**duration** float `Example value: 7`

Actual segment duration, including fractional seconds. When a short tail is merged during uniform splitting, only the final segment may exceed `max_segment_duration`.

**scene_type** string

Scene type or short label.

**description** string

Scene description.

**video_path** string

Scene clip URL; it may be null when export or upload fails. Task completion does not guarantee that every clip can be downloaded.

**characters** array of SegmentCharacterInfo

Characters associated with the scene.

**character_id** string

ID in the global character registry; may be null when unbound.

**alias** string

Character display name in the selected `output_language`.

**bbox** array of integer `Example value: [120,80,760,980]`

Optional bounding box `[xmin, ymin, xmax, ymax]` in 0–1000 coordinates.

The `characters_registry.json` file has the following structure:

* **characters** array of CharacterRegistryItem

   Global character registry.

   * **character_id** string

      Character ID within the current task result.

   * **alias** string

      Primary character alias.

   * **description** string

      Character description.

   * **category** string `Example value: female`

      Character category, such as `male`, `female`, `boy`, or `girl`.

   * **scene_count** integer

      Number of scenes in which the character appears.

   * **appeared_segments** array of string

      Scene IDs in which the character appears.

   * **total_duration** float

      Total appearance duration in seconds.

   * **character_images** array of object

      Selected usable reference images. This list may contain fewer than three entries or be empty; unclear\-face or wrong\-identity images are not retained merely to fill a quota.

   * **reference_status** string `Example value: active`

      Reference\-image status: `active` when a qualified image exists, `pending` when a new image is required, or `stale` when an earlier image is no longer valid.

   * **needs_new_reference_image** boolean `Example value: false`

      Whether a new character reference is required. Analysis remains usable when `true`; generation requiring character consistency should add an image first.

   * **reference_stale_reason** string

      Reason the reference is pending or stale; empty when not applicable.

   * **aliases** array of string

      Merged alias list.

* **total_count** integer

   Total number of global characters.

* **version** string

   Result version.

* **video_duration** float

   Total video duration in seconds.

* **total_frames** integer

   Total number of frames used during processing.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" --header "Content-Type: application/json" --header "Authorization: Bearer $LAS_API_KEY" --data '{
    "operator_id": "las_video_scene_seg",
    "operator_version": "v1",
    "task_id": "task-20260323153012-abc123"
}'
```

#### Response example

```JSON
{
    "metadata": {
        "task_id": "task-20260323153012-abc123",
        "task_status": "COMPLETED",
        "submit_time": "2026-07-21T16:04:06+08:00",
        "end_time": "2026-07-21T16:04:06+08:00",
        "business_code": "0",
        "error_msg": ""
    },
    "data": {
        "video_duration": 98.4,
        "segment_count": 12,
        "character_count": 5,
        "segments_url": "tos://path/to/scene_seg_results/9f4b7c3d12ab_20260323_153012/segments.json",
        "characters_registry_url": "tos://path/to/scene_seg_results/9f4b7c3d12ab_20260323_153012/characters_registry.json",
        "prop_registry_url": "tos://path/to/scene_seg_results/9f4b7c3d12ab_20260323_153012/prop_registry.json",
        "scene_registry_url": "tos://path/to/scene_seg_results/9f4b7c3d12ab_20260323_153012/scene_registry.json",
        "shot_registry_url": "tos://path/to/scene_seg_results/9f4b7c3d12ab_20260323_153012/shot_registry.json",
        "storyboard_bundle_url": "tos://path/to/scene_seg_results/9f4b7c3d12ab_20260323_153012/storyboard_bundle_manifest.json"
    }
}
```

## Error code

|HttpCode |Error code |Error message |Description |
|---|---|---|---|
|400 |TaskId.Missing |The task id is missing. |`task_id` is missing or empty. |
|200 |TaskId.Invalid |The task does not exist. |The task does not exist or is not visible to this account. |
|200 |Parameter.Invalid |The parameter is invalid. |Duration bounds are invalid, the video is shorter than the minimum, or no valid frame partition exists. |
|200 |Url.Invalid |The url is invalid. |The video URL is invalid. |
|200 |Video.Invalid |The video file is invalid. |The video file is invalid or cannot be parsed. |
|200 |Video.DownloadFailed |Video download failed. |The video could not be downloaded. |
|200 |Video.FormatUnsupported |Video format not supported. |The video format is unsupported. |
|200 |Video.DurationExceeded |Video duration exceeds maximum limit. |The video exceeds the processing\-duration limit. |
|200 |Video.FileTooLarge |Video file is too large. |The video exceeds the processing\-size limit. |
|200 |Video.DurationTooShort |Video duration is too short. |The video is shorter than the minimum duration. |
|200 |Video.Timeout |Video processing timeout. |Video processing timed out. |
|200 |Model.Timeout |Model request timed out. |The model request timed out. |
|200 |Model.RateLimited |Model service rate limit reached. |Retry later. |
|200 |Model.OutputInvalid |Model output structure is inconsistent. |The model output is empty or unusable. |
|200 |Video.ModelFailed |VLM call failed. |Inspect the error, then retry or contact support. |
|200 |Video.FrameExtractionFailed |Video frame extraction failed. |Frame extraction failed. |
|200 |Video.ClipFailed |Video clip extraction failed. |Scene clipping failed. |
|200 |Ffmpeg.error |Failed to process video. |Video decoding, encoding, or processing failed. |
|200 |Video.UploadFailed |Video upload failed. |Result upload failed. |
|200 |Tos.AccessFailed |TOS access failed. |TOS access or result writing failed. |
|401 |Authorization.Missing |The authorization header is missing. |Authentication is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The API Key is invalid. |
|200 |InternalError |Video scene segmentation failed; please retry or contact support. |Video processing failed. |
|200 |Server.InternalError |Failed to query the task; try again later. |Task querying or result parsing failed. |
