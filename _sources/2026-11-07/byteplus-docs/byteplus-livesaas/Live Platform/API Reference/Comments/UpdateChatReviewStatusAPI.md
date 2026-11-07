---
title: "UpdateChatReviewStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatechatreviewstatusapi"
---

This API turns on or turns off chat message moderation to have messages approved or blocked before they're sent to the audience of the live\-streaming activity.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `UpdateChatReviewStatusAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=UpdateChatReviewStatusAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|ActivityId |Yes |Integer |The unique identifier for the live\-streaming activity. |
|Status |Yes |Integer |Whether to turn on message moderation:<br><br><br>* 0: Turn off moderation<br><br>* 1: Turn on moderation |


<span id="Sample request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateChatReviewStatusAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "Status" : 1,
}
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
     "RequestId" : "201806041104200100100232280022D30",
     "Action" : "TopChatAPI",
     "Version" : "2020-06-01",
     "Service" : "livesaas",
     "Region" :  "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
