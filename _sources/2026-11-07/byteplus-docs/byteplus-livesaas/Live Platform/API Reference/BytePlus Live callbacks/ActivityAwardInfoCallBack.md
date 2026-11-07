---
title: "ActivityAwardInfoCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/ActivityAwardInfoCallBack"
---

When a real\-time lucky draw is held, BytePlus Live sends a POST request to your custom URL and passes data such as the live room ID, prize information, and winner information in the body.

If the real\-time lucky draw contains multiple prizes, BytePlus Live will send a separate callback message for each prize. Each callback can contain information for up to 2,000 winners. If the winner's information for a prize exceeds this limit, BytePlus Live will send multiple callback messages.

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
    "AccountID": "200000****",
    "ActivityID": "182573526550****",
    "ActivityName": "Live Room A",
    "AwardItemAmounts": "",
    "AwardItemId": "10****",
    "AwardItemNum": "",
    "AwardItemType": "2",
    "AwardName": "Prize A",
    "DeliveryMethod": "",
    "EventType": "ActivityAwardInfoCallBack",
    "RequestUuid": "ActivityAwardInfoCallBack-182572318444****",
    "Sign": "c7594afe578431086bf1c56eff54****",
    "Timestamp": "1741158904",
    "UserInfos": [
        {
            "ExternalID": "78989827691****",
            "Extra": "",
            "IsPriorityUser": "0",
            "NickName": "Audience A",
            "Telephone": "1803738****",
            "UserAccessIP": "fdbd:dc0********",
            "UserAgent": "Windows 10",
            "UserID": "182137188********"
        }
    ]
}
```



|Parameter |Type |Description |
|---|---|---|
|AccountID |String |The account ID of your BytePlus account. You can get the ID by clicking the portrait in the upper\-right corner of the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|ActivityID |String |The activity ID of the live room. |
|EventType |String |The event type for the callback notification, with a fixed value of `ActivityAwardInfoCallBack`. |
|Timestamp |String |The time when the callback request was sent, in Unix timestamp format. Unit: seconds. |
|Sign |String |The signature for verification.<br><br>To get the value of `Sign`, you must complete the following steps:<br><br><br>1. Concatenate the corresponding parameter values in the `AccountSecretAccountIDEventTypeTimestamp` format. Contact your sales representative to get the `AccountSecret` value.<br><br>2. Encrypt the concatenated string in MD5 (32\-bit lowercase).<br><br><br>In this example, assume that the AccountSecret value is abc. The concatenated string would then be abc30001234871823745212348678ActivityAwardInfoCallBack1739273121, with the Sign value as the corresponding MD5 hash. |
|ActivityName |String |The name of the live room. |
|AwardItemId |String |Prize ID. |
|RequestUuid |String |The unique identifier for the callback request. |
|AwardName |String |Prize name. |
|AwardItemType |String |Prize type. Valid values are as follows:<br><br><br>* `1`: Physical prize<br><br>* `2`: Virtual prize<br><br>* `3`: Custom prize<br><br>* `4`: Voucher prize |
|DeliveryMethod |String |Category of a custom prize. Values:<br><br><br>* `1`: Coupon<br><br>* `2`: Points<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>AwardItemType</code> is set to 3.</div><br> |
|AwardItemNum |String |Batch number for points prizes. The length ranges from 1 to 256 characters. You can use this batch number to identify company points and distribute them to viewers. |
|AwardItemAmounts |String |Number of points each winning viewer receives. The value range is [0,99999].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect when <code>AwardItemType</code> is set to 3 and <code>DeliveryMethod</code> is set to 2.</div><br> |
|UserInfos |Array of [UserAwardInfo](https://docs.byteplus.com/docs/byteplus-livesaas/ActivityAwardInfoCallBack#e727d716) |Information about the winners. |


<span id="e727d716"></span>
### UserAwardInfo


|Name |Data Type |Description |
|---|---|---|
|UserId |String |The user ID.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the user does not log in to the live room by providing a nickname or using another method, the user ID is <code>0</code>.</div><br> |
|ExternalID |String |The user's unique identifier on third\-party platforms. You can use this ID to identify the user within your organization, enabling user insights and data analysis as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is populated only for users who authenticate through an integrated identity system, not for guest users who log in by providing only a nickname.</div><br> |
|Extra |String |An extra parameter that corresponds to the extra parameter in the viewing page URL. For example, `https://live.byteplus.com/6688/322****?extra=xxx`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is not populated when using the Viewer SDK for iOS or Android.</div><br> |
|NickName |String |The nickname of the user.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is populated only when the user logs in to the live room.</div><br> |
|UserAccessIP |String |The IP address of the user. |
|UserAgent |String |The device type used by the user. |
|Telephone |String |The mobile number used by the user to log in to the live room. |
|IsPriorityUser |String |Whether the user is prioritized for winning. Valid values are as follows:<br><br><br>* `0`: No<br><br>* `1`: Yes |
