---
title: "UpdateLoopVideoStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateloopvideostatusapi"
---

Call this API to enable or disable the loop play feature for a specified live\-streaming activity.

<span id="request"></span>
## Request

<span id="details"></span>
### Details


* API operation: `UpdateLoopVideoStatusAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoStatusAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="query-string-parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The version of this API operation. Current version: `2020-06-01`. |


<span id="body-parameters"></span>
### Body parameters


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|ActivityId |Yes |Integer |ID of the live\-streaming activity. |
|IsStartLoopVideo |Yes |Integer |Specifies whether to start or stop loop play:<br><br><br>* 1: Start. When loop play starts, the live\-streaming activity also starts.<br><br>* 2: Stop. When loop play stops, the live\-streaming activity also stops. |
|LineId |Yes |Integer |ID of the live stream. |


<span id="sample-request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoStatusAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "IsStartLoopVideo":1,
    "LineId":123
}
```


<span id="response"></span>
## Response

<span id="response-schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Status |Boolean |Indicates whether the loop play status was updated successfully. |


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata":{
    "RequestId":"2018060411042001001002322800xxxx",
    "Action":"UpdateLoopVideoStatusAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
  "Result":{
   "Status":true
}
}
```
