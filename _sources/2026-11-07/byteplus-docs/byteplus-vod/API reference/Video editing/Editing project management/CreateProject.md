---
title: "CreateProject"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-createproject"
---

Call `CreateProject` to create a cloud video editing project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=CreateProject&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`CreateProject` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`ProjectName` |String |Yes |`My-editing-project` |Project name. The recommended length is 1–128 characters. |
|`Space` |String |Yes |`your-space` |Name of the BytePlus VOD space. You can obtain it from the [BytePlus VOD console](https://console.byteplus.com/vodpaas) or by calling [ListSpace](https://docs.byteplus.com/docs/byteplus-vod/reference-listspace). |
|`EditParam` |JSON Map |Yes |`-` |Editing project configuration. See [Editing videos via OpenAPI](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi). |
|`ProjectType` |String |Yes |`track` |Project type. The supported value is `track`. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Web SDK requirements</div>


<div data-tips="true" data-tips-type="warning">When creating a project for the Video Editing Web SDK, set <code>Space</code> and <code>EditParam.Upload.SpaceName</code> to the same value. Set the canvas to <code>1920 × 1080</code> or <code>1080 × 1920</code>.</div>


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Sample value |Description |
|---|---|---|---|
|`ProjectId` |String |`p0ccxxxxxxxxxx` |Project ID. |
|`GroupId` |String |`g0c9xxxxxxxxxx` |ID of the group that contains the project. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=CreateProject&Version=2025-01-01
```


```json
{
  "ProjectName": "My-editing-project",
  "Space": "your-space",
  "EditParam": {
    "Project": {
      "Version": "1.0.0",
      "Name": "My-editing-project",
      "CreateTime": 1757142958344,
      "UpdateTime": 1757142958344,
      "Tag": "TrackEditor"
    },
    "Upload": {
      "SpaceName": "your-space",
      "VideoName": "My-editing-project"
    },
    "Output": {
      "Alpha": false,
      "Fps": 25,
      "Codec": {
        "VideoCodec": "h264",
        "Preset": "slow",
        "Crf": 23,
        "AudioCodec": "aac",
        "AudioBitrate": 128
      },
      "DisableVideo": false,
      "DisableAudio": false,
      "Cover": {
        "DisableCover": false,
        "CoverTime": [0]
      }
    },
    "Canvas": {
      "Width": 1920,
      "Height": 1080,
      "BackgroundColor": "#000000FF"
    }
  },
  "ProjectType": "track"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "CreateProject",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ProjectId": "p0ccxxxxxxxxxx",
    "GroupId": "g0c9xxxxxxxxxx"
  }
}
```


<span id="error-codes"></span>
## Error codes


|HTTP status code |Error code |Error message |Description |
|---|---|---|---|
|400 |`InvalidParameter.InvalidParam` |`parameter error` |A request parameter is invalid. |


For other errors, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
