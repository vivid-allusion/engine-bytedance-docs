---
title: "Voice and background audio separation"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-voice-and-background-audio-separation"
---

The AI MediaKit Voice and Background Audio Separation tool accurately processes an audio or video file you provide. For general and music scenes, it separates the file into a vocal track and a background track. For short drama, voice\-over, and game scenes, it can further separate the file into vocal, music, and sound\-effects tracks. This guide walks you through:

* Understanding the core capability and application scenarios of voice separation.

* Quickly separating a vocal track and a background track from a media file.

## Demo

With the separation tool, you can achieve the following:

|Input audio |Output audio |
|---|---|
|[audio](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/935a00224eba4b94bd6e47d2cc3a1046~tplv-goo7wpa0wc-image.image)<br> |Separated vocals<br><br>[audio](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/90fc6ffdfd1f42e5ab8d1fdba941887f~tplv-goo7wpa0wc-image.image)<br> |
||Separated background music<br><br>[audio](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8d6fd98373ec4f189eecffbce8800c48~tplv-goo7wpa0wc-image.image)<br> |

## Quickstart: Separate vocals and background from a video

This section demonstrates how to extract two independent audio tracks from a video that contains both vocals and background music.

### Prerequisites

1. **Obtain an API key**: Before you begin, visit the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console to create and obtain your **AI MediaKit API Key**.

2. **Prepare a media file**: Have a video or audio file ready for processing. Make it accessible via a public HTTP/HTTPS URL. You can obtain this URL by uploading the file to your own publicly accessible server or to the [BytePlus VOD service](https://docs.byteplus.com/en/docs/byteplus-vod/docs-media-upload).

### Procedure

Voice separation is an asynchronous task. The standard workflow is as follows:

1. Call `POST /api/v1/tools/separate-voice` and get a `task_id` for querying.

2. Either poll `GET /api/v1/tasks/{task_id}` until the task `status` becomes `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to automatically receive task status updates. Once the task is complete, parse the `result` field to get the download URLs of the output audio files from the `voice_audio_url` and `background_audio_url` fields.

#### Step 1: Submit the task

You need to call the [Create a voice and background audio separation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-voice-separation-task) API. You can copy the following cURL command to submit a task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/separate-voice' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "audio_url": "https://your-public-domain.com/path/to/audio.mp3"
}'
```

> **说明**

* > Replace `{Your_API_Key}` with your valid API Key.

* > Replace `audio_url` with your own audio URL. To process a video file, use the `video_url` parameter instead.

* > This example uses the default `Audio` scene for separation. For more fine\-grained separation (for example, splitting the vocals, music, and sound effects of a short drama into three tracks), see [Advanced usage: Selecting a separation scene](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-voice-and-background-audio-separation#b1789509) below.

Upon successful submission, you will receive a response containing a `task_id`. Please save this ID for future queries.

```JSON
{
  "success": true,
  "task_id": "amk-tool-separate-voice-12345678",
  "request_id": "20260417110000A1B2C3D4E5F6G7H8"
}
```

#### Step 2: Get the result

You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task `status` becomes `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
--header 'Authorization: Bearer {Your_API_Key}'
```

> **说明**

> Replace `{task_id}` at the end of the URL with the task ID returned in Step 1.

When the task is successfully completed, you will receive the following response. The `result` field contains the download URLs of the separated vocal track (`voice_audio_url`) and background track (`background_audio_url`), both in **AAC** format and valid for **24 hours**.

```JSON
{
    "success": true,
    "task_id": "amk-tool-separate-voice-12345678",
    "task_type": "separate-voice",
    "status": "completed",
    "result": {
        "voice_audio_url": "https://example.com/voice.aac?sign=...",
        "background_audio_url": "https://example.com/background.aac?sign=...",
        "duration": 120.5
    },
    "expires_at": 1777464650,
    "created_at": 1777291767,
    "finished_at": 1777291851,
    "request_id": "20260417110100F8G7H6E5D4C3B2A1"
}
```

## Advanced usage: Selecting a separation scene

For audio of different content types, the composition of vocals, background audio, and music varies significantly. You can use the scene parameter to select a separation scene that better matches your content type to achieve better separation results:

* Two\-way split: Applies to general and music scenes. It divides the audio into two tracks—"vocals" and "background".

* Three\-way split: Applies to short drama, voice\-over, and game scenes. It splits the audio more granularly into three tracks—"vocals", "music", and "sound effects"—making complex post\-production easier.

|`scene` value |Output tracks |
|---|---|
|`Audio` (default) |2\-track output, which includes a vocal track (`voice_audio_url`) and a background track (`background_audio_url`) |
|`Music` |2\-track output, which includes a vocal track (`voice_audio_url`) and a background track (`background_audio_url`) |
|`Drama` |3\-track output, which includes a vocal track (`voice_audio_url`), a music track (`music_audio_url`), and a sound\-effects track (`sfx_audio_url`) |
|`Narrate` |3\-track output, which includes a vocal track (`voice_audio_url`), a music track (`music_audio_url`), and a sound\-effects track (`sfx_audio_url`) |
|`Game` |3\-track output for game content, which includes a vocal track (`voice_audio_url`), a music track (`music_audio_url`), and a sound\-effects track (`sfx_audio_url`) |

Taking the short drama scene as an example, specify `scene` as `Drama` when submitting the task:

```Plain
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/separate-voice' \
--header 'Content-Type: application/json' \
--header 'Authorization: Bearer {Your_API_Key}' \
--data '{
  "video_url": "https://example.com/your_video.mp4",
  "scene": "Drama"
}'
```

After the task is complete, the `result` field contains three track URLs: `voice_audio_url`, `music_audio_url`, and `sfx_audio_url` (sound effects).

## References

### Application scenarios

* **Video editing and repurposing**: In video editing and when creating derivative content, the separated vocals and background audio can be processed independently—for example, by adjusting the volume of a specific dialogue segment or replacing the background music—making this process more flexible and efficient.

* **Vocal enhancement**: For videos from complex sources, such as mobile\-recorded daily footage, live\-recorded lectures, or non\-professional podcast recordings, separating the vocals allows you to process the vocal part in a targeted way—for example, increasing the volume, improving audio quality, or reducing noise—significantly improving the clarity of the vocals.

* **Video translation and voice cloning**: In video translation scenarios, the vocals in a video can be extracted separately for subsequent voice cloning, keeping the timbre and intonation highly consistent with the original voice, and then combined with TTS to convert the translated text into speech in the target language.

* **ASR optimization**: After extracting the vocals from audio, using the clean vocal part for automatic speech recognition effectively reduces interference from background noise, thereby significantly improving the overall accuracy of ASR.

### Limits

|Limit |Description |
|---|---|
|Input file |* File source: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* Supported formats:<br><br>   * Common video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`.<br><br>   * Common audio formats such as `mp3`, `m4a`, `wav`. |
|Output file |Use the `output_format` parameter to specify the output audio format. Available values are `aac`, `mp3`, `wav`, `m4a`, and `flac`. The default is `aac`. |

## Related APIs

* [Create a voice and background audio separation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-voice-separation-task)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
