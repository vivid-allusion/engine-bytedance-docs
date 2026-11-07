---
title: "DeleteSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteSpeechTask-zh-TW"
---

調用 `DeleteSpeechTask` API 以刪除不再需要的 AI 配音任務。如果任務正在運行，MediaLive 會在刪除任務前先停止該任務。

<span id="Requirements"></span>
## 需求

**速率限制**：每個帳戶每秒 10 次請求。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任務 ID。可通過調用 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 獲取該 ID。 |
|WithRecord |Boolean |否 |`true` |是否同時刪除任務記錄。預設值：`false`。有效值：<br><br><br>* `true`：刪除記錄。記錄刪除後，無法再通過調用 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 查詢該任務。<br><br>* `false`：保留記錄。 |


<span id="Response parameters"></span>
## 回應參數

API 專屬回應參數請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DeleteSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378",
    "WithRecord": true
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111417343916C47E772ECEBC0183DC",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需更多錯誤碼資訊，請參見 [通用錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
