---
title: "Generate videos with ModelArk via AI MediaKit"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/generate-videos-with-modelark-via-ai-mediakit"
---

To generate videos from text prompts using [ModelArk](https://www.byteplus.com/en/product/modelark) models without directly integrating the ModelArk API, you can use AI MediaKit's proxy API. This guide provides step\-by\-step instructions and code examples for calling the video generation API, helping you quickly implement text\-to\-video capabilities.

<span id="quick-start"></span>
## Quick start

This section uses the example of generating a 5\-second video from a single text prompt to demonstrate the complete process of calling a video generation model through AI MediaKit.

<span id="prerequisites"></span>
### Prerequisites


* **Enable the model**: Enable the required video generation model in the [ModelArk](https://www.byteplus.com/en/product/modelark) console, and record the available model ID or endpoint ID.

* **Complete cross\-service authorization**: Go to the [Basic configuration > Authorization management](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=authorization) page in the AI MediaKit console and grant AI MediaKit permission to access your ModelArk resources.

* **Obtain access credentials**: Go to the [API key](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=apiKey) page in the AI MediaKit console and create a MediaKit API Key.


<span id="process"></span>
### Process

Calling a video generation model through AI MediaKit is an asynchronous task. The standard process is as follows:


1. Call `POST /api/v1/tools/call-maas-proxy` to submit a task, with `api` set to `ark.video_generation`, to obtain a task ID.

2. Poll the `GET /api/v1/tasks/{task_id}` interface until the task's status changes to `completed`, or use [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification) to receive task status changes automatically.

3. After the task is completed, read the original result returned by the ModelArk video generation interface (such as the generated video URL) from the `result.maas_result` field in the response.


<span id="step-1-submit-a-video-generation-task"></span>
#### Step 1: Submit a video generation task

Call the [MaaS model proxy API](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy). You can copy the following cURL command directly to submit a video generation task with a single prompt.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/call-maas-proxy' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
  "api": "ark.video_generation",
  "maas_params": {
    "model": "dreamina-seedance-2-5-260628",
    "content": [
      { "type": "text", "text": "An orange tabby cat running across a sunlit grass field, cinematic look, shallow depth of field" }
    ],
    "resolution": "720p",
    "ratio": "16:9",
    "duration": 5
  }
}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default">Replace <code>{Your_API_Key}</code> with your valid MediaKit API Key.</div>


* <div data-tips="true" data-tips-type="default">The content inside <code>maas_params</code> consists of the parameters required by the ModelArk video generation interface; for details, see <a href="https://docs.byteplus.com/docs/ModelArk/1520757">ModelArk \- Video generation API</a>. Replace <code>model</code> with the model ID or inference endpoint you have enabled. For image\-to\-video generation, add an element of the <code>image_url</code> type to <code>content</code>.</div>



After the request succeeds, you receive the following response containing a `task_id`. Save this ID for later queries.

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
    "request_id": "20240523100000ABCDEFG12345"
}
```


<span id="step-2-obtain-the-generated-result"></span>
#### Step 2: Obtain the generated result

Video generation requires some processing time. You need to poll the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) API until the task's status changes to `completed`.

```Bash
curl -X GET 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tasks/{task_id}' \
-H 'Authorization: Bearer {Your_API_Key}'
```


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Replace <code>{task_id}</code> at the end of the URL with the task ID returned in Step 1.</div>


After the task is completed successfully, you receive the following response. `result.maas_result` is the original task result returned by ModelArk. For its structure, see [ModelArk - Retrieve a video generation task](https://docs.byteplus.com/en/docs/modelark/get-video-generation-task-api).

```JSON
{
    "success": true,
    "task_id": "amk-tool-call-maas-proxy-123456789",
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
            "usage": {
                "completion_tokens": 108900,
                "total_tokens": 108900
            }
        }
    }
}
```


<span id="reference"></span>
## Reference

<span id="billing"></span>
### Billing

The usage of the video generation model is billed by **ModelArk** according to its pricing. View usage and bills in ModelArk; AI MediaKit does not charge an additional fee for this call. For specific prices, see [ModelArk Pricing](https://docs.byteplus.com/en/docs/modelark/model-pricing).

<span id="related-api-documents"></span>
## Related APIs


* [MaaS model proxy API](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-call-maas-proxy)

* [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details)

* [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification)
