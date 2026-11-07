---
title: "MediaUnderstand"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-mediaunderstand"
---

Call `MediaUnderstand` to submit an asynchronous media understanding task. You can specify a video or audio file by its Vid or by its space and file path, select preprocessing options, and provide a prompt for a ModelArk model.

Before calling this API, enable the required model services and authorize BytePlus VOD to access them. For instructions, see [Intelligent video understanding](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#prerequisites).

## HTTP request

```http
POST https://vod.byteplusapi.com?Action=MediaUnderstand&Version=2026-08-01
```

## Request parameters

Include the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure), including the authentication information.

### Query

|Parameter |Data type |Required |Value |
|---|---|---|---|
|Action |String |Yes |`MediaUnderstand` |
|Version |String |Yes |`2026-08-01` |

### Body

Pass the following objects in a JSON request body.

|Parameter |Data type |Description |
|---|---|---|
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/123453#input) |Video or audio file to process. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/123453#operation) |Prompt, model, and preprocessing configuration. |
|Control |Object of [Control](https://docs.byteplus.com/en/docs/25/123453#control) |Optional request control parameters. |

### Input

|Parameter |Data type |Required |Description |
|---|---|---|---|
|Type |String |Yes |Input type: `Vid` or `DirectUrl`. |
|Vid |String |Conditional |Media asset ID. Required when `Type` is `Vid`. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/123453#directurl) |Conditional |Required when `Type` is `DirectUrl`. |

### DirectUrl

`DirectUrl` identifies a file in a VOD space by its file path. It does not accept an external HTTP URL.

|Parameter |Data type |Required |Description |
|---|---|---|---|
|SpaceName |String |Yes |Space containing the media file. |
|FileName |String |Yes |File path in the space. |
|BucketName |String |No |Storage bucket name. If omitted, the bucket bound to the space is used. |

### Operation

|Parameter |Data type |Required |Description |
|---|---|---|---|
|Prompt |String |Yes |Non\-empty instructions for the model, encoded in UTF\-8. |
|Model |Object of [Model](https://docs.byteplus.com/en/docs/25/123453#model) |Yes |Model configuration. |
|Segment |Object of [Segment](https://docs.byteplus.com/en/docs/25/123453#segment) |No |Time range to analyze. |
|OcrParam |Object |No |Set `Enable` (Boolean) to enable or disable text recognition from video frames. OCR does not support videos longer than 10 minutes. |
|AsrParam |Object |No |Set `Enable` (Boolean) to enable or disable speech transcription. Speaker identification through `NeedSpeaker=true` is not supported by BytePlus. |
|SmartVideoClipParam |Object |No |Set `Enable` (Boolean) to enable or disable scene segmentation. This supplies scene time ranges for understanding; it does not generate separate scene video files. |
|AudioExtractParam |Object |No |Set `Enable` (Boolean) to request voice and background audio separation. This option takes effect only when ASR is enabled. The voice track is used for transcription. |
|SnapshotParam |Object of [SnapshotParam](https://docs.byteplus.com/en/docs/25/123453#snapshotparam) |No |Snapshot configuration for visual analysis. Omitting this object does not disable snapshots for VLM processing. |

### Model

|Parameter |Data type |Required |Description |
|---|---|---|---|
|ModelType |String |Yes |`VLM` for a vision\-language model, or `LLM` for a language model. VLM uses video and preprocessing context; LLM uses text context from preprocessing. |
|DoubaoEndpoint |String |Yes |ModelArk inference endpoint ID. |
|SpeechAppId |String |Conditional |Seed Speech application ID. Required when `AsrParam.Enable` is `true`. |
|SpeechAppType |String |Conditional |Required when `AsrParam.Enable` is `true`. BytePlus supports `volc.bigasr.sauc.duration` (ASR 1.0) and `volc.seedasr.sauc.duration` (ASR 2.0). Concurrency\-based types and `volc.bigasr.auc_turbo` are not supported. |

For `ModelType=LLM`, provide semantic text context through ASR or OCR.

For audio\-only input, use `ModelType=LLM` with ASR enabled and provide the corresponding speech application parameters. Disable OCR and omit `SnapshotParam`.

### Segment

|Parameter |Data type |Required |Description |
|---|---|---|---|
|Start |Double |No |Start time in seconds. If omitted, processing starts at the beginning of the video. |
|End |Double |No |End time in seconds. If omitted, processing continues to the end of the video. When specified, it must be greater than `Start`. |

### SnapshotParam

|Parameter |Data type |Required |Description |
|---|---|---|---|
|Resolution |String |No |Snapshot resolution: `240p`, `360p`, `480p`, `720p`, or `1080p`. |
|Fps |Double |No |Frames captured per second. Range: `0.01` to `10`. |
|Area |Object of [Area](https://docs.byteplus.com/en/docs/25/123453#area) |No |Region of each frame to capture. |

### Area

Coordinates are expressed as ratios of the video width or height, from `0` to `1`. `TopLeftX` must not exceed `BottomRightX`, and `TopLeftY` must not exceed `BottomRightY`.

|Parameter |Data type |Description |
|---|---|---|
|TopLeftX |Double |Horizontal position of the upper\-left corner. |
|TopLeftY |Double |Vertical position of the upper\-left corner. |
|BottomRightX |Double |Horizontal position of the lower\-right corner. |
|BottomRightY |Double |Vertical position of the lower\-right corner. |

### Control

|Parameter |Data type |Required |Description |
|---|---|---|---|
|ClientToken |String |No |Client\-provided idempotency token. Uses the same semantics as `StartExecution.Control.ClientToken`. |
|CallbackArgs |String |No |Custom data passed through in the task callback. Uses the same semantics as `StartExecution.Control.CallbackArgs`. |

For control parameter limits, see [RuntimeControl](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution#runtimecontrol).

## Response parameters

|Parameter |Data type |Description |
|---|---|---|
|RunId |String |Task execution ID. Use this value to query the task status and output with [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution). |

## Samples

### Sample request

The following example analyzes the first 60 seconds of a video using visual input and ASR transcription. Replace the video ID, endpoint ID, and application ID with your own values.

```json
{
  "Input": {
    "Type": "Vid",
    "Vid": "your-video-id"
  },
  "Operation": {
    "Prompt": "Summarize the main events in this video.",
    "Model": {
      "ModelType": "VLM",
      "DoubaoEndpoint": "your-endpoint-id",
      "SpeechAppId": "your-speech-app-id",
      "SpeechAppType": "volc.seedasr.sauc.duration"
    },
    "Segment": {
      "Start": 0,
      "End": 60
    },
    "AsrParam": {
      "Enable": true
    },
    "SnapshotParam": {
      "Resolution": "720p",
      "Fps": 1
    }
  }
}
```

To use a file path, replace `Input` with the following:

```json
{
  "Type": "DirectUrl",
  "DirectUrl": {
    "SpaceName": "your-space",
    "FileName": "videos/input.mp4"
  }
}
```

### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "your-request-id",
    "Action": "MediaUnderstand",
    "Version": "2026-08-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "RunId": "your-run-id"
  }
}
```

## Retrieve the result

Save the returned `RunId` and call [GetExecution](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution) with version `2025-07-01` to check the task status and retrieve its output. A successful submission means the task was accepted; it does not mean processing has completed.

For tasks submitted with this API, `Result.Output.Type` is `Task`, and `Result.Output.Task.Type` is `VideoUnderstand`. Read the generated text from `Result.Output.Task.VideoUnderstand.Content`. The same object includes `Duration`, `SnapshotsNumber`, and `Model` usage information. For field types, see [OutputTaskVideoUnderstand](https://docs.byteplus.com/docs/byteplus-vod/reference-getexecution#outputtaskvideounderstand).

Check both the task status and the returned content. `Status=Success` can be returned with an empty `Content` string, so a successful status alone does not guarantee a usable understanding result.

Custom prompts can produce results that are visible in the task output but are not saved as structured media asset information. To save structured results, the prompt must preserve the output schema required by VOD. See [Configure prompts](https://docs.byteplus.com/docs/byteplus-vod/docs-ai-media-understanding#configure-prompts).

## Parameter validation

Invalid requests return `ResponseMetadata.Error` with code `InvalidParameter` and do not return a `RunId`. Check the error message and correct the request before retrying.

|Parameter |Validation |
|---|---|
|`Input.Type` |Must be `Vid` or `DirectUrl`. |
|`Operation.Prompt` |Must not be empty. |
|`Operation.Model.ModelType` |Must be `LLM` or `VLM`. |
|`Operation.Segment.End` |Must be greater than `Start` when specified. |
|`OcrParam`, `AsrParam`, `SmartVideoClipParam`, `AudioExtractParam` |Must be JSON objects, with Boolean values for `Enable`. |
|`Operation.SnapshotParam.Resolution` |Must be one of the supported resolution values. |
|`Operation.SnapshotParam.Fps` |Must be between `0.01` and `10`, inclusive. |
|`Operation.SnapshotParam.Area` |The top\-left coordinates must not exceed the corresponding bottom\-right coordinates. |
