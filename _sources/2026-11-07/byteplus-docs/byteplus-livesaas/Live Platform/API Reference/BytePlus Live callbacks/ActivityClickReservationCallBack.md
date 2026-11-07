---
title: "ActivityClickReservationCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityclickreservationcallBack"
---

When a user clicks **Book** on the viewing page to book a live stream, BytePlus Live sends a POST request to your custom URL and passes the user information and live room information in the body.

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
     "AccountId": "200****914",
     "ActivityId": "1721****1234",
     "EventType": "ActivityClickReservationCallBack",
     "LiveTime": "1721099280",
     "ActivityName": "Live room A",
     "RequestUuid": "ActivityClickReservationCallBack-180469199****475",
     "ViewUrl": "https://live.byteplus.com/6688/322****",
     "Timestamp": "1721099426",
     "Sign": "b96c2ac3d6aed7557a****8bec3374fa",
     "UserInfo":{
        "ExternalId": "16057****",
        "Extra": "",
        "NickName": "Viewer A",
        "ReservationTel": "150****1345",
        "UserAccessIP": "43.*.*.143",
        "UserAgent": "Intel Mac OS X 10_15_7",
        "UserId": "17386867****4142"
                }
}
```



|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountId |String |`200****914` |The ID of your BytePlus account. You can find the ID by clicking your profile icon in the upper\-right corner of the BytePlus Live console. |
|ActivityId |String |`1721****1234` |The activity ID of the live room. |
|EventType |String |`ActivityClickReservationCallBack` |The event type. |
|Timestamp |String |`1721099426` |The time to send the callback request, in Unix timestamp format. Unit: seconds. |
|Sign |String |`b96c2ac3d6aed7557a****8bec3374fa` |The signature for verification.<br><br>To get the value of `Sign`, you must complete the following steps:<br><br><br>1. Concatenate the required values in the following order: AccountSecret, AccountId, ActivityId, EventType, and Timestamp. Contact your sales representative to get the AccountSecret value.<br><br>2. Generate a 32\-bit lowercase MD5 hash of the concatenated string.<br><br><br>In this example, assume that the `AccountSecret` value is `abc`. The concatenated string would then be `abc200****9141721****1234ActivityClickReservationCallBack1721099426`, with the `Sign` value as `b96c2ac3d6aed7557a****8bec3374fa`. |
|ActivityName |String |`Live room A` |The name of the live room. |
|ViewUrl |String |`https://live.byteplus.com/6688/322****` |The URL of the live room's viewing page. |
|LiveTime |String |`1721099426` |The scheduled start time of the live stream, in Unix timestamp format. Unit: seconds. |
|RequestUuid |String |`ActivityClickReservationCallBack-180469199****475` |The unique identifier for the callback request. |
|UserInfo |[UserReservationInfo](https://docs.byteplus.com/docs/byteplus-livesaas/activityclickreservationcallBack#30b07c7a) |`-` |The information of the user who clicks **Book** on the viewing page to book a live stream. |


<span id="30b07c7a"></span>
### UserReservationInfo


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|UserId |String |`17386867****4142` |The user ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the user does not log in to the live room by entering the nickname or by other methods, the user ID is <code>0</code>.</div><br> |
|ExternalId |String |`16057****` |The unique identifier on third\-party platforms of the user. You can use this ID to identify the user within your organization, enabling user insights and data analysis as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is populated only for users who authenticate through an integrated identity system, not for guest users who log in by only providing a nickname.</div><br> |
|Extra |String |`abc` |Your extra parameter, corresponding to the extra parameter in the viewing page address. For example, `https://live.byteplus.com/6688/322****?extra=xxx`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not populated when using the Viewer SDK for iOS or Android.</div><br> |
|NickName |String |`Viewer A` |The nickname of the user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameter has a value only when the user logs in to the live room.</div><br> |
|UserAccessIP |String |`43.*.*.143` |The IP address of the user. |
|UserAgent |String |`Intel Mac OS X 10_15_7` |The device type used by the user. |
|ReservationTel |String |`150****1345` |The phone number used to book the live stream.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not populated when using the Viewer SDK for iOS or Android.</div><br> |
