---
title: "UpdateMediaOnlineStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatemediaonlinestatusapi"
---

Call this API to manage the online status of a playback for a live stream activity. You can call this API to release, withdraw, or remove a playback. Before performing this operation, you must first upload a video to serve as the playback.

<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `UpdateMediaOnlineStatusAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=UpdateMediaOnlineStatusAPI&Version=2020-06-01`

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
|ActivityId |Integer |Yes |Activity ID of the live stream. |
|MediaId |Integer |Yes |Video ID of the playback. |
|OnlineStatus |Integer |Yes |Status of the playback.<br><br>Valid values:<br><br><br>* `0`: Withdrawn from the viewing page. The playback is still bound to the live stream, and can be re\-released at any time.<br><br>* `1`: Released to the viewing page.<br><br>* `2`: Removed from the live stream, but still exists in the media library. You need to call [UploadReplayAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/uploadreplayapi) to bind it to the live stream before releasing it to the viewing page. |
|ForceReplayStatus |Boolean |No |Specifies whether to change the live stream status from **Preview** or **Over** to **Playback** after the playback is released.<br><br><br>* `true`: Changes the live stream status to **Playback**, allowing viewers to watch the released playback.<br><br>* `false`: Does not change the live stream status. |


<span id="Sample request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateMediaOnlineStatusAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "MediaId":3706016,   
    "OnlineStatus":1,
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
        "Action":"UpdateMediaOnlineStatusAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1", 
        "SystemTime":1655978114
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
