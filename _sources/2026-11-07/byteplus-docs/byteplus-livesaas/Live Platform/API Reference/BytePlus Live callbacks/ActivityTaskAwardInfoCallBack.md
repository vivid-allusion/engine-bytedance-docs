---
title: "ActivityTaskAwardInfoCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack"
---

When a user participates in a watch time\-based lucky draw and a prize is won, BytePlus Live sends a POST request to your custom URL and passes the live room ID, prize information, and winner information in the body.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback notification.</div>


* <div data-tips="true" data-tips-type="tip">If BytePlus Live's callback server does not receive a response from your server five seconds after the request is sent, the request fails. BytePlus Live retries the failed request two more times at five\-second intervals.</div>


* <div data-tips="true" data-tips-type="tip">Each callback can contain information for up to 1,000 winners. If the winner's information for a prize exceeds this limit, BytePlus Live will send multiple callback messages.</div>



Sample request

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
    "AccountId": "200000****",
    "ActivityId": "185304015484****",
    "ActivityName": "Live room A",
    "AwardItemAmounts": "99999",
    "AwardItemId": "17012",
    "AwardItemNum": "1323421123",
    "AwardItemType": "3",
    "AwardName": "Prize A",
    "DeliveryMethod": "2",
    "EventType": "ActivityTaskAwardInfoCallBack",
    "RequestUuid": "ActivityTaskAwardInfoCallBack-1853040247559201",
    "Sign": "5b81b108bee1e6aba81412a2e8802a3a",
    "Timestamp": "1774943600",
    "UserInfos": [
        {
            "ExternalID": "7613760946837832760",
            "Extra": "",
            "IsPriorityUser": "",
            "NickName": "User A",
            "Telephone": "185****3186",
            "UserAccessIP": "AwardItemAmounts",
            "UserAgent": "Intel Mac OS X 10_15_7",
            "UserID": "185304024682****"
        }
    ]
}
```



|Parameter |Type |Description |
|---|---|---|
|AccountID |String |The account ID of your BytePlus account. You can get the ID by clicking the portrait in the upper\-right corner of the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|ActivityId |String |The activity ID of the live room. |
|ActivityName |String |The name of the live room. |
|AwardItemAmounts |String |Number of points each winning viewer receives. The value range is [0,99999].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>AwardItemType</code> is set to 3 and <code>DeliveryMethod</code> is set to 2.</div><br> |
|AwardItemId |String |Prize ID. |
|AwardItemNum |String |Batch number for points prizes. The length ranges from 1 to 256 characters. You can use this batch number to identify company points and distribute them to viewers. |
|AwardItemType |String |Prize type. Valid values are as follows:<br><br><br>* `1`: Physical prize<br><br>* `2`: Virtual prize<br><br>* `3`: Custom prize<br><br>* `4`: Voucher prize |
|AwardName |String |Prize name. |
|DeliveryMethod |String |The type of custom prize. Values:<br><br><br>* `1`: Coupon<br><br>* `2`: Points<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>AwardItemType</code> is set to 3.</div><br> |
|EventType |String |The event type for the callback notification, with a fixed value of `ActivityTaskAwardInfoCallBack`. |
|RequestUuid |String |The unique identifier for the callback request. |
|Sign |String |The signature for verification.<br><br>To get the value of `Sign`, you must complete the following steps:<br><br><br>1. Concatenate the corresponding parameter values in the `AccountSecretAccountIdActivityIdEventTypeTimestamp` format. Contact your sales representative to get the `AccountSecret` value.<br><br>2. Encrypt the concatenated string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the AccountSecret value is abc. The concatenated string would then be abc30001234871823745212348678ActivityAwardInfoCallBack1739273121, and the Sign value is the corresponding MD5 hash. |
|Timestamp |String |The time when the callback request was sent, in Unix timestamp format. Unit: seconds. |
|UserInfos |Array of [UserInfos](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityTaskAwardInfoCallBack#fd57e72d) |Information about the winners. |


<span id="fd57e72d"></span>
## UserInfos


|Name |Data Type |Description |
|---|---|---|
|UserID |String |The user ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For anonymous users who join the live room without logging in, the user ID is <code>0</code>.</div><br> |
|ExternalID |String |The user's unique identifier on third\-party platforms. You can use this ID to identify the user within your organization, enabling user insights and data analysis as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is populated only for users who authenticate through an integrated identity system, not for guest users who log in by providing only a nickname.</div><br> |
|Extra |String |Your extra parameter, corresponding to the extra parameter in the viewing page address. For example, `https://live.byteplus.com/6688/322****?extra=xxx`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not populated when using the Viewer SDK for iOS or Android.</div><br> |
|IsPriorityUser |String |Whether the user is prioritized for winning. Valid values are as follows:<br><br><br>* `0`: No<br><br>* `1`: Yes |
|NickName |String |The nickname of the user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter has a value only if the user logs in to the live room.</div><br> |
|UserAccessIP |String |The IP address of the user. |
|UserAgent |String |The device type used by the user. |
|Telephone |String |The phone number used to book the live stream.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not populated when using the Viewer SDK for iOS or Android.</div><br> |
