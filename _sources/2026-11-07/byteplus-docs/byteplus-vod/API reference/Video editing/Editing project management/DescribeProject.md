---
title: "DescribeProject"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-describeproject"
---

Call `DescribeProject` to get the details of one or more cloud video editing projects.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=DescribeProject&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`DescribeProject` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`GroupId` |String |Yes |`g03cxxxxxxxxxx` |ID of the group that contains the projects. |
|`ProjectId` |Array of String |Yes |`["p02xxxxxxxxxhss0"]` |Project IDs to query. |


<span id="response-parameters"></span>
## Response parameters

The `Result` value is an array of project objects.


|Parameter |Data type |Description |
|---|---|---|
|`GroupId` |String |ID of the group that contains the project. |
|`ProjectId` |String |Project ID. |
|`ProjectName` |String |Project name. |
|`ProjectType` |String |Project type. |
|`TemplateId` |String |Project template ID. |
|`LatestEditParam` |JSON Map |Latest editing configuration saved for the project. See [Editing videos via OpenAPI](https://docs.byteplus.com/docs/byteplus-vod/editing_videos_via_openapi). |
|`Thumbnails` |String |Project thumbnail URL. |
|`Space` |String |Name of the VOD space that contains the project. |
|`CallbackType` |String |Callback type. |
|`CallbackUri` |String |Callback URL. |
|`CreatedAt` |String |Project creation time in ISO 8601 format. |
|`UpdatedAt` |String |Project update time in ISO 8601 format. |
|`Extra` |String |Additional project information. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=DescribeProject&Version=2025-01-01
```


```json
{
  "GroupId": "g03cxxxxxxxxxx",
  "ProjectId": ["p02xxxxxxxxxhss0"]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "DescribeProject",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": [
    {
      "GroupId": "g03cxxxxxxxxxx",
      "ProjectId": "p02xxxxxxxxxhss0",
      "ProjectName": "My editing project",
      "ProjectType": "track",
      "LatestEditParam": {},
      "Space": "your-space",
      "CreatedAt": "2026-07-13T15:16:38+08:00",
      "UpdatedAt": "2026-07-13T15:33:25+08:00"
    }
  ]
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
