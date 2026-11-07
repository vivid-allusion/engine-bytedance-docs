---
title: "DeleteFrameExtractions"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deleteframeextractions"
---

Deletes some or all persisted frame extraction results for a specified video while retaining the source video.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">This operation deletes both the matching result records and their stored extracted\-frame files. Verify the <code>Vid</code>, <code>UserTag</code>, and <code>RunId</code> before sending the request.</div>


<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteFrameExtractions&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteFrameExtractions` |The API action. For the current API, the value is `DeleteFrameExtractions`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |Space name. |
|Vid |String |Yes |`v0dc24g10***s1v0ipljnh4h0` |Video ID. If neither `UserTag` nor `RunId` is specified, all frame extraction results for this video are deleted. |
|UserTag |String |No |`review_v1` |User\-defined tag. Only one tag can be specified. If omitted, deletion is not filtered by user tag. |
|RunId |String |No |`3732f0bd7565494d8faf7956d4f99f31` |Task ID, the unique identifier of an execution task. Only one run ID can be specified. If omitted, deletion is not filtered by run ID. |


If both `UserTag` and `RunId` are specified, only results matching both values are deleted.

<span id="response-parameters"></span>
## Response parameters

This operation has no API\-specific response parameters. The response contains only `ResponseMetadata`. For details, refer to the [Response](https://docs.byteplus.com/docs/byteplus-vod/reference-introduction#response) section.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```HTTP
https://vod.byteplusapi.com?Action=DeleteFrameExtractions&Version=2023-01-01&SpaceName=test&Vid=v0dc24g10***s1v0ipljnh4h0&UserTag=review_v1&RunId=3732f0bd7565494d8faf7956d4f99f31
```


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202606111230406131E13B603A9C364A09",
    "Action": "DeleteFrameExtractions",
    "Version": "2023-01-01",
    "Service": "vod",
    "Region": "ap-southeast-1"
  }
}
```


<span id="error-codes"></span>
## Error codes

For information about error codes, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/docs/byteplus-vod/reference-common-error-codes).
