---
title: "GetCarouselDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getcarouseldetail-zh-TW"
---

呼叫 `GetCarouselDetail` API 以查詢指定輪播任務的詳細資訊，包括播放狀態、影片列表及目前播放進度，便於管理與監控任務執行狀態。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=GetCarouselDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetCarouselDetail` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`44c5da50318440*********2d62c910b8` |欲查詢的輪播任務 ID，為任務的唯一識別碼。此值於呼叫 `CreateCarouselTask` 介面建立輪播任務時回傳。 |


<span id="Response parameters"></span>
## 回應參數

關於 API 專屬且唯一的回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107439#data) 物件 |`-` |包含輪播任務相關資訊的資料物件。 |


<span id="data"></span>
### 資料


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|LastOperationIndex |Integer |`1` |最新播放列表修改序號，每次呼叫 `UpdateCarouselTask` 介面更新任務時，此值會加 `1`。 |
|LastSuccessOperationIndex |Integer |`1` |目前實際生效的播放列表序號，表示任務目前依此版本的素材列表進行播放。 |
|PlayInfo |String |`{"Loop":1,"SourceID":"2","SourceLoop":1,"SourceSeek":910}` |目前播放或最後播放素材的資訊以 JSON 字串形式回傳。此欄位包含素材詳細資訊，如素材名稱、播放位置等，方便使用者取得與播放相關的具體資料。 |
|Rule |String |`{"Loop":1,"Mode":1,"Output":{"Audio":{"BitRate":144000,"ChannelLayout":"stereo","SampleRate":44100},"Url":["rtmp://push-rtmp-f5.douyincdn.com/zebraedit/dev-114203018399843854?expire=1729119100&sign=a1b23eb99a26816a5db20a1ec4b314cb&volcSecret=a1b23eb99a26816a5db20a1ec4b314cb&volcTime=1729119100"],"Video":{"BitRate":8000000,"Codec":"h264","FrameRate":30,"GOP":2,"Height":1080,"Preset":"faster","Width":1920}},"PlayTime":1,"Source":[{"ID":"1","Type":"vod","Url":"https://tosv.byted.org/obj/fcdn-engine-001/test/douyin_D_90sTVC_1Mbps.mp4"},{"ID":"2","Type":"vod","Url":"https://tosv.byted.org/obj/fcdn-engine-001/test/111.mp4"}]}` |輪播任務的播放規則，以下為部分主要參數：<br><br><br>* `Loop`：是否循環播放及循環次數。<br><br>* `Mode`：播放模式（普通模式／轉碼模式）。<br><br>* `Output`：串流參數，包括 `Audio`（音訊參數）、`Video`（視訊參數）及 `Url`（串流地址）。<br><br>* `Source`：輪播素材列表，包括每個素材的 `ID`、`Type`（如 `vod`）及 `Url`（播放地址）。 |
|Status |String |`running` |任務目前狀態。支援以下值：<br><br><br>* `pending`：任務等待排程；<br><br>* `prepare`：任務初始化中；<br><br>* `running`：任務執行中；<br><br>* `prestop`：任務停止中；<br><br>* `done`：任務已停止。<br><br><br>此欄位用於標示任務生命週期的目前階段，通常用於監控或查詢任務執行進度。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=GetCarouselDetail&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301535298CE0D4E0152CAF10A8AC",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetCarouselDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "LastOperationIndex": 1,
            "LastSuccessOperationIndex": 1,
            "PlayInfo": "{\"Loop\":1,\"SourceID\":\"2\",\"SourceLoop\":1,\"SourceSeek\":910}",
            "Rule": "{\"Loop\":1,\"Mode\":1,\"Output\":{\"Audio\":{\"BitRate\":144000,\"ChannelLayout\":\"stereo\",\"SampleRate\":44100},\"Url\":[\"rtmp://push-rtmp-f5.douyincdn.com/zebraedit/dev-114203018399843854?expire=1729119100&sign=a1b23eb99a26816a5db20a1ec4b314cb&volcSecret=a1b23eb99a26816a5db20a1ec4b314cb&volcTime=1729119100\"],\"Video\":{\"BitRate\":8000000,\"Codec\":\"h264\",\"FrameRate\":30,\"GOP\":2,\"Height\":1080,\"Preset\":\"faster\",\"Width\":1920}},\"PlayTime\":1,\"Source\":[{\"ID\":\"1\",\"Type\":\"vod\",\"Url\":\"https://tosv.byted.org/obj/fcdn-engine-001/test/douyin_D_90sTVC_1Mbps.mp4\"},{\"ID\":\"2\",\"Type\":\"vod\",\"Url\":\"https://tosv.byted.org/obj/fcdn-engine-001/test/111.mp4\"}]}",
            "Status": "running"
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107439#request-parameters)說明進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
