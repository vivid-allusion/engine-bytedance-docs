---
title: "Highlight clipping"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-highlight-clipping"
---

AI MediaKit's highlight clipping tool uses large language models to find key moments in one or more videos, then selects, trims, and combines them into highlight reels with your requested target durations. Use a scene preset, define your own scoring criteria, or specify a storyline to guide the edit. The tool supports a range of uses, including sports highlights, product launches, content marketing, educational videos, and brand campaigns.

This guide starts with a football match example, then covers scene presets, custom scoring criteria, structured highlight data, and a compilation of short drama episodes.

## Quickstart: Generate football highlights

Generate two highlight reels, with target durations of 60 and 90 seconds, from a single football match video.

### Prerequisites

* **Create an API key**: Open the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console and create an API key to authenticate media processing requests.

* **Prepare a video**: Upload your video to a publicly accessible server or [BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload), and obtain a public HTTP/HTTPS URL for the API request.

### Procedure

Highlight clipping runs asynchronously:

1. Submit a task with the [Create a highlight clipping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task) API and save the returned `task_id`.

2. Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until `status` is `completed` or `failed`, or configure [event notifications](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to receive task status updates.

3. When `status` is `completed`, read `result.outputs` to get the download URL for each highlight reel. If the task fails, check the `error` field for details.

#### Step 1: Submit the task

Use the [Create a highlight clipping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task) API to submit the request. The following cURL example uses the `football` preset to generate two highlight reels with target durations of 60 and 90 seconds.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_urls": ["https://example.byteplus.com/football-match-full.mp4"],
  "preset": "football",
  "target_duration": [60, 90]
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your API key.

* > Replace the URL in `video_urls` with your own video URL.

* > `target_duration`: The target duration of each highlight reel, in seconds. This example requests a 60\-second reel and a 90\-second reel. Actual durations may vary depending on the selected clips and replay policy.

* > `preset`: The `football` preset applies analysis and scoring criteria tailored to football matches.

A successful request returns a `task_id`. Save it to query the task status and results.

```JSON
{
    "success": true,
    "task_id": "{task_id}",
    "request_id": "{request_id}"
}
```

#### Step 2: Get the result

Poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until `status` is `completed` or `failed`. If it is `failed`, check the `error` field for details.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task completes successfully, the response contains the generated videos in `result.outputs`, in the same order as `target_duration`. Download and save each video within 24 hours, before its download URL expires. The `duration` in each output is its actual video duration; `result.duration` is the billable duration.

```JSON
{
    "success": true,
    "task_id": "{task_id}",
    "request_id": "{request_id}",
    "status": "completed",
    "result": {
        "duration": 7351.2,
        "input_duration": 7200.0,
        "outputs": [
            {
                "index": 0,
                "target_duration": 60,
                "video_url": "https://example.byteplus.com/highlight-60s.mp4",
                "duration": 60.5,
                "segments": [
                    {
                        "video_index": 0,
                        "segment_index": 0,
                        "source": "https://example.byteplus.com/football-match-full.mp4",
                        "title": "No. 10 scores from long range",
                        "summary": "The midfielder scores a crucial long-range goal in the 75th minute.",
                        "reason": "The goal changes the course of the match and captures the excitement of the game.",
                        "spans": [
                            {
                                "source_start_ms": 4500000,
                                "source_end_ms": 4515000
                            }
                        ]
                    }
                ]
            },
            {
                "index": 1,
                "target_duration": 90,
                "video_url": "https://example.byteplus.com/highlight-90s.mp4",
                "duration": 90.7
            }
        ]
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

## Advanced usage

### Use a scene preset

Use `preset` to apply analysis and scoring criteria tailored to your content without writing a custom prompt. A preset supplies defaults for strategies and prompts you have not explicitly set. The available presets are `football`, `basketball`, `automotive`, `finance`, `product_launch`, `ecommerce`, `knowledge_share`, and `short_drama`. Every request must include at least one of `preset` or `scoring_prompt`.

The following example requests 30\-second and 60\-second basketball highlight reels.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_urls": ["https://example.com/basketball-game.mp4"],
  "target_duration": [30, 60],
  "preset": "basketball"
}'
```

### Define custom scoring criteria

Use `scoring_prompt` to describe what makes a moment worth including. The model scores and selects clips against these criteria. Use `analysis_prompt` to specify additional information to capture during analysis. Each prompt can contain up to 5,000 characters.

The following example selects goals, shots, saves, and celebrations from a football match, and asks the model to record the score shown on screen.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_urls": ["https://example.com/demo/match.mp4"],
  "target_duration": [60],
  "scoring_prompt": "Select goals, impressive shots, key saves, and close-ups of player celebrations.",
  "analysis_prompt": "Record the score shown on screen during each clip."
}'
```

### Return structured highlight data only

Set `skip_video_output` to `true` if you need clip metadata for your own editing workflow, such as source videos, timestamps, titles, and summaries. The task returns structured highlight data in `outputs`, including `segments`, without rendering a video. `outputs[].video_url` may be an empty string or `null` and does not contain a download URL.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_urls": ["https://example.com/demo/match.mp4"],
  "target_duration": [60],
  "preset": "football",
  "skip_video_output": true
}'
```

