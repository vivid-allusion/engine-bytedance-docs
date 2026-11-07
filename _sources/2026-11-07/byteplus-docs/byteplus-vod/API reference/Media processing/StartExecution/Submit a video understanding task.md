---
title: "Submit a video understanding task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution-video-understanding"
---

> **Deprecated task type**

> The `StartExecution` task type `Vision` and all associated `OperationTaskVision` parameters documented on this page are deprecated. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new integrations and migrate existing integrations to its request structure. For configuration instructions, see [Intelligent video understanding](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding).

The following parameter definitions and examples are retained as a reference for existing `Vision` integrations.

For other task types, see [StartExecution API overview](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution).

## Notes

This API currently supports only the Asia Pacific (Johor) region and does not support the Asia Pacific (Singapore) region.

## HTTP request

* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=StartExecution&Version=2025\-07\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

### Query

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`StartExecution` |The API action. For the current API, the value is `StartExecution`. |
|Version |String |Yes |`2025-07-01` |The API version. For the current API, the value is `2025-07-01`. |

### Body

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/121890#input) |No |\- |Information about the input file for the media processing task. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/en/docs/25/121890#runtimecontrol) |No |\- |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/121890#operation) |No |\- |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|SpaceName |String |No |test |The name of the space where the media processing task will be executed. You can obtain the space name by calling the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API or viewing it on the [Spaces](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/overview/?) page of the console. |

### Input

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vid |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the `Vid` parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the `DirectUrl` parameter. |
|Vid |String |No |v0ccfeg7007acsg\*\*\*fog65ubr7niqng |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/121890#directurl) |No |\- |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space and obtain the relevant information. |

### DirectUrl

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|FileName |String |Yes |example.mp4 |The file path. After uploading audio and video to the Video\-on\-Demand (VOD) service, you can obtain the FileName through the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) event. |
|BucketName |String |No |tos\-cn\-v\-cd3a11 |The name of the bucket. You can call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API to obtain the name of the bucket associated with the space. |
|SpaceName |String |Yes |test |The name of the space. You can call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API to obtain information about all spaces under the current account. |

### RuntimeControl

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|CallbackArgs |String |No |Example |A customizable field. The maximum length of the field is 512 bytes. |
|Priority |Integer |No |2 |Task priority for media processing. The default value is `0`. The valid range is `[-5, 5]`, where a higher number indicates higher priority. |
|ClientToken |String |No |QqS3o5L\*\*\*CDxGZ&b |A unique token provided by the client to distinguish different requests, ensuring idempotency. It is case\-sensitive and should not exceed 64 printable ASCII characters. By default, the transcoding service will perform idempotent behavior if the same request is detected. To bypass idempotency (such as when re\-executing the same media processing task with modified configurations), set this parameter. |

