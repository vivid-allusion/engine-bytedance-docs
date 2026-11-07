---
title: "ActivityExplainProductCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityexplainproductcallBack"
---

BytePlus Live sends a POST request to your custom URL and passes information, such as the activity ID of the live room and the product information, in the body when a product in your live room is in any of the following situations:


* Pinned to the top of the menu and displayed in a floating window on the viewing page.

* Restored to its original position under the menu and no longer displayed in a floating window on the viewing page.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Use this callback if the feature of featuring multiple products is disabled. For more information about the feature, see <a href="https://docs.byteplus.com/docs/byteplus-livesaas/docs-adding-product-cards-to-your-live-stream">Managing product cards</a>.</div>


* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback notification.</div>


* <div data-tips="true" data-tips-type="tip">If BytePlus Live's callback server does not receive a response from your server five seconds after the request is sent, the request fails. BytePlus Live will retry the failed request two additional times, with five seconds between attempts.</div>



Sample request

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...
{
     "AccountId": "3000123487",
     "ActivityId": "1823745212348678",
     "CancelExplainExternalProductId": "120056",
     "CancelExplainProductId": "500067",
     "CancelExplainProductName": "Eggs",
     "EventType": "ActivityExplainProductCallBack",
     "ExplainExternalProductId": "780012",
     "ExplainProductId": "500028",
     "ExplainProductName": "Cake",
     "RequestUuid": "ActivityExplainProductCallBack - 1823712342538389",
     "Sign": "e11de95caf53091963fc92092dce9450",
     "Timestamp": "1739273121"
}
```



|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountId |String |`3000123487` |The account ID of your BytePlus account. You can get the ID by clicking your profile icon in the upper\-right corner of the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|ActivityId |String |`1823745212348678` |The activity ID of the live room. |
|EventType |String |`ActivityExplainProductCallBack` |The callback event type. The value is always `ActivityExplainProductCallBack`. |
|Timestamp |String |`1739273121` |The time when the callback request was sent, in Unix timestamp format. Unit: seconds. |
|Sign |String |`e11de95caf53091963fc92092dce9450` |The signature for verification.<br><br>To get the value of `Sign`, you must complete the following steps:<br><br><br>1. Concatenate the values of the AccountSecret, AccountId, ActivityId, EventType, and Timestamp parameters in that order. Contact your sales representative to get the `AccountSecret` value.<br><br>2. Generate a 32\-bit lowercase MD5 hash of the concatenated string.<br><br><br>In this example, assume that the `AccountSecret` value is `abc`. The concatenated string would then be `abc30001234871823745212348678ActivityExplainProductCallBack1739273121`, with the `Sign` value as `e11de95caf53091963fc92092dce9450`. |
|ExplainProductName |String |`Cake` |The name of the product being pinned to the top of the menu and displayed in a floating window. |
|ExplainProductId |String |`500028` |The ID of the product (product card) being pinned to the top of the menu and displayed in a floating window. |
|ExplainExternalProductId |String |`780012` |The external ID of the product being pinned to the top of the menu and displayed in a floating window. |
|CancelExplainProductName |String |`Eggs` |The name of the product that is restored to its original position under the menu and is no longer displayed in a floating window. |
|CancelExplainProductId |String |`500067` |The ID of the product (product card) that is restored to its original position under the menu and is no longer displayed in a floating window. |
|CancelExplainExternalProductId |String |`120056` |The external ID of the product that is restored to its original position under the menu and is no longer displayed in a floating window. |
|RequestUuid |String |`ActivityExplainProductCallBack - 1823712342538389` |The unique identifier for the callback request. |
