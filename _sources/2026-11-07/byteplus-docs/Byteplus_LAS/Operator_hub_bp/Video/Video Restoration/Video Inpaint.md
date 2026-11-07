---
title: "Video Inpaint"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Inpaint-Pro"
---

The video intelligent inpainting operator takes a single video as input and outputs a repaired video with specified content erased. Supports subtitles, scrolling subtitles, text watermarks, corner marks, logos, and episode information, and allows separate control of the erasure range for subtitles and watermarks.

# Operator introduction

> Operator ID: las_video_inpaint_pro

## Application scenarios

## Core capabilities

* standard_subtitle: Standard erasure of subtitles and scrolling subtitles; default mode.

* standard_watermark: Standard erasure of text watermarks; best suited for static text watermarks in the corners of the frame.

* standard_subtitle_watermark: Standard simultaneous erasure of subtitles, scrolling subtitles, and text watermarks.

* precise: When `fixed_bboxes` is null or omitted, non\-empty `targets` can be used to precisely specify watermarks, subtitles, scrolling subtitles, or episode information; when non\-empty `fixed_bboxes` are provided, fixed regions are used directly and `targets` are not required. The standard mode automatically selects objects and ignores the `targets` parameter.

* Supports specifying one or more fixed inpainting regions using `fixed_bboxes`. `fixed_bboxes` must be a non\-empty array, and all coordinates must be integers in the range 0–1000; decimals are not accepted. Coordinates must satisfy `top_left_x < bottom_right_x` and `top_left_y < bottom_right_y`. Omit this parameter or pass `null` when no fixed regions are needed.

* Supports using `fixed_bboxes_intervals` to define the active time range of each fixed region. Each interval corresponds by position to an item in `fixed_bboxes`; `-1` as the end time means until the end of the video.

* Supports stable processing of long videos and retains the original audio in the output video.

## Effect demonstration

* Input video

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/009daacb388e4f2baf491c9aec199efa~tplv-goo7wpa0wc-image.image)

* Targeted inpaint of a specific target type—corner label inpaint as an example

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8904274db63d462a89f5b1b07394a5cb~tplv-goo7wpa0wc-image.image)

* Synchronous inpaint of multiple targets such as subtitles and corner labels

   [video](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/49464cfe408e4c2992a4bbfb276a83f8~tplv-goo7wpa0wc-image.image)

## Supported languages

* `“standard_*”` detection mode: Designed for text detection, supports Simplified Chinese, Traditional Chinese, English, Japanese, French, German, Italian, Spanish, Portuguese, Dutch, Polish, Romanian, Czech, Swedish, Norwegian, Danish, Finnish, Hungarian, Turkish, Vietnamese, Indonesian, Malay, Azerbaijani, Afrikaans, Bosnian, Croatian, Welsh, Estonian, Irish, Icelandic, Kurdish, Lithuanian, Latvian, Maltese, Maori, Occitan, Slovak, Slovenian, Albanian, Swahili, Tagalog, Uzbek, Latin, Serbian (Latin), Catalan, Basque, Galician, Luxembourgish, Romansh, Quechua.

   > **Note**

   > Language support indicates detectable text, but does not guarantee consistent results for all fonts, artistic text, or low\-contrast text. When `model_level` is `lite`, all the languages listed above except Japanese remain supported. Support for Traditional Chinese is incomplete, and some Traditional Chinese characters may not be detected.

* `precise` detection mode: Based on large models for target recognition, supports identification and inpainting of text in various common languages.

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Sub\-items |Performance impact description |
|---|---|
|Submit RPM |600 |
|Poll RPM |600 |
|Maximum concurrency |10 |
|Estimated processing duration |* lite: Processing 720p and 1080p takes approximately 3 times the original video duration, and 4K takes approximately 6 times;<br><br>* pro: 720p takes approximately 6 times, 1080p takes approximately 10 times, and 4K takes approximately 15 times.<br><br><br>Actual processing time may be affected by video content, service load, and task queueing. |

