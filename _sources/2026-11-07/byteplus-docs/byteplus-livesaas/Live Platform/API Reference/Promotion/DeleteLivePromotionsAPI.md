---
title: "DeleteLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletelivepromotionsapi"
---

This API deletes a third\-party platform for live stream promotion in a live\-streaming activity.

<span id="3bd1cae3"></span>
## Request

<span id="b4b95ba8"></span>
### Details


* API operation: `DeleteLivePromotionsAPI`

* Request method: POST

* Request URI: `https://livesaas.byteplusapi.com/?Action=DeleteLivePromotionsAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="15273936"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |


<span id="da228a08"></span>
### Body parameters


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi). |
|Id |Integer |Yes |The ID of the promotion platform. You can get the ID by calling [ListLivePromotionsAPI](https://docs.byteplus.com/byteplus-livesaas/docs/listlivepromotionsapi). |


<span id="6cafa432"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=DeleteLivePromotionsAPI&Version=2020-06-01 
{ 
    "ActivityId": 1231231231, 
    "Id": 123 
} 
```


<span id="e05f6486"></span>
## Response

<span id="696aa8bd"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ActivityId |Integer |The ID of the live\-streaming activity. |


<span id="fc31d626"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "DeleteLivePromotionsAPI", 
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


<span id="fd33babb"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
