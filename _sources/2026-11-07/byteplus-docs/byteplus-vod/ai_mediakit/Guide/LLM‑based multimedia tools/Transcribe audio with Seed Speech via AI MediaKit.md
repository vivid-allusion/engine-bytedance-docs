---
title: "Transcribe audio with Seed Speech via AI MediaKit"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/transcribe-audio-with-seed-speech-via-ai-mediakit"
---

To transcribe audio recordings into text without directly integrating the Seed Speech API, you can use AI MediaKit to call the Seed Speech ASR service. For the supported models and parameters, see [Seed Speech - ASR - Audio File (Standard Mode)](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilesubmittask). This guide walks you through transcribing an audio recording with Seed Speech ASR via AI MediaKit.

<span id="quick-start"></span>
## Quick start

This section uses transcribing an MP3 audio recording into text as an example to demonstrate the complete process of calling a speech recognition model through AI MediaKit.

<span id="prerequisites"></span>
### Prerequisites


* **Enable the model**: Enable Seed Speech ASR for audio files in standard mode, and record the available model identifier. For the supported models and parameters, see [Seed Speech - ASR - Audio File (Standard Mode)](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilesubmittask).

* **Complete cross\-service authorization**: Go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console and grant AI MediaKit permission to access your Seed Speech resources.

* **Obtain access credentials**: Go to the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console and create a MediaKit API Key.

* **Prepare the audio file**: Prepare the audio recording to be recognized and upload it to a publicly accessible address to obtain its URL.


<span id="process"></span>
### Process

Calling a speech recognition model through AI MediaKit runs as an asynchronous task. The standard process is as follows:


1. Call `POST /api/v1/tools/call-maas-proxy` to submit a task, with `api` set to `doubao.asr`, to obtain a task ID.

2. Poll the `GET /api/v1/tasks/{task_id}` interface until the task status `status` changes to `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to receive task status changes automatically.

3. After the task is completed, read the original result of the speech recognition interface (such as the recognized text) from the response `result.maas_result`, and obtain the total duration of the recognized audio in seconds from `result.duration`.


<span id="step-1-submit-a-speech-recognition-task"></span>
#### Step 1: Submit a speech recognition task

Call the [MaaS model proxy API](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy). You can copy the following cURL command directly to submit a speech recognition task for an audio recording.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/call-maas-proxy' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "api": "doubao.asr",
  "maas_params": {
    "audio": {
      "url": "https://example.com/your-audio.mp3",
      "format": "mp3"
    },
    "request": {
      "model_name": "bigmodel",
      "enable_itn": true,
      "enable_punc": true,
      "enable_ddc": false,
      "enable_speaker_info": false,
      "enable_channel_split": false,
      "show_utterances": false
    }
  }
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid MediaKit API Key.</div>


* <div data-tips="true" data-tips-type="default">The content inside <code>maas_params</code> consists of the request parameters for the ASR interface; for details, see <a href="https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilesubmittask">Seed Speech \- ASR \- Audio File (Standard Mode)</a>. Replace <code>audio.url</code> with the address of your own audio recording, and keep <code>request.model_name</code> set to the fixed value <code>bigmodel</code>.</div>



After the request succeeds, you receive the following response containing a `task_id`. Save this ID for later queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="step-2-obtain-the-recognition-result"></span>
#### Step 2: Obtain the recognition result

You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task status `status` changes to `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


After the task is completed successfully, you receive the following response. `result.maas_result` is the original result returned by the ASR interface, containing the recognized text. For its structure, see [Seed Speech - Query Result - HTTP](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilequeryresult).

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "status": "completed",
    "result": {
        "api": "doubao.asr",
        "duration": 34.167,
        "maas_result": {
            "audio_info": {
                "duration": 34167
            },
            "result": {
                "text": "Dusk falls over the world, yet the mountains and rivers remain the same. With one turn, autumn becomes a landscape and winter becomes a promise. Live well, and we will meet again in time.",
                "additions": {
                    "duration": "34167"
                }
            }
        }
    }
}
```


<span id="reference"></span>
## Reference

<span id="billing"></span>
### Billing

The usage of ASR is billed by **Seed Speech** according to its pricing. View usage and bills in Seed Speech; AI MediaKit does not charge an additional fee for this call. For specific prices, see [Seed Speech - Speech-to-Text Pricing](https://docs.byteplus.com/en/docs/byteplusvoice/asrbilling).

<span id="related-api-documents"></span>
## Related APIs


* [MaaS model proxy API](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
