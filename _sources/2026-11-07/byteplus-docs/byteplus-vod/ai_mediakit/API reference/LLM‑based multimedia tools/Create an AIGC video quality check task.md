---
title: "Create an AIGC video quality check task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality`

To automate quality control for large\-scale AIGC video production, you can call this API to submit an asynchronous quality check task. The API assesses the video for quality issues such as reference consistency, world plausibility, content continuity, and visual fidelity. It automatically locates abnormal time ranges and outputs issue descriptions with representative problematic frames, helping you quickly decide whether to adopt, review, or regenerate the video.

> **INFO**

* > AIGC Video Quality Check is currently in public beta and is expected to be officially released in early November 2026. During the public beta, the API and capabilities may be subject to minor adjustments. Refer to the latest documentation for the most up\-to\-date information.

* > For the complete workflow and application examples, see [AIGC video quality check](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-aigc-video-quality-check).

## Prerequisites

Before you call this API, make sure you have completed the following:

* **Enable the ModelArk large model service**: This tool relies on ModelArk vision large models to perform the assessment. Go to the [ModelArk console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint) and ensure that the required large models are enabled and available under your account. The model's capability affects the detection results, so we recommend using a pro model of the `seed` series, for example `seed-2-0-pro-260328`.

* **Perform cross\-service authorization**: Before using this tool for the first time, go to the [Basic configuration > Authorization management page](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) in the AI MediaKit console to grant AI MediaKit permission to access your **ModelArk** resources. Otherwise, the task will fail due to insufficient permissions.

## Request parameters

### Header parameters

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body parameters

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/your_aigc_video.mp4` |The URL of the video to be assessed.<br><br><br>* File source: A publicly accessible HTTP or HTTPS URL.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`.<br><br>* Video duration: A single video must not exceed 3 minutes. |
|`modules` |Array of String |No |`["world_plausibility", "visual_fidelity"]` |The list of check modules to enable, which can be combined as needed for your scenario. Elements must be unique. If you omit this parameter or provide an empty array, all applicable modules are executed, but reference_consistency is enabled only when reference_images is provided. Supported values:<br><br><br>* `reference_consistency`: Reference consistency. Compares elements in the video with the provided reference images. You must provide `reference_images` when this module is enabled.<br><br>* `world_plausibility`: World plausibility. Checks whether the visuals conform to physical and motion laws, such as gravity, collision, clipping, and inertia.<br><br>* `content_continuity`: Content continuity. Checks whether entities such as characters and products remain consistent over time.<br><br>* `visual_fidelity`: Visual fidelity. Checks the structure and naturalness of human bodies, objects, and text. |
|`reference_images` |Array of Object |No |`-` |The list of reference images, required only when the `reference_consistency` module is enabled. The array must contain 1 to 6 images. Each image must be labeled with its category, which is used to compare the consistency of the corresponding element in the video. For details, see [The reference image object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task#reference-image-object). |
|`prefer_models` |Array of String |No |`["seed-2-0-pro-260328"]` |The list of preferred Model IDs. Currently, you must provide exactly one model ID. The model's capability affects the detection results, so we recommend using a pro model of the `seed` series, for example `seed-2-0-pro-260328`. You can view the Model IDs available under your account on the [ModelArk console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint). |
|`output_language` |String |No |`en-US` |The output language code of the issue descriptions (`issues[].description`). Supported values: `zh-CN`, `en-US`. If you omit this parameter, English (`en-US`) is used by default. |
|`client_token` |String |No |`your_unique_request_id_135` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

#### The reference image object

Required only when the `reference_consistency` module is enabled. Each element in the `reference_images` array has the following structure.

|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`image_url` |String |Yes |`https://example.com/character_ref.png` |The reference image URL. A publicly accessible HTTP or HTTPS URL. |
|`category` |String |Yes |`character` |The category of the reference image, used to label the element it represents. Supported values:<br><br><br>* `character`<br><br>* `clothing`<br><br>* `product`<br><br>* `scene`<br><br>* `prop`<br><br>* `other` |

## Request example

### Example 1: Execute all applicable modules

When `modules` is not provided, the tool executes all applicable modules.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_aigc_video.mp4",
  "prefer_models": ["seed-2-0-pro-260328"]
}'
```

### Example 2: Check reference consistency with reference images

When the `reference_consistency` module is enabled, you must provide `reference_images`. The following example combines a product reference image to check reference consistency, world plausibility, and content continuity (this is the request that corresponds to the task shown in [Asynchronous task result](https://docs.byteplus.com/en/docs/25/123402#asynchronous-task-result)).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_aigc_video.mp4",
  "modules": ["reference_consistency", "world_plausibility", "content_continuity"],
  "reference_images": [
    {
      "image_url": "https://example.com/product_ref.png",
      "category": "product"
    }
  ],
  "prefer_models": ["seed-2-0-pro-260328"]
}'
```

