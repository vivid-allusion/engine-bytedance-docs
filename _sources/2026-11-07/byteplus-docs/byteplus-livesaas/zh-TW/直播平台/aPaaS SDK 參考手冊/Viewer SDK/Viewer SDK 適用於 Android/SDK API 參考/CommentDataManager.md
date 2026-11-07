---
title: "CommentDataManager"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/commentdatamanager-zh-TW"
---

直播間訊息列表的管理類。

<span id="8856c66c"></span>
## 成員函式

<span id="6b085a19"></span>
### sendTextMessage

在直播間發送文字評論。

```Java
public void sendTextMessage(String text, ServiceApi.ResultCallback<SendCommentResponse> callback)
```


**輸入參數**


|名稱 |類型 |說明 |
|---|---|---|
|text |String |評論內容。 |
|callback |[ServiceApi.ResultCallback](https://docs.byteplus.com/docs/byteplus-livesaas/android-viewer-sdk-hui-hu-zh-TW#9fb2c3e6) |評論發送時觸發的回呼。回呼參數：[SendCommentResponse](https://docs.byteplus.com/docs/byteplus-livesaas/android-guan-zhong-duan-sdk-xing-bie-ding-yi-zh-TW#c0244d2f) |
