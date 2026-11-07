---
title: "ListVideoClassifications"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications"
---

This interface is used to query the video category by category ID in the specified space. The query results will be returned in a tree structure.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListVideoClassifications&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListVideoClassifications` |The API action. For the current API, the value is `ListVideoClassifications`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The name of the VOD space. You can obtain the name of the space in the following ways:<br><br><br>* View the names of all spaces under the current account on the BytePlus VOD control panel [Spaces](https://console.byteplus.com/vodpaas/overview/).<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|ClassificationId |Long |Yes |`0` |The category ID. If you set it as `0`, this API returns all categories in the space. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ClassificationTrees |Array of [VodClassification](https://docs.byteplus.com/en/docs/25/8032#vodclassification) |`-` |The category list. |


#{.custom\-md\-table\-4}#

<span id="vodclassification"></span>
### VodClassification


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SpaceName |String |`test` |The name of the VOD space. |
|ClassificationId |Long |`1643` |The category ID. |
|Level |Integer |`1` |Category Levels:<br><br><br>* `1`: The first category<br><br>* `2`: The secondary category<br><br>* `3`: The third category |
|Classification |String |`01` |The category name. |
|ParentClassificationId |Long |`1345` |The parent category ID. |
|SubClassification |Object of [VodClassification](https://docs.byteplus.com/en/docs/25/8032#vodclassification) |`-` |The sub\-category information. |
|SubClassificationTrees |Array of [VodClassification](https://docs.byteplus.com/en/docs/25/8032#vodclassification) |`-` |The subcategory list. |
|CreatedAt |String |`2025-07-07T06:44:59Z` |The category creation time. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListVideoClassifications&Version=2023-01-01&SpaceName=test&ClassificationId=0
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202507070645175E0D04C83480820F7E6D",
        "Action": "ListVideoClassifications",
        "Version": "2023-01-01",
        "Service": "vod",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ClassificationTrees": [
            {
                "SpaceName": "test",
                "ClassificationId": "28**9",
                "Level": 1,
                "Classification": "One level - new category",
                "ParentClassificationId": "0",
                "SubClassification": null,
                "SubClassificationTrees": [],
                "CreatedAt": "2025-07-07T06:44:59Z"
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

This operation does not have specific error codes. For more information, see the [shared error codes of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).

&nbsp;
