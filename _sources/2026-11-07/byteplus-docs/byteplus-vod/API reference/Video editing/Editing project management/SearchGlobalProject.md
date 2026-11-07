---
title: "SearchGlobalProject"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-searchglobalproject"
---

Call `SearchGlobalProject` to search editing projects in a BytePlus VOD space without specifying a project group.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=SearchGlobalProject&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`SearchGlobalProject` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Space` |String |Yes |`your-space` |Name of the BytePlus VOD space that contains the projects. |
|`Name` |Array of String |No |`["My editing project"]` |Project names used to filter the results. |
|`Id` |Array of String |No |`["p02a100xxxxxxxxxxxx"]` |Project IDs used to filter the results. |
|`StartTime` |String |No |`2026-08-01T00:00:00+08:00` |Start of the project creation\-time range. |
|`EndTime` |String |No |`2026-08-31T23:59:59+08:00` |End of the project creation\-time range. |
|`Offset` |Integer |No |`0` |Number of projects to skip. |
|`Limit` |Integer |No |`18` |Maximum number of projects to return. |
|`SortBy` |String |No |`updated_at` |Field used to sort the results. |
|`Order` |String |No |`desc` |Sort order. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`Total` |Integer |Total number of matching projects. |
|`Detail` |Array of [ProjectDetail](https://docs.byteplus.com/en/docs/25/118568#projectdetail) |Matching projects. |


<span id="projectdetail"></span>
### ProjectDetail


|Parameter |Data type |Description |
|---|---|---|
|`GroupId` |String |ID of the group that contains the project. |
|`ProjectId` |String |Project ID. |
|`ProjectName` |String |Project name. |
|`ProjectType` |String |Project type. |
|`TemplateId` |String |Project template ID. |
|`LatestEditParam` |Object |Latest editing configuration saved for the project. |
|`Thumbnails` |String |Project thumbnail information. |
|`Space` |String |VOD space that contains the project. |
|`CallbackType` |String |Callback type configured for the project. |
|`CallbackUri` |String |Callback URL configured for the project. |
|`Tasks` |Array of Object |Latest task associated with the project, when available. |
|`CreatedAt` |String |Project creation time in ISO 8601 format. |
|`UpdatedAt` |String |Project update time in ISO 8601 format. |
|`Extra` |String |Additional project information. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=SearchGlobalProject&Version=2025-01-01
```


```json
{
  "Offset": 0,
  "Limit": 18,
  "SortBy": "updated_at",
  "Order": "desc",
  "Space": "your-space"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260813092420****100232280022D31",
    "Action": "SearchGlobalProject",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Total": 1,
    "Detail": [
      {
        "LatestEditParam": {},
        "GroupId": "g03ce00xxxxxxxxxxxx",
        "ProjectId": "p02a100xxxxxxxxxxxx",
        "ProjectName": "My editing project",
        "ProjectType": "track",
        "Space": "your-space",
        "CreatedAt": "2026-08-13T09:16:38+08:00",
        "UpdatedAt": "2026-08-13T09:33:25+08:00",
        "Extra": "",
        "Tasks": []
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

For error codes, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
