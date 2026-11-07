---
title: "ActivityAutoReplayCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityautoreplaycallback"
---

When a video is generated as a playback of a live room, BytePlus Live sends a POST request to your custom URL and passes the activity ID and the video ID in the body.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback.</div>


* <div data-tips="true" data-tips-type="tip">If BytePlus Live's callback server does not receive a response from your server within five seconds, the request times out. BytePlus Live will retry the failed request two more times at five\-second intervals.</div>



Sample request

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityID": "123",
 "EventType": "ActivityAutoReplayCallBack",
 "Sign": "xxxx",
 "Timestamp": "1582518318",
 "LiveStartTime": "1751520600",
 "LiveEndTime": "1751526000",
 "Vid": "v0c251g7007abc1"
}
```



|Parameter |Data Type |Description |
|---|---|---|
|ActivityID |String |The activity ID of the live room. |
|EventType |String |ActivityAutoReplayCallBack |
|Vid |String |The ID of the generated video. |
|Timestamp |String |The time the callback request was sent, in Unix timestamp format. Unit: seconds. |
|LiveStartTime |String |The start time of the live stream corresponding to the playback video, in Unix timestamp format. Unit: seconds.<br><br>For example, if a live stream starts at 2025\-07\-03 13:30:00 and ends at 2025\-07\-03 15:00:00, the value for this parameter is `1751520600`. |
|LiveEndTime |String |The end time of the live stream corresponding to the playback video, in Unix timestamp format. Unit: seconds.<br><br>For example, if a live stream starts at 2025\-07\-03 13:30:00 and ends at 2025\-07\-03 15:00:00, the value for this parameter is `1751526000`. |
|Sign |String |An encrypted string for authentication.<br><br>To obtain the `Sign` value, you must complete the following steps:<br><br><br>1. Concatenate the `AccountSecret`, `ActivityID`, `Timestamp`, and `Vid` values into a single string. Contact your sales representative to obtain the AccountSecret value.<br><br>2. Encrypt the concatenated string using the MD5 algorithm (32\-bit lowercase).<br><br><br>For example, if the `AccountSecret` is abc, the concatenated string is `abc1231582518318v0c251g7007abc1`. The resulting `Sign` value is `884c08f1458e39888fb9ba4f51406c7a`. |