### Operation

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Task |Set to `Task` to submit this task. |
|Task |Object of [OperationTask](https://docs.byteplus.com/en/docs/25/121890#operationtask) |No |\- |Single task configuration. Required when `Type` is `Task`. |

### OperationTask

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vision |Set to `Vision` for an intelligent video understanding task. |
|Vision |Object of [OperationTaskVision](https://docs.byteplus.com/en/docs/25/121890#operationtaskvision) |No |\- |Intelligent video understanding task configuration. Required when `Type` is `Vision`. |

### OperationTaskVision

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Prompt |String |No |# Role<br><br>You are an expert in video understanding, proficient in understanding and analyzing videos.<br><br># Task<br><br>The input content is the segmented description text of the video summarized from the popular online video and the transcribed text of the video audio. Please understand the video based on the input content and describe the content of the video in detail.<br><br># Video segmented description text<br><br>{{PLACEHOLDER_VIDEO_CLIP_RESULT}}<br><br># Video audio transcription text<br><br>{{PLACEHOLDER_ASR_RESULT}} |Large model prompt. Use UTF\-8 encoding. The length cannot exceed 30,000 characters. According to the video understanding mode configured in the `Model` parameter, the prompt must contain the corresponding placeholders:<br><br><br>* **VLM + LLM mode**: The following two placeholders must be included.<br><br>   * `{{PLACEHOLDER_ASR_RESULT}}`: Controls whether to enable ASR (Automatic Speech Recognition).<br><br>   * `{{PLACEHOLDER_VIDEO_CLIP_RESULT}}`: Controls whether to perform video slicing.<br><br>* **VLM\-only or LLM\-only mode**: Only the `{{PLACEHOLDER_ASR_RESULT}}`placeholder needs to be included.<br><br><br>> **Warning**<br><br><br>> `Prompt` and `AnalysisMode`are mutually dependent — at least one must be specified. Leaving both empty will result in a request error.<br> |
|Model |Object of [OperationTaskVisionModel](https://docs.byteplus.com/en/docs/25/121890#operationtaskvisionmodel) |Yes |\- |The large model used for video understanding and its working mode. If not configured, the system default model and multimodal understanding (VLM + LLM) mode will be used. You can use this parameter to customize the configuration of the model and the understanding mode for videos. The following three modes are supported:<br><br><br>* **Pure visual understanding (VLM only)**  : Suitable for scenarios where you need to analyze the content of video frames (such as short videos no longer than 10 minutes). Video screenshots will be taken. It is recommended to set the screenshot resolution to 240p to get more screenshots. It is recommended to use models that support a context of 128k or more (such as `dola-seed-2.0-pro`).<br><br>* **Pure audio understanding (LLM only)**  : Suitable for scenarios where there is no need to understand the content of video frames (such as lecture videos, etc.).<br><br>* **Multimodal understanding (VLM + LLM)**  : Suitable for long \- video understanding (supports a maximum of 2 hours). The long video will be divided into multiple segments. VLM will be used to understand each segment separately, and finally LLM will be used to summarize the understanding results of each segment. |
|Segment |Object of [OperationTaskVisionSegment](https://docs.byteplus.com/en/docs/25/121890#operationtaskvisionsegment) |No |\- |Video segmentation understanding configuration. It is used to specify the start and end times of the video understanding task. If `Start` is not set, it will default to starting from the beginning of the video; if `End` is not set, it will default to ending at the end of the video. `End` must be greater than `Start`. |
|SnapshotParam |Object of [OperationTaskVisionSnapshotParam](https://docs.byteplus.com/en/docs/25/121890#operationtaskvisionsnapshotparam) |No |\- |Screenshot strategy configuration. Screenshots will be taken of the video during the video understanding process. The default screenshot strategy is to take a maximum of 50 screenshots at uniform time intervals. If you need to change the screenshot strategy, you can pass in this parameter. |
|AnalysisMode |Object of [OperationTaskVisionAnalysisMode](https://docs.byteplus.com/en/docs/25/121890#operationtaskvisionanalysismode) |No |\- |Analysis mode. When `AnalysisMode` is specified, the system applies a built\-in prompt for the selected mode and ignores any user\-provided prompt.<br><br>> **Warning**<br><br><br>> `Prompt` and `AnalysisMode`are mutually dependent — at least one must be specified. Leaving both empty will result in a request error.<br> |

### OperationTaskVisionModel

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|DoubaoVisionEndpoint |String |Yes |ep\-202412\*\*\*75335\-cg2p7 |The inference access point ID of the Dola VLM (Vision Language Model). For details, please refer to [Enable large models and create inference nodes](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#enable-models).<br><br>> **Warning**<br><br><br>> Either `DoubaoVisionEndpoint` or `DoubaoTextEndpoint`is required.<br> |
|AsrAppId |String |Yes |3500\*\*\*054 |The APP ID of the Automatic Speech Recognition (ASR) product. For details, please refer to [Activate the large model streaming speech recognition service and obtain the APP ID](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#enable-asr). |
|AsrAppType |String |Yes |volc.bigasr.sauc.duration |In the speech recognition (ASR) product, the type of the streaming speech recognition large model must be consistent with the service type you have activated. The available values are as follows:<br><br><br>* `volc.bigasr.sauc.duration`: Hourly version |
|DoubaoTextEndpoint |String |No |ep\-202412\*\*\*75335\-cg2p7 |The inference access point ID of the Dola LLM (Large Language Model). For details, please refer to [Enable large models and create inference nodes](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#enable-models).<br><br>> **Warning**<br><br><br>> Either `DoubaoVisionEndpoint` or `DoubaoTextEndpoint`is required.<br> |

### OperationTaskVisionSegment

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Start |Double |No |100 |Start time, in seconds. |
|End |Double |No |200 |End time, in seconds. |

### OperationTaskVisionSnapshotParam

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Resolution |String |Yes |720p |The resolution of the video screenshot has the following values:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `720p`<br><br>* `1080p` |
|Fps |Double |Yes |1 |The number of frames captured per second. |
|Area |Object of [RatioRectangle](https://docs.byteplus.com/en/docs/25/121890#ratiorectangle) |No |\- |Screenshot area configuration. |

### RatioRectangle

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|TopLeftX |Double |No |0 |The offset ratio on the X\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates a full offset (aligned with the right edge of the video). |
|TopLeftY |Double |No |0 |The offset ratio on the Y\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a complete offset (aligned with the lower edge of the video). |
|BottomRightX |Double |No |0 |The offset ratio on the X\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates full offset (aligned with the right edge of the video). |
|BottomRightY |Double |No |0 |The offset ratio on the Y\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a full offset (aligned with the lower edge of the video). |

### OperationTaskVisionAnalysisMode

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|SmartTagOption |Object of [OperationTaskVisionAnalysisModeSmartTagOption](https://docs.byteplus.com/en/docs/25/121890#operationtaskvisionanalysismodesmarttagoption) |No |\- |Configuration for smart tag mode. |

### OperationTaskVisionAnalysisModeSmartTagOption

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Enable |Boolean |Yes |true |Enables or disables smart tag mode. |
|MaxTags |Integer |No |10 |Maximum number of tags to generate. Accepted range: `1` – `10`; values exceeding `10` are not permitted. Defaults to `10` if not specified. |
|Language |String |No |English |Language of the generated tags. Accepted values: `"English"` \| `"Chinese"`. Defaults to `"English"` if not specified. |
|ExtraDescription |String |No |custom description |Custom supplementary description to guide tag generation. Maximum 1500 characters. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RunId |String |hb:c5cacd4946bd\*\*\*a5fd9f74159b03ae8 |The execution ID of the media processing task, used to uniquely identify a specific task execution instance. |

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
            "Type": "Vision",
            "Vision": {
                "AnalysisMode": {
                    "SmartTagOption": {
                        "Enable": true,
                        "MaxTags": 3,
                        "Language": "English",
                        "ExtraDescription": "The generated tags are each limited to two words."
                    }
                },
                "Model": {
                    "DoubaoVisionEndpoint": "ep-202412***175335-cg2p7",
                    "AsrAppId": "3500***054",
                    "AsrAppType": "volc.bigasr.sauc.duration",
                    "DoubaoTextEndpoint": "ep-202412***175335-cg2p7"
                },
                "SnapshotParam": {
                    "Resolution": "240p",
                    "Fps": 1
                }
            }
        }
    }
}
```

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

## Retrieve the task result

After the task is submitted, save the returned `RunId`. The system processes the task asynchronously. You can retrieve the result in either of the following ways:

* Call [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) with the `RunId` to query the task status and output.

* Configure [event notifications](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-) and subscribe to [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete) to receive the result when processing finishes.

## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).

## Server SDKs

This API is supported by VOD SDK 2.0. For integration instructions and examples, see [V2.0 SDK introduction and migration guide](https://docs.byteplus.com/docs/byteplus-vod/docs-server-sdk-v2).