# Input and output requirements

## Input requirements

|Subdivision |Detailed description |
|---|---|
|Supported input data modalities |Video |
|Input format: video |* Format: mp4, mov, avi, mkv, and other common formats;<br><br>* Size: 1 second to 3 hours, maximum 10 GB;<br><br>* Resolution: Resolution must not exceed 4K (long side ≤ 3840, short side ≤ 2160). |
|Input path requirements |Supports public URLs and `tos://` video sources. The TOS bucket must belong to the same account and the Asia Pacific (Johor) region (`ap-southeast-1`) as the API Key. |

## Output requirements

|Subdivision |Detailed description |
|---|---|
|Output data modalities |Video |
|Output path: TOS |Specify the storage path for the operator's output results using the request parameter `output_tos_path`. Currently, setting a TOS path is supported.<br><br>TOS path: A writable TOS Bucket directory under the same primary account and in the Asia Pacific (Johor) region (`ap-southeast-1`) as the LAS service. |

# Billing information

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing item |Usage is calculated based on the duration of the output video. For billing, the output video duration is adjusted using coefficients for the output video frame rate and resolution. The adjusted billing duration is used as the billing usage.<br><br>After the task is completed, you can check the actual output video frame rate and resolution values for the current task via the `output_fps` and `resolution` parameters returned by the poll interface. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual billing usage. Billing precision: billed by the minute, accurate to the millisecond |
   |Unit price |The unit price depends on the repair version, target detection, and repair mode you select when using Video Inpaint. When submitting an operator task, you can set the repair version, target detection, and repair mode for the task via<br><br>`model_level` and `detection_mode` request parameters |

   > **Caution**

   * > Total cost paid: In addition to the unit price, service billing is associated with the **actual repaired** video duration, frame rate, and resolution.

   * > Video Inpaint does not change the video frame rate, and the duration of the repaired video may be less than the input video duration.

* Billing details

   Billing formula: `Total cost = unit price * billing usage = unit price * (video duration * duration-output frame rate conversion coefficient * duration-output resolution conversion coefficient)`

   |Sub\-scenarios |Unit price |Billing duration\-output frame rate conversion coefficient |Billing duration\-output resolution conversion coefficient |
   |---|---|---|---|
   |* Fast version repair, that is,<br><br>   * `model_level` : `lite` |0.125 USD/minute |Actual output frame rate:<br><br><br>* (0 , 24fps]: coefficient is 0.8<br><br>* (24fps , 30fps]: coefficient is 1<br><br>* Greater than 30fps: The coefficient is determined by the ratio of the actual output video frame rate to the base frame rate (30fps), rounded up to the nearest integer. |Actual total output pixels:<br><br><br>* (0 , 1920×1080]: coefficient is 1<br><br>* (1920×1080 , 3840×2160]: coefficient is 2 |
   |* Professional edition \- standard\-level object detection and restoration, that is,<br><br>   * `model_level` : `pro`<br><br>   * `detection_mode` : `standard_*` |0.375 USD/minute ||Actual total output pixels:<br><br><br>* (0 , 1280×720]: coefficient is 0.6<br><br>* (1280×720 , 1920×1080]: coefficient is 1<br><br>* (1920×1080 , 3840×2160]: coefficient is 2 |
   |* Professional edition \- precise\-level object detection and restoration, that is,<br><br>   * `model_level` : `pro`<br><br>   * `detection_mode` : `precise` |1.50 USD/minute |||

* Billing example

   When using the professional version – precise level target detection and repair mode for Video Inpaint, if the actual output video has a frame rate of 50fps, a resolution of 1080p (1920×1080), and a video duration of 10 minutes:

   * The multiplier of the actual output video frame rate to the base frame rate is 1.6, rounded up to 2.0.

   * The actual cost is:

      `Total cost = 1.5 USD/minute * (10 minutes * 2 * 1) = 30 USD`.

