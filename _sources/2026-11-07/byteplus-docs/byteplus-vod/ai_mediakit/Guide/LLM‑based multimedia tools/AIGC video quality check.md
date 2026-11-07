---
title: "AIGC video quality check"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-aigc-video-quality-check"
---

The AI MediaKit AIGC Video Quality Check tool is designed for AIGC video production scenarios. It checks a video (optionally combined with reference images) for quality issues such as reference consistency, world plausibility, content continuity, and visual fidelity on demand. It automatically locates abnormal time ranges and outputs issue descriptions and representative problematic frames, helping you quickly decide whether to adopt, review, or regenerate the video. You can use it independently to check generated results, or integrate it into a creation agent to form a "video generation \- quality check \- manual review or regeneration" production loop.

This guide walks you through:

* Understanding the detection modules and issue types of AIGC Video Quality Check.

* Quickly trying out how to run a full\-module quality check on an AIGC video.

* Mastering how to combine check modules by scenario and how to check reference consistency with reference images.

## Detection modules and issue types

AIGC Video Quality Check provides 4 detection modules through the `modules` parameter, covering the most common quality issues in AIGC video production. You can freely combine them by business scenario. Each detected issue is labeled with the module it belongs to (`module`) and its specific issue type (`type`) in the result.

|Detection module (`module`) |Description |Typical issue types |
|---|---|---|
|`reference_consistency` |Compares elements in the video with the reference images you provide. |Character identity consistency, character clothing consistency, product appearance consistency, scene consistency |
|`world_plausibility` |Checks whether the visuals conform to physical and motion laws. |Gravity, collision, fluid behavior, support and balance, inertial motion continuity, light and reflection consistency, scale and perspective consistency, abnormal human interaction and wearing, abnormal entities, other physical anomalies |
|`content_continuity` |Identifies the main character and main product in the video and checks whether they remain consistent across the full timeline. |Character identity continuity, product appearance continuity |
|`visual_fidelity` |Checks the structural plausibility and naturalness (AI feel) of the generated visuals. |Naturalness, human body structure, object structure, text structure (supports Chinese and English font structure detection) |

## Typical scenarios

* **AI short drama and comic drama QA**: Check the consistency of character appearance, clothing, props, and scenes, as well as motion continuity and physical plausibility, to avoid character face swaps, abrupt object changes, and plot inconsistencies.

* **E\-commerce and advertising asset video QA**: Combined with reference images, check whether the product appearance, color, logo, packaging text, and brand elements remain consistent, and detect issues such as product deformation, visual timing, and physical behavior.

* **Creation agent production loop**: Automatically trigger a quality check after a video is generated. Qualified videos proceed to editing, suspected\-issue videos are routed to manual review, and videos with severe issues are automatically regenerated.

## Quickstart: Check the quality of an AIGC video

This section demonstrates how to submit an AIGC Video Quality Check task that runs all applicable modules on a video without specifying any check module.

### Prerequisites

* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Enable the ModelArk large model service**: AIGC Video Quality Check relies on ModelArk vision large models to perform the assessment. Go to the [ModelArk console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint) and ensure that the required large models (such as the Doubao large models) are enabled and available under your account. The model's capability affects the detection results, so we recommend using a pro model of the `seed` series, for example `seed-2-0-pro-260328`.

* **Perform cross\-service authorization**: Before using this tool for the first time, go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console to grant AI MediaKit permission to access your **ModelArk** resources. Otherwise, the task will fail due to insufficient permissions.

* **Prepare a video file**: Have a video file ready for assessment and upload it to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain a URL that the API can call.

### Procedure

AIGC Video Quality Check runs as an asynchronous task. The overall workflow is as follows:

1. After you call `POST /api/v1/tools/evaluate-aigc-video-quality` to submit the task successfully, you receive a unique `task_id`.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task completion notifications.

3. Once the task is complete, parse the `result` field in the response to get the detected issues from the `issues` field. When no issue is detected, `issues` is an empty array.

#### Step 1: Submit the task

Call the [Create an AIGC video quality check task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task) API. You can copy the following cURL command to submit a task that runs all applicable modules.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_aigc_video.mp4",
  "prefer_models": ["seed-2-0-pro-260328"]
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > `video_url`: Replace it with the URL of your own video file.

