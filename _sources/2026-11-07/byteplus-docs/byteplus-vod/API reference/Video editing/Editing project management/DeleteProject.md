---
title: "DeleteProject"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deleteproject"
---

Call `DeleteProject` to delete one or more editing projects from a project group. Task records associated with the deleted projects are also removed.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=DeleteProject&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`DeleteProject` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`ProjectId` |Array of String |Yes |`["p0c2300xxxxxxxxxxxx"]` |IDs of the projects to delete. |
|`GroupId` |String |Yes |`g0c1b0xxxxxxxx` |ID of the group that contains the projects. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`Result` |Integer |Number of deleted projects. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=DeleteProject&Version=2025-01-01
```


```json
{
  "ProjectId": [
    "p0c2300xxxxxxxxxxxx"
  ],
  "GroupId": "g0c1b0xxxxxxxx"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260813092420****100232280022D31",
    "Action": "DeleteProject",
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
