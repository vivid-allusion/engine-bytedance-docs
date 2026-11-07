---
title: "UpdateSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/UpdateSpeechTask-zh-TW"
---

呼叫 `UpdateSpeechTask` API，以更新 AI 配音任務的功能開關狀態。此 API 常用於直播過程中，根據需求開啟或關閉翻譯功能。

<span id="Requirements"></span>
## 需求


* **頻率限制**：每個帳戶每秒最多 10 次請求。

* **計費**：AI 配音任務依據任務的 **實際推流時長**計費。如需更多資訊，請參閱 [AI 配音計費](https://docs.byteplus.com/en/docs/byteplus-media-live/ai_dubbing)。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任務 ID。可透過呼叫 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 取得 ID。 |
|Switch |String |是 |`AllDisable` |開關狀態。有效值：<br><br><br>* `AllDisable`：停用目前模式下的所有功能。<br><br>* `AllEnable`：啟用在建立 AI 配音任務時呼叫 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask) 所啟用的所有功能。<br><br><br>例如，在針對英語使用者的直播中，僅當非英語使用者發言時，可將此參數設為 `AllEnable`，以輸出翻譯內容。其他時段則設為 `AllDisable`，以輸出原始內容，不經 AI 配音處理。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">變更此參數值不會中斷任務。任務仍持續計費。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當此參數設為 <code>AllDisable</code> 時，原始音量配置亦會失效。</div><br> |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參閱下方表格。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118405#data) 物件 |`-` |任務資訊。 |


<span id="data"></span>
### 資料


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|OptID |Integer |`2` |任務更新序號。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378",
    "Switch": "AllDisable"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "20251117142336C37E6DC6C26C2529018E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "OptID": 2
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需錯誤碼相關資訊，請參閱 [通用錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
