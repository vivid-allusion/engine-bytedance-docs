---
title: "SilenceUserAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-silenceuserapi-zh-TW"
---

呼叫此 API 以管理直播活動中用戶的聊天權限。您可以呼叫此 API，禁止特定用戶發送訊息，或解除先前施加的禁言。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`SilenceUserAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=SilenceUserAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|ActivityId |是 |整數 |直播活動的 ID。 |
|UserId |是 |整數 |要禁言的用戶 ID。 |
|Status |是 |布林值 |是否禁止用戶發送聊天訊息：<br><br><br>* true：將用戶禁言。<br><br>* false：解除用戶禁言。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=SilenceUserAPI&Version=2020-06-01
{
     "ActivityId" :732412312,
     "UserId" : 1245231,
     "Status" : true
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
  "ResponseMetadata":{
  "RequestId":"201806041104200100100232280022D30",
  "Action":"SilenceUserAPI",
  "Version":"2020-06-01",
  "Service":"livesaas",
  "Region": "ap-singapore-1"
 },
  "Result": {
  "Status": true
 }
}
```
