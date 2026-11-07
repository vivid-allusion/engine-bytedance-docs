---
title: "DeleteMirrorSrcRule"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-deletemirrorsrcrule"
---

Delete the specified image mirror source rule (mirroring\-based back\-to\-origin rule) in the VOD service, given the `SpaceName` and `Id`.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=DeleteMirrorSrcRule&Version=2023\-07\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteMirrorSrcRule` |The API action. For the current API, the value is `DeleteMirrorSrcRule`. |
|Version |String |Yes |`2023-07-01` |The API version. For the current API, the value is `2023-07-01`. |
|SpaceName |String |Yes |`my-space` |The name of the space where the image source rule is to be deleted. |
|Id |String |Yes |`06d0499eedf84f4e9b4064442fc59993` |The ID of the image source rule to be deleted. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=DeleteMirrorSrcRule&Version=2023-07-01&SpaceName=my-space&Id=06d0499eedf84f4e9b4064442fc59993
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "DeleteMirrorSrcRule",
        "Region": "ap-southeast-1",
        "Service": "vod",
        "Version": "2023-07-01",
        "RequestId": "20230604110420****100232280022D31"
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
