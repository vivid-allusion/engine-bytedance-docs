---
title: "UpdateVideoClassification"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-updatevideoclassification"
---

This interface is used to update the name of a created category in a specified space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=UpdateVideoClassification&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateVideoClassification` |The API action. For the current API, the value is `UpdateVideoClassification`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The name of the on\-demand space. You can obtain the name of the space in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD control panel [Spaces](https://console.byteplus.com/vodpaas/overview/).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|ClassificationId |Long |Yes |`1702994923` |The category ID. It can be obtained in the following ways:<br><br><br>* By calling the [CreateVideoClassification](https://docs.byteplus.com/en/docs/byteplus-vod/reference-createvideoclassification) interface.<br><br>* By calling the [ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications) interface. |
|Classification |String |Yes |`01-The video` |The new category name. The length must not exceed 64 bits. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=UpdateVideoClassification&Version=2023-01-01&SpaceName=test&ClassificationId=1702994923&Classification=01-The video
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "2020112417******034080031B5",
    "Action": "UpdateVideoClassification",
    "Version": "2023-01-01",
    "Service": "vod",
    "Region": "Singapore"
  }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
