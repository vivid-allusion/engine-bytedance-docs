---
title: "EmptyChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-emptychatapi"
---

Call this API to clear all the chat messages of a live\-streaming activity.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `EmptyChatAPI`

* Request method: GET

* Request URI: `http://livesaas.byteplusapi.com/?Action=EmptyChatAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Yes |Integer |ID of the live\-streaming activity. |


<span id="Sample request"></span>
### Sample request

```JSON
Get http://livesaas.byteplusapi.com/?Action=EmptyChatAPI&Version=2020-06-01&ActivityId=1231231231&ChatId=0&Count=20&PollingType=0
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Status |Boolean |Result of the operation:<br><br><br>* true: Success<br><br>* false: Failure |


<span id="Sample response"></span>
### Sample response

The following is a sample response for a successful request:

```JSON
{
     "ResponseMetadata" :{
         "RequestId" : "202201201826170101501312091D1C09D2" ,
         "Action" : "EmptyChatAPI" ,
         "Version" : "2020-06-01" ,
         "Service" : "livesaas" ,
         "Region" : "ap-singapore-1" 
    },
     "Result" :{
         "Status" : true
    }
}
```
