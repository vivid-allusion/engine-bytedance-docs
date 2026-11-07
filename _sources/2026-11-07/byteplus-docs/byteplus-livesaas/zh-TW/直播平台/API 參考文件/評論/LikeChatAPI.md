---
title: "LikeChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-likechatapi-zh-TW"
---

在直播活動期間對聊天訊息點讚。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`LikeChatAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=LikeChatAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**是否必填** |**資料型態** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### 請求內容參數


|**參數名稱** |**是否必填** |**資料型態** |**說明** |
|---|---|---|---|
|ActivityId |是 |整數 |直播活動的 ID。 |
|ChatId |是 |整數 |聊天訊息的 ID。 |


<span id="Sample request"></span>
### 範例請求

```JSON
POST http://livesaas.byteplusapi.com/?Action=LikeChatAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "ChatId" : 1245231
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型態** |**說明** |
|---|---|---|
|LikeCount |整數 |聊天訊息的總點讚數。 |


<span id="Sample response"></span>
### 範例回應

以下為成功請求的範例回應：

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30",
     "Action" : "LikeChatAPI",
     "Version" : "2020-06-01",
     "Service" : "livesaas",
     "Region" : "ap-singapore-1" 
  },
   "Result" : {
       "LikeCount" : 123
  }
}
```
