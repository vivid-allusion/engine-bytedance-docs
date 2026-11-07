---
title: "UpdatePullToPushAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatepulltopushapi"
---

The UpdatePullToPushAPI operation starts or stops pulling a stream for a live\-streaming activity from a specified URL.

<span id="request"></span>
## Request

<span id="details"></span>
### Details


* API operation: `UpdatePullToPushAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=UpdatePullToPushAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="query-string-parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|Action |Yes |String |API operation. |
|Version |Yes |String |The API version. Current version: `2020-06-01`. |


<span id="body-parameters"></span>
### Body parameters


|**Parameter Name** |**Required** |**Data Type** |**Description** |
|---|---|---|---|
|ActivityId |Yes |Integer |ID of the live\-streaming activity. |
|LineId |No |Integer |ID of the live stream. Call the `GetStreamsAPI` operation to get the stream ID for an activity. An activity can have multiple live streams. |
|PullStreamUrl |Yes |String |The URL of the stream to pull. |
|PullStreamStatus |Yes |Integer |Specifies whether to start or stop pulling the stream:<br><br><br>* 1: Start pulling the stream.<br><br>* 2: Stop pulling the stream. |
|PullStreamMode |No |Integer |Specifies whether to operate on the primary or standby stream:<br><br><br>* 0: Primary stream<br><br>* 1: Standby stream |


<span id="sample-request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdatePullToPushAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "PullStreamUrl": "https://xxxx/xxxx/xxxx.flv",
    "PullStreamStatus": 1
}
```


<span id="response"></span>
## Response

<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata":{
    "RequestId":"201806041104200100100232280022D30",
    "Action":"UpdatePullToPushAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
}
```
