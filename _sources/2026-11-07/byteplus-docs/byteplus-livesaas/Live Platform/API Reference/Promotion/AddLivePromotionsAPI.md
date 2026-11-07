---
title: "AddLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-addlivepromotionsapi"
---

Call this API to add multiple third\-party platforms to a live activity for simulcasting. After a platform is added and the activity's stream begins, BytePlus Live automatically pushes the stream to that platform, allowing you to expand your audience reach.

<span id="f6dba5d6"></span>
## Request

<span id="46fe124d"></span>
### Details


* API operation: `AddLivePromotionsAPI`

* Request method: POST

* Request URI: `https://livesaas.byteplusapi.com/?Action=AddLivePromotionsAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="4136eabc"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |


<span id="d4b8acb3"></span>
### Body parameters


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi). |
|AddLivePromotionsInfos |Array of [AddLivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi#AddLivePromotionsInfos) |Yes |A list of third\-party platforms to add for live stream promotion. |


<span id="0b56e510"></span>
#### **AddLivePromotionsInfos**


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Name |String |Yes |The platform name. The maximum length is 100 characters. |
|PushUrl |String |Yes |The push stream address. |


<span id="19bbf454"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=AddLivePromotionsAPI&Version=2020-06-01 
{ 
    "ActivityId": 1231231231, 
    "AddLivePromotionsInfos":[ 
        { 
             "Name": "Platform A", 
             "PushUrl": "rtmp://example" 
        } 
    ] 
} 
```


<span id="19cab44c"></span>
## Response

<span id="d13b0166"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|LivePromotionsInfos |Array of [LivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-addlivepromotionsapi#LivePromotionsInfos) |Details of the added platforms. |


<span id="46024ed2"></span>
#### **LivePromotionsInfos**


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Id |Integer |The platform ID. |
|Name |String |The platform name. |
|PushUrl |String |The push stream address. |
|Status |Integer |Indicates whether the platform is enabled for live stream promotion.<br><br>Valid values:<br><br><br>* `1`: Enabled.<br><br>* `2`: Disabled. |


<span id="96d00acd"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "AddLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
        "LivePromotionsInfos": [ 
              { 
                 "Id": 123, 
                 "Name": "Platform A", 
                 "PushUrl": "rtmp://example", 
                 "Status": 1 
              } 
          ] 
      } 
} 
```


<span id="a499fffb"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
