---
title: "SearchSpeechTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/SearchSpeechTask-zh-TW"
---

呼叫 `SearchSpeechTask` API，以搜尋符合特定條件的 AI 配音任務。

<span id="Requirements"></span>
## 需求

**Rate limit**：每個帳戶每秒最多 10 次請求。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=SearchSpeechTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`SearchSpeechTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskStatus |String 陣列 |否 |`["running", "init"]` |任務狀態。預設會回傳所有狀態的任務。有效值：<br><br><br>* `running`：執行中。<br><br>* `done`：已結束。<br><br>* `prestop`：停止中。<br><br>* `init`：準備中。<br><br>* `prepare`：啟動中。 |
|Name |String |否 |`TaskA` |任務名稱。預設會回傳所有任務。名稱長度必須為 1 到 20 個字元。不支援模糊搜尋，且英文字母區分大小寫。名稱可包含以下字元：<br><br><br>* 數字（0\-9）<br><br>* 大寫字母（A\-Z）<br><br>* 小寫字母（a\-z）<br><br>* 中文字符<br><br>* 底線（_）<br><br>* 連字號（\-） |
|CreateTimeSt |String |否 |`2025-11-13 17:01:06` |回傳此時間之後或同時建立的任務。時間格式為 RFC3339，使用 UTC+8，精確到秒。預設會回傳所有任務。 |
|CreateTimeEd |String |否 |`2025-11-14 15:34:43` |回傳此時間之前或同時建立的任務。時間格式為 RFC3339，使用 UTC+8，精確到秒。預設會回傳所有任務。 |
|Page |Integer |是 |`1` |要回傳的頁碼。值必須為正整數。 |
|PageSize |Integer |是 |`10` |每頁回傳的結果數量。值必須大於 `0`。 |


<span id="Response parameters"></span>
## 回應參數

如需查看 API 專屬回應參數，請參閱下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Code |Integer |`0` |狀態碼。 |
|Message |String |`success` |狀態訊息。 |
|Data |[Data](https://docs.byteplus.com/en/docs/24/118406#data) 物件 |`-` |任務資訊。 |


<span id="data"></span>
### 資料


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Count |Integer |`1` |回傳任務總數。 |
|Tasks |[Tasks](https://docs.byteplus.com/en/docs/24/118406#tasks) 陣列 |`-` |任務資訊。 |


<span id="tasks"></span>
### 任務


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Name |String |`TaskA` |任務名稱。 |
|Status |String |`done` |任務狀態。有效值：<br><br><br>* `running`：執行中。<br><br>* `done`：已結束。<br><br>* `prestop`：停止中。<br><br>* `init`：準備中。<br><br>* `prepare`：啟動中。 |
|TaskID |String |`b71c61469024ae4f` |任務 ID。 |
|CreatedAt |String |`2025-11-14T15:34:43+08:00` |任務開始時間。時間格式為 RFC3339，使用 UTC+8，精確到秒。 |
|UpdatedAt |String |`2025-11-14T16:50:53+08:00` |任務更新時間。時間格式為 RFC3339，使用 UTC+8，精確到秒。 |
|StoppedAt |String |`2025-11-14T16:50:49+08:00` |任務實際結束時間。時間格式為 RFC3339，使用 UTC+8，精確到秒。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=SearchSpeechTask&Version=2023-01-01
{
    "TaskStatus": [
        "running",
        "init"
    ],
    "Name": "TaskA",
    "CreateTimeSt": "2025-11-13 17:01:06",
    "CreateTimeEd": "2025-11-14 15:34:43",
    "Page": 1,
    "PageSize": 10
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "2025111417350416C47E772ECEBC01847B",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "SearchSpeechTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Code": 0,
        "Message": "success",
        "Data": {
            "Count": 1,
            "Tasks": [
                {
                    "Name": "TaskA",
                    "Status": "done",
                    "TaskID": "b71c61****24ae4f",
                    "CreatedAt": "2025-11-14T15:34:43+08:00",
                    "UpdatedAt": "2025-11-14T16:50:53+08:00",
                    "StoppedAt": "2025-11-14T16:50:49+08:00"
                }
            ]
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

如需錯誤碼詳細資訊，請參閱 [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes)。
