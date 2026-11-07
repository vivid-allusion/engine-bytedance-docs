---
title: "ImageProcessComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-imageprocesscomplete"
---

The `ImageProcessComplete` event is sent when an image enhancement or basic image processing task completes. Use `TaskId` to associate the notification with the task returned by [ImageAIProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageaiprocess) or [ImageProcess](https://docs.byteplus.com/docs/byteplus-vod/reference-imageprocess).

For callback configuration and delivery, see [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

## Parameters

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RequestId |String |`ImageProcessComplete:d44f72f76b3372a3****` |The callback request ID. |
|Version |String |`1.0` |The callback version. |
|EventType |String |`ImageProcessComplete` |The event name. |
|EventTime |String |`2026-10-29T06:30:53Z` |The time when the event occurred, in UTC. |
|Data |Object of [Data](https://docs.byteplus.com/en/docs/25/124090#data) |`-` |The callback content. |

## Data

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CallbackArgs |String |`""` |The custom information passed through from the API request. |
|Code |String |`Success` |The result code. `Success` indicates success. |
|Duration |Number |`0` |The duration of the animated image, in seconds. For a static image, the value is 0. |
|FileId |String |`d93c1337cced42139d05e3a572d0c34c` |The image file ID. |
|Format |String |`jpeg` |The image format, such as `jpeg`, `png`, or `webp`. |
|FrameCnt |Number |`1` |The number of frames. For a static image, the value is 1. |
|Height |Number |`1350` |The image height, in pixels. |
|Md5 |String |`e9461142c88731da6f40ab8e6bf4e882` |The MD5 hash of the image file. |
|Message |String |`Success` |The result message. |
|Pid |String |`i186a8gm0018dbhefdqtgd69okvmf9pg` |The image asset ID (Pid). |
|ProcessParameter |String |`{"GenDREnhanceParam":{"Multiple":2.7},"Input":{}}` |The normalized image processing parameters, serialized as a JSON string. |
|ProcessType |String |`AISuperResolution` |The processing type. The super\-resolution example returns `AISuperResolution`. |
|Size |Number |`340698` |The image file size, in bytes. |
|StorageClass |Number |`1` |The numeric storage class code of the output file. |
|StoreUri |String |`tos-vod-bp-mya-v-b4aefc584297584a/<output-file-name>` |The storage URI of the image file. |
|TaskId |String |`d44f72f76b3372a3bf5d6206801f9bfc` |The image processing task ID. |
|Width |Number |`2027` |The image width, in pixels. |

## Example

The following example shows a successful image enhancement task.

The output file name in `StoreUri` is represented by a placeholder.

```json
{
    "Data": {
        "CallbackArgs": "",
        "Code": "Success",
        "Duration": 0,
        "FileId": "d93c1337cced42139d05e3a572d0c34c",
        "Format": "jpeg",
        "FrameCnt": 1,
        "Height": 1350,
        "Md5": "e9461142c88731da6f40ab8e6bf4e882",
        "Message": "Success",
        "Pid": "i186a8gm0018dbhefdqtgd69okvmf9pg",
        "ProcessParameter": "{\"GenDREnhanceParam\":{\"Multiple\":2.7},\"Input\":{}}",
        "ProcessType": "AISuperResolution",
        "Size": 340698,
        "StorageClass": 1,
        "StoreUri": "tos-vod-bp-mya-v-b4aefc584297584a/<output-file-name>",
        "TaskId": "d44f72f76b3372a3bf5d6206801f9bfc",
        "Width": 2027
    },
    "EventTime": "2026-10-29T06:30:53Z",
    "EventType": "ImageProcessComplete",
    "RequestId": "ImageProcessComplete:d44f72f76b3372a3****",
    "Version": "1.0"
}
```
