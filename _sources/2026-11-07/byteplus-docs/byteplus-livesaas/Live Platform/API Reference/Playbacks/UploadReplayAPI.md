---
title: "UploadReplayAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-uploadreplayapi"
---

Call this API to bind a video to a live\-streaming activity as the playback. You must first upload the video to the media library before performing the operation.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `UploadReplayAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=UploadReplayAPI&Version=2020-06-01`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2020-06-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|ActivityId |Integer |Yes |The ID of the live stream activity. |
|Media |Array |Yes |Information about the video. |


<span id="Media"></span>
#### **Media**


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Name |String |Yes |Name of the video in the media library. |
|Vid |String |Yes |ID of the video in the media library. |


<span id="Sample request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=UploadReplayAPI&Version=2020-06-01
{
  "ActivityId": 178465844575,
  "Media": {
    "Name": "123",
    "Vid": "id123"
  }
}
```


<span id="Response"></span>
## Response

<span id="Sample response"></span>
### Sample response

```JSON
{
   "ResponseMetadata":{
     "RequestId":"201806041104200100100232280022D30",
     "Action":"UploadReplayAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1",
     "SystemTime":1656067132
  }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
