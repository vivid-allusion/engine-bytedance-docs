---
title: "StartExecution API overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution"
---

`StartExecution` submits an asynchronous media processing task for a specified file. Choose a task below for the complete request parameters and examples for that feature.

The `Vision` task type and its associated parameters are deprecated. Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for Intelligent video understanding with configurable OCR, ASR, scene segmentation, and custom prompts.

## Notes

* The per\-user QPS limit for this API is 50 requests per second. Requests that exceed this limit are throttled and might affect your services. Plan your request rate accordingly. For more information, see [QPS limits](https://docs.byteplus.com/docs/byteplus-vod/reference-qps-limits-on-api-calls).

* This API currently supports only the Asia Pacific (Johor) region and does not support the Asia Pacific (Singapore) region.

## Submission methods

|Method |Configuration |When to use |
|---|---|---|
|Single task |`Operation.Type = Task` and `Operation.Task` |Configure the processing parameters directly in the request. |
|Single template task |`Operation.Type = Template` and `Operation.Template` |Reuse a media processing template configured in the BytePlus VOD console. |

## Supported tasks

### Single tasks

Set `Operation.Type` to `Task` and use the `Operation.Task.Type` value for the selected feature.

|Feature |`Operation.Task.Type` |API reference |
|---|---|---|
|Precision erasure |`Erase` |[Submit a precision erasure task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-precision-erasure) |
|Intelligent video understanding (deprecated) |`Vision` |[Legacy Vision reference](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-understanding). Use [MediaUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-mediaunderstand) for new integrations. |
|Voice and background audio separation |`AudioExtract` |[Submit a voice and background audio separation task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-audio-separation) |
|Scene segmentation |`Segment` |[Submit a scene segmentation task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-scene-segmentation) |
|Video enhancement |`Enhance` |[Submit a video enhancement task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-video-enhancement) |
|Face mosaic |`FaceMosaic` |[Submit a face mosaic task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-face-mosaic) |
|Frame extraction |`Snapshot` |[Submit a frame extraction task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-frame-extraction) |

### Template tasks

Set `Operation.Type` to `Template` and use the `Operation.Template.Type` value for the selected template.

|Template |`Operation.Template.Type` |API reference |
|---|---|---|
|Video transcoding |`TranscodeVideo` |[Submit a template task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template#operationtemplatetranscodevideo) |
|Low\-bitrate HD |`ByteHD` |[Submit a template task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template#operationtemplatebytehd) |
|Audio transcoding |`TranscodeAudio` |[Submit a template task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template#operationtemplatetranscodeaudio) |
|Video enhancement |`Enhance` |[Submit a template task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template#operationtemplateenhance) |

## HTTP request

* Method: POST

* Endpoint: https://vod.byteplusapi.com?Action=StartExecution&Version=2025\-07\-01

## Retrieve the task result

After the task is submitted, save the returned `RunId`. The system processes the task asynchronously. You can retrieve the result in either of the following ways:

* Call [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) with the `RunId` to query the task status and output.

* Configure [event notifications](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-) and subscribe to [ExecutionComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-executioncomplete) to receive the result when processing finishes.

## Server SDKs

This API is supported by VOD SDK 2.0. For integration instructions and examples, see [V2.0 SDK introduction and migration guide](https://docs.byteplus.com/docs/byteplus-vod/docs-server-sdk-v2).
