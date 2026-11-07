---
title: "Create a video quality enhancement task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video`

To programmatically improve video quality, you can use this API to submit an asynchronous enhancement task. It leverages AI algorithms to perform a series of optimizations, including denoising, color enhancement, artifact removal, and super\-resolution.

> **INFO**

> For a complete usage flow and application examples, please refer to [Video quality enhancement (standard/professional)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement).

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/source.mp4` |The URL of the video to be enhanced.<br><br><br>* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* File size: It is recommended that the size of a single input file not exceed 10 GB.<br><br>* Video resolution: Supports up to 2K. |
|`tool_version` |String |No |`professional` |The tool version determines the strength and scope of the enhancement algorithms and the billing.<br><br><br>* `standard`: (Default) Standard version. Balances processing speed and video quality, includes over 10 frequently used enhancement algorithms, and meets the quality requirements of mainstream playback platforms. Suitable for quality improvement in video distribution scenarios.<br><br>* `professional`: Professional version. Provides professional\-grade quality enhancement with over 30 built\-in algorithms, ensuring shot\-level visual effects. Suitable for cinema\-grade video production.<br><br><br>For details, see [Versions and scenes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement#1a374238). |
|`scene` |String |No |`aigc` |The video enhancement scenario, which only takes effect when `tool_version` is `standard`. Used to select a preset enhancement template for a specific business scenario. Possible values:<br><br><br>* `common`: (Default) General\-purpose template.<br><br>* `ugc`: UGC (User\-Generated Content) short video scenario.<br><br>* `short_series`: Short\-form drama series scenario.<br><br>* `aigc`: AIGC (AI\-Generated Content) scenario.<br><br>* `old_film`: Old film restoration scenario.<br><br><br>For details, see [Versions and scenes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement#1a374238). |
|`enhance_style` |String |No |`natural` |The video enhancement style. Supported by both the Standard and Professional versions.<br><br><br>* `hd`: (Default) High definition. Offers moderate enhancement for a sharp and clear image.<br><br>* `natural`: Natural look. Reduces enhancement strength for fewer sharpening artifacts and a more natural\-looking picture.<br><br><br>For details, see [Configure enhancement style](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement#61c02509). |
|`resolution` |String |No |`1080p` |The target resolution level. You can use this parameter to upscale the video to a specified resolution. Supported values: `240p`, `360p`, `480p`, `540p`, `720p`, `1080p`, `2k`, `4k`, `6k`, `8k`.<br><br>**Note**: This parameter is mutually exclusive with `resolution_limit` and cannot be configured at the same time. |
|`resolution_limit` |Integer |No |`1920` |The pixel limit for the short side of the target resolution, with a value range of `[128, 4320]`. The system will scale the video proportionally to this limit while maintaining the original aspect ratio.<br><br>**Note**: This parameter is mutually exclusive with `resolution` and cannot be configured at the same time. |
|`bitrate_level` |String |No |`medium` |The target bitrate level, used to control the average bitrate of the output video. This parameter affects the visual quality and final file size of the video. Defaults to `medium`.<br><br>• `low`: Low bitrate<br><br>• `medium`: Medium bitrate (recommended)<br><br>• `high`: High bitrate<br><br>**Note**: The actual bitrate is automatically calculated based on the target resolution and frame rate. For the specific bitrates for each level, refer to [Bitrate reference](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-enhancement-task#63decc4e). If you need to specify a precise bitrate, use the `bitrate` parameter. |
|`bitrate` |Integer |No |`8000` |The target average bitrate, in kbps. The value must be within the range of [10, 150000]. If this parameter is not set, the bitrate is automatically determined based on `bitrate_level`, resolution, and frame rate. When both `bitrate` and `bitrate_level` are specified, the `bitrate` parameter takes precedence. |
|`fps` |Number |No |`60` |The target frame rate, in fps. If the `fps` parameter is not specified, the output video will maintain the same frame rate as the original source. The value range is `[15, 120]`. It is recommended not to exceed 4 times the original frame rate. |
|`bit_depth` |Integer |No |`10` |The target bit depth, also known as color depth. Effective only for the Professional version (`tool_version` is `professional`). Values:<br><br><br>* `8`: (Default) 8\-bit depth. Each color channel has 2⁸ (256) levels. Supports the h264 and h265 codecs.<br><br>* `10`: 10\-bit depth. Each color channel has 2¹⁰ (1,024) levels. Supports the h265 and prores codecs.<br><br>* `12`: 12\-bit depth. Each color channel has 2¹² (4,096) levels. Supports the h265 codec.<br><br>* `16`: 16\-bit depth. Each color channel has 2¹⁶ (65,536) levels. Supports the ffv1 and exr codecs. Note the following:<br><br>   * The input video duration must not exceed 40 seconds.<br><br>   * The bitrate is automatically determined by the system; the `bitrate` and `bitrate_level` parameters do not take effect. 16\-bit depth tasks are processed serially (one at a time), which may result in longer processing times.<br><br><br>For details, see [Configure output color depth (Professional version only)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement#1b3390a0). |
|`codec` |String |No |`h265` |The video codec. Effective only for the Professional version (`tool_version` is `professional`). When `codec` is specified, `bit_depth` must also be specified, and the two must form a valid combination. The only exception is when `pix_fmt` is `gbrp16le`: in this case, the system automatically uses `codec=ffv1` and `bit_depth=16`. For details, see [The bit depth, codec, and output container combinations](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement#ab1e0a1c). If you specify only `bit_depth` without `codec`, the tool automatically selects the corresponding codec based on `bit_depth`: the default codec for `8` is `h264`; the default codec for `10` and `12` is `h265`; and the default codec for `16` is `ffv1`. Supported codecs:<br><br><br>* `h264`<br><br>* `h265`<br><br>* `prores`<br><br>* `ffv1`<br><br>* `exr`<br><br><br>Note: The `prores`, `ffv1`, and `exr` codecs do not support a specified bitrate; the `bitrate` and `bitrate_level` parameters do not take effect. |
|`pix_fmt` |String |No |`gbrp16le` |The pixel format of the output video. Effective only for the Professional version (`tool_version` is `professional`). Currently, the only supported value is `gbrp16le`, representing a lossless combination of the GBR color space and 16\-bit color depth. Set this parameter when you need ultimate lossless quality for professional color grading or high\-quality video archiving.<br><br>When set, the system forces the output to be a MOV file with lossless FFV1 encoding, GBR pixel format, and 16\-bit color depth. You do not need to manually pass `codec` and `bit_depth` (if passed, they must be `ffv1` and `16` respectively), and the `bitrate` and `bitrate_level` parameters will automatically become ineffective. If this parameter is omitted, the system automatically selects an appropriate pixel format based on your `codec` and `bit_depth` settings.<br><br>**Note**: This format produces extremely large files, making it unsuitable for direct streaming distribution. Also, the input video duration must not exceed 40 seconds. |
|`dynamic_range` |String |No |`hdr` |The dynamic range of the output video, which controls the brightness details and color richness of the picture. Effective only for the Professional version (`tool_version` is `professional`). Supported values:<br><br><br>* `sdr`: (Default) Outputs a Standard Dynamic Range (SDR) video, ensuring high compatibility for most conventional playback scenarios.<br><br>* `hdr`: Outputs an HDR video that complies with the HLG standard (generated by AI tone mapping from the SDR input). Select this option if you want to enhance the visual impact of your video with stronger contrast and more vivid colors.<br><br><br>When set to `hdr`, the `bit_depth` must be `10`, `12`, or `16` (if `pix_fmt=gbrp16le` is set, the system automatically sets it to `16`). Ensure the final audience uses HDR\-capable displays and players.<br><br>**Note**: When the codec is set to `codec=exr`, the system forces an HDR output, and this parameter will not take effect. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example demonstrates how to submit a "Professional" video enhancement task for a UGC short video, specifying an output resolution of 1080p and a frame rate of 60fps.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/enhance-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/low_quality_gameplay.mp4",
  "tool_version": "professional",
  "resolution": "1080p",
  "fps": 60
}'
```

## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |

#### The error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |

### Response example

#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-video-1703200",
    "request_id": "20260415150000F6DE4C24A6A0D94B7FF1"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240522110500XYZW54321",
  "error": {
    "code": "InvalidParameter",
    "message": "Parameter `resolution` must be one of [720p, 1080p].",
    "param": "resolution",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Video quality enhancement is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information you retrieve contains the following:

|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://example.byteplus.com/output.mp4` |The download URL for the enhanced video file. This URL is valid for **24 hours**. Please be sure to save the output file promptly. |
|`duration` |Number |`120.5` |The total duration of the output video (in seconds). |
|`resolution` |String |`1080p` |The resolution of the output video. |
|`fps` |Number |`60` |The frame rate of the output video. |
|`tool_version` |String |`professional` |The tool version used for the task. |

Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-enhance-video-1703200",
    "request_id": "20260415150000F6DE4C24A6A0D94B7FF1",
    "result": {
        "video_url": "https://example.byteplus.com/enhanced_output.mp4",
        "duration": 120.5,
        "resolution": "1080p",
        "fps": 60,
        "tool_version": "professional"
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

## Reference

### Bitrate reference

The table below lists the **target output bitrates** (in Mbps) for different combinations of resolution and frame rate when the `bitrate_level` parameter is set to `low`, `medium`, and `high`. Please note that to ensure stable quality across various scenarios, the system dynamically adjusts the bitrate based on the complexity of the video content. Therefore, the actual output bitrate will typically be between 0.8 and 1.5 times the target values listed in the table.

|Output Resolution |Output Frame Rate (fps) |Low Bitrate (Mbps) |Medium Bitrate (Mbps) |High Bitrate (Mbps) |
|---|---|---|---|---|
|240p |[15,30] |0.3 |0.45 |0.6 |
||(30,60] |0.65 |0.9 |1.2 |
||(60,120] |1.5 |2.2 |2.8 |
|360p |[15, 30] |0.6 |0.85 |1.2 |
||(30, 60] |1 |1.5 |2 |
||(60, 120] |1.7 |2.5 |3.2 |
|480p |[15, 30] |1.2 |1.8 |2.3 |
||(30, 60] |2.1 |3 |3.9 |
||(60, 120] |3.5 |5 |6.5 |
|540p |[15, 30] |1.7 |2.5 |3.2 |
||(30, 60] |2.8 |4 |5.2 |
||(60, 120] |4.2 |6 |7.8 |
|720p |[15, 30] |2.8 |4 |5.2 |
||(30, 60] |5.6 |8 |10 |
||(60, 120] |8.4 |12 |15 |
|1080p |[15, 30] |5 |7 |9 |
||(30, 60] |10 |14 |18 |
||(60, 120] |15 |22 |28 |
|2K |[15, 30] |10 |15 |20 |
||(30, 60] |17 |24 |32 |
||(60, 120] |28 |40 |52 |
|4K |[15, 30] |21 |30 |39 |
||(30, 60] |32 |45 |58 |
||(60, 120] |53 |75 |100 |
|8K |[15,30] |42 |60 |78 |
||(30,60] |63 |90 |120 |
||(60,120] |84 |120 |150 |
