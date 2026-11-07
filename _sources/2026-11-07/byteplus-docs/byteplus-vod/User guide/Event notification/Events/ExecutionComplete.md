---
title: "ExecutionComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-executioncomplete"
---

This article provides a description of the event parameters and includes examples of the `ExecutionComplete` event.

> **Warning**

> If a processed video file is in an unsupported format, the task callback will not return the corresponding parameters.

# Event description

After configuring the `ExecutionComplete` event notification, you will receive a notification when the media processing task is complete. For configuration details, please refer to [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-). Related APIs: [StartExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution), [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand), and [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution#operationtask).

# Parameter

|**Parameter** |**Data Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|RequestId |String |`202405060***0CF1866` |Yes |The unique ID for the request. |
|Version |String |`1.0` |Yes |The callback version. |
|EventType |String |`ExecutionComplete` |Yes |The name of the event. |
|EventTime |String |`2024-05-06T09:49:33Z` |Yes |The UTC time when the event occurred, accurate to the second. |
|Data |[Data](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#17a91934) |`-` |Yes |The callback content in JSON format. |

## Data

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RunId |String |`lb:75d9a9d137***1f3262fd` |The unique identifier for the current execution task. |
|Status |String |`Success` |The status of the task execution. Possible values are as follows:<br><br><br>* `Success`: The task has completed successfully.<br><br>* `Failed`: The task failed.<br><br>* `PendingStart`: The task is queued and waiting to start.<br><br>* `Running`: The task is currently being executed.<br><br>* `Terminated`: The task has been terminated. |
|Code |String |`InvalidParameter.InvalidMediaStream` |The error code of the task execution. Possible values are as follows:<br><br><br>* `InvalidParameter.InvalidMediaStream`: Failed to parse audio and video streams.<br><br>* `InvalidParameter.MissingMediaStream`: Missing audio or video streams.<br><br>* `InvalidParameter.InvalidUriError`: Invalid user URI.<br><br>* `InvalidParameter.MissingSubtitleStream`: Missing subtitle stream.<br><br>* `InvalidParameter.InvalidParam`: Invalid parameter.<br><br>* `InvalidParameter.InvalidVidOrUri`: Input source does not exist.<br><br>* `InternalError`: Internal error.<br><br>* `InternalError.DownloadError`: System download error.<br><br>* `InternalError.UploadError`: System upload error.<br><br>* `InternalError.ExecutionTimeout`: Execution timeout.<br><br><br>> **Note**<br><br><br>> When the `Status` parameter is `Failed`, the `Code` parameter returns the specific error code for the task.<br> |
|Input |Object of [Input](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#a3778131) |`-` |Information about the input file for the media processing task. |
|Meta |Object of [ExecutionMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#680a92bd) |`-` |Metadata for task execution, including timestamps and space details. This field provides context about when and where the task was executed. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#2b33af2c) |`-` |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|SpaceName |String |`test` |The name of the space where the media processing task will be executed. |
|Operation |Object of [Operation](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#e3af2da4) |`-` |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|Output |Object of [Output](https://docs.byteplus.com/en/docs/25/81609#output) |`-` |The output results of the task execution. |

## Input

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`Vid` |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the Vid parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the DirectUrl parameter. |
|Vid |String |`v0dc24***mu6g` |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#bb3b86e9) |`-` |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the the video to a VOD space and obtain the relevant information. |

## DirectUrl

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |The name of the space. You can call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API to obtain information about all spaces under the current account. |
|FileName |String |`example.mp4` |The file path. After uploading audio and video to the Video\-on\-Demand (VOD) service, you can obtain the FileName through the [FileUploadComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete) event. |
|BucketName |String |`tos-cn-v-cd3a11` |The name of the bucket. You can call the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API to obtain the name of the bucket associated with the space. |

## ExecutionMeta

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|SpaceName |String |`test` |The name of the VOD Space where the media processing task will be executed. |
|Trigger |String |`API` |The source of the task. Possible values are as follows:<br><br><br>* `API`: Triggered by an API call. |
|CreateTime |String |`2025-01-13T10:05:54Z` |The creation time of the task in RFC3339 format (UTC+8), accurate to the second. |
|StartTime |String |`2025-01-14T09:13:07Z` |The start time of the task in RFC3339 format (UTC+8), accurate to the second. |
|EndTime |String |`2025-01-14T09:17:35Z` |The end time of the task in RFC3339 format (UTC+8), accurate to the second. |

## RuntimeControl

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|CallbackArgs |String |`Example` |A customizable field. The maximum length of the field is 512 bytes. This parameter is returned only if you set the `CallbackArgs` parameter when submitting the task. |
|Priority |Integer |`1` |Task priority for media processing. The default value is 0. The value range is [\-5, 5], where a higher number indicates higher priority. |
|ClientToken |String |`QqS3o5L4********` |A unique token provided by the client to distinguish different requests, ensuring idempotency. It is case\-sensitive and should not exceed 64 printable ASCII characters. By default, the transcoding service will perform idempotent behavior if the same request is detected. To bypass idempotency (such as when re\-executing the same media processing task with modified configurations), set this parameter. |

## Operation

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`Template` |Processing type. The valid values are as follows:<br><br><br>* `Task`: Single task.<br><br>* `Template`: Single template task. |
|Task |Object of [OperationTask](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#3ed0014c) |`-` |Configuration for the single task. This parameter is required when `Type` is `Task`. |
|Template |Object of [OperationTemplate](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#3df566b0) |`-` |Configuration for the single template task. This parameter is required when `Type` is `Template`. |

## OperationTask

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |Enhance |Task type:<br><br><br>* `Enhance`: Video enhancement task.<br><br>* `Erase`: Precision erasure task.<br><br>* `FaceMosaic`: Face mosaic task.<br><br>* `Vision`: Deprecated intelligent video understanding task. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new tasks.<br><br>* `VideoUnderstand`: Task submitted through `MediaUnderstand`.<br><br>* `Snapshot`: Frame extraction task.<br><br>* `AudioExtract`: Voice and background audio separation task.<br><br>* `Segment`: Scene segmentation task. |
|AudioExtract |Object of [OperationTaskAudioExtract](https://docs.byteplus.com/en/docs/25/81609#operationtaskaudioextract) |`-` |Voice and background audio separation task configuration. This parameter needs to be set when `Type` is `AudioExtract`. |
|Segment |Object of [OperationTaskSegment](https://docs.byteplus.com/en/docs/25/81609#operationtasksegment) |\- |Scene segmentation task configuration. This parameter needs to be set when `Type` is `Segment`. |
|Erase |Object of [OperationTaskErase](https://docs.byteplus.com/en/docs/25/81609#operationtaskerase) |`-` |Precision erasure task configuration. This parameter is required when `Type` is `Erase`. |
|Enhance |Object of [VolcEnhanceTaskParams](https://docs.byteplus.com/en/docs/25/81609#volcenhancetaskparams) |`-` |Video enhancement task configuration. This parameter is required when `Type` is `Enhance`. |
|FaceMosaic |Object of [OperationTaskFaceMosaic](https://docs.byteplus.com/en/docs/25/81609#operationtaskfacemosaic) |`-` |Face mosaic task configuration. This parameter is required when `Type` is `FaceMosaic`. |
|Vision |Object of [OperationTaskVision](https://docs.byteplus.com/en/docs/25/81609#operationtaskvision) |`-` |Deprecated `Vision` configuration, including all nested parameters. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new tasks. |
|VideoUnderstand |Object of [OperationTaskVideoUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand#operation) |\- |Configuration of a task submitted through `MediaUnderstand`. Returned when `Type` is `VideoUnderstand`. |
|Snapshot |Object of [OperationTaskSnapshot](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshot) |`-` |Frame extraction task configuration. This parameter is required when `Type` is `Snapshot`. |

## OperationTaskAudioExtract

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Voice |Boolean |true |Whether to perform the voice and background audio separation task. This parameter must be set to `true`. |
|AudioOption |Object of [OperationTaskAudioExtractAudioOption](https://docs.byteplus.com/en/docs/25/81609#operationtaskaudioextractaudiooption) |\- |The audio output configuration. |

## OperationTaskAudioExtractAudioOption

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Format |String |aac |The output audio format. Valid values: `aac`, `mp3`, `wav`, `m4a`, and `flac`. The default value is `aac`. |

## OperationTaskVision

> **Deprecated task type**

> This structure and its nested fields belong to the deprecated `Vision` task. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new integrations. The definitions below are retained for interpreting existing `Vision` tasks.

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Prompt |String |# Role<br><br>You are an expert in video understanding, proficient in understanding and analyzing videos.<br><br># Task<br><br>The input content is the segmented description text of the video summarized from the popular online video and the transcribed text of the video audio. Please understand the video based on the input content and describe the content of the video in detail.<br><br># Video segmented description text<br><br>{{PLACEHOLDER_VIDEO_CLIP_RESULT}}<br><br># Video audio transcription text<br><br>{{PLACEHOLDER_ASR_RESULT}} |Large model prompt. Use UTF\-8 encoding. The length cannot exceed 30,000 characters. According to the video understanding mode configured in the `Model` parameter, the prompt must contain the corresponding placeholders:<br><br><br>* **VLM + LLM mode**: The following two placeholders must be included.<br><br>   * `{{PLACEHOLDER_ASR_RESULT}}`: Controls whether to enable ASR (Automatic Speech Recognition).<br><br>   * `{{PLACEHOLDER_VIDEO_CLIP_RESULT}}`: Controls whether to perform video slicing.<br><br>* **VLM\-only or LLM\-only mode**: Only the `{{PLACEHOLDER_ASR_RESULT}}`placeholder needs to be included.<br><br><br>> **Warning**<br><br><br>> `Prompt` and `AnalysisMode`are mutually dependent — at least one must be specified. Leaving both empty will result in a request error.<br> |
|Model |Object of [OperationTaskVisionModel](https://docs.byteplus.com/en/docs/25/81609#operationtaskvisionmodel) |`-` |The large model used for video understanding and its working mode. If not configured, the system default model and multimodal understanding (VLM + LLM) mode will be used. You can use this parameter to customize the configuration of the model and the understanding mode for videos. The following three modes are supported:<br><br><br>* **Pure visual understanding (VLM only)**  : Suitable for scenarios where you need to analyze the content of video frames (such as short videos no longer than 10 minutes). Video screenshots will be taken. It is recommended to set the screenshot resolution to 240p to get more screenshots. It is recommended to use models that support a context of 128k or more (such as dola\-seed\-2.0\-pro).<br><br>* **Pure audio understanding (LLM only)**  : Suitable for scenarios where there is no need to understand the content of video frames (such as lecture videos, etc.).<br><br>* **Multimodal understanding (VLM + LLM)**  : Suitable for long \- video understanding (supports a maximum of 2 hours). The long video will be divided into multiple segments. VLM will be used to understand each segment separately, and finally LLM will be used to summarize the understanding results of each segment. |
|Segment |Object of [OperationTaskVisionSegment](https://docs.byteplus.com/en/docs/25/81609#operationtaskvisionsegment) |`-` |Video segmentation understanding configuration. It is used to specify the start and end times of the video understanding task. If Start is not set, it will default to starting from the beginning of the video; if End is not set, it will default to ending at the end of the video. End must be greater than Start. |
|SnapshotParam |Object of [OperationTaskVisionSnapshotParam](https://docs.byteplus.com/en/docs/25/81609#operationtaskvisionsnapshotparam) |`-` |Screenshot strategy configuration. Screenshots will be taken of the video during the video understanding process. The default screenshot strategy is to take a maximum of 50 screenshots at uniform time intervals. If you need to change the screenshot strategy, you can pass in this parameter. |
|ResponseFormatType |String |json_object |Specify the output format of the video understanding results. The supported values are as follows:<br><br><br>* "": The default value, which has no effect. The output format of the large model is specified in the Prompt.<br><br>* json_object: The large model will refer to the JSON format specified in the Prompt and stably output an accurate JSON format. |
|NeedAsrSpeaker |Boolean |true |Whether to include speaker information in the ASR (Automatic Speech Recognition) results for the inference of the large model. The default value is false.<br><br><br>* true: Include speaker information for inference. This takes effect only when AsrAppType is the large model for recording recognition volc.bigasr.auc_turbo.<br><br>* false: Do not include speaker information. |
|AnalysisMode |Object of [OperationTaskVisionAnalysisMode](https://docs.byteplus.com/en/docs/25/81609#operationtaskvisionanalysismode) |`-` |Analysis mode. When AnalysisMode is specified, the system applies a built\-in prompt for the selected mode and ignores any user\-provided prompt. |

## OperationTaskVisionModel

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|DoubaoVisionEndpoint |String |ep\-202412\*\*\*75335\-cg2p7 |The inference access point ID of the Dola VLM (Vision Language Model). For details, please refer to [Enable large models and create inference nodes](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#enable-models).<br><br>> **Warning**<br><br><br>> Either DoubaoVisionEndpoint or DoubaoTextEndpointis required.<br> |
|AsrAppId |String |3500\*\*\*054 |The APP ID of the Automatic Speech Recognition (ASR) product. For details, please refer to [Activate the large model streaming speech recognition service and obtain the APP ID](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#enable-asr). |
|AsrAppType |String |volc.bigasr.sauc.duration |In the speech recognition (ASR) product, the type of the streaming speech recognition large model must be consistent with the service type you have activated. The available values are as follows:<br><br><br>* volc.bigasr.sauc.duration: Hourly version<br><br>* volc.bigasr.sauc.concurrent: Concurrent version |
|DoubaoTextEndpoint |String |ep\-202412\*\*\*75335\-cg2p7 |The inference access point ID of the Dola LLM (Large Language Model). For details, please refer to [Enable large models and create inference nodes](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#enable-models).<br><br>> **Warning**<br><br><br>> Either DoubaoVisionEndpoint or DoubaoTextEndpointis required.<br> |

## OperationTaskVisionSegment

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Start |Double |100 |Start time, in seconds. |
|End |Double |200 |End time, in seconds. |

## OperationTaskVisionSnapshotParam

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Resolution |String |720p |The resolution of the video screenshot has the following values:<br><br><br>* 240p<br><br>* 360p<br><br>* 480p<br><br>* 720p<br><br>* 1080p |
|Fps |Double |1 |The number of frames captured per second. |
|Area |Object of [RatioRectangle](https://docs.byteplus.com/en/docs/25/81609#ratiorectangle) |`-` |Screenshot area configuration. |

## RatioRectangle

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TopLeftX |Double |0 |The offset ratio on the X\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates a full offset (aligned with the right edge of the video). |
|TopLeftY |Double |0 |The offset ratio on the Y\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a complete offset (aligned with the lower edge of the video). |
|BottomRightX |Double |0 |The offset ratio on the X\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates full offset (aligned with the right edge of the video). |
|BottomRightY |Double |0 |The offset ratio on the Y\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a full offset (aligned with the lower edge of the video). |

## OperationTaskVisionAnalysisMode

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|SmartTagOption |Object of [OperationTaskVisionAnalysisModeSmartTagOption](https://docs.byteplus.com/en/docs/25/81609#operationtaskvisionanalysismodesmarttagoption) |\- |Configuration for smart tag mode. |

## OperationTaskVisionAnalysisModeSmartTagOption

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true |Enables or disables smart tag mode. |
|MaxTags |Integer |10 |Maximum number of tags to generate. Accepted range: 1 – 10; values exceeding 10 are not permitted. Defaults to 10 if not specified. |
|Language |String |English |Language of the generated tags. Accepted values: "English" |
|ExtraDescription |String |custom description |Custom supplementary description to guide tag generation. Maximum 1500 characters. |

## OperationTaskSegment

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|NoFile |Boolean |true |Whether to generate clip files:<br><br><br>* `true`: Do not generate clip files.<br><br>* `false`: (Default) Generate clip files. |
|ClipFade |Boolean |true |Whether to output detected fade\-in/fade\-out segments as independent clips.<br><br><br>* `false`: Default. Do not output them independently. Fade\-in/fade\-out segments are treated as part of the surrounding scenes and merged into adjacent clips.<br><br>* `true`: Output them independently. If the video contains obvious fade\-in/fade\-out transitions, the system splits them into independent clips. |
|Threshold |Double |10 |Sensitivity threshold for scene segmentation. The value range is `[0, 100]`.<br><br><br>* The lower the value, the more sensitive the algorithm is to scene changes, resulting in more segments.<br><br>* The higher the value, the more likely the algorithm is to treat small changes as the same scene, resulting in fewer segments.<br><br><br>> **Note**<br><br><br>> When `MinDuration`, `MaxDuration`, and `Threshold` are all set, the system performs segmentation in the following two stages to ensure that all constraints are met:<br><br><br><br>1. > The algorithm first performs segmentation based on the configured `Threshold` and `MinDuration`.<br><br><br>2. > After the first stage is complete, if any clip duration exceeds the configured `MaxDuration`, the system ignores the effect of `Threshold` and performs segmentation again to ensure that the final duration of every clip does not exceed `MaxDuration`.<br> |
|MinDuration |Double |3 |Minimum duration of a single clip, in seconds. No default value. The system ensures that the duration of any final generated clip is not less than this value. |
|MaxDuration |Double |30 |Maximum duration of a single clip, in seconds. No default value. The system ensures that the duration of any final generated clip is not greater than this value. |

## OperationTaskErase

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Mode |String |Auto |Erasure mode. The available values are as follows:<br><br><br>* Auto: Automatic erasure mode. In this mode, the system will enable OCR and perform erasure operations based on the recognition results.<br><br>* Manual: (Beta) Manual erasure mode. In this mode, the system will not enable OCR and will only erase white subtitle content.<br><br><br>tip<br><br>The usage and applicable scenarios of different modes are as follows:<br><br><br>* Generally, you can set Mode to Auto, and then set Auto.Type to Subtitle (subtitles only) or Text (subtitles and other text) to erase the specified type of text.<br><br>* If you have special requirements for the erasure area, you can specify the erasure area by setting Locations to only erase the text recognized by OCR within the area.<br><br>* In scenarios where you need to erase **subtitles in less common languages other than Chinese and English**, you can set Mode to Manual and set Locationsto specify the erasure area. |
|Auto |Object of [OperationTaskEraseAuto](https://docs.byteplus.com/en/docs/25/81609#operationtaskeraseauto) |`-` |Configuration of the auto erasure mode. |
|Manual |Object of [OperationTaskEraseManual](https://docs.byteplus.com/en/docs/25/81609#operationtaskerasemanual) |`-` |Configuration of manual erasure mode. |
|WithEraseInfo |Boolean |true |Whether to return the details of the erased file. |
|EraseOption |Object of [OperationTaskEraseOption](https://docs.byteplus.com/en/docs/25/81609#operationtaskeraseoption) |`-` |Erasure options. It allows you to designate specific time segments for processing or exclusion, providing granular control over the erasure operation. |
|NewVid |Boolean |true |Whether to generate a new Vid for the erased video. |
|VideoOption |Object of [OperationTaskEraseVideoOption](https://docs.byteplus.com/en/docs/25/81609#operationtaskerasevideooption) |`-` |The video encoding settings for the output video after subtitle erasure. |

## OperationTaskEraseAuto

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |Subtitle |Text erasure types:<br><br><br>* Subtitle: Erase text detected as subtitles by OCR.<br><br>* Text: (Beta) Erase subtitles and other texts. |
|Locations |Array of [OperationTaskEraseLocation](https://docs.byteplus.com/en/docs/25/81609#operationtaskeraselocation) |`-` |Array of erasing areas. After adding erasing areas, the system will only erase the text within the areas. |
|SubtitleFilter |Object of [OperationTaskEraseSubtitleFilter](https://docs.byteplus.com/en/docs/25/81609#operationtaskerasesubtitlefilter) |`-` |It is used to specify the height of the erased text and the ratio of the distance from the center of the video width, so as to precisely control the erasing range.<br><br>warning<br><br>It only takes effect when Mode is Auto and Type is Subtitle. |

## OperationTaskEraseLocation

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RatioLocation |Object of [RatioRectangle](https://docs.byteplus.com/en/docs/25/81609#ratiorectangle) |`-` |The information of the erasing area.<br><br>> **Note**<br><br><br>> For details of the parameters of the erasing area, please refer to [Precision erasure](https://docs.byteplus.com/docs/byteplus-vod/docs-precision-subtitle-erasure).<br> |

## RatioRectangle

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TopLeftX |Double |0 |The offset ratio on the X\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates a full offset (aligned with the right edge of the video). |
|TopLeftY |Double |0 |The offset ratio on the Y\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a complete offset (aligned with the lower edge of the video). |
|BottomRightX |Double |0 |The offset ratio on the X\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates full offset (aligned with the right edge of the video). |
|BottomRightY |Double |0 |The offset ratio on the Y\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a full offset (aligned with the lower edge of the video). |

## OperationTaskEraseSubtitleFilter

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|MinTextHeightRatio |Double |0.01 |The minimum ratio of text height, with a default value of 0.01, which means 1% of the video height. |
|MaxTextHeightRatio |Double |0.1 |The maximum ratio of text height. The default value is 0.1, which means 10% of the video height. |
|RectangleCenterOffsetRatio |Double |0.1 |The ratio of the center of the text area deviating from the center of the video width. The default value is 0.08, which means 8%. |

## OperationTaskEraseManual

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Locations |Array of [OperationTaskEraseLocation](https://docs.byteplus.com/en/docs/25/81609#operationtaskeraselocation) |`-` |Array of erasure boxes. After adding erasure boxes, the system will only erase the text within the boxes. |

## OperationTaskEraseOption

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ClipFilter |Object of [OperationTaskEraseOptionClipFilter](https://docs.byteplus.com/en/docs/25/81609#operationtaskeraseoptionclipfilter) |`-` |Video segment filter. It is used to define one or more time segments and specify the operation mode (erase or skip) to be performed on these segments. |

## OperationTaskEraseOptionClipFilter

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Mode |String |Skip |Clip processing mode. It determines how to handle the time segments defined in the Clips array.<br><br><br>* Skip: Skip mode. The system will erase the entire video but skip the segment areas specified in the Clips array, leaving their subtitles intact.<br><br>* Selected: Selected mode. The system will only perform subtitle erasure on the segment areas specified in the Clipsarray, and the other parts of the video will remain unchanged. |
|Clips |Array of [OperationTaskEraseOptionClip](https://docs.byteplus.com/en/docs/25/81609#operationtaskeraseoptionclip) |`-` |Array of target time segments. |

## OperationTaskEraseOptionClip

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Start |Double |10 |The start time of the segment, in seconds. |
|End |Double |20 |The end time of the segment, in seconds. |

## OperationTaskEraseVideoOption

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|EncodeMode |String |Size |Encoding mode. The supported values are as follows:<br><br><br>* Quality (Default): Quality\-priority mode. In this mode, the system uses a higher target bitrate for encoding to ensure superior visual quality. This typically results in an output bitrate significantly higher than that of the source file, leading to an increase in file size.<br><br>* Size: Size\-priority mode. This mode attempts to align the output bitrate with the source video's bitrate as closely as possible while maintaining an acceptable level of image quality. |

## VolcEnhanceTaskParams

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`Moe` |Enhancement model type for video enhancement tasks. The default is `Custom`. Supported values are as follows:<br><br><br>* `Custom`: A custom enhancement model where you manually combine one or more independent enhancement operators (such as super\-resolution, frame interpolation) via the `Modules` parameter.<br><br>* `Moe`: (Recommended) A scenario\-based enhancement model where you select a preset template for specific scenarios (such as short dramas, AIGC) via the `MoeEnhance` parameter, and the system automatically applies the optimal operator combination. |
|Modules |Array of [VolcEnhanceParam](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#2c21866e) |`-` |List of custom enhancement operators. This parameter is required when `Type` is set to `Custom`, and is used to configure one or more independent enhancement modules. |
|MoeEnhance |Object of [VolcMoeEnhanceParam](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#987f592f) |`-` |Scenario\-based enhancement configuration for video enhancement tasks. This parameter is required when `Type` is set to `Moe`. It allows selecting a preset template optimized for specific business scenarios to automatically apply the best combination of enhancement operators. |

## VolcEnhanceParam

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`SR` |Custom enhancement operator types. The supported values are as follows:<br><br><br>* `SR`: Intelligent Super\-Resolution<br><br>* `AudioDenoise`: Audio Denoising<br><br>* `SDR2HDR`: SDR to HDR Conversion<br><br>* `VFI`: Intelligent Video Frame Interpolation<br><br>* `SDREnhance`: SDR Enhancement |

## VolcMoeEnhanceParam

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Config |String |`ugc` |Scenario\-based template type for video enhancement tasks. Used to select a preset template optimized for specific business scenarios. The supported values are as follows:<br><br><br>* `common`: General template<br><br>* `ugc`: UGC short videos<br><br>* `short_series`: Short dramas<br><br>* `aigc`: AIGC content<br><br>* `old_film`: Old film restoration |
|Target |Object of [VolcMoeTarget](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#0a7469db) |`-` |Configuration for the output video in the scenario\-based enhancement task. It specifies the resolution, frame rate, and other parameters of the enhanced video. If not provided, the system will maintain the same resolution and frame rate as the source video. |
|VideoStrategy |Object of [VolcVideoStrategyParam](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#ddac0423) |`-` |Video processing strategy for scenario\-based enhancement tasks. It controls the style and intensity of video enhancement. |

## VolcMoeTarget

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Res |String |`1080p` |The target resolution for the enhanced video output. Supported values are as follows:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br>* `6k`<br><br>* `8k` |
|ResLimit |Integer |`1080` |The target width limits. Used to specify the maximum pixel value of the short side of the output video. The value range is `[128, 4320]`. |
|Fps |Float |`30` |The target frame rate for the enhanced video output in the scenario\-based enhancement task, measured in fps. The value range is `(0, 120]`. |
|ScaleRatio |Float |`2.5` |The scaling ratio for the resolution of the output video in the scenario\-based enhancement task. It specifies the multiple by which the resolution should be scaled (range: `[1.1, 10]` with 1 decimal place). For example, if the input video resolution is 480\*240 and this parameter is set to \* `*2*`  *, the output video resolution will be scaled to 960*480. |
|Bitrate |Integer |`2000` |The target bitrate for the output video measured in Kbps. The value range is [10, 50000]. The actual output bitrate will be between 0.8 and 1.5 times the specified target. For more information, see [recommended bitrates for different output resolutions](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template?lang=en#recommended-bitrates-for-different-output-resolutions). |
|BitDepth |Integer |10 |The color bit depth of the output video. It is supported only for the Pro enhancement tier and is returned together with `Codec`. For more information, see [Color depth](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement#color-depth). |
|Codec |String |h265 |The video encoding format of the output video. |
|DynamicRange |String |HLG |The dynamic range of the output video. Supported values: `HLG`. This parameter applies only to the Pro enhancement tier and only when `BitDepth` is `10`, `12`, or `16`. An HDR source video is converted to SDR unless this parameter is `HLG`. |
|PixFmt |String |gbrp16le |The pixel format of the output video. Supported values: `gbrp16le`, which requires `Codec` `ffv1` and `BitDepth` `16`. If you do not set it, the system selects the pixel format automatically. |

## VolcVideoStrategyParam

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|RepairStrength |Integer |0 |The video enhancement intensity for scenario\-based enhancement tasks. Supported values are as follows:<br><br><br>* `-50`: Mild (High Fidelity). Applies minor enhancement while keeping the visual texture close to the source video.<br><br>* `0`: Medium. Provides a balanced image quality enhancement. |
|EnhanceLevel |String |Standard |The video enhancement tier for scenario\-based enhancement tasks. The supported values are as follows:<br><br><br>* `Fast`: Integrates essential upscaling and basic enhancements for a good balance between processing speed and visual clarity.<br><br>* `Standard`: Uses adaptive algorithms to provide a superior balance between visual texture and processing speed. version<br><br>* `Pro`: Powered by large\-model\-driven restoration for cinematic\-grade image quality. This tier requires a longer processing time. |

## OperationTemplate

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`TranscodeVideo` |Single template task type. The valid values are as follows:<br><br><br>* `TranscodeVideo`: Video transcoding template task.<br><br>* `ByteHD`: Low\-bitrate HD template task.<br><br>* `TranscodeAudio`: Audio transcoding template task.<br><br>* `Enhance`: Video enhancement template task. |
|TranscodeVideo |Object of [OperationTemplateTranscodeVideo](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#16e091d2) |`-` |Video transcoding template task configuration. This parameter is returned only when `Type` is `TranscodeVideo`. |
|ByteHD |Object of [OperationTemplateByteHD](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#3c23ed53) |`-` |Low\-bitrate HD template task configuration. This parameter is returned only when `Type` is `ByteHD`. |
|TranscodeAudio |Object of [OperationTemplateTranscodeAudio](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#ed63a22b) |`-` |Audio transcoding template task configuration. This parameter is returned only when `Type` is `TranscodeAudio`. |
|Enhance |Object of [OperationTemplateEnhance](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#2a4d6e8c) |`-` |Video enhancement template task configuration. This parameter is returned only when `Type` is `Enhance`. |

## OperationTemplateTranscodeVideo

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TemplateId |String |`ddc7d66386***6056a` |Video transcoding template ID. You can create and configure a video transcoding template in the BytePlus VOD console, see [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template). |
|WatermarkTemplateId |String |`v0dc24g10***c1cepmu6g` |Watermark template ID. You can create and configure a watermark template in the BytePlus VOD console, see [Watermark and ad insertion template](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template). |

## OperationTemplateByteHD

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TemplateId |String |`ddc66386***6056a` |Low\-bitrate HD template ID. You can create and configure a low\-bitrate HD template in the BytePlus VOD console, see [Low-bitrate HD template](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template). |
|WatermarkTemplateId |String |`v0dc24g10***c1cepmu6g` |Watermark template ID. You can create and configure a watermark template in the BytePlus VOD console, see [Watermark and ad insertion template](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template). |

## OperationTemplateTranscodeAudio

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TemplateId |String |`ddc76386***6056a` |Audio transcoding template ID. You can create and configure an audio transcoding template in the BytePlus VOD console, see [Audio transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template). |

## OperationTemplateEnhance

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TemplateId |String |`ddc7d66386***56a` |Video enhancement template ID. You can create and configure a video enhancement template in the BytePlus VOD console, see [Video enhancement template](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template). |

## OperationTaskFaceMosaic

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Confidence |Float |0.35 |Face detection confidence threshold, range (0.0, 1.0]. Detections below this value are discarded. A higher value means more conservative detection. Defaults to 0.35. |
|Mode |String |mosaic |Masking method: mosaic (pixelated) or blur (Gaussian). Defaults to mosaic. |
|Strength |String |medium |Masking strength: low / medium / high. For mosaic, controls pixel block size. For blur, controls kernel size and number of passes. Defaults to medium. |
|Expand |Float |0.2 |Bounding box expansion ratio, range (0.0, 1.0]. Expands the detected face region outward on each side. A value of 0.2 expands by 20% per side. Defaults to 0.2. |
|UprightOnly |Boolean |false |Whether to process only upright faces. Defaults to false. |

## OperationTaskSnapshot

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Strategy |Object of [OperationTaskSnapshotStrategy](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshotstrategy) |\- |Frame extraction strategy. |
|Target |Object of [OperationTaskSnapshotTarget](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshottarget) |\- |Output target configuration. |
|Mode |String |Files |Output mode:<br><br>• `Files`: (Default) File path mode. Limited to 1,000 outputs.<br><br>• `Index`: Index mode. Information is stored in media assets. |
|IndexOption |Object of [OperationTaskSnapshotIndexOption](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshotindexoption) |\- |Index configuration when `Mode` is `Index`. |

## OperationTaskSnapshotStrategy

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |TimeInterval |Frame extraction type:<br><br>• `TimeInterval`: Extract frames at fixed time intervals.<br><br>• `SpecifiedTime`: Extract frames at specified timestamps.<br><br>• `SpecifiedFrames`: Extract frames at specified frame numbers.<br><br>• `SceneChange`: Extract frames on scene change. |
|TimeInterval |Object of [OperationTaskSnapshotTimeInterval](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshottimeinterval) |\- |Configuration for time interval extraction. Required when `Type` is `TimeInterval`. |
|SpecifiedTime |Object of [OperationTaskSnapshotSpecifiedTime](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshotspecifiedtime) |\- |Configuration for specified timestamp extraction. Required when `Type` is `SpecifiedTime`. |
|SpecifiedFrames |Object of [OperationTaskSnapshotSpecifiedFrames](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshotspecifiedframes) |\- |Configuration for specified frame number extraction. Required when `Type` is `SpecifiedFrames`. |
|SceneChange |Object of [OperationTaskSnapshotSceneChange](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshotscenechange) | |Configuration for scene change extraction. Required when `Type` is `SceneChange`. |

## OperationTaskSnapshotTimeInterval

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Interval |Integer |1000 |Time interval in milliseconds. Must be \> 0. Extraction starts from frame 0. |
|Limit |Integer |10 |Maximum number of frames to extract. Default: no limit. Must be \> 0. When the output is a sprite image, this refers to the number of sub\-images. |

## OperationTaskSnapshotSpecifiedTime

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Times |Array of Integer |[0, 1] |Time offsets in milliseconds. Each value must be ≥ 0. The output index corresponds to the input index. List length: [1, 1000]. |

## OperationTaskSnapshotSpecifiedFrames

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Frames |Array of Integer |[0, \-1] |Frame numbers. Currently, only `0` (first frame) and `-1` (last frame) are supported. |

## OperationTaskSnapshotSceneChange

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Threshold |Float |0.1 |Scene change detection threshold. Range: (0, 1). Recommended value: `0.1`. |
|Limit |Integer |10 |Maximum number of frames to extract. Default: no limit. Must be \> 0. |

## OperationTaskSnapshotTarget

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ScaleLong |Integer |1280 |Long edge of the output image in pixels. Default: auto\-adapt to the source aspect ratio. Range: [0, 4096]. When the output is a sprite image, this refers to the sub\-image width.<br><br>> **Note**<br><br><br><br>* > Upscaling is not supported.<br><br><br>* > If neither `ScaleLong` nor `ScaleShort` is specified, the original dimensions are preserved.<br><br><br>* > If only one of `ScaleLong` or `ScaleShort` is specified, the other dimension is scaled proportionally.<br><br><br>   * > Only `ScaleLong: 40` specified: For a 100×400 video, the result is 10×40.<br><br><br>   * > Only `ScaleShort: 40` specified: For a 100×400 video, the result is 40×160.<br><br><br>* > If both `ScaleLong` and `ScaleShort` are specified, the long edge does not exceed `ScaleLong` and the short edge does not exceed `ScaleShort`.<br><br><br>   * > Both specified as 10×20: For a 100×400 video, the result is 5×20.<br> |
|ScaleShort |Integer |720 |Short edge of the output image in pixels. Default: auto\-adapt to the source aspect ratio. Range: [0, 4096]. When the output is a sprite image, this refers to the sub\-image height. |
|SpriteConfig |Object of [OperationTaskSnapshotSpriteConfig](https://docs.byteplus.com/en/docs/25/81609#operationtasksnapshotspriteconfig) |\- |Sprite image configuration. |

## OperationTaskSnapshotSpriteConfig

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Enable |Boolean |true |Whether to generate a sprite image. Default: `false`. Set to `true` to enable. |
|ImgYLen |Integer |10 |Number of sub\-images along the vertical axis. Effective when `Enable` is `true`. Range: [1, 100]. Default: `10`. The maximum total sprite image dimension is 65,535 pixels; values below 16,384 are recommended. |
|ImgXLen |Integer |10 |Number of sub\-images along the horizontal axis. Effective when `Enable` is `true`. Range: [1, 100]. Default: `10`. The maximum total sprite image dimension is 65,535 pixels; values below 16,384 are recommended. |

## OperationTaskSnapshotIndexOption

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Tag |String |\- |Custom category label. Length: [0, 128]. |

## Output

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`Task` |The type of task output. Supported values are as follows:<br><br><br>* `Task`: Single task output result.<br><br>* `Template`: Single template output result. |
|Task |Object of [OutputTask](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#65fb2ab4) |`-` |Task outputs. |
|Template |Object of [OutputTemplate](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#e4e5b695) |`-` |Template outputs. |

## OutputTask

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |Enhance |The type of the task output. Supported values are as follows:<br><br><br>* `Enhance`: Video enhancement task.<br><br>* `Erase`: Precision erasure task.<br><br>* `FaceMosaic`: Face mosaic task.<br><br>* `Vision`: Deprecated intelligent video understanding task. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new tasks.<br><br>* `VideoUnderstand`: Task submitted through `MediaUnderstand`.<br><br>* `Snapshot`: Frame extraction task.<br><br>* `AudioExtract`: Voice and background audio separation task.<br><br>* `Segment`: Scene segmentation task. |
|AudioExtract |Object of [OutputTaskAudioExtract](https://docs.byteplus.com/en/docs/25/81609#outputtaskaudioextract) |\- |The output results of the voice and background audio separation task. |
|Vision |Object of [OutputTaskVision](https://docs.byteplus.com/en/docs/25/81609#outputtaskvision) |\- |Output of the deprecated `Vision` task. |
|VideoUnderstand |Object of [OutputTaskVideoUnderstand](https://docs.byteplus.com/en/docs/25/81609#outputtaskvideounderstand) |\- |The output of a task submitted through `MediaUnderstand`. Returned when `Type` is `VideoUnderstand`. |
|Segment |Object of [OutputTaskSegment](https://docs.byteplus.com/en/docs/25/81609#outputtasksegment) |\- |The output results of the scene segmentation task. |
|Erase |Object of [OutputTaskErase](https://docs.byteplus.com/en/docs/25/81609#outputtaskerase) |\- |The output results of the precision erasure task. |
|Enhance |Object of [VodTranscodeInfo](https://docs.byteplus.com/en/docs/25/81609#vodtranscodeinfo) |\- |The output results of the video enhancement task, including metadata such as file ID, size, format, duration, and encryption status. It also contains detailed information about the video and audio streams. |
|FaceMosaic |Object of [OutputTaskFaceMosaic](https://docs.byteplus.com/en/docs/25/81609#outputtaskfacemosaic) | |The output results of the face mosaic task. |
|Snapshot |Object of [OutputTaskSnapshot](https://docs.byteplus.com/en/docs/25/81609#outputtasksnapshot) | |The output results of the frame extraction task. |

### OutputTaskAudioExtract

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Duration |Double |21.942858 |The duration of the input file, in seconds. |
|Voice |Object of [MediaFileInfo](https://docs.byteplus.com/en/docs/25/81609#mediafileinfo) |\- |Information about the vocal audio file. |
|Background |Object of [MediaFileInfo](https://docs.byteplus.com/en/docs/25/81609#mediafileinfo) |\- |Information about the background audio file. |

### MediaFileInfo

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Size |String |2519064 |The file size of the output file, in bytes. |
|FileName |String |9c78b9bbb841\*\*\*586252231dadc9422_speech.aac |The file name of the output file. |
|Vid |String |v0299fg\*\*\*4d103gsqljht10tatbreg |The Vid of the output video. |

## OutputTaskVision

> **Deprecated task type**

> This structure and its nested fields belong to the deprecated `Vision` task. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new integrations. The definitions below are retained for interpreting existing `Vision` tasks.

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Duration |Double |820.534 |The video duration, in seconds. |
|SnapshotsNumber |Integer |820 |Number of snapshots extracted from the video. |
|Model |Object of [OutputTaskVisionModelUsage](https://docs.byteplus.com/en/docs/25/81609#outputtaskvisionmodelusage) |`-` |Vision Output |
|Mode |String |video |The intelligent video understanding mode. |
|Content |String | |The result returned by the video understanding task. |

## OutputTaskVisionModelUsage

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|DoubaoInputTokens |Integer |72168 |Number of input tokens consumed by the Dola VLM. |
|DoubaoOutputTokens |Integer |46382 |Number of output tokens generated by the Dola VLM. |
|DoubaoTotalTokens |Integer |118550 |Total number of tokens consumed by the Dola VLM. |
|DoubaoTextInputTokens |Integer |23204 |Number of input tokens consumed by the Dola LLM. |
|DoubaoTextOutputTokens |Integer |278 |Number of output tokens generated by the Dola LLM. |
|DoubaoTextTotalTokens |Integer |23482 |Total number of tokens consumed by the Dola LLM. |

## OutputTaskVideoUnderstand

For tasks submitted through [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand), `Output.Type` is `Task` and `Output.Task.Type` is `VideoUnderstand`. The following fields are returned in `Output.Task.VideoUnderstand`.

|Parameter |Data type |Sample value |Description |
|---|---|---|---|
|Duration |Double |`60.79` |Media duration in seconds. |
|SnapshotsNumber |Integer |`60` |Number of extracted snapshots. |
|Model |Object of [OutputTaskVideoUnderstandModelUsage](https://docs.byteplus.com/en/docs/25/81609#outputtaskvideounderstandmodelusage) |\- |Model token usage. |
|Content |String |`A summary of the video content.` |Generated text. The format depends on the prompt. This string can be empty even when the task status is `Success`; check the content before using the result. |

## OutputTaskVideoUnderstandModelUsage

Token counts in `VideoUnderstand.Model` are returned as strings containing numeric values.

|Parameter |Data type |Sample value |Description |
|---|---|---|---|
|DoubaoInputTokens |String |`"31907"` |Input tokens consumed by the VLM. |
|DoubaoOutputTokens |String |`"1256"` |Output tokens generated by the VLM. |
|DoubaoTotalTokens |String |`"33163"` |Total tokens consumed by the VLM. |
|DoubaoTextInputTokens |String |`"241"` |Input tokens consumed by the LLM. |
|DoubaoTextOutputTokens |String |`"559"` |Output tokens generated by the LLM. |
|DoubaoTextTotalTokens |String |`"800"` |Total tokens consumed by the LLM. |

### OutputTaskSegment

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Duration |Double |10.04 |The duration of the original video, in seconds. |
|Segments |Array of [OutputTaskSegmentItem](https://docs.byteplus.com/en/docs/25/81609#outputtasksegmentitem) |\- |The scene segmentation result. |

### OutputTaskSegmentItem

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Start |Double |0 |The start time of the segment in the original video, in seconds. |
|End |Double |10.04 |The end time of the segment in the original video, in seconds. |
|Frames |Array of Integer |[0, 250] |An array containing the start frame and end frame of the segment. |
|File |Object of [MediaFileInfo](https://docs.byteplus.com/en/docs/25/81609#mediafileinfo) |\- |Segment file information. If `NoFile` is set to `true` in the request, this field is empty. |

## OutputTaskErase

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Duration |Double |5 |The duration of the output video, in seconds. |
|File |Object of [MediaFileInfo](https://docs.byteplus.com/en/docs/25/81609#mediafileinfo) |`-` |The information of the output video. |
|Info |Object of [OutputTaskEraseInfo](https://docs.byteplus.com/en/docs/25/81609#outputtaskeraseinfo) |`-` |Erasure details. Only returned when Erase.WithEraseInfo is set to true during task submission. |

## OutputTaskEraseInfo

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Width |Integer |1920 |The width of the video after erasure, in pixels |
|Height |Integer |1080 |The height of the video after erasure, in pixels |
|Areas |Array of [OutputTaskEraseArea](https://docs.byteplus.com/en/docs/25/81609#outputtaskerasearea) |`-` |Erasure area information. |

## OutputTaskEraseArea

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Start |Double |13.88 |The start time, in seconds. |
|End |Double |15.88 |The end time, in seconds. |
|PixelRectangle |Array of [PixelRectangle](https://docs.byteplus.com/en/docs/25/81609#pixelrectangle) |`-` |The location information of the erasure area. |

## PixelRectangle

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|TopLeftX |Integer |0 |The offset ratio on the X\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates a full offset (aligned with the right edge of the video). |
|TopLeftY |Integer |0 |The offset ratio on the Y\-axis of the upper\-left corner of the selected area relative to the upper\-left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a complete offset (aligned with the lower edge of the video). |
|BottomRightX |Integer |0 |The offset ratio on the X\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the left edge of the video), and 1 indicates full offset (aligned with the right edge of the video). |
|BottomRightY |Integer |0 |The offset ratio on the Y\-axis of the lower right corner of the selected area relative to the upper left corner of the video. The value range is [0, 1], where 0 indicates no offset (aligned with the upper edge of the video), and 1 indicates a full offset (aligned with the lower edge of the video). |

## OutputTaskFaceMosaic

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Duration |Double |12.834 |The duration of the generated video, in seconds. |
|File |Object of [OutputTaskFaceMosaicFile](https://docs.byteplus.com/en/docs/25/81609#outputtaskfacemosaicfile) |`-` |The information of the output video. |
|Fps |Float |30 |The frame rate of the output video. The unit is fps. |
|Width |Integer |1920 |The width of the output video. The unit is pixel. |
|Height |Integer |1080 |The height of the output video. The unit is pixel. |

## OutputTaskFaceMosaicFile

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Size |String |32202259 |The file size, in bytes. |
|FileName |String |output.mp4 |The file name. |
|Vid |String |v186f0g0\*\*\*8d858r8v3ks12i84jms10 |The Vid. |

## OutputTaskSnapshot

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Files |Array of [Files](https://docs.byteplus.com/en/docs/25/81609#files) |\- |List of output file information. |
|Number |Integer |5 |Number of extracted frames.<br><br>If sprite image generation is enabled, this parameter indicates the number of sub\-images in the sprite image. |
|Mode |String |Files |Output mode:<br><br>• `Files`: (Default) File path mode. Limited to 1,000 outputs.<br><br>• `Index`: Index mode. Information is stored in media assets. |
|Index |String |\- |Index ID. |

## Files

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Size |String |2519064 |File size in bytes. |
|FileName |String |9301da082a0a4003b76bd217cbc8e2ee |File path. See [Constructing a file access URL from FileName](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses#manually-constructing-the-url). |

## VodTranscodeInfo

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|FileId |String |`v029c1g10003civ2i5mqib*******` |The ID of the file. |
|Md5 |String |`b9fd116504b***88e59a824878f07a` |The MD5 value of the file. |
|FileType |String |`video` |The file type. Supported values are as follows:<br><br><br>* `video`: Video stream.<br><br>* `audio`: Audio stream. |
|LogoType |String |`aa` |The watermark label that you specified when creating a [watermark template ](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion-template)in the BytePlus VOD console. |
|Encrypt |Boolean |`true` |Indicates whether the output video is encrypted. The supported values are as follows:<br><br><br>* `true`: The video is encrypted.<br><br>* `false`: The video is not encrypted. |
|Format |String |`mp4` |The container format of the file. |
|Duration |Float |`5.1` |The video duration in seconds. |
|Size |Double |`1653067` |The video size, in bytes. |
|StoreUri |String |`tos-vod-cn-**/191fe22a1c4a49************` |The file storage location. |
|VideoStreamMeta |Object of [VodVideoStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#77bb0a17) |`-` |Metadata information about the video stream in the enhanced output of the task. |
|AudioStreamMeta |Object of [VodAudioStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#7f96ed1b) |`-` |Metadata information about the audio stream in the enhanced output of the task. |
|CreateTime |String |`2025-01-23T10:05:54Z` |The creation time of the enhanced video output in the task in RFC3339 format (UTC+8), accurate to the second. |
|DynamicRange |String |`HDR` |The dynamic range of the enhanced video output. Supported values are as follows:<br><br><br>* `HDR`: High Dynamic Range;<br><br>* `SDR`: Standard Dynamic Range. |
|TosStorageClass |String |`STANDARD` |The storage class of the enhanced output file in TOS (BytePlus Object Storage). Supported values are as follows:<br><br><br>* `STANDARD`: Standard storage class;<br><br>* `ARCHIVE`: Archive storage class. |
|EncodedType |String |`default` |The encryption type of the output.<br><br><br>* `default`: Unencrypted stream.<br><br>* `encrypt`: Private encrypted video stream.<br><br>* `audio_encrypt`: Private encrypted audio stream.<br><br>* `drm_encrypt`: Widevine and FairPlay DRM encrypted video stream.<br><br>* `drm_audio_encrypt`: Widevine and FairPlay DRM encrypted audio stream.<br><br>* `drm_encrypt_playready`: PlayReady DRM encrypted video stream.<br><br>* `drm_audio_encrypt_playready`: PlayReady DRM encrypted audio stream. |
|Encryption |Object of [VodTranscodeEncryption](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete#3f58c2d6) |`-` |Encryption information for the enhanced video output. |

## VodVideoStreamMeta

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Codec |String |`h264` |The video encoding format. |
|Height |Integer |`270` |The video height, in pixel. |
|Width |Integer |`480` |The video width, in pixel. |
|Duration |Float |`2.944` |The video duration, in seconds. |
|Definition |String |`720p` |The video resolution. |
|Bitrate |Integer |`284910` |The video bitrate, in bps. |
|Fps |Float |`25` |The video frame rate, measured in fps. |

## VodAudioStreamMeta

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Codec |String |`aac` |The audio encoding format. |
|Duration |Float |`2.943` |The audio duration, measured in seconds. |
|SampleRate |Integer |`44100` |The audio sampling rate, in Hz. |
|Bitrate |Integer |`127658` |The audio bitrate, in bps. |
|Quality |String |`higher` |The audio quality. This parameter is returned only after audio transcoding. The possible values are as follows:<br><br><br>* `medium`: The standard audio quality.<br><br>* `higher`: The high audio quality.<br><br>* `highest`: The music audio quality. |

## VodTranscodeEncryption

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Kid |String |`encryption_key_12345` |The key ID used for encryption of the enhanced video output. This identifier is essential for decrypting the encrypted video content. |

## OutputTemplate

|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Type |String |`TranscodeVideo` |Single template task type. Valid values are as follows:<br><br><br>* `TranscodeVideo`: Video transcoding template task.<br><br>* `ByteHD`: Low\-bitrate HD template task.<br><br>* `TranscodeAudio`: Audio transcoding template task.<br><br>* `Enhance`: Video enhancement template task. |
|TranscodeVideo |Object of [VodTranscodeInfo](https://docs.byteplus.com/en/docs/25/81609#vodtranscodeinfo) |`-` |Video transcoding template task output. This parameter is returned only when `Type` is set to `TranscodeVideo`. |
|ByteHD |Object of [VodTranscodeInfo](https://docs.byteplus.com/en/docs/25/81609#vodtranscodeinfo) |`-` |Low\-bitrate HD template task output. This parameter is returned only when `Type` is set to `ByteHD`. |
|TranscodeAudio |Object of [VodTranscodeInfo](https://docs.byteplus.com/en/docs/25/81609#vodtranscodeinfo) |`-` |Audio transcoding template task output. This parameter is returned only when `Type` is set to `TranscodeAudio`. |
|Enhance |Object of [VodTranscodeInfo](https://docs.byteplus.com/en/docs/25/81609#vodtranscodeinfo) |`-` |Video enhancement template task output. This parameter is returned only when `Type` is set to `Enhance`. |

# Example

```JSON
{
  "Data": {
    "Code": "InternalError",
    "Control": {
      "ClientToken": "a1876*****fc7d5245ddb"
    },
    "Input": {
      "Type": "Vid",
      "Vid": "v00751g0*****b7jrjhg"
    },
    "Meta": {
      "SpaceName": "test",
      "Trigger": "API"
    },
    "Operation": {
      "Template": {
        "Enhance": {
          "TemplateId": "6d7162*****5233d29b"
        },
        "Type": "Enhance"
      },
      "Type": "Template"
    },
    "RunId": "p1:e333*****2e3a97eff0",
    "Status": "Failed"
  },
  "EventTime": "2025-12-05T09:59:46Z",
  "EventType": "ExecutionComplete",
  "RequestId": "20251*****7C5029EC5",
  "Version": "1.0"
}
```
