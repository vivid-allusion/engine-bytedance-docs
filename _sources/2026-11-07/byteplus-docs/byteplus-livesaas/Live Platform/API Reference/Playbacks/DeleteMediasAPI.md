---
title: "DeleteMediasAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletemediasapi"
---

Deletes at most 100 videos at a time from the playback list of a live\-streaming activity.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a video is included in the playback lists of multiple activities, deleting it removes it from all of those lists.</div>


* <div data-tips="true" data-tips-type="tip">Deleted videos are permanently removed from BytePlus Live and cannot be restored.</div>


* <div data-tips="true" data-tips-type="tip">If the video being deleted is the active playback on the viewing page, the activity status changes to <strong>Over</strong> after the deletion. However, if the activity is configured to automatically release the playback after the live stream ends and there is more than one video on the playback list of the activity, the next video in the list will start playing after the deletion.</div>



<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `DeleteMediasAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=DeleteMediasAPI&Version=2019-10-10`

* Quota: 120 queries per minute per account


<span id="Query string parameters"></span>
### Query string parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Action |String |Yes |API operation. |
|Version |String |Yes |The version of this API operation. Current version: `2019-10-10`. |


<span id="Body parameter"></span>
### Body parameter


|**Parameter Name** |**Data Type** |**Required** |**Description** |
|---|---|---|---|
|Vids |Array of String |Yes |The IDs of videos to be deleted. You can specify at most 100 IDs. |


<span id="Sample request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteMediasAPI&Version=2019-10-10
{
    "Vids": [
        "v0c251g7007abc1",
        "v0c251g7007abc2"
    ]
}
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Success |Boolean |Indicates whether the deletion is successful.<br><br><br>* `true`: All of the videos are deleted.<br><br>* `false`: One or more videos failed to be deleted. |
|FailedList |Array of String |The IDs of videos that failed to be deleted. This parameter is returned when the value of `Success` is `false`. |


<span id="Sample response"></span>
### **Sample response**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221205033247010251197018041E783F",
        "Action": "DeleteMediasAPI",
        "Version":"2019-10-10",
        "Service":"livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1670211167
    },
    "Result": {
        "Success": false,
        "FailedList": ["v0c251g7007abc1"]
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
