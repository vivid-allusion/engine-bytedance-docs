---
title: "UpdatePullToPushAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updatepulltopushapi-zh-TW"
---

UpdatePullToPushAPI 操作會根據指定的 URL，啟動或停止拉流以進行直播活動。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdatePullToPushAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=UpdatePullToPushAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


<span id="Query string parameters"></span>
### 查詢字串參數

下表未包含所有共用請求參數。完整列表請參見[共用請求參數](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967)。


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|Action |是 |字串 |API 操作。 |
|Version |是 |字串 |API 版本。目前版本：`2020-06-01`。 |


<span id="Body parameters"></span>
### Body 參數


|**參數名稱** |**是否必填** |**資料型別** |**說明** |
|---|---|---|---|
|ActivityId |是 |整數 |直播活動的 ID。 |
|LineId |否 |整數 |直播流的 ID。請呼叫 `GetStreamsAPI` 操作以取得活動的流 ID。一個活動可以有多個直播流。 |
|PullStreamUrl |是 |字串 |要拉取的流的 URL。 |
|PullStreamStatus |是 |整數 |指定是否啟動或停止拉流：<br><br><br>* 1：啟動拉流。<br><br>* 2：停止拉流。 |
|PullStreamMode |否 |整數 |指定操作主流或備流：<br><br><br>* 0：主流<br><br>* 1：備流 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdatePullToPushAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "PullStreamUrl": "https://xxxx/xxxx/xxxx.flv",
    "PullStreamStatus": 1
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
    "Action":"UpdatePullToPushAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
}
```
