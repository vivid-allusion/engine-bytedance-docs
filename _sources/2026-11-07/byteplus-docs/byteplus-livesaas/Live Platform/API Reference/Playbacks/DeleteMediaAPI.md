---
title: "DeleteMediaAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-deletemediaapi"
---

Deletes a video from the playback list of a live\-streaming activity.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If a video is included in the playback lists of multiple activities, deleting it removes it from all of those lists.</div>


* <div data-tips="true" data-tips-type="tip">A deleted video is permanently removed from BytePlus Live and cannot be restored.</div>


* <div data-tips="true" data-tips-type="tip">If the deleted video was being shown as a playback, the activity status changes to <strong>Over</strong>. However, if the activity is configured to automatically play the next video and other videos are in the playback list, the next video is played instead.</div>



<span id="Request"></span>
## Request

<span id="Details"></span>
### Details


* API operation: `DeleteMediaAPI`

* Request method: POST

* Request URI: `http://livesaas.byteplusapi.com/?Action=DeleteMediaAPI&Version=2019-10-10`

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
|Vid |String |Yes |The ID of the video to be deleted. |


<span id="Sample request"></span>
### Sample request

```JSON
POST http://livesaas.byteplusapi.com/?Action=DeleteMediaAPI&Version=2019-10-10
{
    "Vid": "v0c251g7007abc1"
}
```


<span id="Response"></span>
## Response

<span id="Response schema"></span>
### Response schema


|**Parameter Name** |**Data Type** |**Description** |
|---|---|---|
|Success |Boolean |Indicates whether the deletion is successful.<br><br><br>* `true`: The video is deleted.<br><br>* `false`: The deletion failed. |


<span id="Sample response"></span>
### **Sample response**

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221205033247010251197018041E783F",
        "Action": "DeleteMediaAPI",
        "Version":"2019-10-10",
        "Service":"livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1670211167
    },
    "Result": {
        "Success": true
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
