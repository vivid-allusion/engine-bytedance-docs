---
title: "DeleteTask"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deletetask"
---

Call `DeleteTask` to delete a video editing task record by task ID. Deleting the record removes it from task queries; this operation does not describe deletion of the generated media output.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **GET**

* Endpoint: `https://vod.byteplusapi.com?Action=DeleteTask&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`DeleteTask` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |
|`TaskId` |String |Yes |`e070c74xxxxxxxxa5903efa7` |Task ID returned by a task submission operation or [GetTaskList](https://docs.byteplus.com/docs/byteplus-vod/reference-gettasklist). |
|`Type` |Integer |Yes |`1` |Task type: `1` for project\-based editing, `2` for live clipping, `3` for template tasks, `4` for subtitle tasks, `5` for smart editing, `6` for direct editing, or `7` for mosaic tasks. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`Result` |Integer |Number of deleted task records. `1` indicates that one record was deleted. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
GET https://vod.byteplusapi.com?Action=DeleteTask&Version=2025-01-01&TaskId=e070c74xxxxxxxxa5903efa7&Type=1
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260813092420****100232280022D31",
    "Action": "DeleteTask",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": 1
}
```


<span id="error-codes"></span>
## Error codes

For error codes, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
