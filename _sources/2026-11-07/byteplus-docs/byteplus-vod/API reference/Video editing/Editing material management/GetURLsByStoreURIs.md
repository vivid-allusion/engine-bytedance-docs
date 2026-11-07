---
title: "GetURLsByStoreURIs"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-geturlsbystoreuris"
---

Call `GetURLsByStoreURIs` to get accessible URLs for image resources identified by their storage URIs.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **GET**

* Endpoint: `https://vod.byteplusapi.com?Action=GetURLsByStoreURIs&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`GetURLsByStoreURIs` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |
|`Space` |String |Yes |`your-space` |Name of the BytePlus VOD space that contains the resources. |
|`StoreType` |String |Yes |`Image` |Resource storage type. For image resources, set this parameter to `Image`. |
|`StoreURIs` |String |Yes |`tos-vod-ap-southeast-1/xxxx/image.png` |One or more comma\-separated storage URIs. You can specify up to 100 URIs in one request. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data type |Description |
|---|---|---|
|`URLs` |Array of [URLInfo](https://docs.byteplus.com/en/docs/25/118570#urlinfo) |Storage URIs and their accessible URLs. |
|`NoPermissionUris` |Array of String |Storage URIs that cannot be accessed by the current account. |
|`Total` |Integer |Number of URLs returned successfully. |
|`BaseResp` |Object |Downstream status information. A `StatusCode` of `0` indicates success. |


<span id="urlinfo"></span>
### URLInfo


|Parameter |Data type |Description |
|---|---|---|
|`StoreURI` |String |Input storage URI. |
|`URL` |String |Accessible URL corresponding to the storage URI. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
GET https://vod.byteplusapi.com?Action=GetURLsByStoreURIs&Version=2025-01-01&Space=your-space&StoreType=Image&StoreURIs=tos-vod-ap-southeast-1%2Fxxxx%2Fimage.png
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20260813092420****100232280022D31",
    "Action": "GetURLsByStoreURIs",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "URLs": [
      {
        "StoreURI": "tos-vod-ap-southeast-1/xxxx/image.png",
        "URL": "https://example.com/image.png"
      }
    ],
    "NoPermissionUris": [],
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

For error codes, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
