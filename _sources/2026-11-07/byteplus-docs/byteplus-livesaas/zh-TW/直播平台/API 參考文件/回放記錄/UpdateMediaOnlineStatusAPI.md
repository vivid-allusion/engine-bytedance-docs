---
title: "UpdateMediaOnlineStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatemediaonlinestatusapi-zh-TW"
---

呼叫此 API 以管理直播活動的回放線上狀態。您可以呼叫此 API 來發布、撤回或移除回放。在執行此操作前，必須先上傳一段影片作為回放內容。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdateMediaOnlineStatusAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateMediaOnlineStatusAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘最多 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表並未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|Action |String |是 |API 操作。 |
|Version |String |是 |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**資料型別** |**是否必填** |**說明** |
|---|---|---|---|
|ActivityId |Integer |是 |直播活動的 Activity ID。 |
|MediaId |Integer |是 |回放影片的 Video ID。 |
|OnlineStatus |Integer |是 |回放的狀態。<br><br>有效值：<br><br><br>* `0`：從觀看頁面撤回。回放仍綁定於直播活動，可隨時重新發布。<br><br>* `1`：發布至觀看頁面。<br><br>* `2`：從直播活動移除，但仍存在於媒體庫。在發布至觀看頁面前，需呼叫[UploadReplayAPI](https://docs.byteplus.com/en/byteplus-livesaas/docs/uploadreplayapi)將其綁定至直播活動。 |
|ForceReplayStatus |Boolean |否 |指定回放發布後，是否將直播狀態從**Preview**或**Over**變更為**Playback**。<br><br><br>* `true`：將直播狀態變更為**Playback**，允許觀眾觀看已發布的回放。<br><br>* `false`：不變更直播狀態。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateMediaOnlineStatusAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "MediaId":3706016,   
    "OnlineStatus":1,
}
```


<span id="Response"></span>
## 回應

<span id="Sample response"></span>
### 回應範例

```JSON
{
    "ResponseMetadata":{
        "RequestId":"201806041104200100100232280022D30",
        "Action":"UpdateMediaOnlineStatusAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1", 
        "SystemTime":1655978114
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

常見錯誤碼列表請參見[共用錯誤與狀態碼](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes)。
