---
title: "MGetMaterial"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-mgetmaterial"
---

Call `MGetMaterial` to list or search materials in a BytePlus VOD space.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **GET**

* Endpoint: `https://vod.byteplusapi.com?Action=MGetMaterial&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`MGetMaterial` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |
|`Space` |String |Yes |`your-space` |Name of the VOD space to search. |
|`Mid` |String |No |`1234567890ab***` |Material ID. |
|`Vid` |String |No |`v02b69g10000***` |Video ID associated with the material. |
|`Title` |String |No |`Cover image.png` |Material title. |
|`Category` |String |No |`image` |Material type: `video`, `audio`, `image`, `subtitle`, or `font`. |
|`Format` |String |No |`png` |Material format. |
|`ClassificationIds` |String |No |`123456,234567` |Comma\-separated VOD category IDs. |
|`StartTime` |String |No |`2026-07-01T00:00:00Z` |Start of the time range in RFC 3339 format. |
|`EndTime` |String |No |`2026-07-31T23:59:59Z` |End of the time range in RFC 3339 format. |
|`Offset` |Long |No |`0` |Page index. `0` represents the first page. |
|`Limit` |Long |No |`12` |Number of materials per page. |
|`SortBy` |String |No |`Title` |Sort field: `Title`, `Category`, or `Mid`. |
|`Order` |String |No |`desc` |Sort order: `asc` or `desc`. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`MaterialSet` |Object |Material collection. |
|`MaterialSet.MaterialInfos` |Array of [MaterialInfo](https://docs.byteplus.com/en/docs/25/118533#materialinfo) |Matching materials. |
|`Total` |Integer |Total number of matching materials. |
|`BaseResp` |Object |Downstream status information. A `StatusCode` of `0` indicates success. |


<span id="materialinfo"></span>
### MaterialInfo


|Parameter |Data type |Description |
|---|---|---|
|`Vid` |String |Video ID, when the material is associated with an audio or video asset. |
|`Mid` |String |Material ID. |
|`MaterialBasicInfo` |Object |Basic information, including `SpaceName`, `Title`, `Filename`, `Description`, `Category`, `Format`, `Size`, `CreatedAt`, `UpdateAt`, `StoreUri`, `Md5`, `Height`, `Width`, `PosterUrl`, `PlayUrl`, and `OuterImageUrl`. |
|`FileInfos` |Array of Object |File information, when available. |
|`InfoExt` |Object |Extended material information, when available. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
GET https://vod.byteplusapi.com?Action=MGetMaterial&Version=2025-01-01&Space=your-space&Category=image&Format=png&Limit=12&Offset=0&SortBy=Title&Order=desc
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "MGetMaterial",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "MaterialSet": {
      "MaterialInfos": [
        {
          "Mid": "1234567890ab***",
          "MaterialBasicInfo": {
            "SpaceName": "your-space",
            "Mid": "1234567890ab***",
            "Title": "Cover image.png",
            "Filename": "Cover image.png",
            "Category": "image",
            "Format": "png",
            "Size": 661895,
            "Height": 376,
            "Width": 1095,
            "PosterUrl": "https://example.com/cover.png"
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
