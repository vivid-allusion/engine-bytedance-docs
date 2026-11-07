---
title: "GetVideoPlayInfo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-getvideoplayinfo"
---

Call `GetVideoPlayInfo` to get the playback and media information of a video by its `Vid`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **GET**

* Endpoint: `https://vod.byteplusapi.com?Action=GetVideoPlayInfo&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`GetVideoPlayInfo` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |
|`Vid` |String |Yes |`v03819g100xxxxxxxx` |Video ID. |
|`Space` |String |Yes |`your-space` |Name of the VOD space that contains the video. |
|`OutputType` |String |No |`CDN` |Playback URL output type. |
|`DataType` |Integer |No |`0` |Video data type. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`VideoDetail` |[VideoDetail](https://docs.byteplus.com/en/docs/25/118532#videodetail) |Video information. |
|`BaseResp` |Object |Downstream status information. A `StatusCode` of `0` indicates success. |


<span id="videodetail"></span>
### VideoDetail


|Parameter |Data type |Description |
|---|---|---|
|`SpaceName` |String |Name of the VOD space. |
|`Vid` |String |Video ID. |
|`VidBucketType` |Integer |Storage bucket type. |
|`VideoDetailInfo` |[VideoDetailInfo](https://docs.byteplus.com/en/docs/25/118532#videodetailinfo) |Basic video and playback information. |
|`OriginalVideoInfo` |Object |Original\-file information, including format, codec, dimensions, duration, bitrate, file size, playback information, and audio\-stream metadata. |
|`EncodedVideoInfos` |Array of Object |Transcoded video information. |
|`LogoEncodedVideoInfos` |Array of Object |Watermarked transcoded video information. |
|`AbrMasterFileInfos` |Array of Object |Adaptive\-bitrate master file information. |


<span id="videodetailinfo"></span>
### VideoDetailInfo


|Parameter |Data type |Description |
|---|---|---|
|`Title` |String |Video title. |
|`Vid` |String |Video ID. |
|`Filename` |String |File name. |
|`PublishStatus` |String |Publishing status, such as `Published` or `Unpublished`. |
|`Duration` |Float |Duration in seconds. |
|`Codec` |String |Video codec. |
|`Height` |Integer |Video height in pixels. |
|`Width` |Integer |Video width in pixels. |
|`Format` |String |Container format. |
|`Size` |Integer |File size in bytes. |
|`Bitrate` |Integer |Bitrate in bit/s. |
|`PosterUrl` |String |Poster URL. |
|`PlayInfo.MainPlayUrl` |String |Primary playback URL. This URL is valid when `PlayInfo.Status` is `2`. |
|`PlayInfo.BackupPlayUrl` |String |Backup playback URL. |
|`PlayInfo.Status` |Integer |Playback URL status. `2` indicates that the URL is available. |
|`CreatedTime` |String |Video creation time. |
|`UpdatedTime` |String |Video update time. |
|`Classification` |Object |VOD category information. |
|`TosStorageClass` |String |Storage class. |
|`DynamicRange` |String |Dynamic range, such as `SDR` or `HDR`. |
|`FileType` |String |File type. |
|`StoreUri` |String |Storage URI. |
|`VodUploadSource` |String |Upload source. |
|`BlockStatus` |String |Blocking status. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
GET https://vod.byteplusapi.com?Action=GetVideoPlayInfo&Version=2025-01-01&DataType=0&OutputType=CDN&Space=your-space&Vid=v03819g100xxxxxxxx
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "GetVideoPlayInfo",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "VideoDetail": {
      "SpaceName": "your-space",
      "Vid": "v03819g100xxxxxxxx",
      "VideoDetailInfo": {
        "Title": "Opening clip.mp4",
        "Vid": "v03819g100xxxxxxxx",
        "PublishStatus": "Published",
        "Duration": 117.92,
        "Codec": "h264",
        "Height": 1920,
        "Width": 1080,
        "Format": "MP4",
        "PosterUrl": "https://example.com/poster.jpeg",
        "PlayInfo": {
          "MainPlayUrl": "https://example.com/video.mp4",
          "BackupPlayUrl": "",
          "Status": 2
        }
      }
    },
    "BaseResp": {
      "StatusCode": 0,
      "StatusMessage": "success",
      "Extra": null
    }
  }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
