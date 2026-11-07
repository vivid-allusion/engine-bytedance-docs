---
title: "Create a highlight clipping task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm`

This API submits an asynchronous highlight clipping task that intelligently identifies key moments from one or more input videos based on a scene preset, scoring criteria, or a storyline goal. It automatically selects, trims, and concatenates these moments into one or more highlight videos of the specified target durations.

> **INFO**

> For a complete usage flow and application examples, please refer to [Highlight clipping](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-highlight-clipping).

## Request parameters

### Header

|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Please refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |

### Body

|**Parameter** |**Type** |**Required** |**Example Value** |**Description** |
|---|---|---|---|---|
|`video_urls` |Array<String\> |Yes |`["https://example.com/video1.mp4"]` |An array of 1 to 100 input video URLs, which will be analyzed in order.<br><br><br>* Video source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats: Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>* Duration: Each video must not exceed 3 hours. The cumulative duration of all input videos must not exceed 15 hours. |
|`target_duration` |Array<Number\> |Yes |`[60, 180]` |An array of target durations (in seconds) for the output highlight reels. A separate video will be generated for each specified duration. For example, `[30, 60]` will produce two videos, one about 30 seconds long and another about 60 seconds long. Specify 1 to 5 durations without duplicates; for example, `[30, 30]` is invalid. Each value must be at least 1 second and less than the effective cumulative duration of the videos participating in highlight analysis, after applying `analysis_video_count` and any applicable `time_range`. The actual output duration may be shorter or longer than the target depending on the available clips and replay policy. |
|`preset` |String |No |`football` |The scene preset to use. Fills in analysis strategies and prompts that you have not explicitly specified, using defaults tailored for the selected scene. You must provide either `preset` or `scoring_prompt`. Supported values include:<br><br><br>* `football`<br><br>* `basketball`<br><br>* `automotive`<br><br>* `finance`<br><br>* `product_launch`<br><br>* `ecommerce`<br><br>* `knowledge_share`<br><br>* `short_drama` |
|`scoring_prompt` |String |No |`Goals, shots, key saves, and close-ups of player celebrations.` |Custom scoring criteria. Describe the characteristics of what you consider a highlight using natural language. The model will score and filter clips based on this description. This parameter is required if `preset` is not provided. Max length: 5000 characters. |
|`story_prompt` |String |No |`Follow the team from falling behind to equalizing and winning.` |Describe the desired storyline or editing goal in natural language. Max length: 5000 characters. This does not replace `preset` or `scoring_prompt`; at least one of those parameters is still required. |
|`analysis_prompt` |String |No |`Record the real-time score as it appears on screen.` |Additional analysis instructions. Use natural language to specify extra information for the model to focus on and extract during video analysis. Max length: 5000 characters. |
|`voice_language` |String |No |`en-US` |Specifies the spoken language in the video for Automatic Speech Recognition (ASR). This parameter only applies when ASR is already part of the processing workflow; it does not enable ASR by itself.<br><br><br>* If omitted or left empty, the language is automatically detected. Auto\-detection supports Chinese, English, Shanghainese, Minnan, Sichuanese, Shaanxi dialect, and Cantonese.<br><br>* Supported languages:<br><br>   * `zh-CN`: Simplified Chinese<br><br>   * `en-US`: English (United States)<br><br>   * `ja-JP`: Japanese<br><br>   * `id-ID`: Indonesian<br><br>   * `es-MX`: Spanish (Mexico)<br><br>   * `pt-BR`: Portuguese (Brazil)<br><br>   * `de-DE`: German<br><br>   * `fr-FR`: French<br><br>   * `ko-KR`: Korean<br><br>   * `fil-PH`: Filipino<br><br>   * `ms-MY`: Malay<br><br>   * `th-TH`: Thai<br><br>   * `ar-SA`: Arabic<br><br>   * `it-IT`: Italian<br><br>   * `bn-BD`: Bengali<br><br>   * `el-GR`: Greek<br><br>   * `nl-NL`: Dutch<br><br>   * `ru-RU`: Russian<br><br>   * `tr-TR`: Turkish<br><br>   * `vi-VN`: Vietnamese<br><br>   * `pl-PL`: Polish<br><br>   * `ro-RO`: Romanian<br><br>   * `ne-NP`: Nepali<br><br>   * `uk-UA`: Ukrainian<br><br>   * `yue-CN`: Cantonese<br><br><br>Note: Chinese (zh\-CN) and English (en\-US) are fully supported. While other languages can be processed, their quality is not guaranteed. |
|`output_language` |String |No |`en-US` |Sets the language of the output. This parameter affects the language of the `segment.title`, `segment.summary`, and `segment.reason` fields in the result. It does not change the video editing logic. If left empty or omitted, it defaults to `en-US`. Supported languages:<br><br><br>* `zh-CN`: Simplified Chinese<br><br>* `en-US`: English (United States) |
|`allow_replay` |Boolean |No |`true` |Whether to retain linked replay clips. If omitted, the selected `preset` supplies the default replay policy. `true` allows the service to select a replay based on content and target duration, with at most one replay per event; `false` excludes replays. Only specific presets support replay; enabling it for an unsupported preset returns a parameter error. Live footage and the replay of the same event are merged into one `segment` with multiple `spans`. |
|`output_spec` |Object |No |`{"format":"mxf","video_bitrate_bps":50000000}` |The output format and bitrate specification, effective only when `skip_video_output=false`. See [The output spec object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#output-spec-object) below. When `skip_video_output` is `true`, no output video is generated, but the service still validates field types, the format enum, value ranges, and the allowed combination of format and bitrate. |
|`skip_video_output` |Boolean |No |`false` |Whether to skip the final video generation, outputting only structured highlight data.<br><br><br>* `false`: (Default) Generates and returns the download URL (`video_url`) and structured data for the highlight video.<br><br>* `true`: Returns only structured data (like `segments` info) without creating a video file. `outputs[].video_url` does not provide a downloadable video URL and may be an empty string or `null`. Set this to `true` if you only need the analysis results to improve processing speed. |
|`analysis_video_count` |Integer |No |`2` |Only the first N videos in `video_urls` participate in highlight analysis and candidate selection. Must be at least 1 and no greater than the number of input videos. If omitted, all input videos are analyzed. Does not restrict intro/outro detection or source video appending. |
|`analyze_intro_outro_info` |Boolean |No |`false` |Detect structural intros and outros in all complete source videos. Effective only for `preset=short_drama`; defaults to `false`. By default, detection examines the first and last 10 seconds of each video. A detection failure causes the task to fail. Results are returned in `source_video_info`. |
|`append_source_video` |Boolean |No |`true` |Append all source videos after the highlights in input order. Effective only for `preset=short_drama` and `skip_video_output=false`; defaults to `false`. Without intro/outro detection, complete source videos are appended. With detection, the bodies remaining after intro/outro removal are appended, and adjacent source video deduplication is enabled. All source videos are appended in `video_urls` order, regardless of `analysis_video_count` or `time_range`. |
|`time_range` |Object |No |`{"start_ms": 600000, "end_ms": 1800000}` |The time range (in milliseconds) within the video to analyze, formatted as a half\-open interval, which includes the `start_ms` but excludes the `end_ms`. The system will only select highlights from this window. This parameter can be supplied only when `video_urls` contains exactly one video. See [The time range object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#f014bdf3) below for details. |
|`client_token` |String |No |`your_unique_request_id_131` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Managing costs and resources with projects and queues](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |

#### The output spec object

`output_spec` controls the output format and bitrate only when `skip_video_output=false`. Its validation rules still apply when video output is skipped.

|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`format` |String |Yes |The output container format. Supported values are `mp4` and `mxf`. Required whenever the `output_spec` object is supplied. If `output_spec` is omitted, the service outputs `mp4` by default. |
|`video_bitrate_bps` |Integer |No |The target bitrate of the video track, in bps. This field is accepted only when `format` is `mxf`. The valid range is 1000000 to 200000000. If omitted, it defaults to 50000000 (50 Mbps). Supplying this field when `format=mp4` causes request validation to fail.<br><br>**Note**: This parameter restricts only the data volume of the video track itself. Because the final MXF file also includes audio tracks and file metadata, the actual total bitrate and file size of the output video will be slightly higher than theoretical estimates based on this parameter alone. |

#### The time range object

|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|`start_ms` |Integer |Yes |The start time of the range in milliseconds. Must be greater than or equal to 0. |
|`end_ms` |Integer |Yes |The end time of the range in milliseconds. Must be greater than `start_ms` and not exceed the total video duration. |

## Request example

The following example submits a preset\-based highlight task with a storyline and MXF output.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_urls": ["https://example.com/cosmetics-ad.mp4"],
  "target_duration": [30, 60],
  "preset": "ecommerce",
  "story_prompt": "Start with user pain points, then show product benefits and results.",
  "output_spec": {
    "format": "mxf",
    "video_bitrate_bps": 50000000
  }
}'
```

The following short drama example analyzes highlights from the first two videos, detects intros and outros in all three source videos, and appends their remaining bodies after the highlights.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/video-highlights-llm' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_urls": [
    "https://example.com/episode-1.mp4",
    "https://example.com/episode-2.mp4",
    "https://example.com/episode-3.mp4"
  ],
  "target_duration": [60],
  "preset": "short_drama",
  "analysis_video_count": 2,
  "analyze_intro_outro_info": true,
  "append_source_video": true
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
    "task_id": "{task_id}",
    "request_id": "{request_id}"
}
```

#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "{request_id}",
  "error": {
    "code": "InvalidParameter",
    "message": "The parameter `target_duration` is invalid.",
    "param": "target_duration",
    "type": "BadRequest"
  }
}
```

## Asynchronous task result

Highlight clipping is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:

* Method 1: Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* Method 2: Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).

When a task is successfully completed, the `result` field in the task information you retrieve contains the following:

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`duration` |Number |The billable duration in seconds. For parameter combinations, calculation rules, and usage measurement, see [Highlight clipping pricing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#3f805d76). |
|`input_duration` |Number |The effective highlight analysis duration in seconds, restricted by `analysis_video_count` and any applicable `time_range`. It excludes intro/outro detection windows, appended source footage, and all output video durations. |
|`source_video_info` |Array of Objects |Additional information for all source inputs, including intro/outro intervals and ASR text. Returned only for `preset=short_drama`, when intro/outro detection is enabled or ASR results already exist. Entries follow input video order. Detection and ASR data are returned independently. See the source_video_info object below. |
|`outputs` |Array of Objects |The highlight output list, in the same order as the request's `target_duration` array. The structure of each object is detailed in [The output object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#b3f31334) table below. |
|`token_usage` |Object |Statistics on the total Large Language Model token consumption for this task. See [The token usage object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#7078bac1) below. |

### The source_video_info object

|Parameter |Type |Description |
|---|---|---|
|`video_index` |Integer |The 0\-based input index in `video_urls`. |
|`intro` |Object or Null |Structural intro interval. If detection is enabled but no intro is found or its trim is canceled, returns `null`. Omitted when detection is disabled. See the intro and outro objects below. |
|`outro` |Object or Null |Structural outro interval. If detection is enabled but no outro is found or its trim is canceled, returns `null`. Omitted when detection is disabled. See the intro and outro objects below. |
|`asr_lines` |Array of Objects |Original ASR text segments already available from analysis, sorted by ascending `start_ms`. Times are relative to the complete source video, in milliseconds. Does not trigger additional recognition. Omitted when no ASR result exists; returns `[]` when an existing result has no segments. See the asr_lines object below. |

#### The intro and outro objects

|Parameter |Type |Required |Description |
|---|---|---|---|
|`start_ms` |Integer |Yes |Start time in the complete source video, in milliseconds. Must be at least 0. |
|`end_ms` |Integer |Yes |End time in the complete source video, in milliseconds. Must be greater than `start_ms`. |

#### The asr_lines object

|Parameter |Type |Required |Description |
|---|---|---|---|
|`start_ms` |Integer |Yes |Start time of the ASR segment in the complete source video, in milliseconds. Must be at least 0. |
|`end_ms` |Integer |Yes |End time of the ASR segment in the complete source video, in milliseconds. Must be at least 1. |
|`text` |String |Yes |Original ASR segment text. |

### The output object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`index` |Integer |The 0\-based index of the output, corresponding to the order in the `target_duration` request array. |
|`target_duration` |Number |The requested target duration (in seconds) for this highlight video. |
|`video_url` |String or Null |The HTTPS download URL for the generated highlight video, valid for 24 hours. Download and save the video before the URL expires. If `skip_video_output` is `true`, this field does not provide a downloadable video URL and may be an empty string or `null`. |
|`duration` |Number |The actual duration (in seconds) of the complete output video, including highlights and appended source footage. Only the highlight portion contributes to billable output duration. |
|`segments` |Array of Objects |A list of objects containing detailed information about all the highlight clips that make up this video. May be omitted when no segment data is available. See [The segment object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#33926e82) below. |

### The segment object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`video_index` |Integer |The 0\-based index of the source video in the `video_urls` request array. |
|`segment_index` |Integer |The 0\-based sequence number of this clip within the current highlight video. |
|`source` |String |The URL or identifier of the source video. |
|`title` |String |The title generated by the model for this clip. |
|`summary` |String |The content summary generated by the model for this clip. |
|`reason` |String |The model's explanation for why this clip was selected as a highlight. |
|`spans` |Array of Objects |The specific time intervals of this clip within the source video. See [The span object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#6a54fd24) below. |

### The span object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`source_start_ms` |Integer |The start time of the clip in the source video, in milliseconds. |
|`source_end_ms` |Integer |The end time of the clip in the source video, in milliseconds. |

### The token usage object

This object reports the task's model token usage, including task totals and usage by endpoint. Cached, audio, and thinking tokens are breakdowns; do not add them to the totals.

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`total_input_tokens` |Integer |Total input tokens consumed by the task (including text, image, and audio). |
|`total_output_tokens` |Integer |Total output tokens generated by the task. |
|`total_cached_tokens` |Integer |Total number of input tokens that hit the context cache. |
|`total_audio_tokens` |Integer |Total number of tokens from audio input. |
|`total_audio_cached_tokens` |Integer |Total number of cached tokens from audio input. |
|`total_think_tokens` |Integer |Total tokens consumed during the model's thinking process. |
|`endpoint_token_usages` |Array of Objects |A detailed list of token usage, aggregated by the ModelArk endpoint actually called in this task. See [The endpoint token usage object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-highlight-clipping-task#ab9963d6) below. |

#### The endpoint token usage object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`endpoint` |String |The endpoint ID of the ModelArk model that was actually called. |
|`model` |String |The model name corresponding to the endpoint. |
|`input_tokens` |Integer |The number of input tokens consumed by this endpoint. |
|`output_tokens` |Integer |The number of output tokens generated by this endpoint. |
|`cached_tokens` |Integer |The number of cached input tokens consumed by this endpoint. |
|`audio_tokens` |Integer |The number of audio tokens consumed by this endpoint. |
|`audio_cached_tokens` |Integer |The number of cached audio tokens consumed by this endpoint. |
|`think_tokens` |Integer |The number of tokens consumed during thinking by this endpoint. |
|`layer_token_usages` |Array of Objects |Token usage within this endpoint, aggregated by the prompt token range of each model request. See the layer token usage object below. |

#### The layer token usage object

|**Parameter** |**Type** |**Description** |
|---|---|---|
|`prompt_token_range` |String |The prompt token range of an individual model request: `0~32000`, `32000~128000`, `128000~256000`, or `256000+`. |
|`input_tokens` |Integer |Input tokens in this range. |
|`cached_tokens` |Integer |Cached input tokens in this range. |
|`audio_tokens` |Integer |Audio input tokens in this range. |
|`audio_cached_tokens` |Integer |Cached audio input tokens in this range. |
|`think_tokens` |Integer |Thinking tokens in this range. |
|`output_tokens` |Integer |Output tokens in this range. |

### Task response example

The following example shows a completed short drama task, including highlight videos, source video information, and token usage.

```JSON
{
    "success": true,
    "task_id": "{task_id}",
    "request_id": "{request_id}",
    "status": "completed",
    "result": {
        "duration": 5510.3,
        "input_duration": 5400.0,
        "source_video_info": [
            {
                "video_index": 0,
                "intro": {
                    "start_ms": 0,
                    "end_ms": 8500
                },
                "outro": null,
                "asr_lines": [
                    {
                        "start_ms": 10240,
                        "end_ms": 13360,
                        "text": "The first episode begins."
                    }
                ]
            }
        ],
        "outputs": [
            {
                "index": 0,
                "target_duration": 30.0,
                "video_url": "https://example-video.byteplus.com/highlight_output_30s.mp4",
                "duration": 29.8,
                "segments": [
                    {
                        "video_index": 0,
                        "segment_index": 0,
                        "source": "https://example.com/episode-1.mp4",
                        "title": "The protagonist faces a dilemma",
                        "summary": "The protagonist discovers a key clue and faces a new dilemma.",
                        "reason": "Introduces the central conflict and sets up the next turning point.",
                        "spans": [
                            {
                                "source_start_ms": 10240,
                                "source_end_ms": 24680
                            }
                        ]
                    },
                    {
                        "video_index": 0,
                        "segment_index": 1,
                        "source": "https://example.com/episode-1.mp4",
                        "title": "A key clue appears",
                        "summary": "A supporting character delivers a letter that reveals an important clue.",
                        "reason": "Moves the story forward and marks a key turning point.",
                        "spans": [
                            {
                                "source_start_ms": 24680,
                                "source_end_ms": 29105
                            }
                        ]
                    }
                ]
            },
            {
                "index": 1,
                "target_duration": 60.0,
                "video_url": "https://example-video.byteplus.com/highlight_output_60s.mp4",
                "duration": 60.5
            }
        ],
        "token_usage": {
            "total_input_tokens": 1250000,
            "total_cached_tokens": 320000,
            "total_audio_tokens": 48000,
            "total_audio_cached_tokens": 0,
            "total_think_tokens": 15000,
            "total_output_tokens": 8600,
            "endpoint_token_usages": [
                {
                    "endpoint": "ep-20260101000000-abcde",
                    "model": "seed-2-0-lite-260428",
                    "input_tokens": 1100000,
                    "cached_tokens": 300000,
                    "audio_tokens": 48000,
                    "audio_cached_tokens": 0,
                    "think_tokens": 0,
                    "output_tokens": 5200,
                    "layer_token_usages": [
                        {
                            "prompt_token_range": "32000~128000",
                            "input_tokens": 1100000,
                            "cached_tokens": 300000,
                            "audio_tokens": 48000,
                            "audio_cached_tokens": 0,
                            "think_tokens": 0,
                            "output_tokens": 5200
                        }
                    ]
                },
                {
                    "endpoint": "ep-20260101000000-fghij",
                    "model": "seed-2-0-pro-260328",
                    "input_tokens": 150000,
                    "cached_tokens": 20000,
                    "audio_tokens": 0,
                    "audio_cached_tokens": 0,
                    "think_tokens": 15000,
                    "output_tokens": 3400,
                    "layer_token_usages": [
                        {
                            "prompt_token_range": "128000~256000",
                            "input_tokens": 150000,
                            "cached_tokens": 20000,
                            "audio_tokens": 0,
                            "audio_cached_tokens": 0,
                            "think_tokens": 15000,
                            "output_tokens": 3400
                        }
                    ]
                }
            ]
        }
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```
