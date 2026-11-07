---
title: "Basic concepts and prerequisites"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites"
---

This document introduces the common concepts of the AI MediaKit API and the prerequisites you must complete before making API calls. Understanding these basics will help you integrate AI MediaKit capabilities more efficiently.

<span id="17a4192d"></span>
## Prerequisites: obtain and configure your API key

An API Key is the credential used to authenticate requests to AI MediaKit. API Keys are highly sensitive. If an API Key is exposed, others may use your service quota and incur unexpected charges. We recommend storing API Keys in environment variables instead of hardcoding them in your code.

AI MediaKit supports the following types of API Keys:


* **General\-purpose API Key**: An API Key created in the [Identity and Access Management (IAM) console](https://console.byteplus.com/iam/keymanage). You can use it across BytePlus services that support API Key authentication. This type of API Key provides more flexible permission management and supports viewing AI MediaKit usage and costs by API Key in the BytePlus Billing Center. For creation and permission management instructions, see [Access Key & API Key](https://docs.byteplus.com/en/docs/IAM/about-access-keys). For cost allocation instructions, see [Allocating costs by project or API Key](https://docs.byteplus.com/docs/byteplus-vod/projects-and-queues).

* **Service\-specific API Key**: An API Key created in the AI MediaKit console. It can be used only with AI MediaKit.


<span id="d720e1ac"></span>
### Obtain an API Key from the AI MediaKit console


1. Go to the [Settings](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings) page in the AI MediaKit console.

2. Click **Create API key**.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/f9378c585448400d915ea3c8361c38d5) </span>

3. In the **Name** text box in the pop\-up window, confirm or change the API Key name, and then click **Create**.

4. After successful creation, you can view and copy the newly created key from the API Key list.


<span id="65288b08"></span>
### Security recommendations

We strongly recommend storing your API Key in an environment variable instead of hardcoding it in your code. This security practice helps prevent credential exposure caused by improperly configured repository permissions or accidental code sharing.

<span id="6d193e26"></span>
## Core concepts

<span id="0d681e9c"></span>
### Synchronous and asynchronous tasks

AI MediaKit uses synchronous or asynchronous task processing depending on the complexity and expected processing time of each tool.

<span id="8417b62d"></span>
#### Synchronous tasks

Synchronous tasks are suitable for operations that can return results quickly. AI MediaKit image tools currently use synchronous processing.

The standard workflow is as follows:


1. Submit a task and wait: Call the `POST` endpoint of the tool.

2. Get the result directly: After processing is complete, the HTTP response body includes the result, such as the processed image URL or recognized text. You do not need to send another request to query the result.


<span id="3f32aefe"></span>
### Asynchronous tasks

Most audio and video tools, such as video concatenation and video trimming, require more processing time and therefore use asynchronous tasks. Task submission and result retrieval are separate operations, so processing does not block your application in real time.

The standard workflow is as follows:


1. **Submit a task**: Call the `POST` endpoint of the tool to create a processing task, such as `POST /api/v1/tools/concat-video`. If the request parameters pass validation, the API immediately returns a globally unique `task_id`.

2. **Query the task status**: Use the `task_id` to poll the generic `GET /api/v1/tasks/{task_id}` endpoint. The task status can be `processing`, `completed`, or `failed`.

3. **Get the result**: When the task status changes to `completed`, the task details response contains a `result` object with the processing result, such as the generated file URL in `video_url`.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">Instead of polling, you can configure <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification">Event notification</a>. AI MediaKit then sends a notification to your callback URL when a task is completed or fails.</div>


<span id="0e2ee2f8"></span>
### Idempotency control

All asynchronous task submission APIs use idempotency control to prevent the same processing request from being executed repeatedly because of network instability or client retries. Synchronous tasks do not currently support idempotency checks.


* **Why idempotency is needed**: It prevents repeated task execution caused by client retries or network instability, avoiding unnecessary resource consumption and duplicate charges.

