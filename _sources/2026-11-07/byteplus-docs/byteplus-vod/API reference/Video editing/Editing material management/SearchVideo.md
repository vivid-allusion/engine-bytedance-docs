---
title: "SearchVideo"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-searchvideo"
---

Call `SearchVideo` to search audio and video assets in a BytePlus VOD space and return their basic, file, and extended information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **GET**

* Endpoint: `https://vod.byteplusapi.com?Action=SearchVideo&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`SearchVideo` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |
|`Space` |String |Yes |`your-space` |Name of the VOD space to search. |
|`Vid` |String |No |`v02b69g10000***` |Video ID. |
|`Title` |String |No |`Opening clip` |Video title. |
|`Tags` |String |No |`travel` |Video tags. |
|`AuditStatus` |String |No |`Passed` |Audit status: `Passed`, `Failed`, or `Pending`. |
|`PublishStatus` |String |No |`Published` |Publishing status: `Published`, `Unpublished`, or `Deleted`. |
|`TranscodeStatus` |String |No |`Uploaded` |Transcoding status. |
|`DataType` |Integer |No |`0` |Video data type. |
|`ClassificationIds` |Array of Long |No |`[123456]` |Category IDs used to filter the results. |
|`StorageClasses` |Array of Long |No |`[1]` |Storage classes used to filter the results. |
|`VodUploadSources` |Array of String |No |`["upload"]` |Upload sources used to filter the results. |
|`StartTime` |String |No |`2026-07-01T00:00:00Z` |Start of the creation\-time range in RFC 3339 format. |
|`EndTime` |String |No |`2026-07-31T23:59:59Z` |End of the creation\-time range in RFC 3339 format. |
|`Offset` |Long |No |`0` |Result offset. |
|`Limit` |Long |No |`12` |Maximum number of results to return. |
|`SortField` |String |No |`CreatedTime` |Field used to sort the results, such as `CreatedTime` or `UpdatedTime`. |
|`Order` |String |No |`Desc` |Sort order: `Desc` or `Asc`. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`VideoSet` |Object |Video collection. |
|`VideoSet.VideoInfos` |Array of [VideoInfo](https://docs.byteplus.com/en/docs/25/118531#videoinfo) |Matching videos. |
|`Total` |Integer |Total number of matching videos. |
|`BaseResp` |Object |Downstream status information. A `StatusCode` of `0` indicates success. |


<span id="videoinfo"></span>
### VideoInfo


|Parameter |Data type |Description |
|---|---|---|
|`Vid` |String |Video ID. |
|`BasicInfo` |Object |Basic media information, including `Title`, `PosterUrl`, `Duration`, `CreatedTime`, `UpdatedTime`, `PublishStatus`, `TranscodeStatus`, `Format`, `Classification`, `TosStorageClass`, and `VodUploadSource`. |
|`FileInfos` |Array of Object |File information, including `FileID`, `FileHash`, `Height`, `Width`, `Duration`, `Size`, `Format`, `Codec`, `Definition`, and `Bitrate`. |
|`VideoExt` |Object |Extended information, including `FileType` and `BigThumbs`. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
GET https://vod.byteplusapi.com?Action=SearchVideo&Version=2025-01-01&Space=your-space&Limit=12&Offset=0&Order=Desc&SortField=CreatedTime&PublishStatus=Published
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "SearchVideo",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "VideoSet": {
      "VideoInfos": [
        {
          "Vid": "v0d819g1xxxxxxxt8c8te6m8g",
          "BasicInfo": {
            "PosterUrl": "https://example.com/poster.jpeg",
            "Duration": 15.046,
            "CreatedTime": "2026-07-13 14:08:21",
            "PublishStatus": "Published",
            "TranscodeStatus": "Uploaded",
            "Title": "Opening clip",
            "Format": "MP4"
          },
          "FileInfos": [
            {
              "FileID": "v0d819g1xxxxxxxt8c8te6m8g",
              "Height": 1280,
              "Width": 720,
              "Duration": 15.046,
              "Size": 790132,
              "Format": "MP4",
              "Codec": "h264"
            }
          ],
          "VideoExt": {
            "FileType": "video",
            "BigThumbs": ""
          }
        }
      ]
    },
    "Total": 1,
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
