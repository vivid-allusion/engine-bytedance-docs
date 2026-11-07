---
title: "Event notification"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-event-notification"
---

To receive results for asynchronous tasks like video enhancement without constant polling, you can configure event callbacks in AI MediaKit. This guide explains the callback mechanism, shows you how to set up a receiving address in the console, and details the data structure of the "Single task completed event" notification.

<span id="097bb654"></span>
## Callback mechanism

You need to deploy an HTTP/HTTPS service to receive callback messages and configure the callback address in the AI MediaKit console. The callback mechanism works as follows:


* **Request method**: When an event occurs, AI MediaKit will send a `POST` request to your configured callback address.

* **Response requirement**: Your HTTP/HTTPS service must return a `200` status code to acknowledge successful receipt. Any other status code will be considered a failure.

* **Retry mechanism**: If a callback fails (due to a non\-200 response or connection timeout), AI MediaKit will retry up to **3 times** at intervals of 5 seconds, 10 seconds, and 30 seconds, respectively. If all retries fail, the notification will be discarded.

* **Security note**: The current version does not support callback signature authentication. Please ensure your receiving address can handle POST requests from the public internet and consider implementing idempotency checks on your business layer based on the `task_id`.


<span id="c154f28e"></span>
## Configure callback settings

<span id="9ebf2a67"></span>
### Step 1: Subscribe to an event


1. Visit the [Settings](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/ai-mediakit/settings?tab=callback) page in the AI MediaKit console.

2. Under the **Callbacks** tab, click **Edit** and select the event you want to receive. Currently, only the [Single task completed event](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification#d70b78f0) is supported.

   <span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/b04f6f2380574e69a1033b66b760bbb9) </span>

3. Click **Save**.


<span id="71e3b1d0"></span>
### Step 2: Configure receiving address

In the **Callback subscription** area, create a new subscription to specify the address and method for receiving callback notifications.

<span>![图片](https://p9-arcosite.byteimg.com/obj/tos-cn-i-goo7wpa0wc/7ce3dd36f84d40bbbc480722e60a5502) </span>


1. Click **Add subscription**.

2. Configure the following information:

   * **Callback method**: This value is fixed to `http(s)`.

   * **Request Content\-Type**: Select the Content\-Type for the callback request. This affects the data format of the request body sent by the AI MediaKit service. The following types are supported:

      * `application/json`

      * `application/octet-stream`

   * **Receiving address**: Enter the URL for receiving callback notifications. It must start with `http://` or `https://`.

3. Click **OK**. The changes may take a few minutes to take effect.


<span id="00459ff9"></span>
### Step 3: Test connectivity


1. In the **Callback subscription** list, click **Test** in the operation column.

2. In the pop\-up dialog, select the event to test and click **OK**.

3. Wait for the callback to complete under the **Callback records** tab. A pop\-up will appear showing the test result (success or failure). A **Callback succeeded** status indicates that the receiving address is available.


<span id="d70b78f0"></span>
## Single task completed event

When an asynchronous task you submitted (such as video enhancement) is completed (either successfully or with a failure), AI MediaKit will push this event to your configured callback address.


|Field |Type |Example |Description |
|---|---|---|---|
|`RequestId` |String |`2026032520...` |The unique ID of this callback request. |
|`Version` |String |`1.0` |The event version number. |
|`EventType` |String |`AIMediaKitTaskComplete` |The event type, which is always `AIMediaKitTaskComplete`. |
|`EventTime` |String |`2026-03-25T12:44:34Z` |The UTC time when the event occurred, in `YYYY-MM-DDTHH:mm:ssZ` format. |
|`Data` |Object |`{...}` |The core data object containing the task processing result. See [Data](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification#01febc27) for details. |
|`TaskId` |String |`amk_tool_...` |The unique identifier of the task, identical to the value of `Data.TaskId`. |


<span id="01febc27"></span>
### Data

The `Data` object contains the final status and result of the task.


|Field |Type |Example |Description |
|---|---|---|---|
|`Code` |String |`Success` |The status code of the task execution result.<br><br><br>* `Success` indicates success.<br><br>* `Failed` indicates failure. |
|`Message` |String |`AIMediaKit Task Success` |A descriptive message of the task execution result. |
|`TaskId` |String |`amk_tool_...` |The unique identifier of the task. |
|`Result` |Object |`{...}` or `null` |The result data object returned on task success, or `null` on failure. See the [Result](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification#2f6371f9) section for details. |
|`CallbackArgs` |String |`{"user_id":"abc"}` |Custom callback arguments. If you set the `callback_args` parameter when submitting the task, its content will be returned here as\-is. This field is omitted if not set. |
|`queue_id` |String |`q00a9731...` |The ID of the queue to which the task belongs. |


<span id="2f6371f9"></span>
### Result

When a task is successful, the structure of the `Data.Result` object for the Enhance Video task is as follows.


|Parameter |Type |Example |Description |
|---|---|---|---|
|`video_url` |String |`https://media.example.com/output.mp4?auth_key=...` |The download URL for the enhanced video file. This URL is valid for **24 hours**. |
|`duration` |Number |`120.5` |The total duration of the output video (in seconds). |
|`resolution` |String |`1080p` |The resolution of the output video. |
|`fps` |Number |`60` |The frame rate of the output video. |
|`tool_version` |String |`professional` |The tool version actually used for the task. |


<span id="699c7be4"></span>
### Callback example

The following is an example for a completed "Enhance Video" task.

```JSON
{
    "RequestId": "20260325204413EB38CD20C7D66989462D",
    "Version": "1.0",
    "EventType": "AIMediaKitTaskComplete",
    "EventTime": "2026-03-25T12:44:34Z",
    "Data": {
        "Code": "Success",
        "Message": "AIMediaKit Task Success",
        "TaskId": "amk_tool_enhance_video_1703200",
        "Result": {
            "video_url": "https://media.example.com/enhanced_output.mp4?auth_key=...",
            "duration": 120.5,
            "resolution": "1080p",
            "fps": 60,
            "tool_version": "professional"
        }
    },
    "TaskId": "amk_tool_enhance_video_1703200"
}
```