* > `prefer_models`: The Model ID used for the assessment. The model's capability affects the detection results, so we recommend using a pro model of the `seed` series, for example `seed-2-0-pro-260328`. You can view the Model IDs available under your account on the [ModelArk console](https://console.byteplus.com/ark/region:ark+ap-southeast-1/endpoint).

Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-evaluate-aigc-video-quality-123456789",
  "request_id": "20261012194945ABCDEF0123456789"
}
```

#### Step 2: Get the result

Because processing takes some time, poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task is successfully completed, you will receive the following response. Each object in the `result.issues` array represents a conclusion from one detection module, including the detection module `module`, the issue type `type`, the description `description`, the time ranges `time_range` (a two\-dimensional array, in seconds), and representative frames `annotated_frames`. `result.duration` is the video duration in seconds, used for metering and billing.

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
                "module": "world_plausibility",
                "type": "motion_rationality",
                "description": "The character's actions and interactions with objects are continuous and logically coherent: pointing at the floor to introduce the flooring issue, taking out the floor paint bucket and opening the lid, applying the paint with a roller, and showing the finished floor. The actions transition in line with real-world behavior logic, with no implausible motion gaps.",
                "time_range": [[0, 15]],
                "annotated_frames": [
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_01.jpg?preview=1&auth_key=***",
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_02.jpg?preview=1&auth_key=***"
                ]
            },
            {
                "module": "content_continuity",
                "type": "product_consistency",
                "description": "Within 0-15 seconds, the appearance of the work clothes worn by the character remains consistent throughout, and the floor paint stays coherent and uniform from packaging display and lid opening to the finished application result, with no abnormal appearance changes.",
                "time_range": [[0, 15]],
                "annotated_frames": [
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_03.jpg?preview=1&auth_key=***",
                    "https://example.byteplus.com/evaluation/xxxxxxxx/frame_04.jpg?preview=1&auth_key=***"
                ]
            }
        ]
    },
    "expires_at": 1791892453,
    "created_at": 1791805785,
    "finished_at": 1791806054
}
```

When no issue is detected, `issues` is an empty array:

```JSON
{
    "success": true,
    "task_id": "amk-tool-evaluate-aigc-video-quality-987654321",
    "request_id": "20261012195500HIJKLM9876543210",
    "status": "completed",
    "result": {
        "issues": [],
        "duration": 10.0
    },
    "expires_at": 1791892700,
    "created_at": 1791805900,
    "finished_at": 1791805980
}
```

## Advanced usage

### Combine check modules by scenario

The quickstart does not provide `modules`, so it runs all applicable modules. You can also use the `modules` parameter to freely combine check dimensions by business scenario. The available modules are:

* `reference_consistency`: Reference consistency. Compares elements in the video with the provided reference images. `reference_images` must be provided when this module is enabled (array length 1 to 6, and each image must be labeled with its `category`: `character`, `clothing`, `product`, `scene`, `prop`, or `other`).

* `world_plausibility`: World plausibility. Checks whether the visuals conform to physical and motion laws (such as gravity, collision, clipping, and inertia).

* `content_continuity`: Content continuity. Checks whether entities such as characters and products remain consistent over time.

* `visual_fidelity`: Visual fidelity. Checks the structure and naturalness of human bodies, objects, and text.

The following example checks only world plausibility and visual fidelity:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_aigc_video.mp4",
  "modules": ["world_plausibility", "visual_fidelity"],
  "prefer_models": ["seed-2-0-pro-260328"]
}'
```

When you need to verify whether elements in the video are consistent with your reference materials, add `reference_consistency` to `modules` and provide the corresponding reference images through `reference_images`. The following example combines a product reference image to check reference consistency and content continuity:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_aigc_video.mp4",
  "modules": ["reference_consistency", "content_continuity"],
  "reference_images": [
    {
      "image_url": "https://example.com/product_ref.png",
      "category": "product"
    }
  ],
  "prefer_models": ["seed-2-0-pro-260328"]
}'
```

### Specify the output language

You can use the `output_language` parameter to control the output language of the issue descriptions (`issues[].description`). Supported values are `zh-CN` and `en-US`. When not provided, English (`en-US`) is used by default.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/evaluate-aigc-video-quality' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_aigc_video.mp4",
  "prefer_models": ["seed-2-0-pro-260328"],
  "output_language": "zh-CN"
}'
```

## Reference information

### Metering and billing

The cost of AIGC Video Quality Check consists of two parts:

* **AI MediaKit task fee**: Charged by AI MediaKit and metered by the total duration of the input video. **This fee is not charged during the public beta.**

* **ModelArk model invocation fee**: The underlying large models are provided by ModelArk. The fees you incur by using these models through cross\-service authorization are charged directly by ModelArk according to its own pricing.

### Usage limits

|Limit |Description |
|---|---|
|Input video |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* **Video duration**: A single video must not exceed 3 minutes. |
|Reference images |`reference_images` is required only when the `reference_consistency` module is enabled. The array length is 1 to 6 (at least 1 image, at most 6 images). Each image must be labeled with its `category` (`character`, `clothing`, `product`, `scene`, `prop`, or `other`). |

## Related APIs

* [Create an AIGC video quality check task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-aigc-video-quality-check-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
