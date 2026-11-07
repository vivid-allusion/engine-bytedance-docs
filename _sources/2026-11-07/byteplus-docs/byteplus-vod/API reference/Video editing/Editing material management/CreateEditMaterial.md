---
title: "CreateEditMaterial"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-createeditmaterial"
---

Call `CreateEditMaterial` to add a media asset from a BytePlus VOD space to a cloud video editing project. The operation creates a project\-specific material ID (`EditMid`) without duplicating the underlying media asset.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="requirements"></span>
## Requirements

Call [CreateProject](https://docs.byteplus.com/docs/byteplus-vod/reference-createproject) before adding materials to the project.

<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=CreateEditMaterial&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`CreateEditMaterial` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`ProjectId` |String |Yes |`p0c8100dxxxx3phmbbcb8p374kg` |Project ID. |
|`Source` |String |Yes |`vid://v0c2dfxxxxxxxxxxxppfnggtug` |Media source. For the Video Editing Web SDK, use `vid://{Vid}` for video or audio and `mid://{Mid}` for images. |
|`Name` |String |Yes |`Opening clip` |Material name. Use 1–128 characters. |
|`Type` |String |Yes |`video` |Material type: `video`, `audio`, or `image`. |


<span id="response-parameters"></span>
## Response parameters

The `Result` value is the created editing material ID.


|Parameter |Data type |Sample value |Description |
|---|---|---|---|
|`Result` |String |`m0cb600d3xxxx67gp8e6hf0ko790` |Editing material ID (`EditMid`). |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=CreateEditMaterial&Version=2025-01-01
```


```json
{
  "ProjectId": "p0c8100dxxxx3phmbbcb8p374kg",
  "Source": "vid://v0c2dfxxxxxxxxxxxppfnggtug",
  "Name": "Opening clip",
  "Type": "video"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "CreateEditMaterial",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": "m0cb600d3xxxx67gp8e6hf0ko790"
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
