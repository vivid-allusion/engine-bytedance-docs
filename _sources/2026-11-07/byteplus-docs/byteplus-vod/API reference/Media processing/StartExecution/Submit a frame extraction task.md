---
title: "Submit a frame extraction task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution-frame-extraction"
---

Call `StartExecution` to submit an asynchronous frame extraction task. Set `Operation.Type` to `Task` and `Operation.Task.Type` to `Snapshot`. For the feature description and usage workflow, see [Frame extraction](https://docs.byteplus.com/docs/byteplus-vod/docs-frame-extraction).

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
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/121895#input) |No |\- |Information about the input file for the media processing task. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/en/docs/25/121895#runtimecontrol) |No |\- |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/121895#operation) |No |\- |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|SpaceName |String |No |test |The name of the space where the media processing task will be executed. You can obtain the space name by calling the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API or viewing it on the [Spaces](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/overview/?) page of the console. |


<span id="input"></span>
### Input


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vid |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the `Vid` parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the `DirectUrl` parameter. |
|Vid |String |No |v0ccfeg7007acsg\*\*\*fog65ubr7niqng |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/121895#directurl) |No |\- |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space and obtain the relevant information. |


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
|Task |Object of [OperationTask](https://docs.byteplus.com/en/docs/25/121895#operationtask) |No |\- |Single task configuration. Required when `Type` is `Task`. |


<span id="operationtask"></span>
### OperationTask


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Snapshot |Set to `Snapshot` for a frame extraction task. |
|Snapshot |Object of [OperationTaskSnapshot](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshot) |No |\- |Frame extraction task configuration. Required when `Type` is `Snapshot`. |


<span id="operationtasksnapshot"></span>
### OperationTaskSnapshot


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Strategy |Object of [OperationTaskSnapshotStrategy](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshotstrategy) |Yes |\- |Frame extraction strategy. |
|Target |Object of [OperationTaskSnapshotTarget](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshottarget) |No |\- |Output target configuration. |
|Mode |String |No |Files |Output mode:<br><br>• `Files`: (Default) File path mode. Limited to 1,000 outputs.<br><br>• `Index`: Index mode. Information is stored in media assets. |
|IndexOption |Object of [OperationTaskSnapshotIndexOption](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshotindexoption) |No |\- |Index configuration when `Mode` is `Index`. |


<span id="operationtasksnapshotstrategy"></span>
### OperationTaskSnapshotStrategy


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |TimeInterval |Frame extraction type:<br><br>• `TimeInterval`: Extract frames at fixed time intervals.<br><br>• `SpecifiedTime`: Extract frames at specified timestamps.<br><br>• `SpecifiedFrames`: Extract frames at specified frame numbers.<br><br>• `SceneChange`: Extract frames on scene change. |
|TimeInterval |Object of [OperationTaskSnapshotTimeInterval](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshottimeinterval) |No |\- |Configuration for time interval extraction. Required when `Type` is `TimeInterval`. |
|SpecifiedTime |Object of [OperationTaskSnapshotSpecifiedTime](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshotspecifiedtime) |No |\- |Configuration for specified timestamp extraction. Required when `Type` is `SpecifiedTime`. |
|SpecifiedFrames |Object of [OperationTaskSnapshotSpecifiedFrames](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshotspecifiedframes) |No |\- |Configuration for specified frame number extraction. Required when `Type` is `SpecifiedFrames`. |
|SceneChange |Object of [OperationTaskSnapshotSceneChange](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshotscenechange) |No | |Configuration for scene change extraction. Required when `Type` is `SceneChange`. |


<span id="operationtasksnapshottimeinterval"></span>
### OperationTaskSnapshotTimeInterval


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Interval |Integer |Yes |1000 |Time interval in milliseconds. Must be \> 0. Extraction starts from frame 0. |
|Limit |Integer |No |10 |Maximum number of frames to extract. Default: no limit. Must be \> 0. When the output is a sprite image, this refers to the number of sub\-images. |


<span id="operationtasksnapshotspecifiedtime"></span>
### OperationTaskSnapshotSpecifiedTime


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Times |Array of Integer |Yes |[0, 1] |Time offsets in milliseconds. Each value must be ≥ 0. The output index corresponds to the input index. List length: [1, 1000]. |


<span id="operationtasksnapshotspecifiedframes"></span>
### OperationTaskSnapshotSpecifiedFrames


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Frames |Array of Integer |Yes |[0, \-1] |Frame numbers. Currently, only `0` (first frame) and `-1` (last frame) are supported. |


<span id="operationtasksnapshotscenechange"></span>
### OperationTaskSnapshotSceneChange


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Threshold |Float |Yes |0.1 |Scene change detection threshold. Range: (0, 1). Recommended value: `0.1`. |
|Limit |Integer |No |10 |Maximum number of frames to extract. Default: no limit. Must be \> 0. |


<span id="operationtasksnapshottarget"></span>
### OperationTaskSnapshotTarget


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ScaleLong |Integer |No |1280 |Long edge of the output image in pixels. Default: auto\-adapt to the source aspect ratio. Range: [0, 4096]. When the output is a sprite image, this refers to the sub\-image width.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Upscaling is not supported.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If neither <code>ScaleLong</code> nor <code>ScaleShort</code> is specified, the original dimensions are preserved.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If only one of <code>ScaleLong</code> or <code>ScaleShort</code> is specified, the other dimension is scaled proportionally.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Only <code>ScaleLong: 40</code> specified: For a 100×400 video, the result is 10×40.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Only <code>ScaleShort: 40</code> specified: For a 100×400 video, the result is 40×160.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If both <code>ScaleLong</code> and <code>ScaleShort</code> are specified, the long edge does not exceed <code>ScaleLong</code> and the short edge does not exceed <code>ScaleShort</code>.</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">Both specified as 10×20: For a 100×400 video, the result is 5×20.</div><br> |
|ScaleShort |Integer |No |720 |Short edge of the output image in pixels. Default: auto\-adapt to the source aspect ratio. Range: [0, 4096]. When the output is a sprite image, this refers to the sub\-image height. |
|SpriteConfig |Object of [OperationTaskSnapshotSpriteConfig](https://docs.byteplus.com/en/docs/25/121895#operationtasksnapshotspriteconfig) |No |\- |Sprite image configuration. |


<span id="operationtasksnapshotspriteconfig"></span>
### OperationTaskSnapshotSpriteConfig


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Enable |Boolean |No |true |Whether to generate a sprite image. Default: `false`. Set to `true` to enable. |
|ImgYLen |Integer |No |10 |Number of sub\-images along the vertical axis. Effective when `Enable` is `true`. Range: [1, 100]. Default: `10`. The maximum total sprite image dimension is 65,535 pixels; values below 16,384 are recommended. |
|ImgXLen |Integer |No |10 |Number of sub\-images along the horizontal axis. Effective when `Enable` is `true`. Range: [1, 100]. Default: `10`. The maximum total sprite image dimension is 65,535 pixels; values below 16,384 are recommended. |


<span id="operationtasksnapshotindexoption"></span>
### OperationTaskSnapshotIndexOption


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Tag |String |No |\- |Custom category label. Length: [0, 128]. |


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
            "Type": "Snapshot",
            "Snapshot": {
                "Strategy": {
                    "Type": "TimeInterval",
                    "TimeInterval": {
                        "Interval": 1000,
                        "Limit": 10
                    }
                },
                "Target": {
                    "ScaleLong": 1280,
                    "ScaleShort": 720
                },
                "Mode": "Files"
            }
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
