---
title: "GetSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/GetSpeechTask-zh-TW"
---

呼叫 `GetSpeechTask` API 以查詢特定 AI 配音任務的資訊。

<span id="Requirements"></span>
## 需求

**速率限制**：每個帳戶每秒最多 10 次請求。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=GetSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetSpeechTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`49743067b675c378` |任務 ID。可透過呼叫 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask?lang=en) 或 [SearchSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask) 取得此 ID。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參考下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118400#data) 物件 |`-` |任務資訊。 |


<span id="data"></span>
### 資料


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Name |String |`TaskA` |任務名稱。 |
|Status |String |`done` |任務狀態。有效值：<br><br><br>* `running`：執行中。<br><br>* `done`：已結束。<br><br>* `prestop`：停止中。<br><br>* `init`：準備中。<br><br>* `prepare`：啟動中。 |
|TaskID |String |`49743067b675c378` |任務 ID。 |
|CreatedAt |String |`2025-11-14T15:34:43+08:00` |任務建立時間。時間格式為 RFC3339，使用 UTC+8，精確到秒。 |
|UpdatedAt |String |`2025-11-14T16:50:53+08:00` |任務更新時間。時間格式為 RFC3339，使用 UTC+8，精確到秒。 |
|StoppedAt |String |`2025-11-14T16:50:49+08:00` |任務實際結束時間。時間格式為 RFC3339，使用 UTC+8，精確到秒。 |
|Rule |String |`{"Pipe":"mix","Delay":15,"Source":{"Url":"https://pull.example.com/live/cloud.flv"},"Output":{"Url":["rtmp://push.example.com/live/cloud?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901"]},"Subtitle":{"Original":{"Border":{"W":1,"Color":"black@0.5"},"Font":"arial","FontColor":"white","Language":"zh"},"Translation":[{"Border":{"W":1,"Color":"black@0.5"},"Font":"arial","FontColor":"white","Language":"en"}]}}` |任務規則設定。此值為 JSON 字串，包含任務類型、拉流 URL、推流 URL、字幕設定及其他資訊。欄位詳細資訊請參考 [CreateSpeechTask](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateSpeechTask)。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=GetSpeechTask&Version=2023-01-01
{
    "TaskID": "497430****75c378"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestID": "20251114171722145C604658CB14014261",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "Name": "TaskA",
            "Status": "done",
            "TaskID": "497430****75c378",
            "CreatedAt": "2025-11-14T15:34:43+08:00",
            "UpdatedAt": "2025-11-14T16:50:53+08:00",
            "StoppedAt": "2025-11-14T16:50:49+08:00",
            "Rule": "{\"Pipe\":\"mix\",\"Delay\":15,\"Source\":{\"Url\":\"https://pull.example.com/live/cloud.flv\"},\"Output\":{\"Url\":[\"rtmp://push.example.com/live/cloud?auth_key=1779891783-0-0-e1f5a2a****4b5fe21cb3efdc89af901\"]},\"Subtitle\":{\"Original\":{\"Border\":{\"W\":1,\"Color\":\"black@0.5\"},\"Font\":\"arial\",\"FontColor\":\"white\",\"Language\":\"zh\"},\"Translation\":[{\"Border\":{\"W\":1,\"Color\":\"black@0.5\"},\"Font\":\"arial\",\"FontColor\":\"white\",\"Language\":\"en\"}]}}"
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需錯誤碼相關資訊，請參考 [通用錯誤碼](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
