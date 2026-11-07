---
title: "CommentDataManager"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/commentdatamanager"
---

The management class for the message list in a live room.

<span id="8856c66c"></span>
## Member Functions

<span id="6b085a19"></span>
### sendTextMessage

Sends a text comment in the live room.

```Java
public void sendTextMessage(String text, ServiceApi.ResultCallback<SendCommentResponse> callback)
```


**Input Parameters**


|Name |Type |Description |
|---|---|---|
|text |String |The content of the comment. |
|callback |[ServiceApi.ResultCallback](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-callbacks#9fb2c3e6) |The callback triggered when the comment is sent. The callback parameters: [SendCommentResponse](https://docs.byteplus.com/docs/byteplus-livesaas/viewer-sdk-for-android-type-definitions#c0244d2f) |
