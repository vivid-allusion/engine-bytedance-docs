---
title: "GetEffectList"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-geteffectlist"
---

Call `GetEffectList` to get the resource metadata used by the Video Editing Web SDK's transition, special\-effect, and filter panels.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Region availability</div>


<div data-tips="true" data-tips-type="tip">This API is currently available only in the Asia Pacific (Johor) region. Sign the request with region <code>ap-southeast-1</code>.</div>


<span id="http-request"></span>
## HTTP request


* Method: **POST**

* Endpoint: `https://vod.byteplusapi.com?Action=GetEffectList&Version=2025-01-01`


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Action` |String |Yes |`GetEffectList` |The API action. |
|`Version` |String |Yes |`2025-01-01` |The API version. |


<span id="body"></span>
### Body


|Parameter |Data type |Required |Sample value |Description |
|---|---|---|---|---|
|`Panel` |String |Yes |`transition` |Panel type. Supported values:<br><br><br>* `transition`: Transition panel.<br><br>* `flower`: Stylized text panel.<br><br>* `specialeffects`: Special effect panel.<br><br>* `effect`: Filter panel. |


<span id="response-parameters"></span>
## Response parameters

The SDK consumes this response as resource metadata. Return the complete `Result` object to the frontend without renaming or removing fields.


|Parameter |Data type |Description |
|---|---|---|
|`Version` |String |Resource\-list version. |
|`Effects` |Array of [Effect](https://docs.byteplus.com/en/docs/25/118530#effect) |Effect resources. |
|`Category` |Array of [EffectCategory](https://docs.byteplus.com/en/docs/25/118530#effectcategory) |Resource categories. |
|`FrontEffectId` |String |Front effect ID. |
|`RearEffectId` |String |Rear effect ID. |
|`Panel` |Object |Panel metadata. |
|`Collection` |Array of String |Collected resource IDs. |
|`UrlPrefix` |Array of String |URL prefixes used to access resources. |


<span id="effect"></span>
### Effect


|Parameter |Data type |Description |
|---|---|---|
|`Name` |String |Display name. |
|`Id` |String |Resource ID. |
|`EffectId` |String |Effect ID. |
|`FileUrl` |Object |Resource URI and accessible URL list. |
|`IconUrl` |Object |Icon URI and accessible URL list. |
|`SdkVersion` |String |Minimum SDK version required by the resource. |
|`DevicePlatform` |String |Supported device platform. |
|`Types` |Array of String |Resource types. |
|`Tags` |Array of String |Resource tags. |
|`EffectType` |Integer |Effect type identifier. |
|`Parent` |String |Parent effect ID. |
|`Children` |Array of String |Child effect IDs. |
|`Requirements` |Array of String |Resource requirements. |
|`Panel` |String |Panel to which the resource belongs. |
|`Extra` |String |Additional resource metadata. |


The service can return additional effect metadata. Pass all returned fields through to the SDK.

<span id="effectcategory"></span>
### EffectCategory


|Parameter |Data type |Description |
|---|---|---|
|`Id` |String |Category ID. |
|`Name` |String |Category display name. |
|`Icon` |Object |Default category icon. |
|`IconSelected` |Object |Icon displayed when the category is selected. |
|`Effects` |Array of String |Effect IDs in the category. |
|`Tags` |Array of String |Category tags. |
|`Key` |String |Category key. |
|`IsDefault` |Boolean |Whether this is the default category. |
|`Extra` |String |Additional category metadata. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```text
POST https://vod.byteplusapi.com?Action=GetEffectList&Version=2025-01-01
```


```json
{
  "Panel": "transition"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20230604110420****100232280022D31",
    "Action": "GetEffectList",
    "Version": "2025-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "Version": "1698723716140,0,1010,1",
    "Effects": [
      {
        "Name": "Cross fade",
        "Id": "c1e7c6302e773e5196d6c3f72216xxxx",
        "EffectId": "27730518",
        "FileUrl": {
          "Uri": "c1e7c6302e773e5196d6c3f72216xxxx",
          "UrlList": ["https://example.com/effect.zip"]
        },
        "IconUrl": {
          "Uri": "4d5c707800f37b64f35c28a15125xxxx",
          "UrlList": ["https://example.com/effect.png"]
        },
        "DevicePlatform": "all",
        "Panel": "transition"
      }
    ],
    "Category": [],
    "Collection": [],
    "UrlPrefix": []
  }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have operation\-specific error codes. For more information, see [BytePlus VOD shared error codes](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
