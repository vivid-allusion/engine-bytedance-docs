---
title: "ListCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcarouseltask-zh-TW"
---

呼叫 `ListCarouselTask` API 以取得所有目前輪播任務的清單，包括任務 ID、狀態及建立時間，可用於任務管理與批次查詢。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListCarouselTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Page |Integer |是 |`1` |查詢資料的頁碼。 |
|PageSize |Integer |是 |`30` |每頁顯示的資料筆數，最大值為 1000。 |


<span id="Response parameters"></span>
## 回應參數

如需唯一的專屬 API 回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107429#data) 物件 |`-` |輪播任務資料物件。 |


<span id="data"></span>
### 資料


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Count |Integer |`29` |符合查詢條件的輪播任務總數。 |
|Result |[Result](https://docs.byteplus.com/en/docs/24/107429#result) 陣列 |`-` |輪播任務陣列，每個元素代表一個任務的詳細資訊。 |


<span id="result"></span>
### 結果


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|CreatedAt |[CreatedAt](https://docs.byteplus.com/en/docs/24/107429#createdat) 物件 |`{"Time":"2023-03-15T08:00:00+08:00"}` |任務建立時間，RFC3339 格式的時間戳，精確到秒。 |
|Name |String |`Carousel test` |輪播任務名稱。 |
|Status |String |`running` |輪播任務目前狀態。值及其含義如下：<br><br><br>* `pending`：任務等待排程；<br><br>* `prepare`：任務初始化中；<br><br>* `running`：任務執行中；<br><br>* `prestop`：任務停止中；<br><br>* `done`：任務已停止。 |
|StoppedAt |[StoppedAt](https://docs.byteplus.com/en/docs/24/107429#stoppedat) 物件 |`{"Time":"2023-03-16T08:00:00+08:00"}` |任務結束時間，RFC3339 格式的時間戳，精確到秒。 |
|TaskID |String |`e1fb009334fc5b16` |輪播任務的唯一識別碼。 |
|UpdatedAt |[UpdatedAt](https://docs.byteplus.com/en/docs/24/107429#updatedat) 物件 |`{"Time":"2023-03-15T10:00:00+08:00"}` |任務更新時間，RFC3339 格式的時間戳，精確到秒。 |


<span id="createdat"></span>
### CreatedAt


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Time |String |`2024-10-30T15:25:07+08:00` |任務建立時間，RFC3339 格式的時間戳，精確到秒。 |


<span id="stoppedat"></span>
### StoppedAt


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Time |String |`0001-01-01T00:00:00Z` |任務結束時間，RFC3339 格式的時間戳，精確到秒。 |


<span id="updatedat"></span>
### UpdatedAt


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Time |String |`2024-10-30T15:25:08+08:00` |任務更新時間，RFC3339 格式的時間戳，精確到秒。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListCarouselTask&Version=2023-01-01
{
    "Page": 1,
    "PageSize": 30
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301540353C34785110C816119A9E",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": {
            "Count": 29,
            "Result": [
                {
                    "CreatedAt": {
                        "Time": "2024-10-30T15:25:07+08:00"
                    },
                    "Name": "Carousel test",
                    "Status": "running",
                    "StoppedAt": {
                        "Time": "0001-01-01T00:00:00Z"
                    },
                    "TaskID": "e1fb009334fc5b16",
                    "UpdatedAt": {
                        "Time": "2024-10-30T15:25:08+08:00"
                    }
                }
            ]
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](#Request Parameters) 說明進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
