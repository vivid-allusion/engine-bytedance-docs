---
title: "TopChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-topchatapi-zh-TW"
---

在直播活動期間，呼叫此 API 以將聊天訊息置頂或取消置頂。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`TopChatAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=TopChatAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表並未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|ActivityId |是 |整數 |直播活動的 ID。 |
|ChatId |是 |整數 |聊天訊息的 ID。 |
|TopStatus |是 |整數 |指定訊息的置頂狀態。<br><br><br>* 1：將訊息置頂<br><br>* 2：取消訊息置頂 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=TopChatAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "ChatId" : 1245231,
     "TopStatus" : 2
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Status |布林值 |表示操作是否成功。<br><br><br>* true：成功<br><br>* false：失敗 |


<span id="Sample response"></span>
### 回應範例

以下為成功請求的回應範例。

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30" ,
     "Action" : "TopChatAPI" ,
     "Version" : "2020-06-01",
     "Service" : "livesaas",
     "Region" :  "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
