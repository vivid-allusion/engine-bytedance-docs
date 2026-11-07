---
title: "UploadGetMetaComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-uploadgetmetacomplete"
---

The `UploadGetMetaComplete` event notifies you when the metadata extraction for an uploaded file is finished. This reference document describes the structure and parameters of the event callback, including a full JSON example, to help you correctly parse and utilize the metadata in your application.

<span id="69b3b93a"></span>
## Parameter


|Parameter |Type |Required |Description |
|---|---|---|---|
|RequestId |String |Yes |The unique ID of the request. |
|Version |String |Yes |The callback version. |
|EventType |String |Yes |The name of the event. |
|EventTime |String |Yes |The time when the event occurred in UTC. |
|Data |[Data](https://docs.byteplus.com/docs/byteplus-vod/docs-uploadgetmetacomplete#1d45c414) |Yes |The callback content in JSON format. |


<span id="1d45c414"></span>
### **Data**


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Vid |String |Yes |The ID of the video. |
|SpaceName |String |Yes |The name of the space. |
|Code |String |Yes |The error code. `Success` indicates a successful operation. |
|Message |String |Yes |The error message. |
|SourceInfo |[SourceInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-uploadgetmetacomplete#4c1439e4) |Yes |Information about the source file. |
|PosterUri |String |No |The URI of the cover image. |


<span id="4c1439e4"></span>
### SourceInfo


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|StoreUri |String |Yes |The file storage location. |
|Height |Integer |No |The height of the video, measured in pixels. |
|Width |Integer |No |The width of the video, measured in pixels. |
|Duration |Float |No |The duration of the video, measured in seconds. |
|Bitrate |Integer |No |The bitrate of the video, measured in bps. |
|FileName |String |Yes |The file path. |
|Md5 |String |No |The MD5 value of the file. |
|Format |String |No |The video format. |
|Size |Integer |No |The size of the video, measured in bytes. |
|FileType |String |No |The file type (video/audio). |
|VideoStreamMeta |[VideoStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-uploadgetmetacomplete#a3e73ede) |No |The metadata of the video stream. |
|AudioStreamMeta |[AudioStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-uploadgetmetacomplete#da719d62) |No |The metadata of the audio stream. |


<span id="a3e73ede"></span>
### VideoStreamMeta


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Height |Integer |No |The height of the video, measured in pixels. |
|Width |Integer |No |The width of the video, measured in pixels. |
|Duration |Float |No |The duration of the video, measured in seconds. |
|Bitrate |Integer |No |The bitrate of the video, measured in bps. |
|Codec |String |No |The video codec format. |
|Fps |Float |No |The frame rate of the video, measured in FPS. |
|Definition |String |No |The resolution of the video. |


<span id="da719d62"></span>
### AudioStreamMeta


|**Parameter** |**Type** |**Required** |**Description** |
|---|---|---|---|
|Bitrate |Integer |No |The bitrate of the audio, measured in bps. |
|Duration |Float |No |The duration of the audio, measured in seconds. |
|SampleRate |Integer |No |The audio sample rate. |
|Channels |int32 |No |The number of audio channels. |


<span id="ac862dc5"></span>
## **Example**

```JSON
{
    "RequestId":"021669647428538fdbdd***100090225024000705fdf32",
    "Version":"1.0",
    "EventTime":"2022-11-28T14:57:52Z",
    "EventType":"UploadGetMetaComplete",
    "Data":{
        "Code":"Success",
        "Message":"Upload Video Success",
        "Vid":"v0cca4g7007a***7uecgavoirg",
        "SpaceName": "0106test123",
        "SourceInfo":{
            "Md5":"8c1a25f11f6***cbec198d8974",
            "FileType":"video",
            "Height":1080,
            "Width":1920,
            "Format":"MP4",
            "Duration":256.46933,
            "Size":330042590,
            "StoreUri":"tos-vo**5e1acdfe042daa72598a6376a812d",
             "FileName":"16f439d73e***906a603f587749e1",
            "Bitrate":10294956,
            "VideoStreamMeta":{
                "Codec":"h264",
                "Definition":"unknown",
                "Fps":30.3,
                "Height":1080,
                "Width":1920,
                "Duration":256.46933,
                "Bitrate":10294956
            },
            "AudioStreamMeta":{
                "Duration":256.42,
                "SampleRate":48000,
                "Bitrate":317375,
                "Channels":4
            }
        },
        "PosterUri":"tos-vod-***o0dE3XDIhVz1wm9fmIABCxzXOkZBIlBqE5GSN8"
    }
}
```
