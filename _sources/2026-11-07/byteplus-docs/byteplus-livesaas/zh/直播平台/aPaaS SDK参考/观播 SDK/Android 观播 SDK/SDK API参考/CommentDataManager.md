---
title: "CommentDataManager"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/commentdatamanager-zh-CN"
---

直播间消息列表的管理类。

<span id="8856c66c"></span>
## 成员函数

<span id="6b085a19"></span>
### sendTextMessage

在直播间发送文本评论。

```Java
public void sendTextMessage(String text, ServiceApi.ResultCallback<SendCommentResponse> callback)
```


**输入参数**


|名称 |类型 |接口行为 |
|---|---|---|
|text |String |评论内容。 |
|callback |[ServiceApi.ResultCallback](https://docs.byteplus.com/docs/byteplus-livesaas/docs-callback-the-viewer-sdk-for-android-zh-CN#9fb2c3e6) |发送评论时触发的回调。回调参数：[SendCommentResponse](https://docs.byteplus.com/docs/byteplus-livesaas/docs-type-the-viewer-sdk-for-android-zh-CN#c0244d2f) |
