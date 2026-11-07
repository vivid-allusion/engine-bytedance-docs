---
title: "UpdateLoopVideoAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateloopvideoapi-zh-TW"
---

呼叫此 API 以編輯指定直播活動的循環播放影片配置。

<span id="Request"></span>
## 請求

<span id="Details"></span>
### 詳細資訊


* API 操作：`UpdateLoopVideoAPI`

* 請求方法：POST

* 請求 URI：`http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoAPI&Version=2020-06-01`

* 配額：每個帳戶每分鐘 120 次查詢


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
|ActivityId |是 |整數 |直播活動的 ID。可透過呼叫[ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi-zh-TW)取得 ID。 |
|LineId |是 |整數 |直播流的 ID。可透過呼叫[GetStreamsAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getstreamsapi-zh-TW)取得 ID。 |
|LoopNumber |是 |整數 |影片播放次數。目前僅可設定為`1`。 |
|LoopVideo |是 |[LoopVideo](https://docs.byteplus.com/docs/byteplus-livesaas/docs-updateloopvideoapi-zh-TW#LoopVideo)陣列 |循環播放配置。 |


<span id="LoopVideo"></span>
#### LoopVideo


|**參數名稱** |**必填** |**資料型別** |**說明** |
|---|---|---|---|
|Index |是 |整數 |影片索引，從`1`開始，依序遞增。 |
|VideoCoverImage |否 |整數 |影片封面圖片。此參數已棄用。 |
|VideoName |是 |字串 |影片名稱。 |
|VideoVid |是 |字串 |影片的唯一 ID。可透過呼叫[ListActivityMediaAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivitymediaapi)取得 ID。 |


<span id="Sample request"></span>
### 請求範例

```JSON
POST http://livesaas.byteplusapi.com/?Action=UpdateLoopVideoAPI&Version=2020-06-01
{
    "ActivityId":732412312,
    "LineId":1234,
    "LoopNumber":1,
    "LoopVideo":[
        {
            "Index":1,
            "VideoName":"video.mp4",
            "VideoVid":"v02a49370000b****gbiokkno91"
        }
    ]
}
```


<span id="Response"></span>
## 回應

<span id="Response schema"></span>
### 回應結構


|**參數名稱** |**資料型別** |**說明** |
|---|---|---|
|Id |整數 |循環播放配置的 ID。 |


<span id="Sample response"></span>
### 回應範例

```JSON
{
  "ResponseMetadata":{
    "RequestId":"201806041104200100100232280022D30",
    "Action":"UpdateLoopVideoAPI",
    "Version":"2020-06-01",
    "Service":"livesaas",
    "Region": "ap-singapore-1"
  }
  "Result":{
   "Id": 123
}
}
```
