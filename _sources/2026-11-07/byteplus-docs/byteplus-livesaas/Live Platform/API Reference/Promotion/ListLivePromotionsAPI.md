---
title: "ListLivePromotionsAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listlivepromotionsapi"
---

Call this API to get the list of third\-party platforms for live stream promotion that have been added to a specific live\-streaming activity.

<span id="ac70d9a3"></span>
## Request

<span id="8f3ec89a"></span>
### Details


* API operation: `ListLivePromotionsAPI`

* Request method: GET

* Request URI: `https://livesaas.byteplusapi.com/?Action=ListLivePromotionsAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="2fdeadeb"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling the [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi) operation. |


<span id="63c837a9"></span>
### Sample request

```JSON
Get https://livesaas.byteplusapi.com/?Action=ListLivePromotionsAPI&Version=2020-06-01&ActivityId=1231231231 
```


<span id="33f74cf8"></span>
## Response

<span id="55db58b6"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|LivePromotionsInfos |Array of [LivePromotionsInfos](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listlivepromotionsapi#LivePromotionsInfos) |A list of live stream promotion platforms. |


<span id="13a56d96"></span>
#### **LivePromotionsInfos**


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Id |Integer |The platform ID. |
|Name |String |The platform name. |
|PushUrl |String |The push stream address. |
|Status |Integer |Specifies whether the platform is enabled for live stream promotion.<br><br>Valid values:<br><br><br>* `1`: Enabled.<br><br>* `2`: Disabled. |


<span id="b6394dd7"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "ListLivePromotionsAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656419846 
    }, 
    "Result": {
            "LivePromotionsInfos":[ 
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


<span id="b117450f"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