# Caution and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model invocation billing - BytePlus](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |The BaseURL for the supported Asia Pacific (Johor) region (`ap-southeast-1`) is `https://operator.las.ap-southeast-1.bytepluses.com`. Use this value to configure the path for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |

# Rest API invocation

## API invocation instructions

* The API of this operator is an asynchronous task interface. You need to submit a task via the `Submit` interface to obtain the task's `task_id`, then use the `Poll` interface to check the status of the corresponding task (`task_id`) and retrieve the operator's processing result.

* Caution: After a task is submitted, the `task_id` is valid for 3 days. After 3 days, you will not be able to retrieve the operator's processing result using this `task_id`.

## Submit

### Interface description

Submit an asynchronous Video Inpaint task. The operator reads a video, determines the inpainting range based on detection mode or fixed region, outputs the inpainted video, and retains the original audio.

### Request parameters

**operator_id** string 必选 `Example value: las_video_inpaint_pro`

Fixed as `las_video_inpaint_pro`.

**operator_version** string 必选 `Example value: v1`

Fixed as `v1`.

**data** VideoInpaintUserReqParams 必选

Video input, detection method, restoration scope, and output settings.

**video_url** string 必选 `Example value: https://example.com/video.mp4`

Default value: None. Downloadable address for the input video. Supports HTTP/HTTPS and BytePlus TOS (`tos://bucket/key`); the address cannot be empty and the service must have read permissions. Supports common formats such as mp4, mov, avi, and mkv. The video must be at least 1 second, up to 3 hours, and a maximum of 10 GB; input resolution must not exceed 4K (long side no more than 3840 and short side no more than 2160).

**output_tos_path** string 必选 `Example value: tos://bucket/output/`

Default value: None. You must specify the TOS result directory via `tos://bucket/path`; the TOS bucket must be in the Asia Pacific (Johor) region (`ap-southeast-1`), matching the operator's BaseURL, and the current account must have write permissions. The trailing `/` in the path can be omitted.

**model_level** string 必选 `Example value: pro`

Select the Video Inpaint model level. Options are `lite` (fast version, suitable for scenarios sensitive to processing speed and cost) and `pro` (professional version, seamless removal, suitable for scenarios with high requirements for restoration quality).

**detection_mode** string `Example value: standard_subtitle_watermark`

Default value: standard_subtitle. Determines the target detection method and removal category: `standard_subtitle` uses general text detection and only removes regular subtitles and scrolling subtitles; `standard_watermark` only removes text watermarks, which is more suitable for static text watermarks in corners; `standard_subtitle_watermark` removes subtitles, scrolling subtitles, and text watermarks simultaneously; `precise` uses precise detection, and targets are determined by `targets`. In standard mode, `targets` in the request will be ignored. Use `precise` for non\-text watermarks or when it is necessary to accurately distinguish between subtitles and watermarks. The `precise` mode is not supported when model_level is set to `lite`.

**targets** array of string `Conditionally required` `Example value: ["watermark", "subtitle"]`

No default value. When `detection_mode=precise` and `fixed_bboxes` is null or not set, this field is required and must be a non\-empty array, used to specify the target categories for precise detection. If a non\-empty `fixed_bboxes` is set, the fixed regions are used directly and this field does not need to be provided. Optional values: `watermark` (watermark, corner mark, logo), `subtitle` (regular subtitles), `scrolling_subtitle` (scrolling subtitles), `drama_info` (episode number, title, character names, and other drama information). These values can be combined. In standard mode, the targets are automatically selected according to the mode and this field is ignored, so it does not need to be provided.

**return_subtitle_bbox** boolean `Example value: true`

Default value: true. Whether to return the detected subtitle regions in the task result. The corresponding field is returned only if subtitle bounding boxes are present in the detection result. When set to `false`, do not rely on the subtitle bounding box result.

**max_process_frames** integer `Example value: 300`

Default value: \-1. Limits the number of frames processed from the beginning of the original video. For example, if the source video is 30 fps, setting this to 300 processes approximately the first 10 seconds. `-1` means no limit; the entire video is processed. This value refers to the number of frames, not seconds.

