---
title: "Adaptive video understanding"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-adaptive-video-understanding"
---

The AI MediaKit adaptive video understanding tool is based on ModelArk visual understanding models. It takes the video and natural\-language instruction (prompt) you provide and, based on the video duration, instruction content, and your specified preferences (such as cost and quality), automatically decides the optimal analysis pipeline (including the frame\-sampling strategy, whether to analyze audio, and which model to select), and ultimately outputs a video\-level structured understanding result. This tool provides truly out\-of\-the\-box video understanding that balances cost and quality for scenarios such as content moderation, video retrieval, smart tag generation, and video summarization. This development guide walks you through how to:


* Quickly submit a video to the tool and get the analysis result.

* Understand how the tool works and how parameters such as the `level` tier and `manual_option` affect the analysis strategy.

* Master the tool's advanced usage and usage limits.


<span id="6d6b3c3d"></span>
## Quickstart: Analyze a publicly accessible video

This section demonstrates how to submit an analysis task for a publicly accessible video and get the result.

<span id="af6609d1"></span>
### Prerequisites


* **Obtain an API key**: Visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your AI MediaKit API Key (used for authenticating media processing features).

* **Enable the ModelArk service**: The adaptive video understanding tool relies on ModelArk visual understanding models. Go to the [ModelArk Console](https://console.byteplus.com/ark/region:ap-southeast-1/overview) and ensure that a visual understanding model is enabled and available under your account.

* **Perform cross\-service authorization**: Before using the adaptive video understanding tool for the first time, go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console to grant AI MediaKit permission to access your ModelArk resources.

* **Prepare a video file**: Have one or more video files ready and upload them to a publicly accessible server or the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain URLs that the API can access.


<span id="58acd19f"></span>
### Procedure

Adaptive video understanding is an asynchronous task. The overall flow is as follows:


1. After you successfully call `POST /api/v1/tools/video-understand-router` to submit the task, you obtain a task ID.

2. You can poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`. Alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates.

3. Once the task is complete, parse the `result` field in the response to get the analysis result of each video in the `contents` array.


<span id="9394c406"></span>
#### Step 1: Submit the task

Call the [Create an adaptive video understanding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task) API. You can directly copy the following cURL command to submit a minimal runnable analysis task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-understand-router' \
  -H 'Authorization: Bearer {Your_API_Key}' \
  -H 'Content-Type: application/json' \
  -d '{
    "video_urls": [
      "https://example.com/sample_video.mp4"
    ],
    "prompt": "Summarize the key events in the video and mark the time range in which each event appears"
  }'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid API Key.</div>


* <div data-tips="true" data-tips-type="default">Replace the URLs in the <code>video_urls</code> list with your real video addresses.</div>


* <div data-tips="true" data-tips-type="default"><code>prompt</code> is used to guide the large model's output; you can customize it for your business scenario.</div>



Upon successful submission, you will receive the following response containing a `task_id`. Please save this ID for future queries.

```Plain Text
{
  "success": true,
  "task_id": "amk-tool-video-understand-router-123456789",
  "request_id": "20260624150000ABCDEFG12345"
}
```


<span id="4c5ac137"></span>
#### Step 2: Get the result

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Plain Text
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
  -H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1. </div>


When the task is complete, you will receive the following response. Each item in the `result.contents` array corresponds to the analysis result of the video at the same index in `video_urls`.

```JSON
{
  "success": true,
  "task_id": "amk-tool-video-understand-router-123456789",
  "request_id": "20260624150000ABCDEFG12345",
  "status": "completed",
  "result": {
    "duration": 120.5,
    "contents": [
      "The video is 120 seconds long and mainly shows city street scenes. 0-30s is a daytime overhead shot of a busy street..."
    ],
    "token_usage": {
      "input_tokens": 850,
      "output_tokens": 150,
      "total_tokens": 1000
    }
  },
  "expires_at": 1782001650,
  "created_at": 1781828767,
  "finished_at": 1781828851
}
```


<span id="1f547fbe"></span>
## Advanced usage

<span id="f7ebb100"></span>
### How it works

To balance cost, quality, and performance across different scenarios, the adaptive video understanding tool has a built\-in intelligent routing and decision mechanism.

<span id="87af3178"></span>
#### Core processing flow

After you submit a task, the system executes the following steps in order to determine the final analysis pipeline:


1. Candidate model pool confirmation:

   * If you specify `prefer_endpoints` in the request, the system prioritizes selecting a service from your specified list of custom endpoints.

   * If you do not specify `prefer_endpoints` but specify `prefer_models`, the system selects from your specified list of models.

   * If neither is specified, the system uses all available models preset under your account as the candidate pool.

2. Audio analysis detection: The system detects whether the `prompt` contains **Chinese** audio keywords (such as words meaning "sound," "music," "voice," or "dialogue"). If matched, the system forcibly enables audio analysis and selects a model that supports audio\-video multimodal understanding (currently `seed-2-0-lite-260428`). In this case, the subsequent `level` tier no longer affects model selection. 


> **Note**: Automatic keyword detection recognizes **Chinese keywords only**. If your `prompt` is in English or another language, audio analysis will not be triggered automatically—set `manual_option.need_audio` to `true` to enable it explicitly.



3. Video duration classification: The system classifies videos into three categories by duration:

   * Short video: Less than 1 minute.

   * Medium video: 1 minute to 20 minutes.

   * Long video: 20 minutes to 120 minutes.

4. Frame sampling and model selection: Based on the mode (automatic/manual), video duration, and `level` tier, the system selects the final frame\-sampling strategy and analysis model.


<span id="79d8b912"></span>
#### Automatic mode

When you do not pass the `manual_option` parameter, the task enters automatic mode. In this mode, the system automatically selects the optimal strategy based on the `level` tier and video duration.


|Video type |`level` tier |Frame\-sampling strategy |Analysis model (without audio) |
|---|---|---|---|
|Short video (< 1 minute) |This parameter is ignored |Uniform sampling at `fps=1` |`seed-2-0-mini-260428` |
|Medium/long video (≥ 1 minute) |`Economy` |**Smart frame sampling**, with a target frame count of about 30% of the total frames sampled from the original video at 1 fps |`seed-2-0-mini-260428` |
||`Balanced` |**Smart frame sampling**, with a target frame count of about 60% of the total frames sampled from the original video at 1 fps |`seed-2-0-pro-260328` |
||`Quality` |Uniform sampling at `fps=1` |`seed-2-0-pro-260328` |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Smart frame sampling: An adaptive keyframe selection algorithm based on image\-text similarity computation, designed to capture the core content of a video with fewer frames, effectively reducing the cost of analyzing long videos.</div>


* <div data-tips="true" data-tips-type="default">1000\-frame cap: To ensure processing performance, the number of frames finally extracted by all frame\-sampling strategies (including uniform sampling and smart frame sampling) is capped at 1000. If the number of frames computed by the strategy exceeds 1000, the system automatically adjusts to extract 1000 frames at equal intervals across the video's total duration.</div>


* <div data-tips="true" data-tips-type="default">Audio\-first principle: If the <code>prompt</code> matches Chinese audio keywords (see the note in the audio analysis detection step above), the model selection logic in the table above is overridden, and the system forcibly uses a model that supports audio analysis.</div>



<span id="e38319c0"></span>
#### Manual mode

When you pass the `manual_option` object in the request, the task enters manual mode, overriding part of the strategy in automatic mode.


* `manual_option.max_snapshot_number`: Directly specifies the maximum number of snapshots (frames) used for analysis, with a value range of `[0, 1000]`. This value overrides the frame\-sampling strategy determined by the `level` tier. For example, even if `level` is `Quality`, if you set `max_snapshot_number: 100`, the system extracts only 100 frames at equal intervals for analysis.

* `manual_option.fps`: Directly specifies the frame\-sampling rate, with a value range of [0.2, 5.0] and a default of 1.0. The system uniformly samples frames at the rate you specify.

* `manual_option.need_audio`: A boolean value that enables or disables audio analysis.

   * When set to `true`, the system selects a model that supports audio analysis from the candidate model pool (currently `doubao-seed-2-0-lite-260428` and `doubao-seed-2-0-mini-260428`). If no such model is in the candidate pool, the request returns an error.

   * When set to `false`, the system analyzes only the video frames.


The following request example forcibly limits the number of snapshots to 200 frames and enables audio analysis:

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-understand-router' \
  -H 'Authorization: Bearer {Your_API_Key}' \
  -H 'Content-Type: application/json' \
  -d '{
    "video_urls": ["https://example.com/sample_video.mp4"],
    "prompt": "What is the background music in this video?",
    "level": "Balanced",
    "manual_option": {
      "max_snapshot_number": 200,
      "need_audio": true
    }
  }'
```


<span id="412099b9"></span>
### Specify the analysis tier (`level`)

The tool provides 3 `level` tiers to balance speed, cost, and result quality. The default is `Economy`.


|Tier |Applicable scenarios |
|---|---|
|`Economy` |Speed\- and cost\-first, suitable for large\-batch content annotation with lower requirements for result detail. |
|`Balanced` |Balances speed and quality, suitable for general content moderation and retrieval scenarios. |
|`Quality` |Result\-quality\-first, suitable for scenarios requiring finer semantic understanding, generating high\-quality summaries, and other similar tasks. |


<span id="675f1549"></span>
#### Example: Use the `Quality` tier

```Plain Text
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-understand-router' \
  -H 'Authorization: Bearer {Your_API_Key}' \
  -H 'Content-Type: application/json' \
  -d '{
    "video_urls": ["https://example.com/sample_video.mp4"],
    "prompt": "Describe each scene of this video in detail, in a formal style.",
    "level": "Quality"
  }'
```


<span id="d744a5d4"></span>
## Reference

<span id="8743709d"></span>
### Usage limits


|Limit |Description |
|---|---|
|Input video limits |* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported. <br><br>* **Supported formats**: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. <br><br>* **Quantity limit**: A single task supports up to 10 video files. <br><br>* **Single\-video duration limit**: A single video must not exceed 2 hours. |


<span id="0638ad10"></span>
### Billing

The cost of the adaptive video understanding tool consists of the following two parts, billed separately by AI MediaKit and ModelArk based on their respective service usage:


* **AI MediaKit fee**: This fee covers media preprocessing operations such as fetching the video, smart frame sampling, and audio analysis (when the `prompt` matches Chinese keywords or it is manually enabled), and is billed based on the input video duration. For the specific unit price, see [Adaptive video understanding (pricing)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#1e818a84).

* **ModelArk fee**: This fee covers the core compute resources for the visual understanding models to understand and analyze the video content and generate structured text, and is billed based on the number of tokens actually consumed during model invocation, including input tokens and output tokens. After the task succeeds, you can get detailed token consumption data for the task in the `result.token_usage` field of the Get task details API response (see [The token usage object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task#1329818e)). For the token pricing of different models, refer to [ModelArk Pricing](https://docs.byteplus.com/en/docs/modelark/1544106).


<span id="14a4ce0a"></span>
## API references


* [Create an adaptive video understanding task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-adaptive-video-understanding-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
