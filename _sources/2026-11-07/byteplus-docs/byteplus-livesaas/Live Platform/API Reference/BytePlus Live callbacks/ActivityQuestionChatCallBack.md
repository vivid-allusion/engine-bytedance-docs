---
title: "ActivityQuestionChatCallBack"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/activityquestionchatcallback"
---

When a user sends a question under the menu for Q&A, BytePlus Live sends a POST request to your custom URL and passes the question data in the body.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">You must first contact your BytePlus Live sales representative and provide a custom URL to receive the callback.</div>


* <div data-tips="true" data-tips-type="tip">If your server does not respond within five seconds, the request fails. BytePlus Live then retries the request two more times at five\-second intervals.</div>



Sample request

```JSON
POST /xxxxx HTTP/1.1
Header1: ...
Header2: ...
...

{
 "ActivityId": "172183121234",
 "EventType": "ActivityQuestionChatCallBack",
 "CreateTime": "1716795991",
 "QuestionMsgId": "5941305",
 "UserNickName": "Viewer A",
 "UserExternalId": "123874041231234",
 "Content": "Question A",
 "Sign": "5ad620fab18b8c78ab90f277aea8c562"
}
```



|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |String |`172183121234` |The activity ID of the live room. |
|EventType |String |`ActivityQuestionChatCallBack` |The event type. |
|CreateTime |String |`1716795991` |The time when the question was sent in Unix timestamp format. Unit: seconds. |
|QuestionMsgId |String |`5941305` |The question ID. |
|UserNickName |String |`Viewer A` |The nickname of the user who sent the question. |
|UserExternalId |String |`123874041231234` |The user's unique identifier from a third\-party platform. You can use this ID to identify the user within your organization for insights and data analysis.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is populated only when the user logs in to the live room. It is not available for users who join with only a nickname.</div><br> |
|Content |String |`Question A` |The content of the question. |
|Sign |String |`5ad620fab18b8c78ab90f277aea8c562` |The signature for verification.<br><br>To calculate the `Sign` value, you must complete the following steps:<br><br><br>1. Concatenate the values of the following parameters in order: `AccountSecret`, ActivityId, CreateTime, EventType, QuestionMsgId, UserExternalId, and UserNickName. Contact your sales representative to get the `AccountSecret` value.<br><br>2. Encrypt the concatenated string using the MD5 algorithm (32\-bit lowercase).<br><br><br>For example, if the `AccountSecret` is `abc`, the concatenated string is `abc1721831212341716795991ActivityQuestionChatCallBack5941305123874041231234Viewer A`, and the resulting `Sign` value is `5ad620fab18b8c78ab90f277aea8c562`. |
