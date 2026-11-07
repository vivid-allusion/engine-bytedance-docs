---
title: "Generate audio with Seed Speech via AI MediaKit"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/generate-audio-with-seed-speech-via-ai-mediakit"
---

You can use AI MediaKit to call an audio generation model that you have already enabled in [Seed Speech](https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01). This lets you generate audio from a text prompt without separately integrating the Seed Speech API.

This guide walks you through generating audio from a text prompt with a Seed Speech audio generation model via AI MediaKit.

<span id="quick-start-generate-audio"></span>
## Quick start: Generate audio

This section uses an example of generating an MP3 audio file from a text prompt to demonstrate the complete process of calling an audio generation model through AI MediaKit.

<span id="prerequisites"></span>
### Prerequisites


* **Enable the model**: Enable the required audio generation model in Seed Speech, and record the available model identifier. For the supported models and parameters, see [Seed Speech - Audio generation](https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01).

* **Complete cross\-service authorization**: Go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console and grant AI MediaKit permission to access your Seed Speech resources.

* **Obtain access credentials**: Go to the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console and create a MediaKit API Key.


<span id="process"></span>
### Process

Calling an audio generation model through AI MediaKit runs as an asynchronous task. The standard process is as follows:


1. Call `POST /api/v1/tools/call-maas-proxy` to submit a task, with `api` set to `doubao.audio_generation`, to obtain a task ID.

2. Poll the `GET /api/v1/tasks/{task_id}` interface until the task status `status` changes to `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to receive task status changes automatically.

3. After the task is completed, read the original result returned by the audio generation interface (such as the audio data) from the response `result.maas_result`.


<span id="step-1-submit-an-audio-generation-task"></span>
#### Step 1: Submit an audio generation task

Call the [MaaS model proxy API](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy). You can copy the following cURL command directly to submit a piece of text for an audio generation task.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/call-maas-proxy' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "api": "doubao.audio_generation",
  "maas_params": {
    "model": "seed-audio-1.0",
    "text_prompt": "Welcome to AI MediaKit. This is an audio generation example.",
    "audio_config": {
      "format": "mp3",
      "sample_rate": 48000,
      "pitch_rate": 0,
      "speech_rate": 0,
      "loudness_rate": 0
    }
  }
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid MediaKit API Key.</div>


* <div data-tips="true" data-tips-type="default">The content inside <code>maas_params</code> consists of the parameters required by the audio generation interface; for details, see <a href="https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01">Seed Speech \- Audio generation</a>. Configure the model, reference resources, and output audio settings as needed.</div>



After the request succeeds, you receive the following response containing a `task_id`. Save this ID for later queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="step-2-obtain-the-generated-audio"></span>
#### Step 2: Obtain the generated audio

You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task status `status` changes to `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


After the task is completed successfully, you receive the following response. `result.maas_result` is the original result returned by the audio generation interface. For its structure, see [Seed Speech - Audio generation](https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01).

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "status": "completed",
    "result": {
        "api": "doubao.audio_generation",
        "maas_result": {
            "audio": "SUQzBAAAAAAAA... (Base64-encoded audio data, truncated here)",
            "duration": 4.72,
            "original_duration": 4.72,
            "url": "https://example.com/generated-audio.mp3"
        }
    }
}
```


<span id="reference"></span>
## Reference

<span id="billing"></span>
### Billing

The usage of the audio generation model is billed by **Seed Speech** according to its pricing. View usage and bills in Seed Speech; AI MediaKit does not charge an additional fee for this call. For specific prices, see [Seed Speech - Text-to-Speech Pricing](https://docs.byteplus.com/en/docs/byteplusvoice/TTS_Billing).

<span id="related-api-documents"></span>
## Related APIs


* [MaaS model proxy API](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
