---
title: "ActivityStatusModifyCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activitystatusmodifycallback"
---

When the status of a live room changes, BytePlus Live sends a GET request to your custom URL and passes the activity ID and the new status in the query string.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback.</div>


* <div data-tips="true" data-tips-type="tip">If BytePlus Live's callback server does not receive a response from your server five seconds after the request is sent, the request fails. BytePlus Live retries the failed request up to two more times at five\-second intervals.</div>



Sample request

```Plain
http://abc.com/test.do?ActivityID=123&EventType=ActivityStatusModifyCallBack&Status=1&Timestamp=1582518318&Sign=xxxx
```



|Parameter |Data Type |Description |
|---|---|---|
|ActivityID |String |The activity ID of the live room. |
|EventType |String |ActivityStatusModifyCallBack |
|Status |String |The status of the live room.<br><br>Valid values:<br><br><br>* `1`: Live<br><br>* `2`: Preview<br><br>* `3`: Playback<br><br>* `4`: Over |
|Timestamp |String |The time when the callback request is sent, in Unix timestamp format. Unit: seconds. |
|Sign |String |An encrypted string for authentication.<br><br>To obtain the `Sign` value, you must complete the following steps:<br><br><br>1. Concatenate a string in the `AccountSecretActivityIDEventTypeStatusTimestamp` format. Contact your sales representative to obtain the `AccountSecret` value.<br><br>2. Generate a 32\-character lowercase MD5 hash of the concatenated string.<br><br><br>In this example, assume that the `AccountSecret` value is `abc`. The concatenated string would then be `abc123ActivityStatusModifyCallBack11582518318`, and the resulting `Sign` value is `3d5fc13702c89c3c34c811ba8ac8fbbc`. |
