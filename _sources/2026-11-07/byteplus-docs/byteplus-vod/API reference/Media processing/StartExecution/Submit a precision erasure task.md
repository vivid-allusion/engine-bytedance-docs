---
title: "Submit a precision erasure task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution-precision-erasure"
---

Call `StartExecution` to submit an asynchronous precision erasure task. Set `Operation.Type` to `Task` and `Operation.Task.Type` to `Erase`. For the feature description and usage workflow, see [Precision erasure](https://docs.byteplus.com/docs/byteplus-vod/docs-precision-subtitle-erasure).

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
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/121889#input) |No |\- |Information about the input file for the media processing task. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/en/docs/25/121889#runtimecontrol) |No |\- |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/121889#operation) |No |\- |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|SpaceName |String |No |test |The name of the space where the media processing task will be executed. You can obtain the space name by calling the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API or viewing it on the [Spaces](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/overview/?) page of the console. |


<span id="input"></span>
### Input


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vid |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the `Vid` parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the `DirectUrl` parameter. |
|Vid |String |No |v0ccfeg7007acsg\*\*\*fog65ubr7niqng |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/121889#directurl) |No |\- |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space and obtain the relevant information. |


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
|Task |Object of [OperationTask](https://docs.byteplus.com/en/docs/25/121889#operationtask) |No |\- |Single task configuration. Required when `Type` is `Task`. |


<span id="operationtask"></span>
### OperationTask


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Erase |Set to `Erase` for a precision erasure task. |
|Erase |Object of [OperationTaskErase](https://docs.byteplus.com/en/docs/25/121889#operationtaskerase) |No |\- |Precision erasure task configuration. Required when `Type` is `Erase`. |


<span id="operationtaskerase"></span>
### OperationTaskErase


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Mode |String |No |Auto |Erasure mode. The available values are as follows:<br><br><br>* `Auto`: Automatic erasure mode. In this mode, the system will enable OCR and perform erasure operations based on the recognition results.<br><br>* `Manual`: (Beta) Manual erasure mode. In this mode, the system will not enable OCR and will only erase white subtitle content.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">The usage and applicable scenarios of different modes are as follows:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Generally, you can set <code>Mode</code> to <code>Auto</code>, and then set <code>Auto.Type</code> to <code>Subtitle</code> (subtitles only) or <code>Text</code> (subtitles and other text) to erase the specified type of text.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you have special requirements for the erasure area, you can specify the erasure area by setting <code>Locations</code> to only erase the text recognized by OCR within the area.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">In scenarios where you need to erase <strong>subtitles in less common languages other than Chinese and English</strong>, you can set <code>Mode</code> to <code>Manual</code> and set <code>Locations</code>to specify the erasure area.</div><br> |
|Auto |Object of [OperationTaskEraseAuto](https://docs.byteplus.com/en/docs/25/121889#operationtaskeraseauto) |No |\- |Configuration of the auto erasure mode. |
|Manual |Object of [OperationTaskEraseManual](https://docs.byteplus.com/en/docs/25/121889#operationtaskerasemanual) |No |\- |Configuration of manual erasure mode. |
|WithEraseInfo |Boolean |No |true |Whether to return the details of the erased file. |
|EraseOption |Object of [OperationTaskEraseOption](https://docs.byteplus.com/en/docs/25/121889#operationtaskeraseoption) |No |\- |Erasure options. It allows you to designate specific time segments for processing or exclusion, providing granular control over the erasure operation. |
|NewVid |Boolean |No |true |Whether to generate a new `Vid` for the erased video. |
|VideoOption |Object of [OperationTaskEraseVideoOption](https://docs.byteplus.com/en/docs/25/121889#operationtaskerasevideooption) |No |\- |The video encoding settings for the output video after subtitle erasure. |


<span id="operationtaskeraseauto"></span>
### OperationTaskEraseAuto


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |No |Subtitle |Text erasure types:<br><br><br>* `Subtitle`: Erase text detected as subtitles by OCR.<br><br>* `Text`: (Beta) Erase subtitles and other texts. |
|Locations |Array of [OperationTaskEraseLocation](https://docs.byteplus.com/en/docs/25/121889#operationtaskeraselocation) |No |\- |Array of erasing areas. After adding erasing areas, the system will only erase the text within the areas. |
|SubtitleFilter |Object of [OperationTaskEraseSubtitleFilter](https://docs.byteplus.com/en/docs/25/121889#operationtaskerasesubtitlefilter) |No |\- |It is used to specify the height of the erased text and the ratio of the distance from the center of the video width, so as to precisely control the erasing range.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div><br><br><br><div data-tips="true" data-tips-type="warning">It only takes effect when <code>Mode</code> is <code>Auto</code> and <code>Type</code> is <code>Subtitle</code>.</div><br> |


<span id="operationtaskeraselocation"></span>
### OperationTaskEraseLocation


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|RatioLocation |Object of [RatioRectangle](https://docs.byteplus.com/en/docs/25/121889#ratiorectangle) |No |\- |The information of the erasing area.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="tip">For details of the parameters of the erasing area, please refer to <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-precision-subtitle-erasure">Precision erasure</a>.</div><br> |


<span id="operationtaskerasesubtitlefilter"></span>
### OperationTaskEraseSubtitleFilter


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|MinTextHeightRatio |Double |No |0.01 |The minimum ratio of text height, with a default value of `0.01`, which means 1% of the video height. |
|MaxTextHeightRatio |Double |No |0.1 |The maximum ratio of text height. The default value is `0.1`, which means 10% of the video height. |
|RectangleCenterOffsetRatio |Double |No |0.1 |The ratio of the center of the text area deviating from the center of the video width. The default value is `0.08`, which means 8%. |


<span id="operationtaskerasemanual"></span>
### OperationTaskEraseManual


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Locations |Array of [OperationTaskEraseLocation](https://docs.byteplus.com/en/docs/25/121889#operationtaskeraselocation) |No |\- |Array of erasure boxes. After adding erasure boxes, the system will only erase the text within the boxes. |


<span id="operationtaskeraseoption"></span>
### OperationTaskEraseOption


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ClipFilter |Object of [OperationTaskEraseOptionClipFilter](https://docs.byteplus.com/en/docs/25/121889#operationtaskeraseoptionclipfilter) |No |\- |Video segment filter. It is used to define one or more time segments and specify the operation mode (erase or skip) to be performed on these segments. |


<span id="operationtaskeraseoptionclipfilter"></span>
### OperationTaskEraseOptionClipFilter


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Mode |String |No |Skip |Clip processing mode. It determines how to handle the time segments defined in the `Clips` array.<br><br><br>* `Skip`: Skip mode. The system will erase the entire video but skip the segment areas specified in the `Clips` array, leaving their subtitles intact.<br><br>* `Selected`: Selected mode. The system will only perform subtitle erasure on the segment areas specified in the `Clips`array, and the other parts of the video will remain unchanged. |
|Clips |Array of [OperationTaskEraseOptionClip](https://docs.byteplus.com/en/docs/25/121889#operationtaskeraseoptionclip) |No |\- |Array of target time segments. |


<span id="operationtaskeraseoptionclip"></span>
### OperationTaskEraseOptionClip


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Start |Double |No |10 |The start time of the segment, in seconds. |
|End |Double |No |20 |The end time of the segment, in seconds. |


<span id="operationtaskerasevideooption"></span>
### OperationTaskEraseVideoOption


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|EncodeMode |String |No |Size |Encoding mode. The supported values are as follows:<br><br><br>* `Quality` (Default): Quality\-priority mode. In this mode, the system uses a higher target bitrate for encoding to ensure superior visual quality. This typically results in an output bitrate significantly higher than that of the source file, leading to an increase in file size.<br><br>* `Size`: Size\-priority mode. This mode attempts to align the output bitrate with the source video's bitrate as closely as possible while maintaining an acceptable level of image quality. |


<span id="ratiorectangle"></span>
### RatioRectangle


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TopLeftX |Double |No |0 |The offset ratio on the X\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates a full offset (aligned with the right edge of the video). |
|TopLeftY |Double |No |0 |The offset ratio on the Y\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a complete offset (aligned with the lower edge of the video). |
|BottomRightX |Double |No |0 |The offset ratio on the X\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates full offset (aligned with the right edge of the video). |
|BottomRightY |Double |No |0 |The offset ratio on the Y\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a full offset (aligned with the lower edge of the video). |


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
            "Type": "Erase",
            "Erase": {
                "Mode": "Auto",
                "Auto": {
                    "Type": "Subtitle",
                    "SubtitleFilter": {}
                },
                "WithEraseInfo": true,
                "NewVid": true
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
