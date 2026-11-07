---
title: "ActivityModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitymodifycallBack"
---

When a live room is created or deleted, BytePlus Live sends a GET request to your custom URL and passes the activity ID and the operation performed on the live room in the query string.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback.</div>


* <div data-tips="true" data-tips-type="tip">If your server does not respond within five seconds, the request fails. BytePlus Live then retries the request two more times at five\-second intervals.</div>



Sample request

```Plain
http://abc.com/test.do?ActivityID=123&EventType=ActivityModifyCallBack&Type=1&Timestamp=1582518318&Sign=xxxx
```



|Parameter |Data Type |Description |
|---|---|---|
|ActivityID |String |The activity ID of the live room. |
|EventType |String |ActivityModifyCallBack |
|Timestamp |String |The time the callback request was sent, represented as a Unix timestamp in seconds. |
|Type |String |Indicates whether the live room is created or deleted.<br><br>Valid values:<br><br><br>* `1`: Created<br><br>* `2`: Deleted |
|Sign |String |An encrypted string for authentication.<br><br>To obtain the `Sign` value, you must complete the following steps:<br><br><br>1. Concatenate a string in the `AccountSecretActivityIDEventTypeStatusTimestamp` format. Contact your sales representative to obtain the `AccountSecret` value.<br><br>2. Generate a 32\-character lowercase MD5 hash of the concatenated string.<br><br><br>In this example, assume that the `AccountSecret` value is `abc`. The concatenated string would then be `abc123ActivityModifyCallBack11582518318`, and the resulting `Sign` value is `3d5fc13702c89c3c34c811ba8ac8fbbc`. |
