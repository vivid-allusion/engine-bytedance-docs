---
title: "ListSiteTagAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listsitetagapiv2"
---

Call this API to get the complete list of category and text labels that are configured for live rooms within your BytePlus account.

<span id="cfe8a431"></span>
## Request

<span id="7160a064"></span>
### Details


* API operation: `ListSiteTagAPIV2`

* Request method: GET

* Request URI: `https://livesaas.byteplusapi.com/?Action=ListSiteTagAPIV2&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="e3183224"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |


<span id="db442151"></span>
### Sample request

```JSON
Get https://livesaas.byteplusapi.com/?Action=ListSiteTagAPIV2&Version=2020-06-01
```


<span id="916b2c22"></span>
## Response

<span id="426c0334"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|SiteTags |Array of [Tag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2#539ba0fe) |List of category labels. |
|TextSiteTags |Array of [TextTag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2#b066ce5e) |List of text labels. |


<span id="539ba0fe"></span>
#### Tag


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Name |String |Name of the category label. |
|Value |Array of String |Label values. |
|Show |Integer |Deprecated. |
|Index |Integer |The display order index of the category label on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |


<span id="b066ce5e"></span>
#### TextTag


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Name |String |Name of the text label. |
|Index |Integer |The display order index of the text label on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |


<span id="d6c5e207"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "ListSiteTagAPIV2",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656419846 
    },
    "Result": {
        "SiteTags": [
            {
                "Index": 0,
                "Name": "Label 1",
                "Value": [
                    "A"
                ],
                "Show": 0
            },
            {
                "Index": 1,
                "Name": "Label 2",
                "Value": [
                    "B",
                    "C",
                    "D",
                    "E"
                ],
                "Show": 0
            }
        ],
        "TextSiteTags": [
            {
                "Index": 0,
                "Name": "Label 3"
            },
            {
                "Index": 1,
                "Name": "Label 4"
            }
        ]
    }
}
```


<span id="f43dff76"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
