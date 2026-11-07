---
title: "Create a semantic segmentation (pro) task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment-pro`

This API submits an asynchronous semantic segmentation (pro) task. Building on the basic edition's semantic segmentation, it combines shot boundaries, scene semantics, ASR/OCR text, and duration constraints to split a long video into segments that are semantically complete and appropriately sized. It supports short dramas, film and TV series, mini\-games, and custom strategies. The detailed segment, shot, scene, and sentence results are returned directly in the task result.

> **Note**

> For the complete usage flow and application examples, see [Semantic segmentation (pro)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-semantic-segmentation-pro).

## Request parameters

### Header

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example.com/media.mp4` |The URL of the video to be segmented.<br><br><br>* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* Video duration: A single video must not exceed 3.5 hours. |
|`strategy` |String |Yes |`short_drama` |The segmentation strategy. The following values are supported:<br><br><br>* `short_drama`: Short dramas and narrative content. Fuses OCR and ASR and protects sentence integrity.<br><br>* `movie_series`: Film and TV series content. Automatically performs scene detection and semantic merging.<br><br>* `mini_game`: Mini\-game screen recordings. Filters out static, low\-quality, and pop\-up segments.<br><br>* `custom`: Custom scene detection and sentence\-integrity protection. |
|`min_duration` |Integer |No |`3` |The minimum duration of a single segment, in seconds. The value range is `[1, 600]`, and it must not be greater than `max_duration`. Defaults to `3` seconds when omitted. |
|`max_duration` |Integer |No |`30` |The maximum duration of a single segment, in seconds. The value range is `[1, 600]`, and it must not be less than `min_duration`. Defaults to `30` seconds when omitted. |
|`enable_scene_detection` |Boolean |No |`false` |Whether to enable scene detection. This takes effect only when `strategy` is `custom`; other `strategy` options use their own built\-in configurations, and this parameter has no effect.<br><br><br>* `true`: Enabled. The system performs semantic scene merging on top of shot segmentation.<br><br>* `false`: (Default) Disabled. |
|`avoid_sentence_cutoff` |Boolean |No |`false` |Whether to enable sentence detection and try to avoid cutting a segment in the middle of a sentence. This takes effect only when `strategy` is `custom`; other `strategy` options use their own built\-in configurations, and this parameter has no effect.<br><br><br>* `true`: Enabled. The system tries to cut at complete sentence boundaries. This capability relies on ASR/OCR; for videos with no recognizable speech or subtitles, enabling it may have no noticeable effect.<br><br>* `false`: (Default) Disabled. |
|`return_segment_videos` |Boolean |No |`false` |Whether to generate and return segment video files.<br><br><br>* `true`: Generates a video file for each segment and returns its download link in the `segments[].video_url` field of the task result.<br><br>* `false`: (Default) Does not generate segment videos and returns only metadata such as segment timelines. |
|`include_detail_types` |Array |No |`["shot_list", "scene_list"]` |Controls which optional details are included in the task result. Multiple values can be selected. The supported values are:<br><br><br>* `shot_list` (shot list)<br><br>* `scene_list` (scene shot list)<br><br>* `sentence_list` (sentence results)<br><br><br>The segment list `segments` is always returned. Defaults to an empty array `[]`.<br><br>Because the `shot_ids` field in the `Scene` object and the `Sentence` object references specific information in the shot list `shots`, when you request `scene_list` or `sentence_list` in `include_detail_types`, we recommend that you also include `shot_list`. Otherwise, `shot_ids` cannot be resolved to the corresponding shot details in the returned result. |
|`client_token` |String |No |`your_unique_request_id_135` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the default queue within the project associated with your API key. You can create and manage queues on the Queues page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

## Request example

The following example demonstrates how to perform pro semantic segmentation on a short\-drama video and additionally return shot details.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/semantic-segment-pro' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_url": "https://example.com/your_long_video.mp4",
  "strategy": "short_drama",
  "min_duration": 5,
  "max_duration": 20,
  "include_detail_types": ["shot_list"]
}'
```

## Response

After you call the API to submit the task, the API immediately returns a synchronous response indicating whether the task successfully entered the background processing queue.

