---
title: "UpdateSiteTagAPIV2"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatesitetagapiv2"
---

Call this API to update the information of labels for live\-streaming activities under your BytePlus account.

<span id="8baab3a6"></span>
## Request

<span id="dc5f59cd"></span>
### Details


* API operation: `UpdateSiteTagAPIV2`

* Request method: POST

* Request URI: `https://livesaas.byteplusapi.com/?Action=UpdateSiteTagAPIV2&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="6e979a4a"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |


<span id="b23059ea"></span>
### Body parameters


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|SiteTags |Array of [Tag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2#Tag) |Yes |The list of all category labels.<br><br>To update labels, retrieve the current list by calling [ListSiteTagAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/listsitetagapiv2), modify the values as needed, and then include the complete, updated list in your request. |
|TextSiteTags |Array of [TextTag](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updatesitetagapiv2#TextTag) |Yes |The list of all text labels.<br><br>To update labels, retrieve the current list by calling [ListSiteTagAPIV2](https://docs.byteplus.com/byteplus-livesaas/docs/listsitetagapiv2), modify the values as needed, and then include the complete, updated list in your request. |


<span id="7c2f115d"></span>
#### **Tag**


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Name |String |Yes |The name of the category label. The name cannot exceed 50 characters or be the same as that of another category label. |
|Value |Array of String |Yes |An array of values for the label. Each label value cannot exceed 50 characters and must be unique within the same category label. |
|Show |Integer |Yes |Deprecated. |
|Index |Integer |Yes |The index of the category label, which determines the display order on the BytePlus Live console.<br><br>Value range: [0,19]. |


<span id="b07ec8d0"></span>
#### **TextTag**


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Name |String |Yes |Name of the text label. The name cannot exceed 50 characters or be the same as that of another text label. |
|Index |Integer |Yes |The index of the text label, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Value range: [0,4]. |


<span id="b52be3c9"></span>
### Sample request

```JSON
Post https://livesaas.byteplusapi.com/?Action=UpdateSiteTagAPIV2&Version=2020-06-01 
{ 
      "SiteTags":   [ 
            { 
                  "Name": "Label 1", 
                  "Value": [ 
                        "A", 
                        "B" 
                  ], 
                  "Show": 0, 
                  "Index": 0 
            }, 
           { 
                  "Name": "Label 2", 
                  "Value": [ 
                        "C", 
                        "D" 
                  ], 
                  "Show": 0, 
                  "Index": 1 
            } 
      ], 
      "TextSiteTags":   [ 
            { 
                  "Name": "Label 3", 
                  "Index": 0 
            }, 
            { 
                  "Name": "Label 4", 
                  "Index": 1 
            } 
      ] 
} 
```


<span id="be0e1229"></span>
## Response

<span id="3e7e53c1"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Status |Boolean |Indicates whether the update is successful.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="7f2c5f49"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "UpdateSiteTagAPIV2", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": { 
        "Status": true 
    } 
} 
```


<span id="22d08a72"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
