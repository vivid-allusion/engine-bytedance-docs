---
title: "ListLiveVideoQualityAnalysisTasks"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listlivevideoqualityanalysistasks-2023-zh-TW"
---

調用 `ListLiveVideoQualityAnalysisTasks` API 以查詢視頻質量分析任務資訊列表。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListLiveVideoQualityAnalysisTasks&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須傳入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListLiveVideoQualityAnalysisTasks` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Names |Array of String |否 |`["test"]` |查詢任務名稱列表，預設為空，表示查詢結果不會依任務名稱過濾。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Name</code> 與 <code>ID</code> 不可同時輸入。</div><br> |
|IDs |Array of Long |否 |`[23123523]` |查詢任務 ID 列表，預設為空，表示查詢結果不會依任務 ID 過濾。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Name</code> 與 <code>ID</code> 不可同時輸入。</div><br> |
|PageNum |Integer |是 |`1` |資料查詢頁碼，必須為正整數。 |
|PageSize |Integer |是 |`10` |每頁顯示的資料筆數，最大為 1000。 |


<span id="Response parameters"></span>
## 回應參數

如需查看 API 專屬回應參數，請參閱下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Tasks |Array of [Tasks](https://docs.byteplus.com/en/docs/24/107398#tasks) |`-` |視頻質量分析任務列表。 |
|PageNum |Integer |`1` |查詢資料的頁碼。 |
|PageSize |Integer |`10` |每頁顯示的項目數。 |


<span id="tasks"></span>
### 任務


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Name |String |`concert` |任務名稱。 |
|SrcURL |String |`https://pull.example.com/live/example_stream.flv` |分析用的串流地址。 |
|Interval |Integer |`5` |質量分析點的間隔（秒）。預設為 10，合法範圍為 3 到 10。 |
|Duration |Integer |`300` |分析任務的持續時間 |
|ID |Long |`23123523` |任務 ID。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListLiveVideoQualityAnalysisTasks&Version=2023-01-01
{
    "PageNum": 1,
    "PageSize": 10,
    "IDs": [
        23123523
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListLiveVideoQualityAnalysisTasks",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Tasks": [
            {
                "Name": "test",
                "SrcURL": "https://pull.example.com/live/example_stream.flv",
                "Interval": 5,
                "Duration": 300,
                "ID": 23123523
            }
        ],
        "PageNum": 1,
        "PageSize": 10
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107398#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Empty |%s 為必填 |缺少參數。請檢查錯誤訊息中指定的參數是否有傳入。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.Length |%s 不得超過 %d |參數長度不正確。請檢查錯誤訊息中指定的參數長度是否超出限制。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 到 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出允許範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime，及其他類似情況。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：<br><br><br>* 開始時間晚於結束時間。<br><br>* 過期時間早於目前時間。 |
|400 |InvalidParam.DomainAndApp |domain 與 app 不可同時存在 |不可同時傳入 Domain 與 App。請修改輸入參數。 |
|400 |InvalidParam.VhostOrDomainEmpty |請輸入 vhost 或 domain |Vhost 或 Domain 其中之一需作為輸入參數傳入。請修改輸入參數。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，因此無法刪除。請釋放該資源後重試。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳號下無請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、設定及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為當前帳號下無請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、設定及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 的計費狀態不可用，請開通服務或儲值。 |尚未啟用視訊直播服務或帳號欠費，導致帳單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、設定及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |找不到 vhost |找不到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用中的一致。 |
|404 |ResourceNotFound.DomainNotExist |找不到 domain |找不到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用中的一致。 |
|404 |ResourceNotFound.AppNotExist |找不到 app |找不到應用程式名稱（App）。請檢查傳入的應用程式名稱是否與實際使用中的一致。 |
|404 |ResourceNotFound.PresetNotExist |找不到 preset |找不到設定。請檢查傳入的設定是否與已建立的設定一致。 |
|429 |RequestLimitExceeded |*  |請求建立的資源（包括網域名稱空間、網域名稱、應用程式名稱、設定、憑證）超出上限。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |請求建立的資源（包括網域名稱空間、網域名稱、應用程式名稱、設定、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.ServicesOrBilling |發生與服務或帳單相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Stream |發生與串流相關的內部錯誤，請聯絡管理員。 |發生與串流相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
