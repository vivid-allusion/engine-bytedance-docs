---
title: "Script reconstruction"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-script-reconstruction"
---

To automatically convert live\-action short dramas into structured script text, you can use the AI MediaKit script reconstruction tool. This development guide provides step\-by\-step instructions on how to use API calls to submit videos for analysis. You will learn the asynchronous workflow for checking task status and how to retrieve the final, complete script file in JSON format, which greatly improves the efficiency of content analysis, repurposing, and retrieval.

## Quickstart: Perform script reconstruction

### Prerequisites

* **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

* **Prepare video files**: Have one or more episode video files ready for analysis, and upload them to a publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload) to obtain URLs for API calls.

### Procedure

Script reconstruction is an asynchronous task. The full call flow is as follows:

1. After you successfully call `POST /api/v1/tools/drama-script` to submit the task, the API returns a task ID.

2. You can poll the `GET /api/v1/tasks/{task_id}` API to query the task status until `status` becomes `completed`; alternatively, use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status changes.

3. Once the task is complete, obtain the script file download URL (`result_url`) from the `result` field in the response, and download the final JSON file.

#### Step 1: Submit the script reconstruction task

You need to call the [Create a script reconstruction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-script-reconstruction-task) API. You can directly copy the following cURL command to submit a script reconstruction task. This example inputs two episode video files.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/drama-script' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_urls": [
    "https://example.com/drama_episode_01.mp4",
    "https://example.com/drama_episode_02.mp4"
  ]
}'
```

> **INFO**

* > Replace `{Your_API_Key}` with your valid API Key.

* > `video_urls`: Replace with your own video URLs.

Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-drama-script-123456789",
  "request_id": "20240522150000ABCDEFG12345"
}
```

#### Step 2: Get the task result

Script reconstruction takes some time to process. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API to obtain the final result until the task status becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```

> **INFO**

> Replace the `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task completes successfully, you will receive a response containing the script file download URL. `result.result_url` is the download URL for the generated script file. This URL is valid for **24 hours**, so be sure to save it promptly.

```JSON
{
    "success": true,
    "task_id": "amk-tool-drama-script-123456789",
    "status": "completed",
    "result": {
        "result_url": "https://example.byteplus.com/result.json.gz?auth_key=...",
        "duration": 245.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851
}
```

#### Step 3: Download and use the script data

Access the `result_url` obtained in Step 2 to download a Gzip\-compressed JSON file. The output format varies depending on the `return_pkg` parameter you set when submitting the task.

**Default case (return_pkg=false): Get the core script data**

By default, you download a Gzip\-compressed JSON file (result.json.gz). After decompression, you obtain a JSON file containing the complete structured script data.

**Full package case (return_pkg=true): Get all parsed assets**

If you set `return_pkg: true` when submitting the task, you download an archive (.tar.gz) that contains all analysis outputs. This is useful for in\-depth custom development. The decompressed file structure is as follows:

```Plain
.tar.gz
├── result.json         # Core output: the structured script reconstruction result
├── faces/              # Character clustering images, in folders named by the recognized characters
│   ├── CharacterA/
│   │   ├── 12.jpg
│   │   └── 35.jpg
│   └── CharacterB/
│       └── 48.jpg
├── scene_frames/       # Video frame screenshots segmented by scene
    ├── 000/
    │   ├── 0001.jpg
    │   └── 0002.jpg
    └── ...
```

**Script JSON file structure example:**