### Response parameters

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |The error detail object, returned only when `success` is `false`. See the [Error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task#error-object) below. |

#### Error object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information about each error code, see [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The macro type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |

### Response example

#### Success response

```JSON
{
  "success": true,
  "task_id": "amk-tool-semantic-segment-pro-123456789",
  "request_id": "20260807130000ABCDEFG12345"
}
```

#### Failure response

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20260807130500XYZW12345",
  "error": {
    "code": "InvalidParameter",
    "message": "`strategy` is required.",
    "param": "strategy",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Semantic segmentation (pro) is an asynchronous task. The execution status and final result are not returned synchronously at submission time. You can obtain the task result in the following two ways:

* **Method 1 (polling)** : Use the `task_id` obtained at submission time to periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the `status` field becomes `completed` or `failed`.

* **Method 2 (event notification)** : Configure a callback\-receiving URL in advance in the AI MediaKit console, or specify a callback address for a single task via the `callback_url` parameter when submitting the task. Once the task is complete, the system POSTs the detailed information containing the final result to your specified address. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When the task is successfully completed, the `result` field in the task information you obtain contains the following. The segment list `segments` is always returned; details such as `shots`/`scenes`/`sentences` are returned on demand based on the request parameter `include_detail_types` and the selected strategy.

|Parameter |Type |Description |
|---|---|---|
|`duration` |Number |The total duration of the input video, in seconds, used for metering and billing. |
|`segment_count` |Integer |The total number of segments. |
|`segments` |Array |The list of semantic segments. Always returned, arranged in chronological order. See the [Segment object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task#segment-object) below for the element structure. |
|`shot_count` |Integer |The total number of shots. Returned only when the request parameter `include_detail_types` includes `shot_list` and the underlying workflow successfully produces shot results. |
|`shots` |Array |The shot list. Returned only when the request parameter `include_detail_types` includes `shot_list` and the underlying workflow successfully produces shot results. See the [Shot object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task#shot-object) below for the element structure. |
|`scene_count` |Integer |The total number of scene shots. Returned only when the request parameter `include_detail_types` includes `scene_list`, and `strategy` is `movie_series`, or `strategy` is `custom` with `enable_scene_detection` set to `true`. |
|`scenes` |Array |The scene shot list. Returned only when the request parameter `include_detail_types` includes `scene_list`, and `strategy` is `movie_series`, or `strategy` is `custom` with `enable_scene_detection` set to `true`. See the [Scene object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task#scene-object) below for the element structure. |
|`sentence_count` |Integer |The total number of sentence results. Returned only when the request parameter `include_detail_types` includes `sentence_list`, the selected `strategy` enables sentence detection, and the video contains recognizable speech or subtitles. The `mini_game` strategy never returns this list. |
|`sentences` |Array |The sentence result list. Returned only when the request parameter `include_detail_types` includes `sentence_list`, the selected `strategy` enables sentence detection, and the video contains recognizable speech or subtitles. The `mini_game` strategy never returns this list. See the [Sentence object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-semantic-segmentation-pro-task#sentence-object) below for the element structure. |

### Segment object

|Parameter |Type |Description |
|---|---|---|
|`index` |Integer |The segment index, starting from `0` and increasing sequentially. |
|`start_ms` |Integer |The start time of the segment, in milliseconds. |
|`end_ms` |Integer |The end time of the segment, in milliseconds. |
|`start` |String |The start time of the segment, in the format `HH:MM:SS.mmm`. |
|`end` |String |The end time of the segment, in the format `HH:MM:SS.mmm`. |
|`shot_ids` |Array |The list of shot IDs contained in this segment. |
|`text` |String |The text content of this segment. Strategies without text, such as `mini_game`, do not return this field. |
|`video_url` |String |The download link of the segment video. Returned only when `return_segment_videos=true` and the video is successfully generated. |

### Shot object

Returned only when `include_detail_types` includes `shot_list` and the underlying workflow produces shot results.

|Parameter |Type |Description |
|---|---|---|
|`id` |Integer |The shot ID. |
|`start_ms` |Integer |The start time of the shot, in milliseconds. |
|`end_ms` |Integer |The end time of the shot, in milliseconds. |
|`start` |String |The start time of the shot, in the format `HH:MM:SS.mmm`. |
|`end` |String |The end time of the shot, in the format `HH:MM:SS.mmm`. |
|`frames` |Array |The start and end frame numbers of the shot, in the format `[start_frame, end_frame]`. |
|`text` |String |The shot text; not returned when there is no text. |

### Scene object

Returned only when the request parameter `include_detail_types` includes `scene_list`, and `strategy` is `movie_series`, or `strategy` is `custom` with `enable_scene_detection` set to `true`.

|Parameter |Type |Description |
|---|---|---|
|`start_ms` |Integer |The start time of the scene, in milliseconds. |
|`end_ms` |Integer |The end time of the scene, in milliseconds. |
|`start` |String |The start time of the scene, in the format `HH:MM:SS.mmm`. |
|`end` |String |The end time of the scene, in the format `HH:MM:SS.mmm`. |
|`shot_ids` |Array |The list of shot IDs contained in this scene. |

### Sentence object

Returned only when the request parameter `include_detail_types` includes `sentence_list`, the selected `strategy` enables sentence detection, and the video contains recognizable speech or subtitles. The `mini_game` strategy never returns this list.

|Parameter |Type |Description |
|---|---|---|
|`speaker_id` |Integer |The speaker ID. |
|`text` |String |The sentence text. |
|`start_ms` |Integer |The start time of the sentence, in milliseconds. |
|`end_ms` |Integer |The end time of the sentence, in milliseconds. |
|`start` |String |The start time of the sentence, in the format `HH:MM:SS.mmm`. |
|`end` |String |The end time of the sentence, in the format `HH:MM:SS.mmm`. |
|`shot_ids` |Array |The list of shot IDs associated with this sentence. |

Example of a complete final task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-semantic-segment-pro-123456789",
    "request_id": "20260807130000ABCDEFG12345",
    "result": {
        "duration": 185.5,
        "segment_count": 2,
        "segments": [
            {
                "index": 0,
                "start_ms": 0,
                "end_ms": 12500,
                "start": "00:00:00.000",
                "end": "00:00:12.500",
                "shot_ids": [0, 1],
                "text": "Segment text",
                "video_url": "https://example.byteplus.com/segment_0.mp4?auth_key=..."
            },
            {
                "index": 1,
                "start_ms": 12500,
                "end_ms": 27800,
                "start": "00:00:12.500",
                "end": "00:00:27.800",
                "shot_ids": [2, 3],
                "text": "Segment text",
                "video_url": "https://example.byteplus.com/segment_1.mp4?auth_key=..."
            }
        ],
        "shot_count": 4,
        "shots": [
            {
                "id": 0,
                "start_ms": 0,
                "end_ms": 4500,
                "start": "00:00:00.000",
                "end": "00:00:04.500",
                "frames": [1, 135],
                "text": "Dialogue text"
            }
        ]
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```
