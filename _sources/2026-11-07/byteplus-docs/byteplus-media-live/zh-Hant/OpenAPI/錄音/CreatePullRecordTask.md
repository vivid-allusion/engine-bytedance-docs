---
title: "CreatePullRecordTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreatePullRecordTask-zh-TW"
---

調用`CreatePullRecordTask` API 以建立在指定時間開始與結束的直播拉流錄製任務。建立成功後，可於直播期間錄製任意時長的單路直播流，並將其保存為視頻文件。

<span id="bdd0cccc"></span>
## 使用場景

通過調用此 API，可根據配置的錄製開始時間`StartTime`與結束時間`EndTime`，對指定的拉流地址`StreamURL`進行錄製。該任務的錄製規則與所關聯的錄製配置保持一致。錄製任務與錄製配置通過`Domain`與`App`參數關聯。因此，直播錄製任務的`Vhost`、`Domain`及`App`需在錄製配置的有效範圍內。例如，若需建立`"Vhost":" live.example.com"`、`"Domain":" live.example.push.com"`及`"App":"live"`的錄製任務，則在調用[CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)新增錄製配置時，`Vhost`的值應為`live.example.com`，`App`的值應為`live`或`*`。

<span id="722109d2"></span>
## 需求


* 使用限制：同一路流必須在上一個錄製任務結束後，才能建立新的錄製任務。

* 流中斷策略：若流中斷超過 120 秒，錄製任務將立即停止。若中斷時長在 120 秒以內，則錄製將根據[錄製配置](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)中定義的規則繼續進行。

* 頻率限制：每個帳戶每秒最多 50 次查詢。

* 前置條件：啟動錄製任務前，必須為對應的`Vhost`、`Domain`及`App`配置錄製設置。詳情請參見[CreateRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023)。


<span id="a60cf2a4"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreatePullRecordTask&Version=2023\-01\-01


<span id="29eb6e50"></span>
## 請求參數

<span id="75ca53a5"></span>
### 通用參數

所有 API 調用除需傳入 API 專屬參數外，還需傳入[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="24b22b6f"></span>
### 查詢參數


|參數 |數據類型 |是否必填 |示例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`CreatePullRecordTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="2dd6a206"></span>
### Body 參數


|參數 |數據類型 |是否必填 |示例值 |說明 |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空間。可調用[ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 查看所用錄製配置的`Vhost`值。 |
|Domain |String |是 |`push.example.com` |直播流所用的推流域名或拉流域名。可調用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面獲取域名。 |
|App |String |是 |`Live` |應用名稱，即直播流地址中的`AppName`欄位值，支持大小寫字母（A\-Z, a\-z）、數字（0\-9）、下劃線（_）、連字符（\-）及點（.），長度為 1 至 30 個字符。 |
|Stream |String |是 |`example_stream` |串流名稱，即直播串流地址中`StreamName`欄位的值，支援由大寫及小寫字母（A \- Z，a \- z）、數字（0 \- 9）、字母、底線（_）、連字號（\-）及句點（.）組成，長度為1至100個字元。 |
|StreamURL |String |是 |`http://example.push.com/Live/example_stream.flv` |待錄製的直播串流拉流地址。<br><br>tip<br><br>目前僅支援FLV格式的拉流地址。 |
|StartTime |String |否 |`2023-06-30T15:04:05Z` |指定錄製任務的開始時間。時間戳記採用RFC3339格式，精確到秒。預設為空，表示立即開始。 |
|EndTime |String |否 |`2023-06-30T15:05:05Z` |指定錄製任務的結束時間，時間戳記採用RFC3339格式，精確到秒。預設值為空，表示錄製將持續至直播結束。 |


<span id="6af9371c"></span>
## 響應參數

有關 API 專屬響應參數，請參見下表。更多詳情請參見[請求響應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|參數 |資料型別 |範例值 |說明 |
|---|---|---|---|
|TaskId |String |`f831f3b0********1aa4dcf7621` |任務ID，錄製任務的唯一識別碼。 |


<span id="933121a9"></span>
## 示例

<span id="59803f74"></span>
### 請求示例

```JSON
POST https://open.byteplusapi.com/?Action=CreatePullRecordTask&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "push.example.com",
    "App": "Live",
    "Stream": "example_stream",
    "StreamURL": "http://example.push.com/Live/example_stream.flv",
    "StartTime": "2023-06-30T15:04:05Z",
    "EndTime": "2023-06-30T15:05:05Z"
}
```


<span id="7274cd08"></span>
### 響應示例

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreatePullRecordTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskId": "f831f3b0123412341aa4dcf7621"
    }
}
```


<span id="7685b1ca"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回此錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](#Request Parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數未通過驗證。請檢查參數型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕。當前帳戶下無請求資源（域名空間、域名、應用、配置模板、憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此AccountID無權訪問對應資源，請檢查請求參數 |請求被拒絕。當前帳戶下無請求資源（域名空間、域名、應用、配置模板、憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID的計費狀態不可用，請開通服務或充值。 |未開通視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（域名空間、域名、應用、配置模板、憑證）。建議重試。若仍返回此錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |請求創建的資源（域名空間、域名、應用、配置模板、憑證）超出限制。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |服務間發生錯誤，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |服務間發生錯誤，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
