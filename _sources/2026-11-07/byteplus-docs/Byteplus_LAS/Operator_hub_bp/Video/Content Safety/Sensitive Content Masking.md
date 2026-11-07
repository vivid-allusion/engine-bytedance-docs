---
title: "Sensitive Content Masking"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/sensitive-content-masking"
---

The sensitive\-content masking operator applies multimodal large\-model vision analysis to adaptively sampled video frames or images. It combines RapidOCR text extraction and semantic review with ASR\-based audio review to locate and mask sexual, political, violent, abusive\-text, and other sensitive content, while muting sensitive speech. It outputs the processed media file and a JSON detection result.

# Operator introduction

> Operator ID: `las_sensitive_blur`

## Core capabilities

* Multi\-category sensitive\-content detection and localization:

   * Uses a multimodal large model to accurately identify multiple categories of sensitive content, such as sexual, political, violent, and abusive text, in images or sampled video frames.

   * Supports CSRT, KCF, and NCC tracking strategies to follow target regions reliably within scene boundaries.

   * Converts videos to CFR (constant frame rate), then performs scene segmentation and adaptive frame sampling to reduce information loss.

* Sensitive\-content masking and audio muting:

   * Supports multiple masking methods: Gaussian blur, mosaic, solid black masking, and radial blur.

   * Uses RapidOCR to extract on\-screen text and performs semantic review to refine masking regions for sensitive text.

   * Optionally performs ASR\-based audio review and mutes abusive, sexual, and political terms.

   * Supports an additional review pass for political sensitive\-content results.

* Flexible outputs:

   * Preserves the source video's media parameters whenever possible, including codec, profile/level, pixel format, target bitrate, FPS, resolution, and the audio codec, bitrate, sample rate, and channels.

   * If no sensitive content is detected and rendered output is requested, copies the input media directly without re\-encoding.

   * Automatically uploads outputs to the specified TOS path. The output can include the processed media (image or video), `result.json`, and frame\-level video masks stored in the `frames` field of `result.json`.

## Effect display

* Input video

   [video](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/e5dbe681-251c-44b5-bca7-3a4829c2e60d.mp4)

* Core parameters

   ```json
   {
     "categories": [
       "gambling",
       "gambling_text"
     ],
     "mask_mode": "mosaic",
     "render_output": true
   }
   ```

