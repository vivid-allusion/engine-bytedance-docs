---
title: "CheckinStatusModifyCallback"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/CheckinStatusModifyCallback"
---

When check\-in events occur, such as check\-in creation, deletion, sending, or the deadline being reached, BytePlus Live sends a POST request to your custom URL and passes the live room ID and updated check\-in status in the body.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback notification.</div>


* <div data-tips="true" data-tips-type="tip">If BytePlus Live's callback server does not receive a response from your server five seconds after the request is sent, the request fails. BytePlus Live retries the failed request two more times at five\-second intervals.</div>



Sample request

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "ActivityId": "1840847565136997",
    "CheckInId": "checkIn1853040247525505",
    "EventType": "CheckinStatusModifyCallback",
    "RequestUuid": "CheckinStatusModifyCallback-1853040247354881",
    "Sign": "c26ca0fe5c09f56222d22e9525bd3739",
    "Status": "Init",
    "SubAccountName": "admin@example.com",
    "Timestamp": "1774933967"
}
```



|Name |Data Type |Description |
|---|---|---|
|ActivityId |String |The activity ID of the live room. |
|CheckInId |String |Check\-in ID. |
|EventType |String |The event type for the callback notification, with a fixed value of `CheckinStatusModifyCallback`. |
|RequestUuid |String |The unique identifier for the callback request. |
|Sign |String |The signature for verification.<br><br>To get the value of `Sign`, you must complete the following steps:<br><br><br>1. Concatenate the string in the `AccountSecretActivityIdCheckInIdEventTypeStatusTimestamp` format. Contact your sales representative to get the `AccountSecret` value.<br><br>2. Hash the concatenated string using MD5 (32\-bit lowercase). |
|Status |String |Check\-in status. Valid values are as follows:<br><br><br>* `Init`: Created<br><br>* `Export`: Sent<br><br>* `Deadline`: Ended<br><br>* `Delete`: Deleted<br><br>* `Retract`: Withdrawn |
|SubAccountName |String |The account used to create the live room. The parameter value `admin@bytedance.com` indicates that the live room is created by the BytePlus account. |
|Timestamp |String |The time the callback request was sent, in Unix timestamp format. Unit: seconds. |