```JSON
{
    "Plot": "A young woman, Shiyue, recalls how during college she \"bought\" the impoverished top student Lu Sinian...",
    "Scenes": [
        {
            "Id": 0,
            "Title": "Sweet memories of falling in love in college",
            "Start": 0,
            "End": 2,
            "Desc": "The opening is a warmly lit, soft bedroom scene...",
            "Plot": "Shiyue recalls her college romance in voice-over...",
            "StartTime": 0,
            "EndTime": 10833,
            "Segments": [
                {
                    "Id": 0,
                    "Vid": "v03cd6g10067d8j77h2ljht207m89p7g",
                    "StartInVideo": 0,
                    "EndInVideo": 3666,
                    "Start": 0,
                    "End": 3666,
                    "Plot": "The bedroom lighting is soft and warm...",
                    "AudioDesc": "Accompanied by gentle, soothing lyrical background music...",
                    "Camera": {
                        "Angle": "Eye level",
                        "Height": "Level angle",
                        "Direction": "Oblique side",
                        "LensFocalLength": "Standard",
                        "ShotSize": "Medium shot",
                        "Movement": "Fixed shot"
                    },
                    "Visual": {
                        "BackgroundBlur": "Slight blur",
                        "ColorTone": "Realistic",
                        "Style": "Warm tone",
                        "Lighting": "Soft light"
                    }
                }
            ]
        }
    ],
    "People": [
        {
            "Id": "Character101",
            "Name": "Shiyue",
            "Names": [],
            "Desc": "Was in a relationship with Lu Sinian for four years in college...",
            "Looks": "In college, wore a black embellished top...",
            "Gender": "Female",
            "Age": "Young adult",
            "RealName": "",
            "Position": "",
            "Expression": "",
            "MicroExpression": "",
            "Action": ""
        }
    ],
    "Dialogues": [
        {
            "Id": 0,
            "Start": "00:00:00.440",
            "End": "00:00:02.840",
            "Vid": "v03cd6g10067d8j77h2ljht207m89p7g",
            "VideoIndex": 0,
            "StartInVideo": "00:00:00.440",
            "EndInVideo": "00:00:02.840",
            "StartInVideoMillis": 440,
            "EndInVideoMillis": 2840,
            "SegStart": 0,
            "SegEnd": 1,
            "StartInMillis": 440,
            "EndInMillis": 2840,
            "Content": "In college, I once bought a boyfriend",
            "People": "Shiyue",
            "PeopleId": "Character101",
            "Emotion": "Calm with a touch of reminiscence",
            "EmotionId": "neutral",
            "Second": "",
            "VoiceDesc": "A young woman speaking at close range, like a voice-over, with a clear and gentle timbre and a calm, reminiscent tone.",
            "HasOnlyToneWords": null
        }
    ],
    "Videos": [
        {
            "Index": 0,
            "Vid": "v03cd6g10067d8j77h2ljht207m89p7g",
            "Height": 1920,
            "Width": 1080,
            "DurationInMillis": 159100,
            "Size": 0,
            "StoreUri": "tos-vod-cn-v-2d4440844053eb6e/7177ff5f238640cd90bf3ff3812a1cb2",
            "Plot": "Shiyue and Lu Sinian were in love for four years in college...",
            "SpeechAudioFile": "7177ff5f238640cd90bf3ff3812a1cb2_audiospeech.mp3",
            "BackgroundAudioFile": "7177ff5f238640cd90bf3ff3812a1cb2_background.mp3"
        }
    ]
}
```

**Script JSON file structure description:**

|**Field path** |**Data type** |**Example value** |**Description** |
|---|---|---|---|
|Plot |String |"The video opens with Shiyue's narration..." |An overall plot summary of all input video content. |
|Scenes |Array |[...] |The list of scene storyboards. The video is intelligently split into several logically coherent core scenes. |
|Scenes[].Id |Integer |0 |The scene index, incrementing from 0. |
|Scenes[].Title |String |"College romance and proposing a breakup" |A summary title of this storyboard scene. |
|Scenes[].Start |Integer |0 |The index in the Segments list of the first segment included in this scene. |
|Scenes[].End |Integer |2 |The index in the Segments list of the last segment included in this scene. |
|Scenes[].Desc |String |"The opening is an indoor college setting..." |A description of the visual environment of this scene. |
|Scenes[].Plot |String |"Shiyue recalls in voice\-over..." |The specific plot development and behavior summary within this scene. |
|Scenes[].StartTime |Integer |0 |The absolute start time of this scene on the global timeline, in milliseconds. |
|Scenes[].EndTime |Integer |24200 |The absolute end time of this scene on the global timeline, in milliseconds. |
|Scenes[].Segments |Array |[...] |The list of finer\-grained video segment information that makes up this core scene. |
|Scenes[].Segments[].Id |Integer |0 |The index of the segment within this scene, starting from 0. |
|Scenes[].Segments[].StartInVideo |Integer |0 |The start time of the segment within its source video, in milliseconds. |
|Scenes[].Segments[].EndInVideo |Integer |3666 |The end time of the segment within its source video, in milliseconds. |
|Scenes[].Segments[].Start |Integer |0 |The start time of the segment on the global timeline, in milliseconds. |
|Scenes[].Segments[].End |Integer |3666 |The end time of the segment on the global timeline, in milliseconds. |
|Scenes[].Segments[].AudioDesc |String |"Accompanied by gentle, soothing..." |A description of the ambient sound of this segment. |
|Scenes[].Segments[].Camera |Object |{...} |The camera parameters of this segment, including angle, shot size, and movement. |
|.Scenes[].Segments[].Camera.Angle |String |"Eye level" |The shooting angle. |
|.Scenes[].Segments[].Camera.Height |String |"Level angle" |The shooting height. |
|.Scenes[].Segments[].Camera.Direction |String |"Oblique side" |The shooting direction. |
|.Scenes[].Segments[].Camera.LensFocalLength |String |"Standard" |The lens focal length. |
|.Scenes[].Segments[].Camera.ShotSize |String |"Medium shot" |The shot size. |
|.Scenes[].Segments[].Camera.Movement |String |"Fixed shot" |The camera movement. |
|Scenes[].Segments[].Visual |Object |{...} |The visual style parameters of this segment, including color tone, lighting, and style. |
|Scenes[].Segments[].Visual.BackgroundBlur |String |"Slight blur" |The degree of background blur. |
|Scenes[].Segments[].Visual.ColorTone |String |"Realistic" |The color tone style. |
|Scenes[].Segments[].Visual.Style |String |"Warm tone" |The visual aesthetic. |
|Scenes[].Segments[].Visual.Lighting |String |"Soft light" |The lighting method. |
|People |Array |[...] |The list of character information for those appearing in the video. |
|People[].Id |String |"Character101" |The unique identifier of the appearing character. |
|People[].Name |String |"Shiyue" |The primary name or designation of the character. |
|People[].Looks |String |"College period: dark hair in an updo..." |A description of the character's visual features. |
|Dialogues |Array |[...] |A list of the dialogue from the video, transcribed sentence by sentence. |
|Dialogues[].Id |Integer |0 |The dialogue index. |
|Dialogues[].Start |String |"00:00:00.440" |The start timecode of this line of dialogue on the global timeline, in the format HH:mm:ss.SSS. |
|Dialogues[].End |String |"00:00:02.840" |The end timecode of this line of dialogue on the global timeline, in the format HH:mm:ss.SSS. |
|Dialogues[].StartInMillis |Integer |440 |The start time of this line of dialogue on the global timeline, in milliseconds. |
|Dialogues[].EndInMillis |Integer |2840 |The end time of this line of dialogue on the global timeline, in milliseconds. |
|Dialogues[].StartInVideoMillis |Integer |440 |The start time of this line of dialogue within its source video, in milliseconds. |
|Dialogues[].EndInVideoMillis |Integer |2840 |The end time of this line of dialogue within its source video, in milliseconds. |
|Dialogues[].VoiceDesc |String |"A young woman speaking at close range..." |A description of the speaker's voice characteristics (such as timbre and tone). |
|Dialogues[].PeopleId |String |"Character101" |The unique character ID of the speaker, corresponding to People[].Id. |
|Videos |Array |[...] |The metadata list of the input source videos. |
|Videos[].SpeechAudioFile |String |"..._audiospeech.mp3" |The filename of the separated human\-voice audio for this video. |
|Videos[].BackgroundAudioFile |String |"..._background.mp3" |The filename of the separated background audio for this video. |