* Output video (mosaic masking)

   [video](https://lf3-static.bytednsdoc.com/obj/eden-cn/fgeh7lpauhz/d5542e3a-86df-47fc-851b-661e5ce53db0.mp4)

## Supported regions

* Asia Pacific(Johor)：ap\-southeast\-1

## Operator performance

|Breakdown item |Performance impact |
|---|---|
|Processing time |* Total processing time depends on video duration, resolution, number of detections, content complexity, and network conditions.<br><br>* For more stable performance, keep TOS inputs and outputs in the same BytePlus region as the API Key. |
|Retry behavior |Visual model calls use a fail\-open strategy. Each sampled frame is attempted up to three times; after three failures, that frame is skipped without failing the entire task. |

# Input and output requirements

## Input requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported input data modalities |* Image<br><br>* Video |
|Input format: Image |Format: `jpg`, `jpeg`, `png`, `webp`, or `bmp`. |
|Input format: Video |Format: `mp4`, `mov`, `mkv`, `avi`, `webm`, `flv`, `ts`, or `m4v`. |
|Input path requirements |Provide the input through the `url` request parameter. Public URLs and TOS paths are supported.<br><br><br>* Public URL: A publicly accessible media URL using HTTP or HTTPS.<br><br>* TOS path: Upload the input to a TOS bucket under the same primary account and in the same region as the current LAS service, then provide a path in the format `tos://bucket_name/demo`. |

## Output requirements

|Breakdown item |Detailed requirements |
|---|---|
|Supported output data modalities |* Image<br><br>* Video<br><br>* Text (JSON detection result) |
|Output format: Text |Format: JSON. `result.json` contains the detection result, and video frame\-level masks are stored in its `frames` field. The operator can return only the JSON result without rendering output media. |
|Output path requirements |`output_tos_path` is required and must be a writable BytePlus Object Storage path. |

# Billing information

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |The billing item depends on the input data type:<br><br><br>* Image input: Usage is measured and billed by the number of input images.<br><br>* Video input: Usage is measured and billed by input video duration. |
   |Billing type |Pay\-as\-you\-go. Charges are generated hourly based on actual billable usage. |
   |Unit price |* Image: 0.005 USD/image;<br><br>* video: 0.4 USD/minute. |

# Cautions and prerequisites

|Details |Caution and prerequisites |
|---|---|
|Costs |Before calling an operator, you need to understand the model invocation costs associated with using the operator. For details, see [Large model billing](https://docs.byteplus.com/docs/Byteplus_LAS/Large_model_billing). |
|Authentication (API Key) |Before calling an operator, you need to generate an API Key for operator invocation. It is recommended to configure the API Key as an environment variable to ensure safer operator calls. For details, see [Obtain and configure API Key](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_and_configure_the_API_Key). |
|BaseURL |Before calling an operator, you need to determine the BaseURL for operator invocation based on the region where your current LAS service is deployed. This is used to configure the path parameter values for operator calls.<br><br>For details, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). The Examples below are for reference only; when making actual calls, replace the path values with those corresponding to your region. |

# Rest API call

## Submit

### Interface description

Submits a sensitive\-content masking task. A successful submission returns a task ID that can be used with the Poll interface to query status and results.

### Request parameters

**operator_id** string 必选 `Example value: las_sensitive_blur`

The operator ID is `las_sensitive_blur`.

**operator_version** string 必选 `Example value: v1`

Currently only `v1` is supported.

**data** SensitiveBlurInfo 必选

Operator parameters

**url** string 必选 `Example value: https://example.com/a.mp4`

Downloadable input media URL. Supports HTTP/HTTPS, BytePlus Object Storage (TOS) (`tos://bucket/key`). Images and videos are supported.

**output_tos_path** string 必选 `Example value: tos://bucket/output`

TOS root path or path containing an output filename. The operator creates a `<input basename>_<8-character request ID>` subdirectory and stores the processed media and `result.json` in it. The TOS bucket region must match the operator BaseURL region.

**media_type** string `Optional` `Example value: auto`

Media type. Valid values: auto, image, and video. Default: auto. In auto mode, the type is inferred from the URL suffix. Recognized image extensions are `jpg`, `jpeg`, `png`, `webp`, and `bmp`; recognized video extensions are `mp4`, `mov`, `mkv`, `avi`, `webm`, `flv`, `ts`, and `m4v`. Specify image or video explicitly when the suffix is ambiguous.

**output_filename** string `Optional` `Example value: output.mp4`

Output filename. By default, it is derived from the input filename; image outputs retain the image extension.

**enable_thinking** boolean `Optional` `Example value: true`

Whether to enable thinking for primary visual detection and audio review. Default: true. When set to true, sensitive\-content detection is more accurate but takes longer to process.

**categories** list of string `Optional` `Example value: ["sexual","political"]`

Sensitive\-content categories to mask. Supported values: sexual, sexual_text, abusive_text, political, political_text, religious, religious_text, gambling, gambling_text, drug, violent, and violent_text. If omitted, all supported sensitive content is masked. Mutually exclusive with `segments`; declare categories inside each segment instead.

**confidence_threshold** float `Optional` `Example value: 0.5`

Confidence threshold in the range [0, 1]. Default: 0.5. Detection boxes below this value are filtered out.

**mask_mode** string `Optional` `Example value: blur`

Masking mode. Default: `blur`. `blur`: Gaussian blur to soften details; `mosaic`: pixelate the region; `black`: fill the region with solid black; `radial_blur`: radial blur with a stronger blurring effect than `blur`.

**render_output** boolean `Optional` `Example value: true`

Whether to render output media. Default: true. When false, only the JSON detection result is returned and no processed media is generated.

**enable_audio_censor** boolean `Optional` `Example value: true`

[Video only] Whether to run ASR and mute abusive, sexual, or political terms. Default: true. With segments, `data.segments[].enable_audio_censor` controls each interval; this global flag does not control segment audio processing.

**segments** list of SensitiveBlurSegment `Optional`

[Video only] Processing intervals. Omitted or null by default for whole\-video processing; otherwise supply 1–64 items. An empty array is invalid. Mutually exclusive with global `categories`.

**start_sec** float 必选 `Example value: 1.0`

Inclusive start on the original timeline in seconds. Must be finite and greater than or equal to 0.

**end_sec** float 必选 `Example value: 3.0`

Exclusive end in seconds, strictly greater than `start_sec`. An end beyond video duration is clipped; an interval entirely outside the video fails.

**categories** list of string `Optional` `Example value: ["abusive_text"]`

Preset categories for this interval. Defaults to an empty array. At least one of `categories` or `text_terms` must be nonempty.

**text_terms** list of string `Optional` `Example value: ["Example Brand"]`

Custom text to mask. Defaults to an empty array. Supports at most 50 distinct nonempty terms per interval and 64 characters per term after trimming.

**enable_audio_censor** boolean `Optional` `Example value: true`

Per\-interval flag, default `false`. Requires `text_terms` or a text category ending in `_text`. Matching speech is silenced only inside this interval.

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Asynchronous task ID used for Poll queries.

**task_status** string `Example value: PENDING`

Task status. PENDING: waiting, RUNNING: in progress, COMPLETED: completed, FAILED: failed, TIMEOUT: timed out.

**business_code** string `Example value: 0`

Business code. `"0"` indicates success.

**error_msg** string

Detailed error information if an exception occurs.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/submit" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_sensitive_blur",
    "operator_version": "v1",
    "data": {
        "url": "https://las-ai-ap-southeast-1-online-bp.tos-ap-southeast-1.bytepluses.com/operator_cards_serving/public/online/las_sensitive_blur/v1/sensitive_sample.mp4",
        "output_tos_path": "tos://bucket/output",
        "mask_mode": "blur",
        "enable_audio_censor": true,
        "segments": [
            {"start_sec": 1.0, "end_sec": 3.0, "text_terms": ["Example Brand"], "enable_audio_censor": true},
            {"start_sec": 11.0, "end_sec": 14.0, "text_terms": ["Example Brand"], "enable_audio_censor": true}
        ]
    }
}'
```

#### Response example

```json
{
    "metadata": {
        "task_id": "task-xxx",
        "task_status": "PENDING",
        "business_code": "0",
        "error_msg": ""
    }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Missing |Missing required parameter |A required parameter is missing. |
|400 |Parameter.Invalid |invalid parameter |Invalid parameter, such as an input whose media type cannot be inferred automatically. |
|400 |Url.Invalid |Sensitive blur request failed |The input URL scheme is not supported. |
|400 |SensitiveBlur.DownloadFailed |Failed to download sensitive\-blur input media |Failed to download the input media. |
|400 |SensitiveBlur.UploadFailed |Failed to upload sensitive\-blur output media |Failed to upload the output media or result JSON. |
|500 |SensitiveBlur.ProcessFailed |Failed to process sensitive\-blur video |Model client initialization, media preprocessing, rendering, or another processing stage failed. |
|401 |Authorization.Missing |Missing Authorization. |Platform authentication is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The platform API key is invalid. |
|500 |InternalError |Internal server error |Unexpected internal service error. |

## Poll

### Interface description

Queries the execution status and result of a sensitive\-content masking task.

### Request parameters

**operator_id** string 必选 `Example value: las_sensitive_blur`

Operator ID

**operator_version** string 必选 `Example value: v1`

Operator version

**task_id** string 必选 `Example value: task-xxx`

Task ID

### Response parameters

**metadata** metadata

Request metadata

**task_id** string `Example value: task-xxx`

Task ID.

**task_status** string `Example value: COMPLETED`

Task status. PENDING: waiting, RUNNING: in progress, COMPLETED: completed, FAILED: failed, TIMEOUT: timed out.

**submit_time** string `Example value: 2026-09-15T10:00:00+08:00`

Task submission time in ISO 8601 format.

**end_time** string `Example value: 2026-09-15T10:03:00+08:00`

Task completion time in ISO 8601 format.

**business_code** string `Example value: 0`

Business code. `"0"` indicates success.

**error_msg** string

Detailed error information if an exception occurs.

**data** SensitiveBlurResult

Task result

**media_type** string `Example value: video`

Resolved media type: image or video.

**processed** boolean `Example value: true`

Whether output media was generated. This is false when `render_output=false`. It remains true when no sensitive content is detected but the input media is copied through.

**output_tos_uri** string `Example value: tos://bucket/output/xxx/output.mp4`

TOS URI of the output media. Null when no output media is generated.

**result_json_tos_uri** string `Example value: tos://bucket/output/xxx/result.json`

TOS URI of the complete `result.json`.

**coordinate_space** string `Example value: normalized_0_999`

Coordinate space normalized to 0\-999.

**fps** float `Example value: 30.0`

[Video only] Input video frame rate.

**width** integer `Example value: 1080`

[Video only] Input video width in pixels.

**height** integer `Example value: 1920`

[Video only] Input video height in pixels.

**total_frames** integer `Example value: 1801`

[Video only] Total number of input video frames.

**masked_frame_count** integer `Example value: 320`

[Video only] Number of frames containing at least one mask.

**mask_count** integer `Example value: 408`

[Video only] Total number of masks across all frames.

**audio_spans** list of audio_span

[Video only] Audio muting intervals. Empty when no sensitive audio is detected or audio review is not run.

**start_sec** float `Example value: 12.3`

Muting interval start time in seconds. Must be greater than or equal to 0.

**end_sec** float `Example value: 12.9`

Muting interval end time in seconds. Must be strictly greater than start_sec.

**category** string `Example value: abusive`

Detected category. Audio review uses abusive, sexual, or political.

**text** string `Example value: idiot`

Matched ASR text.

**segments** list of SensitiveBlurSegmentResult

[Video only] Segment receipts in request order; null in whole\-video mode.

**index** integer `Example value: 0`

Zero\-based index of the corresponding input segment.

**start_sec** float `Example value: 1.0`

Requested start time, retaining fractional precision.

**end_sec** float `Example value: 3.0`

Requested exclusive end time.

**effective_start_sec** float `Example value: 1.0`

Effective inclusive start without backward padding.

**effective_end_sec** float `Example value: 3.0`

Effective exclusive end clipped to video duration.

**categories** list of string `Example value: []`

Preset categories requested for this interval.

**text_terms** list of string `Example value: ["Example Brand"]`

Custom terms requested for the interval.

**enable_audio_censor** boolean `Example value: true`

Requested interval muting flag; it does not indicate that silence was applied.

**hit_categories** list of string `Example value: ["custom_text"]`

Detected categories for this interval.

**visual_box_count** integer `Example value: 2`

Number of visual detection boxes belonging to this interval's rules.

**audio_muted** boolean `Example value: true`

Whether output media was actually silenced for this interval.

**visual_boxes** list of visual_box

[Image only] Visual detection boxes.

**x1** integer `Example value: 120`

Top\-left x\-coordinate in the range 0\-999.

**y1** integer `Example value: 680`

Top\-left y\-coordinate in the range 0\-999.

**x2** integer `Example value: 310`

Bottom\-right x\-coordinate in the range 0\-999.

**y2** integer `Example value: 740`

Bottom\-right y\-coordinate in the range 0\-999.

**category** string `Example value: abusive_text`

Sensitive\-content category.

**text** string `Example value: idiot`

Matched text. Usually an empty string for non\-text categories.

**polygon** array `Example value: [[120,680],[310,680],[310,740],[120,740]]`

[Image only] Polygon coordinates for a text detection box. Each point is [x, y], in the range 0–999. Returned only when the detection result contains polygon information; otherwise omitted. Video masks do not return this field.

**stats** image_stats

[Image only] Detection result statistics. Videos do not return this object; see `masked_frame_count` and `mask_count` for video mask counts.

**visual_box_count** integer `Example value: 3`

[Image only] Number of detection boxes returned, equal to the length of the `visual_boxes` array.

**oversize_filtered** integer `Example value: 0`

[Image only] Retained statistics field, fixed at 0 in the current version. Oversize\-box filtering is disabled and cannot be configured through request parameters.

**category_filtered** integer `Example value: 1`

[Image only] Number of detection boxes filtered out because their categories are not included in the request's `categories`. Equals 0 when no categories are specified.

**width** integer `Example value: 1080`

[Image only] Input image width in pixels, within `stats`.

**height** integer `Example value: 1920`

[Image only] Input image height in pixels, within `stats`.

#### frames (video result.json only; not returned by Poll)

**frame_index** integer `Example value: 369`

Zero\-based frame index.

**timestamp_sec** float `Example value: 12.3`

Frame timestamp in seconds, with a tolerance of up to 0.01 seconds from frame_index / fps.

**masks** list of mask

Masks for the current frame, available only in the `frames` array of the video `result.json` referenced by `result_json_tos_uri`.

#### mask (video result.json only; not returned by Poll)

**x1** integer `Example value: 120`

Top\-left x\-coordinate in the range 0\-999.

**y1** integer `Example value: 680`

Top\-left y\-coordinate in the range 0\-999.

**x2** integer `Example value: 310`

Bottom\-right x\-coordinate in the range 0\-999.

**y2** integer `Example value: 740`

Bottom\-right y\-coordinate in the range 0\-999.

**category** string `Example value: abusive_text`

Sensitive\-content category.

**text** string `Example value: idiot`

Matched text. Usually an empty string for non\-text categories.

### Examples

#### Request example

```bash
curl --location "${LAS_ENDPOINT}/api/v1/poll" \
--header "Content-Type: application/json" \
--header "Authorization: Bearer ${LAS_API_KEY}" \
--data '{
    "operator_id": "las_sensitive_blur",
    "operator_version": "v1",
    "task_id": "task-xxx"
}'
```

#### Response example

```json
{
    "metadata": {
        "task_id": "task-xxx",
        "task_status": "COMPLETED",
        "submit_time": "2026-09-15T10:00:00+08:00",
        "end_time": "2026-09-15T10:03:00+08:00",
        "business_code": "0",
        "error_msg": ""
    },
    "data": {
        "media_type": "video",
        "processed": true,
        "output_tos_uri": "tos://bucket/output/sensitive_sample_a1b2c3d4/sensitive_sample_sensitive_blur.mp4",
        "result_json_tos_uri": "tos://bucket/output/sensitive_sample_a1b2c3d4/result.json",
        "coordinate_space": "normalized_0_999",
        "fps": 30.0,
        "width": 1080,
        "height": 1920,
        "total_frames": 1801,
        "masked_frame_count": 320,
        "mask_count": 408,

        "audio_spans": [
            {
                "start_sec": 12.3,
                "end_sec": 12.9,
                "category": "abusive",
                "text": "idiot"
            }
        ]
    }
}
```

### Error codes

|HttpStatusCode |Error code |Error message |Description |
|---|---|---|---|
|400 |Parameter.Missing |Missing required parameter |A required parameter is missing. |
|400 |Parameter.Invalid |invalid parameter |Invalid parameter. |
|400 |Url.Invalid |Sensitive blur request failed |The input URL scheme is not supported. |
|400 |SensitiveBlur.DownloadFailed |Failed to download sensitive\-blur input media |Failed to download the input media. |
|400 |SensitiveBlur.UploadFailed |Failed to upload sensitive\-blur output media |Failed to upload the output media or result JSON. |
|500 |SensitiveBlur.ProcessFailed |Failed to process sensitive\-blur video |Model client initialization, media preprocessing, rendering, or another processing stage failed. |
|401 |Authorization.Missing |Missing Authorization. |Platform authentication is missing. |
|401 |ApiKey.Invalid |The api key is invalid. |The platform API key is invalid. |
|500 |InternalError |Internal server error |Unexpected internal service error. |
