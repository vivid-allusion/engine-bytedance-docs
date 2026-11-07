---
title: "GetTaskList"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-gettasklist"
---

Call `GetTaskList` to query video editing task records. You can filter the records by task type, VOD space, and task ID, and retrieve task status and output information.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **GET**

* Endpoint: `https://vod.byteplusapi.com?Action=GetTaskList&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`GetTaskList` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |
|`Type` |Integer |Yes |`1` |Task type: `1` for project\-based editing, `2` for live clipping, `3` for template tasks, `4` for subtitle tasks, `5` for smart editing, `6` for direct editing, or `7` for mosaic tasks. |
|`Space` |String |Yes |`your-space` |Name of the BytePlus VOD space that contains the tasks. |
|`TaskId` |String |No |`e070c74xxxxxxxxa5903efa7` |One or more comma\-separated task IDs. |
|`Offset` |Integer |No |`0` |Number of records to skip. |
|`Limit` |Integer |No |`10` |Maximum number of records to return. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`Total` |Integer |Total number of matching task records. |
|`Detail` |Array of [TaskDetail](https://docs.byteplus.com/en/docs/25/118566#taskdetail) |Matching task records. |


<span id="taskdetail"></span>
### TaskDetail


|Parameter |Data type |Description |
|---|---|---|
|`Id` |String |Project ID. This field is returned when the task belongs to an editing project. |
|`Name` |String |Task or output name. |
|`TaskId` |String |Editing task ID. |
|`VideoId` |String |Output video ID. |
|`Definition` |String |Output resolution in width\-by\-height format. |
|`PosterUri` |String |URI of the output poster. |
|`Space` |String |VOD space that contains the task. |
|`Status` |Integer |Task status. `1` indicates processing, `2` indicates success, and `3` indicates failure. |
|`Cost` |Integer |Processing time calculated from the task creation and update timestamps, in seconds. |
|`CreateAt` |String |Task creation time in ISO 8601 format. |
|`TaskType` |String |Task subtype returned by the service. |
|`FileName` |String |Output file name. |
|`SubMode` |String |Task submode, when available. |
|`TemplateType` |Integer |Template type, when available. |
|`TemplateSubType` |Integer |Template subtype, when available. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
GET https://vod.byteplusapi.com?Action=GetTaskList&Version=2025-01-01&Type=1&Space=your-space&Offset=0&Limit=10
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260813092420****100232280022D31",
    "Action": "GetTaskList",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Total": 1,
    "Detail": [
      {
        "Id": "p0c1c00xxxxxxxxx44n0",
        "Name": "My exported video",
        "TaskId": "e070c74xxxxxxxxa5903efa7",
        "VideoId": "v0225cgxxxxxxxxxxxxxxx38f0",
        "Definition": "1920*1080",
        "PosterUri": "tos-vod-ap-southeast-1/xxxx/poster.jpeg",
        "Space": "your-space",
        "Status": 2,
        "Cost": 20,
        "CreateAt": "2026-08-13T09:24:20+08:00",
        "TaskType": "VideoTrackHighlight",
        "FileName": "my-exported-video.mp4"
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

For error codes, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
