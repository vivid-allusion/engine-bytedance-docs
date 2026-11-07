---
title: "RestartSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/RestartSpeechTask-zh-TW"
---

調用 `RestartSpeechTask` API 以重新啟動正在運行或啟動中的 AI 配音任務。

<span id="Requirements"></span>
## 需求


* **速率限制**：每個帳戶每秒 10 次請求。

* **前置條件**：AI 配音任務正在運行或啟動中。您可以調用 [GetSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask) 以獲取任務狀態，並確保 `Status` 的值為 `running` 或 `prepare`。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=RestartSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`RestartSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任務 ID。您可以通過調用 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 獲取該 ID。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=RestartSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111815174611F9EB957342DF410655",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "RestartSpeechTask",
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