**fixed_bboxes** array `Example value: [[100,600,900,750],[0,100,100,600]]`

Default value: null. Specify one or more fixed repair regions. This parameter must be a non\-empty array; omit it or pass `null` when no fixed regions are needed. Each item is in the format `[top_left_x, top_left_y, bottom_right_x, bottom_right_y]`. The coordinates use the top\-left corner of the video as the origin and are represented on a 1000×1000 normalized canvas, where x is the horizontal coordinate and y is the vertical coordinate. After this is set, these fixed regions are used directly and dynamic target detection is skipped, so `detection_mode` and `targets` no longer determine the repair regions. All coordinates must be integers in the range 0–1000; decimals are not accepted. The coordinates must satisfy `top_left_x < bottom_right_x` and `top_left_y < bottom_right_y`.

**fixed_bboxes_intervals** array `Example value: [[0.5,6.3],[0,-1]]`

Empty by default. Specifies when each region in `fixed_bboxes` is active. Each item uses `[bbox_start, bbox_end]` in seconds and corresponds by position to the region at the same position in `fixed_bboxes`. The corresponding region is restored throughout the closed interval from `bbox_start` to `bbox_end`. A `bbox_end` value of `-1` means until the end of the video. If this field is omitted or an empty array is provided, every region remains active from the beginning to the end of the video. When a non\-empty array is provided, it must contain the same number of items as `fixed_bboxes`.

**maximum_output_fps** integer `Example value: 30`

Default value: 30. The value must be greater than 0. This sets the upper limit for output and processing frame rate. The actual frame rate is the lower value between the source video frame rate and this value; if the source frame rate is lower than the limit, no frames are interpolated. Lowering this value can usually reduce processing load, but will change the output frame rate for high\-frame\-rate source videos.

**maximum_resolution** string `Example value: 1080p`

Default value: 1080p. Maximum output resolution. Options are `720p`, `1080p`, and `4k`. If the source exceeds the target pixel size, it will be scaled down proportionally; smaller inputs will not be upscaled. When `4k` is selected, source video resolutions up to 4K can be retained. This parameter is used to limit the output size and will not upscale smaller inputs to 4K.

**output_video_mode** string `Example value: balanced`

Default value: `balanced`. Output quality levels: `economy` produces smaller output files with average image quality; `balanced` strikes a balance between file size and image quality, providing a well\-rounded result; `high` generates larger output files with higher image quality; `source` attempts to use the input video's encoding format and determines the target bitrate based on the input video bitrate, output resolution, and output frame rate, but does not guarantee that the final bitrate will exactly match the input. When `output_codec` is explicitly set, that codec is used; when `output_bitrate` is explicitly set, that target bitrate is used.

**output_codec** string `Example value: h265`

Default value: `h264`. Explicitly specify the output video codec. Options are `h264` and `h265`. Once set, this overrides the automatic codec selection by `output_video_mode`, but does not change the quality level itself.

**output_bitrate** integer `Example value: 8000`

Not specified by default. Target video bitrate, in Kbps. Must be a positive integer. Once explicitly set, this overrides the target bitrate automatically determined by `output_video_mode`; `output_codec` is still used to determine the encoding format. There is no guarantee that the actual bitrate of the final file will exactly match the target bitrate.

**subtitle_persistent** boolean `Example value: true`

Default value: false. Subtitle region persistence mode. When enabled, detected subtitle positions are merged based on a time window, and the merged region is continuously repaired within the window to reduce missed detections of subtitles or scrolling subtitles on a frame\-by\-frame basis. The region may expand as a result, potentially modifying more of the background. This takes effect directly in standard subtitle mode; in precise mode, it is only meaningful when the target includes `subtitle` or `scrolling_subtitle`.

**subtitle_protect** boolean `Example value: false`