## Response

After you call the API to submit a task, the API immediately returns a synchronous response indicating whether the task was successfully submitted to the background processing queue.

### Response parameters

|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was successfully submitted.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier of the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and result. |
|`request_id` |String |The unique identifier of this API request, which can be used for troubleshooting. |
|`error` |Object |The error details object, returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task#error-object) below. |

#### The error object

|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For details about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error. For example, `BadRequest`. |
|`message` |String |A detailed description of the error, which can be used for development and debugging. |
|`param` |String |The specific parameter that caused the error. This field is optional. |

### Response examples

#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-evaluate-aigc-video-quality-123456789",
  "request_id": "20261012194945ABCDEF0123456789"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20261012195005XYZW0123456789",
  "error": {
    "code": "InvalidParameter",
    "message": "reference_images must contain at least one non-empty image_url when modules contains reference_consistency",
    "param": "reference_images",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

The AIGC video quality check runs as an asynchronous task. The execution status and final result are not returned synchronously when you submit the task. You can use either of the following methods to obtain the task result:

* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

After the task is successfully completed, the `result` field in the task details contains the following fields.

|Parameter |Type |Example value |Description |
|---|---|---|---|
|`issues` |Array of Object |See the example below |The list of detected issues. When no issue is detected, this is an empty array `[]`. Each element represents a detected issue. For details, see [The issue object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task#issue-object) below. |
|`duration` |Number |`12.5` |The duration of the video, in seconds, used for metering and billing. |

### The issue object

|Parameter |Type |Example value |Description |
|---|---|---|---|
|`module` |String |`world_plausibility` |The detection module the issue belongs to. One of `reference_consistency`, `world_plausibility`, `content_continuity`, or `visual_fidelity`. |
|`type` |String |`gravity_plausibility` |The specific issue type (such as `gravity_plausibility` or `character_identity_consistency`), used to assist with issue statistics. |
|`description` |String |`An arm clips through the character between the 3rd and 5th second.` |A human\-readable description of the issue. |
|`time_range` |Array of Array of Number |`[[3.2, 5.8], [12.0, 14.5]]` |The list of time ranges (in seconds) where the issue appears, used by the player for positioning and seeking. This is a two\-dimensional array, where each element is a `[start, end]` range; multiple time ranges can be returned. |
|`annotated_frames` |Array of String |`["https://.../frame_1.jpg", "https://.../frame_2.jpg"]` |The list of annotated image URLs of representative problematic frames (one or more of the most representative frames; entity continuity issues return at least 2 frames). |

The following example shows a complete task details response (it corresponds to [Example 2: Check reference consistency with reference images](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task#example-2-check-reference-consistency-with-reference-images), which enables `reference_consistency`, `world_plausibility`, and `content_continuity` and provides a `product` reference image).

```JSON
{
    "success": true,
    "task_id": "amk-tool-evaluate-aigc-video-quality-123456789",
    "request_id": "20261012194945ABCDEF0123456789",
    "status": "completed",
    "result": {
        "duration": 15.134,
        "issues": [
            {
                "module": "reference_consistency",
                "type": "reference_gate",
                "description": "The target reference product is visible in the video frames at 3000ms, 4000ms, and 5000ms, matching the product appearance in the reference image, with no noticeable mismatch.",
                "time_range": [[0, 0]],
                "annotated_frames": [
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_01.jpg?preview=1&auth_key=***",
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_02.jpg?preview=1&auth_key=***",
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_03.jpg?preview=1&auth_key=***"
                ]
            },
            {
                "module": "world_plausibility",
                "type": "motion_rationality",
                "description": "The character's actions and interactions with objects are continuous and logically coherent: pointing at the floor to introduce the flooring issue, taking out the floor paint bucket and opening the lid, applying the paint with a roller, and showing the finished floor. The actions transition in line with real-world behavior logic, with no implausible motion gaps.",
                "time_range": [[0, 15]],
                "annotated_frames": [
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_04.jpg?preview=1&auth_key=***",
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_05.jpg?preview=1&auth_key=***"
                ]
            },
            {
                "module": "content_continuity",
                "type": "product_consistency",
                "description": "Within 0-15 seconds, the appearance of the work clothes worn by the character remains consistent throughout, and the floor paint stays coherent and uniform from packaging display and lid opening to the finished application result, with no abnormal appearance changes.",
                "time_range": [[0, 15]],
                "annotated_frames": [
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_06.jpg?preview=1&auth_key=***",
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_07.jpg?preview=1&auth_key=***"
                ]
            }
        ]
    },
    "expires_at": 1791892453,
    "created_at": 1791805785,
    "finished_at": 1791806054
}
```