## Use case: Create a short drama compilation

To promote a short drama series, you can open with highlights from the first few episodes, then follow them with the full series in a single video. Use `preset=short_drama` and combine the following parameters:

* **Select an opening hook**: Set `analysis_video_count` to analyze only the first N videos, such as the first 10 episodes. N must be between 1 and the number of input videos. If omitted, all input videos are analyzed. This setting limits highlight selection; intro/outro detection and source video appending still cover all inputs.

* **Append the episodes**: Set `append_source_video` to `true` to add all input videos after the highlights, in `video_urls` order. This option takes effect only with `preset=short_drama` and `skip_video_output=false`. It defaults to `false`.

* **Remove intros, outros, and repeated content**: Set `analyze_intro_outro_info` to `true` to detect intros and outros in all source videos and return the detected intervals in `source_video_info`. Detection applies only to `short_drama` and defaults to `false`; it examines the first and last 10 seconds of each complete source video by default. If detection fails, the task fails. When `append_source_video` is `true`, the service removes detected intros and outros and removes duplicate content from adjacent episodes. If intro/outro detection is disabled, it appends each source video in full.

* **Render the video**: Keep `skip_video_output` set to `false`, its default value, to generate the final compilation.

The following example creates an opening highlight reel with a target duration of 60 seconds from the first two episodes, detects intros and outros in all three episodes, and appends the episodes after the highlights. `target_duration` applies to the highlight section; the full compilation also includes the appended episodes.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
--header 'Authorization: Bearer {Your_API_Key}' \
--header 'Content-Type: application/json' \
--data '{
  "video_urls": [
    "https://example.com/episode-1.mp4",
    "https://example.com/episode-2.mp4",
    "https://example.com/episode-3.mp4"
  ],
  "target_duration": [60],
  "preset": "short_drama",
  "analysis_video_count": 2,
  "analyze_intro_outro_info": true,
  "append_source_video": true,
  "skip_video_output": false
}'
```

## References

### Billing

AI MediaKit charges for highlight clipping based on the billable duration returned in `result.duration`. This is the sum of the effective input duration analyzed for highlights, the actual duration of the generated highlight sections across all outputs, and the billable intro/outro analysis duration, as applicable. For billing scenarios and duration calculations for different parameter combinations, see [Highlight Clipping Pricing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#3f805d76).

### Limits

|Category |Limits |
|---|---|
|Input video sources |Each request accepts 1–100 videos. Only publicly accessible HTTP/HTTPS URLs are supported. |
|Supported formats |Common formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, and `mkv`. |
|Input duration |Each video must be no longer than 3 hours. All input videos combined must be no longer than 15 hours. |
|Input language |`voice_language` specifies the spoken language for ASR when the workflow uses it; it does not enable ASR. If omitted or empty, the language is detected automatically, including Chinese, English, and the Chinese dialects listed in the API reference. Chinese (`zh-CN`) and English (`en-US`) are fully supported; recognition quality for other supported languages is not guaranteed. See [Create a highlight clipping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task) for the full language list. |
|Output language |`output_language` sets the language of structured titles, summaries, and selection reasons. Supports `zh-CN` (Simplified Chinese) and `en-US` (English). Defaults to `en-US` when omitted or empty. |
|Target durations |`target_duration` accepts 1–5 unique values, in seconds. Each must be at least 1 and less than the effective cumulative highlight analysis duration after applying `analysis_video_count` and any applicable `time_range`. Actual highlight durations may vary. |

## Related APIs

* [Create a highlight clipping task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
