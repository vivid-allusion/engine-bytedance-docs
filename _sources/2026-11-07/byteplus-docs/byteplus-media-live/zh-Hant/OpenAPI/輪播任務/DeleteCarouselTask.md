---
title: "DeleteCarouselTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletecarouseltask-zh-TW"
---

呼叫 `DeleteCarouselTask` API 以刪除指定的輪播任務。任務刪除後，系統將停止播放該任務的所有輪播內容，並釋放相關資源。

<span id="Requirements"></span>
## 需求


* 速率限制：每個帳戶每秒最多 10 次查詢。

* 不可恢復：呼叫 `DeleteCarouselTask` 介面後，該任務及其相關資源將被釋放且無法恢復。請謹慎操作。

* 立即停止：任務刪除後，所有正在進行的輪播播放將立即停止，無需等待當前播放完成。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteCarouselTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteCarouselTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TaskID |String |是 |`44c5da50318440*********2d62c910b8` |待刪除輪播任務的 ID，即該任務的唯一識別碼。該值於呼叫 `CreateCarouselTask` 介面建立輪播任務時返回。 |


<span id="Response parameters"></span>
## 回應參數

如需專屬 API 回應參數，請參見下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Data |String |`kill task [e1fb009334fc5b16] success,mesos id is [live_bff26015_000000000025852],rowsAffect [0]` |已刪除任務的操作結果資訊，返回任務是否刪除成功、相關 Mesos ID 及操作影響記錄數量。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteCarouselTask&Version=2023-01-01
{
    "TaskID": "44c5da50318440*********2d62c910b8"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "202410301524025B4509E7E242BD12477C",
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteCarouselTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": "kill task [e1fb009334fc5b16] success,mesos id is [live_bff26015_000000000025852],rowsAffect [0]"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](#Request Parameters) 說明進行檢查。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [contact support](https://console.byteplus.com/workorder/create)。 |