Default value: `false`. When enabled, watermark masks exclude regular and scrolling subtitle regions to protect subtitles. This applies only when `detection_mode=standard_watermark`, or when `detection_mode=precise` and `targets` includes watermark categories but excludes subtitle categories. It has no effect when `fixed_bboxes` is set. Any part of a watermark that overlaps a subtitle region remains unremoved, and this option does not guarantee that subtitle pixels remain completely unchanged.

### Response parameters

**metadata** metadata

Asynchronous task metadata. A successful Submit only indicates that the task has been accepted, not that the repair is complete.

**task_id** string `Example value: task-xxx`

Task ID. Pass it as\-is when calling Poll subsequently.

**task_status** string `Example value: PENDING`

Task status: `PENDING` (received/queued), `RUNNING`, `COMPLETED`, `FAILED`, `TIMEOUT`.

**business_code** string `Example value: 0`

Business status code. Whether the operation is successful should be determined together with `task_status`.

**error_msg** string

Error message when the operation fails; usually empty when successful.

### Example

#### Request example

```Bash
export OUTPUT_TOS_PATH="tos://path/to/output/"

curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_inpaint_pro",
  "operator_version": "v1",
  "data": {
    "video_url": "https://${LAS_TOS_BUCKET}.${TOS_ENDPOINT}/operator_cards_serving/public/${LAS_ENVIRONMENT}/las_video_inpaint_pro/v1/input.mp4",
    "output_tos_path": "$OUTPUT_TOS_PATH",
    "model_level": "pro",
    "detection_mode": "precise",
    "targets": ["watermark", "subtitle"],
    "maximum_output_fps": 30,
    "maximum_resolution": "1080p",
    "output_video_mode": "balanced"
  }
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20260812154600-abc123",
    "task_status": "PENDING",
    "business_code": "0",
    "error_msg": ""
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Url.Invalid |`video_url` is invalid or inaccessible; check the URL, validity period, and TOS read permissions. |`video_url` is invalid or inaccessible; check the URL, validity period, and TOS read permissions. |
|400 |Video.Invalid |The file is corrupted, cannot be decoded, or is not recognized as a valid video; check the source file and try again. |The file is corrupted, cannot be decoded, or is not recognized as a valid video; check the source file and try again. |
|400 |Video.FormatUnsupported |The container or encoding format is not supported; convert to a common format and try again. |The container or encoding format is not supported; convert to a common format and try again. |
|400 |Video.DownloadFailed |Failed to download the source video; check the network, URL validity period, and access permissions. |Failed to download the source video; check the network, URL validity period, and access permissions. |
|400 |Video.DurationTooShort |The video is less than 1 second. |The video is less than 1 second. |
|400 |Video.DurationExceeded |The video exceeds 3 hours; submit after trimming or splitting. |The video exceeds 3 hours; submit after trimming or splitting. |
|400 |Video.FileTooLarge |The video exceeds 10 GB; submit after compressing or splitting. |The video exceeds 10 GB; submit after compressing or splitting. |
|400 |Parameter.Invalid |The type, enumeration, coordinates, or value is invalid; correct according to the parameter table. |The type, enumeration, coordinates, or value is invalid; correct according to the parameter table. |
|400 |Video.Timeout |Processing timed out; you can try again after shortening the video or reducing the frame rate/resolution. |Processing timed out; you can try again after shortening the video or reducing the frame rate/resolution. |
|400 |Video.VLMFailed |Precision detection failed; you can retry, or use the standard detection mode when applicable. |Precision detection failed; you can retry, or use the standard detection mode when applicable. |
|400 |Video.UploadFailed |Failed to upload the result; check the output directory and write permissions. |Failed to upload the result; check the output directory and write permissions. |
|401 |Authorization.Missing |Authentication information not provided. |Authentication information not provided. |
|401 |ApiKey.Invalid |API Key is invalid. |API Key is invalid. |

## Poll

### Interface description

Query the status of the Video Inpaint task using the `task_id` returned by Submit. After the task is completed, `data` returns the result address and information about the regions requested to be enabled and actually detected.

### Request parameters

**operator_id** string 必选 `Example value: las_video_inpaint_pro`

Must be consistent with the task submission, and fixed to `las_video_inpaint_pro`.

**operator_version** string 必选 `Example value: v1`

Must be consistent with the task submission, and fixed to `v1`.

**task_id** string 必选 `Example value: task-20260812154600-abc123`

The asynchronous task ID returned by Submit. If the task ID does not exist, is misspelled, or does not belong to the current request context, the result cannot be obtained.

### Response parameters

**metadata** metadata `Example value: Always`

Task ID, status, business code, and error information.

**task_id** string `Example value: task-20260812154600-abc123`

The task ID for the current query.

**task_status** string `Example value: COMPLETED`

`PENDING`: Received or queued; `RUNNING`: Processing; `COMPLETED`: Completed, `data` can be read; `FAILED`: Failed, see `error_msg`; `TIMEOUT`: Task timed out.

**business_code** string `Example value: 0`

Business status code. The client should check `task_status` as well; do not determine whether the task is completed based only on the HTTP status.

**error_msg** string

Failure reason; usually empty if successful.

**data** VideoInpaintResponse `Example value: Usually after the task is completed`

Inpaint result. This object should not be assumed to exist when the task is queued, in progress, or has failed.

**inpainted_video_path** string `Example value: tos://bucket/output/video_inpaint/xxx/output.mp4`

