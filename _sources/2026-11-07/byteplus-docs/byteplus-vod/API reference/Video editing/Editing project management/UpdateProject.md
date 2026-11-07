---
title: "UpdateProject"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updateproject"
---

Call `UpdateProject` to update a cloud video editing project, including its name and latest editing configuration.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=UpdateProject&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`UpdateProject` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Description |
|---|---|---|---|
|`GroupId` |String |Yes |ID of the group that contains the project. |
|`ProjectId` |String |Yes |Project ID. |
|`ProjectName` |String |No |Updated project name. |
|`LatestEditParam` |Object |No |Latest editing configuration. It can contain `Project`, `Upload`, `Output`, `Canvas`, and `Track`. See [Editing videos via OpenAPI](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi). |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Sample value |Description |
|---|---|---|---|
|`Result` |Integer |`1` |Operation result. `1` indicates success. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=UpdateProject&Version=2025-01-01
```


```json
{
  "GroupId": "g03ce0xxxxxxxxxxx2g",
  "ProjectId": "p03efxxxxxxxxxxxxxxxk74bm0",
  "ProjectName": "Updated project",
  "LatestEditParam": {
    "Project": {
      "Version": "1.0.0",
      "Name": "Updated project",
      "CreateTime": 1759060604253,
      "UpdateTime": 1760842914243,
      "Tag": "TrackEditor"
    },
    "Upload": {
      "SpaceName": "your-space",
      "VideoName": "Updated project",
      "FileName": "/updated-project.mp4"
    },
    "Canvas": {
      "Width": 1920,
      "Height": 1080,
      "BackgroundColor": "#000000FF"
    },
    "Track": []
  }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "UpdateProject",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": 1
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
