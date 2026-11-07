---
title: "UpdateLivePromotionsStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatelivepromotionsstatusapi"
---

Updates the distribution status of a third\-party platform in a live\-streaming activity to specify whether the platform is enabled for live stream promotion.

<span id="e3f87cdb"></span>
## Request

<span id="bfd37204"></span>
### Details


* API operation: `UpdateLivePromotionsStatusAPI`

* Request method: POST

* Request URI: `https://livesaas.byteplusapi.com/?Action=UpdateLivePromotionsStatusAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="4486e7e1"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |


<span id="5f330622"></span>
### Body parameters


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi). |
|Id |Integer |Yes |The platform ID. You can get the ID by calling [ListLivePromotionsAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listlivepromotionsapi). |
|Status |Integer |Yes |Specifies whether the platform is enabled for live\-stream promotion.<br><br>Valid values:<br><br><br>* `1`: Enabled.<br><br>* `2`: Disabled. |


<span id="3c33a17e"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateLivePromotionsStatusAPI&Version=2020-06-01 
{ 
    "ActivityId": 1231231231, 
    "Id": 12, 
    "Status": 1 
} 
```


<span id="4713a872"></span>
## Response

<span id="1d1c8f48"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ActivityId |Integer |The ID of the live\-streaming activity. |


<span id="104a3dd9"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "UpdateLivePromotionsStatusAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
            "ActivityId": 1231231231 
      } 
} 
```


<span id="d3b604ed"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
