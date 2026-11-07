---
title: "CreateCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createcarouseltask-zh-TW"
---

調用 `CreateCarouselTask` API 以建立輪播任務。在直播過程中，視頻直播伺服器將根據任務配置，按照設定順序循環播放指定的視頻內容。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須攜帶 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |字串 |是 |`CreateCarouselTask` |API 操作名稱。 |
|Version |字串 |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|名稱 |字串 |是 |`## 商品輪播` |輪播任務名稱用於標識該任務。支持由中文、大小寫英文字母（A\-Z, a\-z）及數字（0\-9）組成。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">該名稱不得與其他運行中的任務名稱重複。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">已啟動的任務不允許使用重複名稱。</div><br> |
|規則 |[Rule](https://docs.byteplus.com/en/docs/24/107320#rule) 物件 |是 |`-` |輪播規則用於指定輪播播放的素材及行為。 |


<span id="rule"></span>
### 規則


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Loop |整數 |是 |`-1` |輪播循環次數，用於控制直播循環播放的次數。支持的取值及含義如下：<br><br><br>* `-1`：無限循環；<br><br>* `0`：不循環；<br><br>* 其他正整數：指定輪播循環的具體次數。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">直播循環的行為同時受 <code>Loop</code> 與 <code>StopTime</code> 欄位影響：</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>Loop</code> 次數達到設定值時，無論是否到達 <code>StopTime</code>，輪播將自動停止。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當到達 <code>StopTime</code> 時，即使 <code>Loop</code> 尚未完成，輪播也會停止。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若未設置 <code>StopTime</code>，系統預設最大輪播時長為 3 天。</div><br> |
|Mode |整數 |是 |`1` |該欄位用於指定輪播素材的拼接模式，決定多個點播素材在播放時的銜接方式。支持的取值如下：<br><br><br>* `0`：普通模式。前後素材的音視頻參數（如解析度、碼率、編碼格式等）將進行檢查。若參數一致，素材可無縫銜接；若參數不同，切換時可能會有短暫中斷。<br><br>* `1`：轉碼模式。系統會將所有點播素材格式化為相同的音視頻參數，以確保切換時素材始終順暢無縫銜接。用戶可手動配置目標參數。如未配置，則預設採用第一個素材的參數。 |
|輸出 |[Output](https://docs.byteplus.com/en/docs/24/107320#output) 的物件 |是 |`-` |輪播任務的推流參數，包括視頻、音頻、推流地址及回調資訊。 |
|PlayTime |Long |是 |`1672531200000` |輪播任務的開始時間，以 Unix 時戳表示，精度為 `ms`。參數要求如下：<br><br><br>* 當值為 `0` 時，表示立即開始推流；<br><br>* 若設定了具體時間，必須為晚於當前時間的值。 |
|StopTime |Long |否 |`1672800000000` |輪播任務的結束時間，Unix 時戳，精度為 `ms`。設定此欄位後，系統將根據該時間點自動關閉任務。最大時間範圍為 `3 天`，預設值為 `3 天`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">輪播任務的結束時間 <code>StopTime</code> 必須晚於開始時間 <code>PlayTime</code>。</div><br> |
|Source |[Source](https://docs.byteplus.com/en/docs/24/107320#source) 陣列 |是 |`-` |輪播素材清單，用於指定輪播過程中播放的素材資源。 |


<span id="output"></span>
### 輸出


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Video |[Video](https://docs.byteplus.com/en/docs/24/107320#video) 的物件 |否 |`-` |在轉碼模式下（即 `Rule.Mode = 1`），可選擇性配置推流的視頻參數。預設情況下，所有參數（除 GOP 外）均依據第一個素材的設定以輪播方式處理。 |
|Audio |[Audio](https://docs.byteplus.com/en/docs/24/107320#audio) 的物件 |否 |`-` |在轉碼模式下（即 `Rule.Mode = 1`），可用於配置推流的音頻參數。 |
|Url |字串陣列 |是 |`[ "rtmp://push.example.com/live/stream1" ]` |推流用的 RTMP 或 RTMPS 地址，支援 **多路推流**（即同時將相同直播內容推送至多個推流地址）。地址最少為 1 個，最多支援 8 個。 |
|Callback |[Callback](https://docs.byteplus.com/en/docs/24/107320#callback) 的物件 |否 |`-` |回調函數配置，用於接收任務狀態更新等通知。 |


<span id="source"></span>
### 來源


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|ID |字串 |是 |`1` |輪播素材的唯一識別碼。在同一播放清單中，每個素材的 `ID` 必須唯一，不得重複。 |
|Type |字串 |是 |`vod` |輪播素材的檔案類型，用於指定素材的檔案來源類型。支援以下值：<br><br><br>* `vod`：點播 MP4 或 FLV 檔案；<br><br>* `m3u8`：點播 M3U8 檔案。 |
|Url |字串 |是 |`https://live.example.com/video.mp4` |輪播素材的公開可訪問地址。請確保所提供的地址可被公網正常訪問，以正確載入輪播素材內容。 |
|Loop |整數 |否 |`1` |指定此素材連續播放的次數。此欄位的值必須大於或等於 `0`，預設值為 `0`。支援的值及其含義如下：<br><br><br>* `0`：不循環播放；<br><br>* 其他正整數：依指定次數循環播放。 |
|Seek |整數 |否 |`10` |用於控制播放當前素材時跳過開頭的一段時間。例如跳過片頭，單位為秒。此欄位僅在素材類型為隨選視訊（`type=vod`）時有效。以下為此欄位的使用規則：<br><br><br>* 若`Seek`的值小於或等於`0`，或大於影片實際時長，則此欄位不會生效。<br><br>* 請根據隨選素材的實際長度設置合適的值，以達到跳過片頭的效果。 |


<span id="video"></span>
### 視頻


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|BitRate |整數 |否 |`15` |影片的位元率，單位為`bit`，且值必須小於或等於`20000`。若指定`Video`物件，則此欄位為必填。 |
|FrameRate |整數 |否 |`30` |影片幀率，取值範圍為`[10, 60]`。若指定`Video`物件，則此欄位為必填。 |
|GOP |整數 |否 |`5` |IDR 幀之間的最大間隔，單位為秒。預設值為`2`，取值範圍為`[1,10]`。 |
|Preset |字串 |否 |`faster` |**編碼預設值**<br><br>此參數用於指定編碼速度與壓縮率之間的平衡，支援以下選項（從最快到最慢）：<br><br><br>* **`ultrafast`**：編碼速度最快，CPU 使用率最低，但壓縮率最低且檔案體積最大。適用於對即時性要求極高的場景。<br><br>* **`superfast`**：編碼速度非常快，壓縮率較低，適用於對延遲敏感但可接受較大檔案體積的場景。<br><br>* **`veryfast`**：編碼速度較快，適用於對即時性有較高要求的場景。<br><br>* **`faster`**（預設）：編碼速度較快，品質與壓縮率均衡，適用於大多數直播或短影片場景。<br><br>* **`fast`**：編碼速度適中，壓縮率較高，適用於對畫質與檔案體積有一定要求的場景。<br><br>* **`medium`**：編碼速度與壓縮率均衡，適用於大多數常規影片處理任務。<br><br>* **`slow`**：編碼速度較慢，但壓縮率較高且影片品質更佳，適用於對畫質要求較高的場景，例如存檔或高品質隨選內容。 |
|Width |整數 |否 |`1920` |影片寬度，單位為像素。支援的取值範圍為`[10, 2160]`。若指定`Video`物件，則此欄位為必填。 |
|Height |整數 |否 |`1080` |影片高度（單位：像素），取值範圍為`[10, 2160]`。若指定`Video`物件，則此欄位為必填。 |


<span id="audio"></span>
### 音訊


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|BitRate |整數 |否 |`320000` |音訊位元率的設定範圍，支援的取值為`[128000, 640000]`，單位為`bps`。若指定`Audio`物件，則此欄位為必填項。 |
|ChannelLayout |字串 |否 |`stereo` |音訊的聲道配置。若指定`Audio`物件，則此欄位為必填。支援以下取值：<br><br><br>* `mono`：單聲道。<br><br>* `stereo`：立體聲。 |
|取樣率 |整數 |否 |`48000` |音訊的取樣率參數。若指定了`Audio`物件，則此欄位為必填。支援的取樣率值包括：<br><br><br>* `22000`<br><br>* `32000`<br><br>* `44100`<br><br>* `48000`<br><br><br>請根據您的業務需求選擇合適的取樣率進行配置。 |


<span id="callback"></span>
### 回調


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Url |字串 |是 |`https://callback.example.com/notify` |回調地址。此欄位需準確配置，用於接收系統回調資訊。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107320#data)物件 |`-` |輪播任務資料物件。 |


<span id="data"></span>
### 資料


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TaskID |字串 |`e1fb009334fc5b16` |輪播任務的唯一識別碼。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=CreateCarouselTask&Version=2023-01-01
{
    "Name": "Commodity Carousel",
    "Rule": {
        "Loop": -1,
        "Mode": 1,
        "Output": {
            "Video": {
                "BitRate": 15,
                "FrameRate": 30,
                "GOP": 5,
                "Preset": "faster",
                "Width": 1920,
                "Height": 1080
            },
            "Audio": {
                "BitRate": 320000,
                "ChannelLayout": "stereo",
                "SampleRate": 48000
            },
            "Url": [
                "rtmp://push.example.com/live/stream1"
            ],
            "Callback": {
                "Url": "https://callback.example.com/notify"
            }
        },
        "PlayTime": 1672531200000,
        "Source": [
            {
                "ID": "1",
                "Type": "vod",
                "Url": "https://live.example.com/video.mp4",
                "Loop": 1,
                "Seek": 10
            }
        ],
        "StopTime": 1672800000000
    }
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301432037DE157BFBC968410056C",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "TaskID": "e1fb009334fc5b16"
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](#Request Parameters)說明進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請聯絡[Technical Support](https://console.volcengine.com/workorder/create?step=2&SubProductID=P00000076)。 |
