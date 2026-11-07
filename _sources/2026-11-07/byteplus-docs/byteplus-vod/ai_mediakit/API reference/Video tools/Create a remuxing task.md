---
title: "Create a remuxing task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-create-a-remuxing-task"
---

`POST https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/remux-video`

This API submits an asynchronous video remuxing task. Remuxing only changes the container format and does not re\-encode or re\-decode the audio/video bitstreams, so it can quickly convert between mainstream container formats such as MP4, FLV, and MPEG\-TS with no quality loss and at very low cost. This feature is widely used in scenarios such as VOD distribution adaptation, streaming segmentation and packaging, and multi\-device compatibility.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">INFO</div>


<div data-tips="true" data-tips-type="default">For the complete usage flow and application examples, see <a href="https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-remuxing">Remuxing</a>.</div>


<span id="request-parameters"></span>
## Request parameters

<span id="header"></span>
### Header


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`Authorization` |String |Yes |`Bearer {Your_API_Key}` |Refer to [Basic concepts and prerequisites](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites) to obtain an API Key. |


<span id="body"></span>
### Body


|Parameter |Type |Required |Example Value |Description |
|---|---|---|---|---|
|`video_url` |String |Yes |`https://example-video.com/input.mov` |The URL of the video to be transcoded.<br><br><br>* **File source**: Only publicly accessible HTTP/HTTPS URLs are supported.<br><br>* **Supported formats**: Mainstream video formats such as `mp4`, `flv`, `ts`, `avi`, `mov`, `wmv`, `mkv`. |
|`container_format` |String |Yes |`FLV` |The target container format. Supported values:<br><br><br>* `MP4` (Default)<br><br>* `FLV`<br><br>* `MPEGTS` |
|`metadata_keep_tags` |Array of Strings |No |`["title", "artist"]` |The list of metadata tags to keep from the source video. By default, transcoding discards most metadata (such as title and artist). Use this parameter to specify the tag keys to keep. This parameter does not take effect when the `container_format` is set to `MPEGTS`. |
|`metadata_add_tags` |Array of Objects |No |`[{"key": "album", "value": "2024 Remaster"}]` |The list of metadata tags to add to the output video. Each tag consists of a `key` and a `value`. If an added tag has the same name as a kept tag, the setting here **overrides** the source file's value. This parameter does not take effect when the `container_format` is set to `MPEGTS`. |
|`client_token` |String |No |`your_unique_request_id_132` |A user request token for idempotency control. It is case\-sensitive and must not exceed 64 printable ASCII characters. For details, see [Idempotency control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-concepts-and-prerequisites#0e2ee2f8). |
|`callback_args` |String |No |`your_custom_callback_args` |Custom callback arguments. The content you provide is returned as\-is through an event upon task completion, allowing you to associate it with your business logic. The field length is limited to 512 bytes. For details, see [Event notification](https://docs.byteplus.com/uchbv7an/yf0irz3g). |
|`callback_url` |String |No |`https://example.com/callback` |A task\-specific endpoint to receive event notifications. If provided, this URL overrides the global callback URL configured in the console. The endpoint must be a publicly accessible URL starting with `http://` or `https://`. For details on the callback process and payload structure, refer to [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification). |


<span id="request-example"></span>
## Request example

The following example demonstrates how to submit a remuxing task that converts the source video to `FLV` format and adds a custom metadata tag.

```Bash
curl -X POST 'https://mediakit.ap-southeast-1.bytepluses.com/api/v1/tools/remux-video' \
-H 'Authorization: Bearer {Your_API_Key}' \
-H 'Content-Type: application/json' \
-d '{
    "video_url": "https://example.com/source_video.mp4",
    "container_format": "FLV",
    "metadata_add_tags": [
        {
            "key": "source_id",
            "value": "video_001"
        }
    ]
 }'
```


<span id="response-description"></span>
## Response

After submitting the task, the API immediately returns a synchronous response indicating whether the task has been successfully enqueued for processing.

<span id="b910b2fa"></span>
### Response parameters


|Parameter |Type |Description |
|---|---|---|
|`success` |Boolean |Indicates whether the task was submitted successfully.<br><br><br>* `true`: The task has been successfully submitted to the processing queue.<br><br>* `false`: The request contains errors, and the task submission failed. Check the `error` field for details. |
|`task_id` |String |The unique identifier for the task. A valid value is returned only when `success` is `true`. You can use this ID to query the task status and results. |
|`request_id` |String |The unique identifier for this API request, which can be used for troubleshooting. |
|`error` |Object |An object containing error details, returned only when `success` is `false`. See the Error object below. |


<span id="dc2bad88"></span>
#### The error object


|Parameter |Type |Description |
|---|---|---|
|`code` |String |The specific error code. For detailed information on each error code, refer to [Error codes](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-error-codes). |
|`type` |String |The general type of the error, such as `BadRequest`. |
|`message` |String |A detailed description of the error for debugging purposes. |
|`param` |String |(Optional) Indicates the specific parameter that caused the error. |


<span id="33da971c"></span>
### Response example

<span id="b48b0ebc"></span>
#### Success

```JSON
{
    "success": true,
    "task_id": "amk-tool-remux-video-123456789",
    "request_id": "20240522190000ABCDEFG67890"
}
```


<span id="497fa061"></span>
#### Failure

```JSON
{
    "success": false,
    "task_id": "",
    "request_id": "20240522190500XYZW54321",
    "error": {
        "code": "InvalidParameter",
        "message": "The parameter 'container_format' is missing or invalid.",
        "type": "BadRequest"
    }
}
```


<span id="asynchronous-task-result"></span>
## Asynchronous task result

Remuxing is an asynchronous task. The execution status and final result are not returned synchronously upon submission. You can obtain the task result in two ways:


* **Method 1:**  Periodically call the [Get task details](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-get-task-details) with the `task_id` obtained after submitting the task, until the `status` field changes to `completed` or `failed`.

* **Method 2:**  Pre\-configure a callback URL in the AI MediaKit console, or specify a callback address for a single task using the `callback_url` parameter during submission. Once the task is complete, the system will POST the detailed results to your specified URL. For more details, see [Event notification](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-event-notification).


When a task is successfully completed, the `result` field in the task information you retrieve contains the following:


|Parameter |Type |Description |
|---|---|---|
|`video_url` |String |The download URL of the output video. This URL is valid for **24 hours** by default; please save the output file promptly. |
|`duration` |Number |The duration of the output video, in seconds. |


Example of a complete task information response:

```JSON
{
    "success": true,
    "task_id": "amk-tool-remux-video-123456789",
    "request_id": "20240522190000ABCDEFG67890",
    "result": {
        "video_url": "https://example.byteplus.com/remux_output.flv?auth_key=...",
        "duration": 180.5
    },
    "expires_at": 1777468800,
    "created_at": 1777292400,
    "finished_at": 1777292415
}
```
