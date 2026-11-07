---
title: "SilenceUserAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-silenceuserapi"
---

Call this API to manage user chat permissions in a live\-streaming activity. You can call this API to either prohibit a specific user from posting messages or to lift a previously imposed prohibition.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `SilenceUserAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=SilenceUserAPI&Version=2020-06-01`

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
|ActivityId |Yes |Integer |ID of the live\-streaming activity. |
|UserId |Yes |Integer |The ID of the user to silence. |
|Status |Yes |Boolean |Whether to prohibit the user from sending chat messages:<br><br><br>* true: Silences the user.<br><br>* false: Unsilences the user. |


<span id="Sample request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=SilenceUserAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "UserId" : 1245231,
     "Status" : true
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
  "ResponseMetadata":{
  "RequestId":"201806041104200100100232280022D30",
  "Action":"SilenceUserAPI",
  "Version":"2020-06-01",
  "Service":"livesaas",
  "Region": "ap-singapore-1"
 },
  "Result": {
  "Status": true
 }
}
```