TOS path of the inpainted video. The result is saved in the output directory specified in the request.

**output_video_url** string `Example value: https://example.com/output.mp4`

Downloadable pre\-signed URL of the inpainted video. Returned only when the download address is successfully generated; the link is valid for 24 hours. Please download promptly and do not use it as a long\-term address.

**subtitle_bbox** string `Example value: 120,800,1800,960`

Single subtitle aggregation area, format is `x1,y1,x2,y2`; the coordinates are the pixel coordinates of the original video. Returned only when `return_subtitle_bbox=true` and the detection result contains a subtitle box; may be omitted if no subtitle is detected.

**resolution** string `Example value: 1920x1080`

The resolution of the actual output video, format is `width x height`. Returned when the task is successfully completed and the output video is generated.

**output_fps** double `Example value: 29.97`

The frame rate (fps) of the actual output video, which may be a decimal. Returned when the task is successfully completed and the output video is generated.

### Example

#### Request example

```Bash
curl --location "https://operator.las.ap-southeast-1.bytepluses.com/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer $LAS_API_KEY" \
--data '{
  "operator_id": "las_video_inpaint_pro",
  "operator_version": "v1",
  "task_id": "task-20260812154600-abc123"
}'
```

#### Response example

```JSON
{
  "metadata": {
    "task_id": "task-20260812154600-abc123",
    "task_status": "COMPLETED",
    "business_code": "0",
    "error_msg": ""
  },
  "data": {
    "inpainted_video_path": "tos://bucket/output/video_inpaint/xxx/output.mp4",
    "output_video_url": "https://example.com/output.mp4",
    "subtitle_bbox": "120,800,1800,960",
    "resolution": "1920x1080",
    "output_fps": 29.97
  }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Operator.InvalidId |The operator is invalid. |Missing `operator_id` or `operator_version`, or the operator and version combination is not supported. |
|400 |TaskId.Missing |The task id is missing. |Missing `task_id` or its value is empty. |
|200 |TaskId.Invalid |The task does not exist |Poll returns normally, `metadata.task_status` is `FAILED`, `metadata.business_code` is `TaskId.Invalid`, and `data` is `{}`. Check whether the task ID is correct. |
|400 |Parameter.Invalid |The parameter type or value is invalid. |The parameter type or value is invalid. |
|401 |Authorization.Missing |Missing authentication information. |Missing authentication information. |
|401 |ApiKey.Invalid |The API Key is invalid. |The API Key is invalid. |

* HTTP 200 only indicates that the Poll request was successful; it does not mean the task was successful. If the task fails, check metadata.task_status, metadata.business_code, and metadata.error_msg.