* **Default idempotent behavior**: When you call a task submission API, AI MediaKit generates a unique identifier from your account information and the core request parameters. For example, the core parameters of a video trimming task include `video_url`, `start_time`, and `end_time`. If AI MediaKit receives another request with the same identifier within 24 hours after the task was successfully submitted, it does not create a new task and instead returns the same result as the first request, such as the same `task_id`.

* **Use ** **`client_token`** ** to control idempotency**: You can provide the optional `client_token` parameter for more precise idempotency control. `client_token` is a client\-generated unique string of up to 64 characters.

   * **Scenario 1: Prevent duplicate execution**

      * **Purpose**: Ensure that retrying a request after a network timeout or unresponsive client does not create a duplicate task.

      * **Action**: Use the same `client_token` in the retry request as in the original request.

      * **Example**: You submit a video enhancement task with `client_token` set to `"task-enhance-user123-20251125"`. If the request times out, retry the request with the same `client_token`. AI MediaKit recognizes the retry and returns the original task information without creating a new task.

   * **Scenario 2: Force the task to run again**

      * **Purpose**: Create a new task with the same media source and processing parameters.

      * **Action**: Provide a new, unique `client_token`.

      * **Example**: You have successfully processed a video and need to run the same operation on it again. Provide a new `client_token` in the second request. Otherwise, idempotency control is triggered and a new task is not created.


<span id="1173f727"></span>
## API QPS limits

To ensure service stability and fair usage, AI MediaKit limits API call frequency in queries per second (QPS). QPS limits apply to your entire BytePlus account. Calls from the main account and all its IAM users are counted together and cannot exceed the account limit.

AI MediaKit applies different rate\-limiting strategies for asynchronous and synchronous tasks.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>



* <div data-tips="true" data-tips-type="default"><strong>Exceeding the limit</strong>: If your call frequency exceeds a QPS limit, the API returns a rate\-limiting error. Reduce the call frequency or retry later.</div>


* <div data-tips="true" data-tips-type="default"><strong>Requesting a quota increase</strong>: The values below are default limits. If they do not meet your business requirements, contact your account manager or submit a <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112&_vtm_=a78999.b69280.0_0.0_0.0.295_7657844606814127669">support ticket</a> to request an increase.</div>


* <div data-tips="true" data-tips-type="default"><strong>Asynchronous task concurrency limit</strong>: AI MediaKit limits the number of asynchronous tasks that can be processed simultaneously under one account. This is an account\-level limit shared by all projects and queues. The default limit is 20. Creating additional projects or queues does not increase the account concurrency limit. To request a higher limit, submit a <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112&_vtm_=a78999.b69280.0_0.0_0.0.295_7657844606814127669">support ticket</a>. Synchronous tasks, such as image tool tasks, are not subject to this concurrency limit.</div>



<span id="d5c61014"></span>
### QPS limits for asynchronous tasks

All asynchronous tasks share a single, account\-level rate limit.


* **Limit rule**: Global rate limit at the account level.

* **Default limit**: The total QPS limit for all asynchronous APIs is **10** for each main account (including all its sub\-accounts).


<span id="eb7c5e40"></span>
### QPS limits for synchronous tasks

Each synchronous tool has an independent limit. Each synchronous tool API has its own QPS quota, and calls to different tools do not affect each other. The default QPS limits for each synchronous tool are as follows:


|**Tool API** |**Default QPS limit (queries/second)**  |
|---|---|
|[Create an image quality enhancement task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-quality-enhancement-task) |1 |
|[Create an image metadata acquisition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task) |10 |
|[Create a rounded corner task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-rounded-corner-task) |10 |
|[Create an image rotation task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-rotation-task) |10 |
|[Create an image flip task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-flip-task) |10 |
|[Create an image sharpening task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-sharpening-task) |10 |
|[Create an image gaussian blur task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-gaussian-blur-task) |1 |
|[Create an image color adjustment task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-color-adjustment-task) |10 |
|[Create an image resize task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-resize-task) |10 |
|[Create an image negative task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-negative-task) |10 |
