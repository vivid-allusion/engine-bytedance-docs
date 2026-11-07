---
title: "UpdateChatReviewStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatechatreviewstatusapi-zh-TW"
---

此 API 用於開啟或關閉聊天訊息審核功能，使訊息在發送給直播活動的觀眾之前，先經過審核批准或阻擋。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdateChatReviewStatusAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateChatReviewStatusAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


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
|ActivityId |是 |整數 |直播活動的唯一識別碼。 |
|Status |是 |整數 |是否開啟訊息審核：<br><br><br>* 0：關閉審核<br><br>* 1：開啟審核 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateChatReviewStatusAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "Status" : 1,
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Status |布林值 |操作結果：<br><br><br>* true：成功<br><br>* false：失敗 |


<span id="Sample response"></span>
### 回應範例

以下為成功請求的回應範例：

```JSON
{
   "ResponseMetadata" :{
     "RequestId" : "201806041104200100100232280022D30",
     "Action" : "TopChatAPI",
     "Version" : "2020-06-01",
     "Service" : "livesaas",
     "Region" :  "ap-singapore-1" 
  },
   "Result" : {
       "Status" : true
  }
}
```
