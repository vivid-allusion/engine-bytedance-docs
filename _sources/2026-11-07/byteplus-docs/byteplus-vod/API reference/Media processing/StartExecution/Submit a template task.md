---
title: "Submit a template task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution-template"
---

Call `StartExecution` to submit an asynchronous task using an existing media processing template. Set `Operation.Type` to `Template`, select the template type, and pass its `TemplateId`. Create and configure the template in the BytePlus VOD console before submitting the task.


|Template type |`Operation.Template.Type` |Configuration |
|---|---|---|
|Video transcoding |`TranscodeVideo` |[OperationTemplateTranscodeVideo](https://docs.byteplus.com/en/docs/25/121896#operationtemplatetranscodevideo) |
|Low\-bitrate HD |`ByteHD` |[OperationTemplateByteHD](https://docs.byteplus.com/en/docs/25/121896#operationtemplatebytehd) |
|Audio transcoding |`TranscodeAudio` |[OperationTemplateTranscodeAudio](https://docs.byteplus.com/en/docs/25/121896#operationtemplatetranscodeaudio) |
|Video enhancement |`Enhance` |[OperationTemplateEnhance](https://docs.byteplus.com/en/docs/25/121896#operationtemplateenhance) |


For tasks configured directly in the request, see [StartExecution API overview](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution).

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
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/121896#input) |No |\- |Information about the input file for the media processing task. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/en/docs/25/121896#runtimecontrol) |No |\- |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/121896#operation) |No |\- |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|SpaceName |String |No |test |The name of the space where the media processing task will be executed. You can obtain the space name by calling the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API or viewing it on the [Spaces](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/overview/?) page of the console. |


<span id="input"></span>
### Input


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vid |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the `Vid` parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the `DirectUrl` parameter. |
|Vid |String |No |v0ccfeg7007acsg\*\*\*fog65ubr7niqng |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/121896#directurl) |No |\- |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space and obtain the relevant information. |


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
|Type |String |Yes |Template |Set to `Template` to submit a template task. |
|Template |Object of [OperationTemplate](https://docs.byteplus.com/en/docs/25/121896#operationtemplate) |No |\- |Single template configuration. Required when `Type` is `Template`. |


<span id="operationtemplate"></span>
### OperationTemplate


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |No |TranscodeVideo |Single template task type. The valid values are as follows:<br><br><br>* `TranscodeVideo`: Video transcoding template task.<br><br>* `ByteHD`: Low\-bitrate HD template task.<br><br>* `TranscodeAudio`: Audio transcoding template task.<br><br>* `Enhance`: Video enhancement template task. |
|TranscodeVideo |Object of [OperationTemplateTranscodeVideo](https://docs.byteplus.com/en/docs/25/121896#operationtemplatetranscodevideo) |No |\- |Video transcoding template task configuration. The parameter is required when `Type` is `TranscodeVideo`. |
|ByteHD |Object of [OperationTemplateByteHD](https://docs.byteplus.com/en/docs/25/121896#operationtemplatebytehd) |No |\- |Low\-bitrate HD template task configuration. The parameter is required when `Type` is `ByteHD`. |
|TranscodeAudio |Object of [OperationTemplateTranscodeAudio](https://docs.byteplus.com/en/docs/25/121896#operationtemplatetranscodeaudio) |No |\- |Audio transcoding template task configuration. The parameter is required when `Type` is `TranscodeAudio`. |
|Enhance |Object of [OperationTemplateEnhance](https://docs.byteplus.com/en/docs/25/121896#operationtemplateenhance) |No |\- |Video enhancement template task configuration. The parameter is required when `Type` is `Enhance`. |


<span id="operationtemplatetranscodevideo"></span>
### OperationTemplateTranscodeVideo


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TemplateId |String |No |ddc7d66386\*\*\*6056a |Video transcoding template ID. You can create and configure a video transcoding template in the BytePlus VOD console, see [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template). |
|WatermarkTemplateId |String |No |v0dc24g10\*\*\*c1cepmu6g |Watermark template ID. You can create and configure a watermark template in the BytePlus VOD console, see [Watermark and ad insertion template](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template). |


<span id="operationtemplatebytehd"></span>
### OperationTemplateByteHD


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TemplateId |String |No |ddc66386\*\*\*6056a |Low\-bitrate HD template ID. You can create and configure a low\-bitrate HD template in the BytePlus VOD console, see [Low-bitrate HD template](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template). |
|WatermarkTemplateId |String |No |v0dc24g10\*\*\*c1cepmu6g |Watermark template ID. You can create and configure a watermark template in the BytePlus VOD console, see [Watermark and ad insertion template](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template). |


<span id="operationtemplatetranscodeaudio"></span>
### OperationTemplateTranscodeAudio


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TemplateId |String |No |ddc7d66386\*\*\*6056a |Audio transcoding template ID. You can create and configure an audio transcoding template in the BytePlus VOD console, see [Audio transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template). |


<span id="operationtemplateenhance"></span>
### OperationTemplateEnhance


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TemplateId |String |No |ddc7d66386\*\*\*6056a |Video enhancement template ID. You can create and configure a video enhancement template in the BytePlus VOD console, see [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template). |


<span id="Response parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RunId |String |hb:c5cacd4946bd\*\*\*a5fd9f74159b03ae8 |The execution ID of the media processing task, used to uniquely identify a specific task execution instance. |


<span id="sample-requests"></span>
## Sample requests

Use the same endpoint for all template types:

```HTTP
POST https://vod.byteplusapi.com?Action=StartExecution&Version=2025-07-01
```


<span id="video-transcoding"></span>
### Video transcoding

```JSON
{
    "SpaceName": "test",
    "Input": {
        "Type": "Vid",
        "Vid": "v0ccfeg7007acsg***fog65ubr7niqng"
    },
    "Operation": {
        "Type": "Template",
        "Template": {
            "Type": "TranscodeVideo",
            "TranscodeVideo": {
                "TemplateId": "ddc7d66386***6056a"
            }
        }
    }
}
```


<span id="low-bitrate-hd"></span>
### Low\-bitrate HD

```JSON
{
    "SpaceName": "test",
    "Input": {
        "Type": "Vid",
        "Vid": "v0ccfeg7007acsg***fog65ubr7niqng"
    },
    "Operation": {
        "Type": "Template",
        "Template": {
            "Type": "ByteHD",
            "ByteHD": {
                "TemplateId": "ddc7d66386***6056a"
            }
        }
    }
}
```


<span id="audio-transcoding"></span>
### Audio transcoding

```JSON
{
    "SpaceName": "test",
    "Input": {
        "Type": "Vid",
        "Vid": "v0ccfeg7007acsg***fog65ubr7niqng"
    },
    "Operation": {
        "Type": "Template",
        "Template": {
            "Type": "TranscodeAudio",
            "TranscodeAudio": {
                "TemplateId": "ddc7d66386***6056a"
            }
        }
    }
}
```


<span id="video-enhancement"></span>
### Video enhancement

```JSON
{
    "SpaceName": "test",
    "Input": {
        "Type": "Vid",
        "Vid": "v0ccfeg7007acsg***fog65ubr7niqng"
    },
    "Operation": {
        "Type": "Template",
        "Template": {
            "Type": "Enhance",
            "Enhance": {
                "TemplateId": "ddc7d66386***6056a"
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
