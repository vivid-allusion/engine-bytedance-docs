---
title: "CreateLiveVideoQualityAnalysisTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createlivevideoqualityanalysistask-2023-zh-TW"
---

調用 `CreateLiveVideoQualityAnalysisTask` API 以建立具有指定時長的影片畫質分析任務。該任務將根據您設定的間隔獲取每個分析點的即時碼率，並對分析點的畫質進行評分。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳號每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateLiveVideoQualityAnalysisTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須傳入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateLiveVideoQualityAnalysisTask` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Name |String |否 |`testname` |任務名稱，預設為空且必須唯一。由 1 至 50 個字元組成，包括數字（0\-9）、大小寫字母（A\-Z, a\-z）、底線（_）、連字號（\-）及句點（.）。 |
|SrcURL |String |是 |`https://pull.example.com/live/example_stream.flv` |待測影片串流的播放位址。系統將使用此位址獲取影片串流並進行畫質評估。支援 FLV、HLS、RTMP 串流位址。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">請確保所提供的位址可存取且影片串流可正常播放。若位址無效或影片串流不存在，評估任務將無法正常進行。</div><br> |
|Interval |Integer |否 |`5` |設定畫質評分的間隔時間，表示系統每隔指定秒數評估一次影片串流畫質。單位為秒，預設值為 10，可設定範圍為 [3,10]。 |
|Duration |Integer |否 |`300` |評估任務的持續時間，即任務開始至結束的時間長度。單位為秒，預設為 180，取值範圍為 [60, 300]。 |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Name |String |`concert` |任務名稱。 |
|ID |Long |`123983123` |任務 ID。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=CreateLiveVideoQualityAnalysisTask&Version=2023-01-01
{
    "Name": "test",
    "SrcURL": "https://pull.example.com/live/example_stream.flv",
    "Interval": 5,
    "Duration": 300
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateLiveVideoQualityAnalysisTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Name": "testname",
        "ID": 123983123
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與當前操作相關的錯誤碼。如需其他錯誤碼，請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107353#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Empty |%s 為必填 |缺少參數。請檢查錯誤訊息中指定的參數是否有傳入。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.Length |%s 不得超過 %d 字元 |參數長度不正確。請檢查錯誤訊息中指定參數的長度是否超過限制。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一，%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出允許範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime 等。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：<br><br><br>* 開始時間晚於結束時間。<br><br>* 過期時間早於目前時間。 |
|400 |InvalidParam.DomainAndApp |domain 和 app 不可同時存在 |不可同時傳入 Domain 和 App。請修改輸入參數。 |
|400 |InvalidParam.VhostOrDomainEmpty |請輸入 vhost 或 domain |Vhost 或 Domain 其中之一需作為輸入參數傳入。請修改輸入參數。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，導致無法刪除。請釋放資源後再重試。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 的計費狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用的網域名稱空間一致。 |
|404 |ResourceNotFound.DomainNotExist |未找到 domain |未找到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|404 |ResourceNotFound.AppNotExist |未找到 app |未找到 App 名稱（App）。請檢查傳入的 App 名稱是否與實際使用的 App 名稱一致。 |
|404 |ResourceNotFound.PresetNotExist |未找到 preset |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|429 |RequestLimitExceeded |*  |請求建立的資源（包括網域名稱空間、網域名稱、App 名稱、配置、憑證）超過限制。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |請求建立的資源（包括網域名稱空間、網域名稱、App 名稱、配置、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與虛擬主機或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.ServicesOrBilling |發生與服務或帳單相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設值相關的內部錯誤，請聯絡管理員。 |發生與預設值相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Stream |發生與串流相關的內部錯誤，請聯絡管理員。 |發生與串流相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
