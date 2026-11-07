---
title: "VideoTrackComplete"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-videotrackcomplete"
---

This article provides a description of the event parameters and includes examples of the `VideoTrackComplete` event.

<span id="33345951"></span>
## Event description

After configuring the `VideoTrackComplete` event notification, you will receive a notification when the video editing task is complete. For configuration details, please refer to [Event notification overview](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-).

<span id="cce813a5"></span>
## Parameter


|**Parameter** |**Type** |**Sample Value** |**Required** |**Description** |
|---|---|---|---|---|
|RequestId |String |`202405060***0CF1866` |Yes |The unique ID for the request |
|Version |String |`1.0` |Yes |Callback version |
|EventType |String |`VideoTrackComplete` |Yes |The name of the event |
|EventTime |String |`2024-05-06T09:49:33Z` |Yes |The UTC time when the event occurred, accurate to the second |
|Data |[Data](https://docs.byteplus.com/docs/byteplus-vod/docs-videotrackcomplete#af4e4f41) |`-` |Yes |The callback content in JSON format |


<span id="af4e4f41"></span>
### Data


|**Parameter** |**Type** |**Description** |
|---|---|---|
|CallbackArgs |String |Pass\-through information. This parameter is returned only if you set the `CallbackArgs` parameter to pass custom data when submitting the editing task. |
|PosterUri |String |The cover image URI of the video. |
|ReqId |String |The request ID of the editing task. |
|SpaceName |String |The VOD space name. |
|Status |String |Editing status. Valid values are as follows:<br><br><br>* `Success`: Task succeeded.<br><br>* `Failed`: Task failed. |
|StoreUri |String |The storage URI of the video. |
|FileName |String |The file path of the video. |
|TaskId |String |The ID of the computing task. This is different from `ReqId`. |
|Vid |String |The video ID. |
|Message |String |Information about the task. This parameter is returned only when `Status` is `Failed` and contains the task error message. For more details, see [Video editing error codes](https://docs.byteplus.com/docs/byteplus-vod/video_editing_error_codes). |
|SubVid |Array of [SubVidDetail](https://docs.byteplus.com/docs/byteplus-vod/docs-videotrackcomplete#7a46eee5) |An array of video details. This parameter is returned only when an editing task, such as splitting, produces multiple output videos. |


<span id="7a46eee5"></span>
### SubVidDetail


|**Parameter** |**Type** |**Description** |
|---|---|---|
|Vid |String |The video ID. |
|PosterUri |String |The cover image URI of the video. |


<span id="d5dd3950"></span>
## Example

```JSON
{
  "Data": {
    "CallbackArgs": "abc",
    "PosterUri": "tos-vod-******d4e320a842d5ac76078c1fa48f51",
    "ReqId": "e070c521d782***c8ddea1876",
    "SpaceName": "test",
    "Status": "Success",
    "StoreUri": "",
    "FileName": "",
    "TaskId": "2049:UhA***",
    "Vid": "v0c7b4g7***q6rb8bd1460"
  },
  "EventTime": "2022-10-25 11:12:13.502796743 +0800 CST m=+50034.619039680",
  "EventType": "VideoTrackComplete",
  "RequestId": "0216666674315******000ffff0ae1858ae05e61",
  "Version": "1.0"
}
```
