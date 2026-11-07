---
title: "Submit a scene segmentation task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution-scene-segmentation"
---

Call `StartExecution` to submit an asynchronous scene segmentation task. Set `Operation.Type` to `Task` and `Operation.Task.Type` to `Segment`. For the feature description and usage workflow, see [Scene segmentation](https://docs.byteplus.com/docs/byteplus-vod/docs-scene-segmentation).

For other task types, see [StartExecution API overview](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution).

<span id="Requirements"></span>
## Notes

This API currently supports only the Asia Pacific (Johor) region and does not support the Asia Pacific (Singapore) region.

<span id="HTTP request"></span>
## HTTP request


* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=StartExecution&Version=2025\-07\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`StartExecution` |The API action. For the current API, the value is `StartExecution`. |
|Version |String |Yes |`2025-07-01` |The API version. For the current API, the value is `2025-07-01`. |


<span id="Body"></span>
### Body


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/121892#input) |No |\- |Information about the input file for the media processing task. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/en/docs/25/121892#runtimecontrol) |No |\- |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/121892#operation) |No |\- |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|SpaceName |String |No |test |The name of the space where the media processing task will be executed. You can obtain the space name by calling the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API or viewing it on the [Spaces](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/overview/?) page of the console. |


<span id="input"></span>
### Input


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vid |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the `Vid` parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the `DirectUrl` parameter. |
|Vid |String |No |v0ccfeg7007acsg\*\*\*fog65ubr7niqng |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/121892#directurl) |No |\- |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space and obtain the relevant information. |


<span id="directurl"></span>
### DirectUrl


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|FileName |String |Yes |example.mp4 |The file path. After uploading audio and video to the Video\-on\-Demand (VOD) service, you can obtain the FileName through the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) event. |
|BucketName |String |No |tos\-cn\-v\-cd3a11 |The name of the bucket. You can call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API to obtain the name of the bucket associated with the space. |
|SpaceName |String |Yes |test |The name of the space. You can call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API to obtain information about all spaces under the current account. |


<span id="runtimecontrol"></span>
### RuntimeControl


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|CallbackArgs |String |No |Example |A customizable field. The maximum length of the field is 512 bytes. |
|Priority |Integer |No |2 |Task priority for media processing. The default value is `0`. The valid range is `[-5, 5]`, where a higher number indicates higher priority. |
|ClientToken |String |No |QqS3o5L\*\*\*CDxGZ&b |A unique token provided by the client to distinguish different requests, ensuring idempotency. It is case\-sensitive and should not exceed 64 printable ASCII characters. By default, the transcoding service will perform idempotent behavior if the same request is detected. To bypass idempotency (such as when re\-executing the same media processing task with modified configurations), set this parameter. |


<span id="operation"></span>
### Operation


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Task |Set to `Task` to submit this task. |
|Task |Object of [OperationTask](https://docs.byteplus.com/en/docs/25/121892#operationtask) |No |\- |Single task configuration. Required when `Type` is `Task`. |


<span id="operationtask"></span>
### OperationTask


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Segment |Set to `Segment` for a scene segmentation task. |
|Segment |Object of [OperationTaskSegment](https://docs.byteplus.com/en/docs/25/121892#operationtasksegment) |No |\- |Scene segmentation task configuration. Required when `Type` is `Segment`. |


<span id="operationtasksegment"></span>
### OperationTaskSegment


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|NoFile |Boolean |No |true |Whether to generate clip files:<br><br><br>* `true`: Do not generate clip files.<br><br>* `false`: (Default) Generate clip files. |
|ClipFade |Boolean |No |true |Whether to output detected fade\-in/fade\-out segments as independent clips.<br><br><br>* `false`: Default. Do not output them independently. Fade\-in/fade\-out segments are treated as part of the surrounding scenes and merged into adjacent clips.<br><br>* `true`: Output them independently. If the video contains obvious fade\-in/fade\-out transitions, the system splits them into independent clips. |
|Threshold |Double |No |10 |Sensitivity threshold for scene segmentation. The value range is `[0, 100]`.<br><br><br>* The lower the value, the more sensitive the algorithm is to scene changes, resulting in more segments.<br><br>* The higher the value, the more likely the algorithm is to treat small changes as the same scene, resulting in fewer segments.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">When <code>MinDuration</code>, <code>MaxDuration</code>, and <code>Threshold</code> are all set, the system performs segmentation in the following two stages to ensure that all constraints are met:</div><br><br><br><br>1. <div data-tips="true" data-tips-type="tip">The algorithm first performs segmentation based on the configured <code>Threshold</code> and <code>MinDuration</code>.</div><br><br><br>2. <div data-tips="true" data-tips-type="tip">After the first stage is complete, if any clip duration exceeds the configured <code>MaxDuration</code>, the system ignores the effect of <code>Threshold</code> and performs segmentation again to ensure that the final duration of every clip does not exceed <code>MaxDuration</code>.</div><br> |
|MinDuration |Double |No |3 |Minimum duration of a single clip, in seconds. No default value. The system ensures that the duration of any final generated clip is not less than this value. |
|MaxDuration |Double |No |30 |Maximum duration of a single clip, in seconds. No default value. The system ensures that the duration of any final generated clip is not greater than this value. |


<span id="Response parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RunId |String |hb:c5cacd4946bd\*\*\*a5fd9f74159b03ae8 |The execution ID of the media processing task, used to uniquely identify a specific task execution instance. |


<span id="sample-request"></span>
## Sample request

```HTTP
POST https://vod.byteplusapi.com?Action=StartExecution&Version=2025-07-01
```


```JSON
{
    "SpaceName": "test",
    "Input": {
        "Type": "Vid",
        "Vid": "v0ccfeg7007acsg***fog65ubr7niqng"
    },
    "Operation": {
        "Type": "Task",
        "Task": {
            "Type": "Segment",
            "Segment": {}
        }
    }
}
```


<span id="sample-response"></span>
## Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "StartExecution",
        "Version": "2025-07-01",
        "Service": "vod",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "RunId": "hb:c5cacd4946bd***a5fd9f74159b03ae8"
    }
}
```


<span id="retrieve-the-task-result"></span>
## Retrieve the task result

After the task is submitted, save the returned `RunId`. The system processes the task asynchronously. You can retrieve the result in either of the following ways:


* Call [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) with the `RunId` to query the task status and output.

* Configure [event notifications](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-) and subscribe to [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete) to receive the result when processing finishes.


<span id="Error codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

<span id="server-sdks"></span>
## Server SDKs

This API is supported by VOD SDK 2.0. For integration instructions and examples, see [V2.0 SDK introduction and migration guide](https://docs.byteplus.com/docs/byteplus-vod/docs-server-sdk-v2).
