---
title: "UploadReplayAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-uploadreplayapi-zh-TW"
---

呼叫此 API 以將影片綁定至直播活動作為回放。在執行此操作前，必須先將影片上傳至媒體庫。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UploadReplayAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=UploadReplayAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見 [共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|ActivityId |Integer |是 |直播活動的 ID。 |
|Media |Array |是 |影片資訊。 |


<span id="Media"></span>
#### **Media**


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Name |String |是 |媒體庫中影片的名稱。 |
|Vid |String |是 |媒體庫中影片的 ID。 |


<span id="Sample request"></span>
### 範例請求

```JSON
POST http://livesaas.byteplusapi.com/?Action=UploadReplayAPI&Version=2020-06-01
{
  "ActivityId": 178465844575,
  "Media": {
    "Name": "123",
    "Vid": "id123"
  }
}
```


<span id="Response"></span>
## 回應

<span id="Sample response"></span>
### 範例回應

```JSON
{
   "ResponseMetadata":{
     "RequestId":"201806041104200100100232280022D30",
     "Action":"UploadReplayAPI",
     "Version":"2020-06-01",
     "Service":"livesaas",
     "Region":"ap-singapore-1",
     "SystemTime":1656067132
  }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參見 [共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
