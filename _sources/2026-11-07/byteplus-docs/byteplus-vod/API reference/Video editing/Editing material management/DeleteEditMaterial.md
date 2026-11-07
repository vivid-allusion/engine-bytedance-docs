---
title: "DeleteEditMaterial"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deleteeditmaterial"
---

Call `DeleteEditMaterial` to remove a material from a cloud video editing project by its `EditMid`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=DeleteEditMaterial&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`DeleteEditMaterial` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`EditMid` |String |Yes |`m0cb6xxxxxxxxhf0ko790` |Editing material ID returned by [CreateEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-createeditmaterial) or [SearchEditMaterial](https://docs.byteplus.com/docs/byteplus-vod/reference-searcheditmaterial). |


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
POST https://vod.byteplusapi.com?Action=DeleteEditMaterial&Version=2025-01-01
```


```json
{
  "EditMid": "m0cb6xxxxxxxxhf0ko790"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "DeleteEditMaterial",
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
