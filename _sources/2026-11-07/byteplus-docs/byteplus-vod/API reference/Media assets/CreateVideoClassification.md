---
title: "CreateVideoClassification"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-createvideoclassification"
---

This interface is used to create a video category by setting parameters such as the category name and category level in the specified space. BytePlus VOD supports up to three levels of categories.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=CreateVideoClassification&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateVideoClassification` |The API action. For the current API, the value is `CreateVideoClassification`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The name of the VOD space. The space name can be obtained in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD control panel [Spaces](https://console.byteplus.com/vodpaas/overview/).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|Level |Integer |Yes |`1` |The category level. Supported values:<br><br><br>* `1`: First\-level category.<br><br>* `2`: Second\-level category.<br><br>* `3`: Third\-level category. |
|ParentId |Long |No |`0` |The parent category ID. It defaults to `0`, indicating the first\-level category. The parent category of all first\-level categories is `0`. |
|Classification |String |Yes |`The video.` |The category name. The length cannot exceed 64 bits. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ClassificationId |Long |`1702994923` |The category ID. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=CreateVideoClassification&Version=2023-01-01&SpaceName=test&Level=1&ParentId=0&Classification=The video.
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateVideoClassification",
        "Region": "ap-singapore-1",
        "Service": "vod",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "ClassificationId": 1702994923
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
