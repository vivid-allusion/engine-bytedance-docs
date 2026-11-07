---
title: "GetPageWatchDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getpagewatchdataapi"
---

Call this API to get the basic data of a live\-streaming activity, including page views, unique visitors, total visit duration, average visit duration per visitor, and page views per visitor. The data is updated every five minutes.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `GetPageWatchDataAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=GetPageWatchDataAPI&Version=2020-06-01`

* Quota: 1,000 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Integer |Yes |The ID of the live\-streaming activity. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/listactivityapi). |
|Source |Integer |No |Specifies the source of the data to return. Default value: `0`.<br><br>Valid values:<br><br><br>* `-1`: Returns data from all addresses.<br><br>* `0`: Returns data from the default address only.<br><br>* `1`: Returns data from address A only.<br><br>* `2`: Returns data from address B only.<br><br>* `3`: Returns data from address C only.<br><br>* `4`: Returns data from address D only. |


<span id="Sample request"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=GetPageWatchDataAPI&Version=2020-06-01&ActivityId=1231231231&Source=0
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|ActivityId |Integer |The ID of the live\-streaming activity. |
|PageClicks |Object of [PageClicks](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getpagewatchdataapi#PageClicks) |Contains the basic data for the live\-streaming activity. |


<span id="PageClicks"></span>
#### PageClicks


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|PV |Integer |Page views. |
|UV |Integer |Unique visitors. |
|TotalTime |Integer |The total visit duration, in minutes. |
|AvgTime |Float |The average visit duration per visitor, in minutes. |
|AvgNumber |Float |The average page views per visitor. |
|Pcu |Integer |The peak concurrent visitors. |


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetPageWatchDataAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result": {
        "ActivityId": 1231231231,
        "PageClicks": { 
            "PV": 33,
            "UV": 7, 
            "TotalTime": 844, 
            "AvgTime": 120.57142857142857, 
            "AvgNumber": 4.714285714285714,  
            "Pcu": 1  
        }
    }
}
```


<span id="c8a9401d"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
