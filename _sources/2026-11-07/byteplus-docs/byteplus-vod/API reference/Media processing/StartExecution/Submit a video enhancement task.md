---
title: "Submit a video enhancement task"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-startexecution-video-enhancement"
---

Call `StartExecution` to submit an asynchronous video enhancement task. Set `Operation.Type` to `Task` and `Operation.Task.Type` to `Enhance`. For the feature description and usage workflow, see [Video enhancement](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement).

For other task types, see [StartExecution API overview](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution).

This page covers custom and scenario\-based enhancement configured in the request. To reuse a video enhancement template, see [Submit a template task](https://docs.byteplus.com/docs/byteplus-vod/reference-startexecution-template).

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
|Input |Object of [Input](https://docs.byteplus.com/en/docs/25/121893#input) |No |\- |Information about the input file for the media processing task. |
|Control |Object of [RuntimeControl](https://docs.byteplus.com/en/docs/25/121893#runtimecontrol) |No |\- |Configuration for controlling the execution of the media processing task. It includes settings for task priority, idempotency control, and callback handling. |
|Operation |Object of [Operation](https://docs.byteplus.com/en/docs/25/121893#operation) |No |\- |Configuration for the media processing operation. It specifies the type of operation to be performed. |
|SpaceName |String |No |test |The name of the space where the media processing task will be executed. You can obtain the space name by calling the [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace) API or viewing it on the [Spaces](https://console.byteplus.com/vodpaas/region:vodpaas+ap-southeast-1/overview/?) page of the console. |

### Input

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Vid |The type of the input file. The available values are as follows:<br><br><br>* `Vid`: Vid mode. In this mode, you also need to set the `Vid` parameter.<br><br>* `DirectUrl`：DirectUrl mode. In this mode, you also need to set the `DirectUrl` parameter. |
|Vid |String |No |v0ccfeg7007acsg\*\*\*fog65ubr7niqng |The Vid of the video to be processed. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space using any supported method and obtain its Vid. |
|DirectUrl |Object of [DirectUrl](https://docs.byteplus.com/en/docs/25/121893#directurl) |No |\- |Specifies the information of the video to be processed in DirectUrl mode. Before calling this API, you must [upload](https://docs.byteplus.com/docs/byteplus-vod/docs-media-upload-overview) the video to a VOD space and obtain the relevant information. |

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
|Task |Object of [OperationTask](https://docs.byteplus.com/en/docs/25/121893#operationtask) |No |\- |Single task configuration. Required when `Type` is `Task`. |

### OperationTask

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |Yes |Enhance |Set to `Enhance` for a video enhancement task. |
|Enhance |Object of [VolcEnhanceTaskParams](https://docs.byteplus.com/en/docs/25/121893#volcenhancetaskparams) |No |\- |Video enhancement task configuration. Required when `Type` is `Enhance`. |

### VolcEnhanceTaskParams

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |No |Moe |Enhanced model type for video enhancement tasks. The default is `Custom`. Supported values are as follows:<br><br><br>* `Custom`: A custom enhanced model where you manually combine one or more independent enhancement operators (such as super\-resolution, frame interpolation) via the `Modules` parameter.<br><br>* `Moe`: (Recommended) A scenario\-based enhanced model where you select a preset template for specific scenarios (such as short dramas, AIGC) via the `MoeEnhance` parameter, and the system automatically applies the optimal operator combination. |
|Modules |Array of [VolcEnhanceParam](https://docs.byteplus.com/en/docs/25/121893#volcenhanceparam) |No |\- |List of custom enhancement operators. This parameter is required when `Type` is set to `Custom`, and is used to configure one or more independent enhancement modules. |
|MoeEnhance |Object of [VolcMoeEnhanceParam](https://docs.byteplus.com/en/docs/25/121893#volcmoeenhanceparam) |No |\- |Scenario\-based enhancement configuration for video enhancement tasks. This parameter is required when `Type` is set to `Moe`. It allows selecting a preset template optimized for specific business scenarios to automatically apply the best combination of enhancement operators. |

### VolcEnhanceParam

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Type |String |No |SR |Custom enhanced operator types. The supported values are as follows:<br><br><br>* `SR`: Intelligent Super\-Resolution<br><br>* `AudioDenoise`: Audio Denoising<br><br>* `SDR2HDR`: SDR to HDR Conversion<br><br>* `VFI`: Intelligent Video Frame Interpolation<br><br>* `SDREnhance`: SDR Enhancement |

### VolcMoeEnhanceParam

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Config |String |No |ugc |Scenario\-based template type for video enhancement tasks. Used to select a preset template optimized for specific business scenarios. The supported values are as follows:<br><br><br>* `common`: General template<br><br>* `ugc`: UGC short videos<br><br>* `short_series`: Short dramas<br><br>* `aigc`: AIGC content<br><br>* `old_film`: Old film restoration |
|Target |Object of [VolcMoeTarget](https://docs.byteplus.com/en/docs/25/121893#volcmoetarget) |No |\- |Configuration for the output video in the scenario\-based enhancement task. It specifies the resolution, frame rate, and other parameters of the enhanced video. If not provided, the system will maintain the same resolution and frame rate as the source video. |
|VideoStrategy |Object of [VolcVideoStrategyParam](https://docs.byteplus.com/en/docs/25/121893#volcvideostrategyparam) |Yes |\- |Video processing strategy for scenario\-based enhancement tasks. It controls the style and intensity of video enhancement. |

### VolcMoeTarget

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Res |String |No |1080p |The target resolution for the enhanced video output. Supported values are as follows:<br><br><br>* `240p`<br><br>* `360p`<br><br>* `480p`<br><br>* `540p`<br><br>* `720p`<br><br>* `1080p`<br><br>* `2k`<br><br>* `4k`<br><br>* `6k`<br><br>* `8k` |
|ResLimit |Integer |No |1080 |The target width limits. Used to specify the maximum pixel value of the short side of the output video. The value range is `[128, 4320]`. |
|Fps |Float |No |30 |The target frame rate for the enhanced video output in the scenario\-based enhancement task, measured in fps. The value range is `(0, 120]`. |
|DynamicRange |String |No |HLG |The dynamic range of the output video. This parameter is supported only for the Pro enhancement tier, and only when `BitDepth` is `10`, `12`, or `16`. If you omit it, the system determines the dynamic range automatically: an `exr` output uses HDR, and all other outputs use SDR. An HDR source video is converted to SDR unless you set this parameter to `HLG`. Supported values: `HLG` converts the enhanced output to HLG (Hybrid Log\-Gamma) HDR. For more information, see [Dynamic range and SDR to HDR](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement#dynamic-range-and-sdr-to-hdr). |
|ScaleRatio |Float |No |2.5 |The scaling ratio for the resolution of the output video in the scenario\-based enhancement task. It specifies the multiple by which the resolution should be scaled (range: `[1.1, 10]` with 1 decimal place). For example, if the input video resolution is 480\*240 and this parameter is set to `2`, the output video resolution will be scaled to 960\*480. |
|Bitrate |Integer |No |2000 |The target bitrate for the output video measured in Kbps. The value range is [10, 50000]. The actual output bitrate will be between 0.8 and 1.5 times the specified target. This parameter is not supported when `Codec` is `prores`, `ffv1`, or `exr`. For more information, see [recommended bitrates for different output resolutions](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement-template#recommended-bitrates-for-different-output-resolutions). |
|BitDepth |Integer |No |10 |The color bit depth of the output video. This parameter is supported only for the Pro enhancement tier. Supported values: `8`, `10`, `12`, and `16`. The default value is `8`. If you set `BitDepth` without `Codec`, the system uses the default encoding format for that color depth (`8`: `h264`; `10` and `12`: `h265`; `16`: `ffv1`). When this parameter is set to `16`, the input video duration must not exceed 40 seconds. For the encoding formats supported by each color depth, see [Encoding format and color depth combinations](https://docs.byteplus.com/en/docs/25/121893#encoding-format-and-color-depth-combinations). For more information, see [Color depth](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement#color-depth). |
|Codec |String |No |h265 |The video encoding format of the output. This parameter is supported only for the Pro enhancement tier and must be provided together with `BitDepth`. If you omit it, the system uses the default encoding format for the specified `BitDepth`. The output container is determined automatically by `Codec` and `BitDepth`. Supported values:<br><br><br>* `h264`: Supports `BitDepth` `8`. The output container is MP4.<br><br>* `h265`: Supports `BitDepth` `8`, `10`, and `12`. The output container is MP4.<br><br>* `prores`: Supports `BitDepth` `10`. The output container is MOV. Setting `Bitrate` is not supported.<br><br>* `ffv1`: Supports `BitDepth` `16`. The output container is MOV. Setting `Bitrate` is not supported.<br><br>* `exr`: Supports `BitDepth` `16`. The output is an EXR image sequence. Setting `Bitrate` is not supported.<br><br>   For the full mapping, see [Encoding format and color depth combinations](https://docs.byteplus.com/en/docs/25/121893#encoding-format-and-color-depth-combinations). |
|PixFmt |String |No |gbrp16le |The pixel format of the output video. This parameter is supported only for the Pro enhancement tier. If you omit it, the system selects the pixel format automatically. Supported values: `gbrp16le`, which requires `Codec` `ffv1` and `BitDepth` `16`. If the value does not match the selected `Codec` and `BitDepth`, the request fails with `InvalidParameter`. For more information, see [GBR pixel format](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement#gbr-pixel-format). |

**Encoding format and color depth combinations**

`Codec` requires `BitDepth`, but you can set `BitDepth` on its own. When you provide both, they must form one of the combinations in the following table; when you provide only `BitDepth`, the system applies the default `Codec` for that color depth.

|`BitDepth` |Supported `Codec` |Default `Codec` |
|---|---|---|
|`8` |`h264`, `h265` |`h264` |
|`10` |`h265`, `prores` |`h265` |
|`12` |`h265` |`h265` |
|`16` |`ffv1`, `exr` |`ffv1` |

### VolcVideoStrategyParam

|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|RepairStrength |Integer |No |0 |The video enhancement intensity for scenario\-based enhancement tasks. This option is available for the **Standard** and **Pro** tiers, and it is not supported by the **Fast** tier. Supported values are as follows:<br><br><br>* `-50`: Natural version. Applies a softer enhancement while keeping the visual texture close to the source video. This setting can help reduce an oil\-paint\-like appearance in certain scenarios, such as AI\-generated human\-like videos.<br><br>* `0`: (Default) High definition. Applies a sharper enhancement style. |
|EnhanceLevel |String |Yes |Standard |The video enhancement tier for scenario\-based enhancement tasks. The supported values are as follows:<br><br><br>* `Fast`: Integrates essential upscaling and basic enhancements for a good balance between processing speed and visual clarity.<br><br>* `Standard`: Uses adaptive algorithms to provide a superior balance between visual texture and processing speed.<br><br>* `Pro`: Powered by large\-model\-driven restoration for cinematic\-grade image quality. This tier requires a longer processing time. |

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
            "Type": "Enhance",
            "Enhance": {
                "Type": "Moe",
                "MoeEnhance": {
                    "Config": "short_series",
                    "Target": {
                        "Res": "1080p",
                        "Fps": 30
                    },
                    "VideoStrategy": {
                        "RepairStrength": 0,
                        "EnhanceLevel": "Standard"
                    }
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
