---
title: "MaaS model proxy API"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-call-maas-proxy"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/call-maas-proxy`

To access a wide range of generative AI capabilities—such as video generation, image generation, and audio generation—through a single, unified interface, you can use the MaaS model proxy API. It allows you to call different model services like ModelArk and Seed Speech with one method, while AI MediaKit automatically handles the complexities of asynchronous execution, result callbacks, idempotency, and task queuing for you.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">This API provides access to capabilities from model services such as ModelArk and Seed Speech; it does not run AI MediaKit's own algorithms. Before using it, you must enable the required capability in the corresponding model service and complete cross\-service authorization for that model service in the AI MediaKit console. For the complete feature descriptions and usage examples of each capability, see the corresponding guides:</div>



* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/docs/byteplus-vod/generate-images-with-modelark-via-ai-mediakit">Generate images with ModelArk via AI MediaKit</a></div>


* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/docs/byteplus-vod/generate-videos-with-modelark-via-ai-mediakit">Generate videos with ModelArk via AI MediaKit</a></div>


* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/docs/byteplus-vod/generate-audio-with-seed-speech-via-ai-mediakit">Generate audio with Seed Speech via AI MediaKit</a></div>


* <div data-tips="true" data-tips-type="default"><a href="https://docs.byteplus.com/docs/byteplus-vod/transcribe-audio-with-seed-speech-via-ai-mediakit">Transcribe audio with Seed Speech via AI MediaKit</a></div>



<span id="request-parameters"></span>
## Request parameters

<span id="header-parameters"></span>
### Header parameters


|Parameter |Type |Required |Example value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body-parameters"></span>
### Body parameters


