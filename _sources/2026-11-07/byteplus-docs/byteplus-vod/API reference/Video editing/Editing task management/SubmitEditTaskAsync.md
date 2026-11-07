---
title: "SubmitEditTaskAsync"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-submitedittaskasync"
---

Call `SubmitEditTaskAsync` to asynchronously submit a video editing task for an existing cloud editing project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="requirements"></span>
## Requirements

Call [CreateProject](https://docs.byteplus.com/docs/byteplus-vod/reference-createproject) before submitting the editing task.

<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=SubmitEditTaskAsync&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`SubmitEditTaskAsync` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`GroupId` |String |Yes |`g03cexxxxxxxxxxxxxxxxxqt2g` |ID of the group that contains the project. |
|`ProjectId` |String |Yes |`p03ef0xxxxxxxxxxxxx4bm0` |Project ID. |
|`ProjectType` |String |Yes |`track` |Project type. The supported value is `track`. |
|`EditParam` |Object |Yes |`-` |Complete editing configuration to submit. See [Editing videos via OpenAPI](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Sample value |Description |
|---|---|---|---|
|`TaskId` |String |`e070c0xxxxxxxxxx1fc7b6143` |Editing task ID. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=SubmitEditTaskAsync&Version=2025-01-01
```


```json
{
  "GroupId": "g03cexxxxxxxxxxxxxxxxxqt2g",
  "ProjectId": "p03ef0xxxxxxxxxxxxx4bm0",
  "ProjectType": "track",
  "EditParam": {
    "Project": {
      "Version": "1.0.0",
      "Name": "My editing project",
      "CreateTime": 1759060604253,
      "UpdateTime": 1760844323139,
      "Tag": "TrackEditor"
    },
    "Upload": {
      "SpaceName": "your-space",
      "VideoName": "My exported video",
      "FileName": "/my-exported-video.mp4"
    },
    "Output": {
      "Alpha": false,
      "Fps": 30,
      "Codec": {
        "VideoCodec": "h264",
        "Preset": "slow",
        "Crf": 23,
        "AudioCodec": "aac",
        "AudioBitrate": 128
      },
      "DisableVideo": false,
      "DisableAudio": false,
      "Format": "mp4"
    },
    "Canvas": {
      "Width": 1920,
      "Height": 1080,
      "BackgroundColor": "#000000FF"
    },
    "Track": [
      [
        {
          "Type": "video",
          "Source": "vid://v0c2dfxxxxxxxxxxxppfnggtug",
          "TargetTime": [0, 10000]
        }
      ]
    ]
  }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "SubmitEditTaskAsync",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "TaskId": "e070c0xxxxxxxxxx1fc7b6143"
  }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