## Advanced usage

### Specify the output language (`output_language`)

Use `output_language` to control the language of the output script. It supports `zh-CN` (Simplified Chinese) and `en-US` (US English). When left empty or unset, the default language is English (`en-US`).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/drama-script' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "video_urls": ["https://example.com/drama_episode_01.mp4"],
  "output_language": "en-US"
}'
```

### Specify the spoken language (`voice_language`)

Use `voice_language` to specify the spoken language in the video for speech recognition (ASR). If left empty or unset, the tool automatically detects the language. Chinese (`zh-CN`) and English (`en-US`) are explicitly supported; the other languages are usable but their recognition quality is not guaranteed.

### Get all parsed assets (`return_pkg`)

Set `return_pkg` to `true` to package all task outputs into a `.tar.gz` archive, which additionally includes character images and per\-scene screenshots on top of the core script JSON. This is useful for in\-depth secondary development. See [Step 3: Download and use the script data](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-script-reconstruction#step-3-download-and-use-the-script-data).

## Reference

### Usage limits

To ensure the best reconstruction results, note the following input limits:

|Limit |Description |
|---|---|
|Content type |Suitable for live\-action content centered on character dialogue and plot development, such as short dramas, series, and films. Not suitable for content lacking coherent live\-action plot or facial\-recognition cues, such as animation, documentaries, ads, or livestream recordings. |
|Subtitle requirement |Videos must contain clearly legible embedded (hard) subtitles. |
|Language support |* Input video language: By default, the main language in the video is auto\-detected (supports Chinese, English, and some dialects). You can also specify the language via `voice_language` to improve recognition accuracy.<br><br>* Output script language: Supports output as Simplified Chinese (`zh-CN`) or English (`en-US`), with English as the default. You can set it via `output_language`. |
|Resolution |All videos submitted in one task must have identical resolution (width and height). |
|Quantity and duration |* A single task supports 1 to 100 video files.<br><br>* A single file must not exceed 120 minutes.<br><br>* The cumulative duration of all videos must not exceed 300 minutes. |
|Video format |Supports mainstream video formats such as mp4, mov, and mkv. HLS (M3U8) is not supported. |

### Billing

The script reconstruction tool uses a **pay\-as\-you\-go** model, billed by input video duration. For detailed billing rules and unit prices, see [Script reconstruction pricing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-pricing#6d2a19db).

## Related APIs

* [Create a script reconstruction task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-script-reconstruction-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
