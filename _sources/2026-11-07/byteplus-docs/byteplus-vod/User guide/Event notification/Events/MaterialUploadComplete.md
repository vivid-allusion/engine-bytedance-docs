---
title: "MaterialUploadComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-materialuploadcomplete"
---

The `MaterialUploadComplete` event is triggered when the upload of a material file is completed. This article provides a description of the event parameters and includes examples of the `MaterialUploadComplete` event.

## Parameter

|Parameter |Type |Example |Description |
|---|---|---|---|
|RequestId |String |`202405060***0CF1866` |The unique ID of the request |
|Version |String |`1.0` |The callback version |
|EventType |String |`FileUploadComplete` |The name of the event |
|EventTime |String |`2024-05-06T09:49:33Z` |The time when the event occurred in UTC |
|Data |Data |`-` |The callback content in JSON format |

### **Data**

|**Parameter** |**Type** |**Description** |
|---|---|---|
|Mid |String |The unique ID of the material file |
|SpaceName |String |The name of the space |
|CallbackArgs |String |Pass\-through information. If you set the `CallbackArgs` parameter during upload, the custom data will be returned in the event. |
|PosterUri |String |The video cover image URI. This parameter is returned only if you set a video cover during upload. For details, see [Video covers](https://docs.byteplus.com/docs/byteplus-vod/docs-video-cover). |
|SourceInfo |[SourceInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-materialuploadcomplete#6f5bd774) |Information about the material file if it is an audio or video file |

### **SourceInfo**

|**Parameter** |**Type** |**Description** |
|---|---|---|
|StoreUri |String |The file storage location |
|Height |Integer |The height of the video or image |
|Width |Integer |The width of the video or image |
|Duration |Float |The duration of the audio or video |
|Bitrate |Integer |The bitrate of the audio or video |
|Md5 |String |The MD5 value of the file |
|Format |String |The format of the audio or video |
|Size |Integer |The size of the file |
|FileName |String |The name of the file |

## **Example**

Below is an example of the event that is triggered when the upload of an MP4 file is completed:

```JSON
{
    "RequestId":"202104201631470102251070341F001***",
    "Version":"1.0",
    "EventType":"MaterialUploadComplete",
    "EventTime":"2021-04-20T08:31:48Z",
    "Data":{
        "CallbackArgs":"my callback",
        "Code":"Success",
        "Message":"Upload Video Success",
        "Mid":"v0c255g7007ac1v92s2l39gm9iobo***",
        "PosterUri":"tos-path-v-da1******88b54472984b86102ee732***",
        "SourceInfo":{
            "Bitrate":10021186,
            "Duration":39.68,
            "FileType":"video",
            "Format":"MP4",
            "Height":720,
            "Md5":"56c27acc22177facb342dd0477307***",
            "Size":49705086,
            "StoreUri":"tos-path-v-da1******b8df4a8eb8cf1297ecdec***",
            "FileName": "e4c13e55058***94b1e74c8616",
            "Width":1280
        },
        "SpaceName":"james-test"
    }
}
```

Below is an example of the event that is triggered when the upload of an image is completed:

```JSON
{
    "RequestId":"202104201647260102251070340E002***",
    "Version":"1.0",
    "EventType":"MaterialUploadComplete",
    "EventTime":"2021-04-20T08:47:26Z",
    "Data":{
        "CallbackArgs":"",
        "Code":"Success",
        "Message":"Upload Image Success",
        "Mid":"i00c1xti37eoc1v9a7mhkgmncko9s***",
        "PosterUri":"",
        "SourceInfo":{
            "Height":1280,
            "Md5":"e521c9e25296f10fd3ac996cfe93****",
            "StoreUri":"tos-path-v-da1421/6017f40ca39c4680902333c8d5e6a***",
            "FileName": "e4c13e55058***94b1e74c8616",
            "Width":720
        },
        "SpaceName":"james-test"
    }
}
```

Below is an example of the event that is triggered when the upload of a caption file is completed:

```JSON
{
    "RequestId":"2021042016463201022510703427001***",
    "Version":"1.0",
    "EventType":"MaterialUploadComplete",
    "EventTime":"2021-04-20T08:46:32Z",
    "Data":{
        "CallbackArgs":"",
        "Code":"Success",
        "Message":"Upload Object Success",
        "Mid":"f00c1r5f82ofc1v99q6hkgmncko9s***",
        "PosterUri":"",
        "SourceInfo":{
            "Md5":"5cede5d5ef20c351873bc0273da1****",
            "StoreUri":"tos-path-v-da1421/6238ee765d2f4bb8a0f4a03e01902***",
            "FileName": "e4c13e55058***94b1e74c8616"
        },
        "SpaceName":"james-test"
    }
}
```
