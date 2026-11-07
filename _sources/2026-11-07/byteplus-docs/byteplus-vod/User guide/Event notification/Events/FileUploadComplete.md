---
title: "FileUploadComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadcomplete"
---

This article provides a description of the event parameters and includes examples of the `FileUploadComplete` event.

## Event description

After configuring the `FileUploadComplete` event notification, you will receive a notification when the media upload is complete. To set up an event notification, see [Callbacks](https://docs.byteplus.com/docs/byteplus-vod/docs-system#aed0518b). Related API: [CommitUploadInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-commituploadinfo)

## Parameter

|Parameter |Type |Required |Description |
|---|---|---|---|
|RequestId |String |Yes |The unique ID of the request |
|Version |String |Yes |The callback version |
|EventType |String |Yes |The name of the event |
|EventTime |String |Yes |The time when the event occurred in UTC |
|Data |[Data](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete#f3f2a64e) |Yes |The callback content in JSON format |

### **Data**

|Parameter |Type |Required |Description |
|---|---|---|---|
|Code |String |Yes |The status code |
|Message |String |Yes |The message |
|Vid |String |Yes |The video ID |
|OptionInfo |[OptionInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete#733fccca) |No |The media information. |
|SpaceName |String |Yes |The VOD space name |
|SourceInfo |[SourceInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete#1c6393a1) |Yes |Information about the source video |
|CallbackArgs |String |No |Pass\-through information. This parameter is returned only if you set the `CallbackArgs` parameter during upload. |
|PosterUri |String |No |The video cover image URI. This parameter is returned only if you set a video cover during upload. For details, see [Video covers](https://docs.byteplus.com/docs/byteplus-vod/docs-video-cover). This parameter may be empty if the system fails to generate the video cover. |

### OptionInfo

The media information

|Parameter |Type |Required |Description |
|---|---|---|---|
|TemplateId |String |No |The workflow ID. The parameter is returned only if you specify a workflow ID when uploading audio and video files to trigger media processing tasks. |

### **SourceInfo**

Information about the source video

> **Warning**

> The full metadata may not always be returned upon completion of the media asset upload. In cases where metadata retrieval is incomplete or unsuccessful, all the following parameters except for `StoreUri` and `FileName` may be left empty.

|Parameter |Type |Required |Description |
|---|---|---|---|
|AudioStreamMeta |[AudioStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete#c4fe010f) |No |Audio stream metadata |
|VideoStreamMeta |[VideoStreamMeta](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadcomplete#c73795fd) |No |Video stream metadata |
|StoreUri |String |Yes |The file storage location |
|Height |Integer |No |The height of the video in pixels |
|Width |Integer |No |The width of the video in pixels |
|Duration |Float |No |The duration of the video in seconds |
|Bitrate |Integer |No |The bitrate of the video in bps |
|Md5 |String |No |The MD5 value of the file |
|Format |String |No |The file format |
|Size |Integer |No |The file size in bytes |
|FileName |String |Yes |The file path |

### AudioStreamMeta

Audio stream metadata

|Parameter |Type |Required |Description |
|---|---|---|---|
|Bitrate |Integer |No |The audio bitrate in bps |
|Duration |Float |No |The audio duration in seconds |
|SampleRate |Integer |No |The audio sample rate |

### VideoStreamMeta

Video stream metadata

|Parameter |Type |Required |Description |
|---|---|---|---|
|Bitrate |Integer |No |The video bitrate in bps |
|Codec |String |No |The video codec |
|Definition |String |No |The video resolution |
|Duration |Float |No |The video duration in seconds |
|Fps |Float |No |The video frame rate in fps |
|Height |Integer |No |The video height in pixels |
|Width |Integer |No |The video width in pixels |

## **Example**

```JSON
{
    "EventType": "FileUploadComplete", 
    "EventTime": "2023-03-09T06:54:09Z", 
    "RequestId": "20230309145***2AB872171C3F4E", 
    "Version": "1.0"
    "Data": {
        "Code": "Success", 
        "Message": "Upload Video Success", 
        "OptionInfo": {
            "TemplateId": "abf6274b6b594***d1ebfa5cb009041"
        }, 
        "SourceInfo": {
            "AudioStreamMeta": {
                "Bitrate": 64091, 
                "Duration": 60.138004, 
                "SampleRate": 44100
            }, 
            "Bitrate": 552396, 
            "Duration": 60.185, 
            "FileName": "12345.mp4", 
            "FileType": "video", 
            "Format": "MP4", 
            "Height": 360, 
            "Size": 4155745, 
            "StoreUri": "abc2/12345.mp4", 
            "VideoStreamMeta": {
                "Bitrate": 552396, 
                "Codec": "h264", 
                "Definition": "unknown", 
                "Duration": 60.185, 
                "Fps": 24, 
                "Height": 360, 
                "Width": 640
            }, 
            "Width": 640
        }, 
        "SpaceName": "0106test123", 
        "Vid": "v037a3g1000***3relauaatb8u8j0"
    }, 

}
```
