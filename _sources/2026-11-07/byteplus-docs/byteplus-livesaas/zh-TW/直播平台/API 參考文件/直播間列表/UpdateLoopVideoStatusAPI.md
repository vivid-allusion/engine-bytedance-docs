---
title: "UpdateLoopVideoStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateloopvideostatusapi-zh-TW"
---

調用此 API 以啟用或停用指定直播活動的循環播放功能。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdateLoopVideoStatusAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoStatusAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。如需完整清單，請參閱[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |String |API 操作。 |
|Version |是 |String |此 API 操作的版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|ActivityId |是 |Integer |直播活動的 ID。 |
|IsStartLoopVideo |是 |Integer |指定是否啟動或停止循環播放：<br><br><br>* 1：啟動。當循環播放啟動時，直播活動也會開始。<br><br>* 2：停止。當循環播放停止時，直播活動也會停止。 |
|LineId |是 |Integer |直播流的 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoStatusAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "IsStartLoopVideo":1,
    "LineId":123
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Status |Boolean |表示循環播放狀態是否更新成功。 |


<span id="Sample response"></span>
### 回應範例

```JSON
{
  "ResponseMetadata":{
    "RequestId":"2018060411042001001002322800xxxx",
    "Action":"UpdateLoopVideoStatusAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
  "Result":{
   "Status":true
}
}
```
