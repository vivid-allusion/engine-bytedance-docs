---
title: "ActivityBasicConfigModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitybasicconfigmodifycallback"
---

When the basic configurations of a live room change, BytePlus Live sends a POST request to your custom URL and passes the activity ID and the basic configurations in the body.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback.</div>


* <div data-tips="true" data-tips-type="tip">If BytePlus Live's callback server does not receive a response from your server five seconds after the request is sent, the request fails. BytePlus Live will retry the failed request two additional times, with five seconds between attempts.</div>



Sample request

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityID": "123",
 "EventType": "ActivityBasicConfigModifyCallBack",
 "Timestamp": "1582518318",
 "Sign": "xxxx",
 "Name": "Live Room A",
 "Announcement": "Live Room A",
 "CoverImage": "//gjr78lqtd0-image.image",
 "ViewUrl": "https://live.byteplus.com/7420/1234",
 "LiveTime": "1583070536"
}
```



|Parameter |Data Type |Description |
|---|---|---|
|ActivityID |String |The activity ID of the live room. |
|EventType |String |ActivityBasicConfigModifyCallBack |
|Timestamp |String |The timestamp of the callback request, in Unix format. Unit: seconds. |
|Sign |String |An encrypted string for authentication.<br><br>To obtain the `Sign` value, you must complete the following steps:<br><br><br>1. Concatenate a string in the `AccountSecretActivityIDAnnouncementCoverImageEventTypeLiveTimeNameTimestampViewUrl` format. Contact your sales representative to obtain the `AccountSecret` value.<br><br>2. Generate a 32\-character lowercase MD5 hash of the concatenated string.<br><br><br>In this example, assume that the `AccountSecret` value is `abc`. The concatenated string would then be `abc123Live Room A//gjr78lqtd0-image.imageActivityBasicConfigModifyCallBack1583070536Live Room A1582518318https://live.byteplus.com/7420/1234`, and the resulting `Sign` value is `85c1ba868bf4e30b6055ccfbbdd7bc3a`. |
|Name |String |The name of the live room. |
|Announcement |String |The description of the live room. |
|CoverImage |String |The URL of the live room's cover image. |
|ViewUrl |String |The URL of the live room's viewing page. |
|LiveTime |String |The time when the live stream starts in Unix timestamp format. Unit: seconds.<br><br>This time may not reflect the actual start time of the live stream. |
