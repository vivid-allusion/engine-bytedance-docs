---
title: "FileUploadByUrlComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-fileuploadbyurlcomplete"
---

To correctly handle the callback after a URL batch pull upload, you can use this document to understand the `FileUploadByUrlComplete` event. This reference details the complete parameter structure, provides JSON examples for both success and failure cases, and lists relevant error codes, enabling you to effectively parse and process the event data in your application.

## Event description

The `FileUploadByUrlComplete` event is triggered when each upload from a URL is completed during a batch upload. Related API: [UploadMediaByUrl](https://docs.byteplus.com/docs/byteplus-vod/reference-uploadmediabyurl)

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
|Code |String |The error code |
|Message |String |A detailed error message |
|JobId |String |The ID of the job |
|SourceUrl |String |The URL of the source video |
|CallbackArgs |String |Pass\-through information. If you set the `CallbackArgs` parameter during upload, the custom data will be returned in the event. |
|Vid |String |The video ID. This parameter is returned when an audio or video file is uploaded successfully. |
|Mid |String |The material asset ID. This parameter is returned when a material asset is uploaded successfully. |
|SpaceName |String |The VOD space name |
|SourceInfo |[SourceInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadbyurlcomplete#26b927cd) |Information about the source video |
|PosterUri |String |The video cover image URI. This parameter is returned only if you set a video cover during upload. For details, see [Video covers](https://docs.byteplus.com/docs/byteplus-vod/docs-video-cover). |
|OptionInfo |[OptionInfo](https://docs.byteplus.com/docs/byteplus-vod/docs-fileuploadbyurlcomplete#001750f4) |The media information |

### **SourceInfo**

Information about the source video

|**Parameter** |**Type** |**Description** |
|---|---|---|
|StoreUri |String |The file storage location |
|Height |Integer |The video height in pixels |
|Width |Integer |The video width in pixels |
|Duration |Float |The video duration in seconds |
|Bitrate |Integer |The video bitrate in bps |
|Md5 |String |The MD5 value of the video |
|Format |String |The file format |
|Size |Integer |The file size in bytes |
|FileName |String |The file path |

### OptionInfo

The media information

|Parameter |Type |Description |
|---|---|---|
|TemplateId |String |The workflow ID |

## **Example**

### Example of successful audio or video upload

```JSON
{
    "RequestId": "2020072711510***05207114001CC4",
    "Version": "1.0",
    "EventType": "FileUploadByUrlComplete",
    "EventTime": "2020-07-27T11:04:05Z",
    "Data": {
        "Code": "Success",
        "Message": "file upload success",
        "JobId": "f08d26b0e963***9f208c1ca79cfd5d",
        "SourceUrl": "http://xxx.mp4",
        "CallbackArgs": "item id",
        "Vid": "v02af6e500***3pbvh148u6ung0",
        "SpaceName": "ecqc-live",
        "SourceInfo": {
            "StoreUri": "",
            "Md5": "",
            "Width": 544,
            "Height": 960,
            "Duration": 143.98,
            "Bitrate": 0,
            "Format": "mp4",
            "FileName": "e4c13e5505874e***4b1e74c8616",
            "Size": 1024
        },
        "PosterUri": "tos-cn-v-f4fc******505874e58908b94b1e74c8616",
        "OptionInfo": {
            "TemplateId": "abf6274b6b594***d1ebfa5cb009041"
        }
    }
}
```

### Example of successful image material upload

```JSON
{
    "RequestId": "2026063011510***05207114001CC4",
    "Version": "1.0",
    "EventType": "FileUploadByUrlComplete",
    "EventTime": "2026-06-30T11:04:05Z",
    "Data": {
        "Code": "Success",
        "Message": "file upload success",
        "JobId": "f08d26b0e963***9f208c1ca79cfd5d",
        "SourceUrl": "https://example.com/image.png",
        "CallbackArgs": "item id",
        "Vid": "",
        "Mid": "i00c1xti37eoc1v9a7mhkgmncko9s***",
        "SpaceName": "your-space",
        "SourceInfo": {
            "StoreUri": "tos-path-v-da1421/6017f40ca39c4680902333c8d5e6a***",
            "Height": 1280,
            "Width": 720,
            "Md5": "e521c9e25296f10fd3ac996cfe930e01",
            "Format": "png_pipe",
            "FileName": "example.png",
            "Size": 1024
        }
    }
}
```

### Example of failed upload

```JSON
{
    "RequestId":"202206161501***216519620B65717",
    "Version":"1.0",
    "EventTime":"2022-06-16T15:02:08Z",
    "EventType":"FileUploadByUrlComplete",
    "Data":{
        "Code":"DownloadFailed.UrlDownloadFail",
        "Message":"404 Not Found",
        "JobId":"3f91953e99***9e9044ab8eb98bd8",
        "SourceUrl":"https://str****.com/******transcode/202002/18/ooooooooooooooo.mp4",
        "CallbackArgs":"",
        "Vid":"",
        "SpaceName":"vod-v2-test",
        "SourceInfo":{
            "StoreUri":"",
            "Width":0,
            "Height":0,
            "FileName": "e4c13e5505874e***4b1e74c8616",
            "FileType":""
        },
        "PosterUri":"",
        "OptionInfo":{
            "TemplateId":""
        }
    }
}
```

## **Error code**

|**Error code** |**Description** |
|---|---|
|Success |The upload was successful. |
|InvalidParameter.InvalidParam |An invalid input parameter was provided, such as a URL that does not start with "http" or passing a random string. |
|DownloadFailed.UrlDownloadFail |There was an error while downloading the video. This could be due to the resource not existing, issues with the service providing the resource, or a network error. |
|CheckError.Md5MissMatch |The MD5 value provided as an input parameter does not match the file's actual MD5 value. |
|UploadFailed.UrlUploadFailed |An error occurred during the upload process. This is typically caused by a backend exception. |
|InternalError.UrlUploadError |There was an internal server error during the upload process, usually due to a dependency service exception. |
