---
title: "SearchEditMaterial"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-searcheditmaterial"
---

Call `SearchEditMaterial` to get one or more materials associated with a cloud video editing project.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=SearchEditMaterial&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`SearchEditMaterial` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`ProjectId` |String |Yes |`p0c8100d3xxxxphmbbcb8p374kg` |Project ID. |
|`EditMids` |Array of String |Yes |`["m0cb60xxxxxxx0ko790"]` |Editing material IDs to query. |
|`Space` |String |Yes |`your-space` |Name of the VOD space that contains the materials. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`Total` |Integer |Number of matching materials. |
|`Detail` |Array of [MaterialDetail](https://docs.byteplus.com/en/docs/25/118529#materialdetail) |Matching editing materials. |


<span id="materialdetail"></span>
### MaterialDetail


|Parameter |Data type |Description |
|---|---|---|
|`EditMid` |String |Editing material ID. |
|`ProjectId` |String |Project ID. |
|`Name` |String |Material name. |
|`Type` |String |Material type, such as `video`, `audio`, or `image`. |
|`Status` |String |Material processing status. |
|`Source` |String |Source media URI. |
|`Content` |String |Material content information, when applicable. |
|`CreatedAt` |String |Material creation time in ISO 8601 format. |
|`UpdatedAt` |String |Material update time in ISO 8601 format. |
|`Extra` |String |Additional material information. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=SearchEditMaterial&Version=2025-01-01
```


```json
{
  "ProjectId": "p0c8100d3xxxxphmbbcb8p374kg",
  "EditMids": ["m0cb60xxxxxxx0ko790"],
  "Space": "your-space"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "SearchEditMaterial",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Total": 1,
    "Detail": [
      {
        "EditMid": "m0cb60xxxxxxx0ko790",
        "ProjectId": "p0c8100d3xxxxphmbbcb8p374kg",
        "Name": "Opening clip",
        "Type": "video",
        "Status": "Running",
        "Source": "vid://v0c2dfxxxxxxxxxxxppfnggtug",
        "CreatedAt": "2026-07-13T10:59:37+08:00",
        "UpdatedAt": "2026-07-13T10:59:37+08:00",
        "Extra": ""
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