|**Parameter** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|`api` |String |Yes |`ark.video_generation` |The identifier of the target model interface. Supported values:<br><br><br>* `ark.image_generation`: Image generation<br><br>* `ark.video_generation`: Video generation<br><br>* `doubao.audio_generation`: Audio generation<br><br>* `doubao.asr`: ASR for audio files in standard mode |
|`maas_params` |Object |Yes |`{...}` |The parameters required by the target model interface (such as the model and prompt). Provide these parameters exactly as required by the corresponding model service; AI MediaKit passes them to the target model unchanged. Asynchronous execution, result callbacks, and idempotency control are handled by AI MediaKit, so you do not need to configure them here. For the fields, refer to the official documentation of the model service corresponding to the `api` parameter:<br><br><br>* `ark.image_generation`: See [ModelArk - Image generation API](https://docs.byteplus.com/docs/ModelArk/1541523).<br><br>* `ark.video_generation`: See [ModelArk - Video generation API](https://docs.byteplus.com/docs/ModelArk/1520757).<br><br>* `doubao.audio_generation`: See [Seed Speech - Audio generation](https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01).<br><br>* `doubao.asr`: See [Seed Speech - ASR - Audio File (Standard Mode)](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilesubmittask).<br><br><br>Note: For image\-to\-image generation through this API, AI MediaKit supports reference images provided only by URL (`image_url`). Base64\-encoded reference images (`image_base64`) are not supported. |
|`client_token` |String |No |`your_unique_request_id_185` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_unique_callback_args` |Custom callback arguments. The content you provide will be returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |
|`queue_id` |String |No |`q00a9731598092652e4a95292434198` |The ID of the queue to which the task will be submitted. Using different queues is the primary way to allocate costs to specific projects. If this parameter is omitted, the task is sent to the `default` queue within the project associated with your API key. You can create and manage queues on the **Queues** page in the AI MediaKit console. For a detailed guide, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues). |


<span id="request-examples"></span>
## Request examples

This section provides request examples by model service.

<span id="image-generation-ark-image-generation"></span>
### Image generation

Set `api` to `ark.image_generation`, and provide the parameters in `maas_params` according to the [ModelArk - Image generation API](https://docs.byteplus.com/docs/ModelArk/1541523).

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/call-maas-proxy' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "api": "ark.image_generation",
  "maas_params": {
    "model": "dola-seedream-5-0-pro-260628",
    "prompt": "A cyberpunk-style city night scene poster, neon lights, cinematic look",
    "size": "1024x1024"
  }
}'
```


<span id="video-generation-ark-video-generation"></span>
### Video generation

Set `api` to `ark.video_generation`, and provide the parameters in `maas_params` according to the [ModelArk - Video generation API](https://docs.byteplus.com/docs/ModelArk/1520757). The following is an image\-to\-video example, where `content` includes both a text prompt and a reference image.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/call-maas-proxy' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "api": "ark.video_generation",
  "maas_params": {
    "model": "dreamina-seedance-2-5-260628",
    "content": [
      {
        "type": "text",
        "text": "A girl holding a fox; the girl opens her eyes and looks gently at the camera; the camera slowly pulls back; the girl's hair is blown by the wind"
      },
      {
        "type": "image_url",
        "image_url": {
          "url": "https://example.com/your-reference-image.png"
        }
      }
    ],
    "generate_audio": true,
    "ratio": "adaptive",
    "duration": 5,
    "watermark": false
  }
}'
```


<span id="speech-synthesis-doubao-audio-generation"></span>
### Audio generation

Set `api` to `doubao.audio_generation`, and provide the parameters in `maas_params` according to [Seed Speech - Audio generation](https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01).

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


<span id="speech-recognition-doubao-asr"></span>
### Speech recognition

Set `api` to `doubao.asr`, and provide the parameters in `maas_params` according to [Seed Speech - ASR - Audio File (Standard Mode)](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilesubmittask).

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


<span id="response"></span>
## Response

After you call the API to submit a task, the interface immediately returns a synchronous response indicating whether the task successfully entered the background processing queue.

<span id="response-parameters"></span>
### Response parameters


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`success` |Boolean |Indicates whether the task was successfully submitted.<br><br><br>* `true`: The task was successfully submitted to the background processing queue.<br><br>* `false`: The request contains an error and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier of the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and result. |
|`request_id` |String |The unique identifier of this API request, which can be used for troubleshooting. |
|`error` |Object |The error details object, returned only when `success` is `false`. For details, see [The error object](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy#error-object) below. |


<span id="error-object"></span>
#### The error object


|**Parameter** |**Type** |**Description** |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error. For example, `BadRequest`. |
|`message` |String |A detailed description of the error, useful for development and debugging. |
|`param` |String |(Optional) The specific parameter that caused the error. |


<span id="response-example"></span>
### Response example

<span id="success-response"></span>
#### Success

```JSON
{
  "success": true,
  "task_id": "amk-tool-call-maas-proxy-123456789",
  "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="failure-response"></span>
#### Failure

```JSON
{
  "success": false,
  "task_id": "",
  "request_id": "20240523101000WXYZ54321",
  "error": {
    "code": "InvalidParameter",
    "message": "The 'api' parameter is required",
    "param": "api",
    "type": "BadRequest"
  }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

<span id="how-to-obtain-the-result"></span>
### How to obtain the result

A call to a model capability is an asynchronous task, so the execution status and final result are not returned synchronously upon submission. You can obtain the task result in either of the following ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


After the task is completed successfully, the `result` field in the task information you obtain contains the following.


|Parameter |Type |Description |
|---|---|---|
|`api` |String |The identifier of the model interface actually called, consistent with the `api` in the request. |
|`duration` |Number |The total audio or video duration, in seconds. For image scenarios, the value is `0`. Some tasks (e.g., speech recognition) may not return this field. |
|`maas_result` |Object |This is the original result from the target model interface, which AI MediaKit returns unchanged. Its structure may include token usage, generated asset URLs, and other fields. For the specific structure, refer to the official documentation of the model service corresponding to `api`: <br><br><br>* `ark.image_generation`: [ModelArk - Image generation API](https://docs.byteplus.com/docs/ModelArk/1541523). <br><br>* `ark.video_generation`: [ModelArk - Video generation API](https://docs.byteplus.com/en/docs/modelark/get-video-generation-task-api). <br><br>* `doubao.audio_generation`: [Seed Speech - Audio generation](https://docs.byteplus.com/en/docs/byteplusvoice/seedaudio-01). <br><br>* `doubao.asr`: [Seed Speech - ASR - Audio File (Standard Mode)](https://docs.byteplus.com/en/docs/byteplusvoice/asraudiofilequeryresult). |


<span id="result-examples"></span>
### Result examples

The following provides complete task information examples after task completion, by model service. `maas_result` is the original result from the target model interface, and its fields are defined in the corresponding model service's official documentation. The `task_id`, `request_id`, and resource addresses in the examples are desensitized placeholders; the actual values are provided in the interface response.

<span id="image-generation-ark-image-generation"></span>
#### Image generation

`maas_result` includes fields such as the generated image URL, and `result.duration` is `0`.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "api": "ark.image_generation",
        "duration": 0,
        "maas_result": {
            "created": 1777358420,
            "model": "dola-seedream-5-0-pro-260628",
            "data": [
                {
                    "url": "https://example.com/generated-image.jpeg?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Expires=86400&X-Tos-Signature=***",
                    "size": "1024x1024",
                    "output_format": "jpeg"
                }
            ],
            "usage": {
                "generated_images": 1,
                "input_images": 0,
                "output_tokens": 4096,
                "total_tokens": 4096
            }
        }
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777358420
}
```


<span id="video-generation-ark-video-generation"></span>
#### Video generation

`maas_result.content.video_url` is the generated video URL, and `result.duration` is the total video duration in seconds.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "api": "ark.video_generation",
        "duration": 5.0,
        "maas_result": {
            "id": "cgt-20240523100000-abcde",
            "model": "dreamina-seedance-2-5-260628",
            "status": "succeeded",
            "content": {
                "video_url": "https://example.com/generated-video.mp4?X-Tos-Algorithm=TOS4-HMAC-SHA256&X-Tos-Expires=86400&X-Tos-Signature=***"
            },
            "resolution": "720p",
            "ratio": "16:9",
            "framespersecond": 24,
            "duration": 5,
            "created_at": 1777358413,
            "updated_at": 1777358420,
            "usage": {
                "completion_tokens": 108900,
                "total_tokens": 108900
            }
        }
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777358420
}
```


<span id="speech-synthesis-doubao-audio-generation"></span>
#### Audio generation

`maas_result.audio` is the Base64\-encoded audio data.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345",
    "status": "completed",
    "result": {
        "api": "doubao.audio_generation",
        "maas_result": {
            "audio": "SUQzBAAAAAAAA... (Base64-encoded audio data, truncated here)"
        }
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777358420
}
```


<span id="speech-recognition-doubao-asr"></span>
#### ASR for audio files in standard mode `doubao.asr`

`maas_result.result.text` is the recognized text, and `result.duration` is the total recognized audio duration in seconds.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345",
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
    },
    "expires_at": 1777531298,
    "created_at": 1777358413,
    "finished_at": 1777358420,
    "queue_id": "q00a9731598092652e4a95292434198"
}
```
