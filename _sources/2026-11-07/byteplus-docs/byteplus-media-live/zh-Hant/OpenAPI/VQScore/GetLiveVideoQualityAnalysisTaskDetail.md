---
title: "GetLiveVideoQualityAnalysisTaskDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getlivevideoqualityanalysistaskdetail-2023-zh-TW"
---

呼叫 `GetLiveVideoQualityAnalysisTaskDetail` API，以查詢單一影片品質分析任務的詳情，包括在指定分析點取得的影片碼率與品質分析分數。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=GetLiveVideoQualityAnalysisTaskDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GetLiveVideoQualityAnalysisTaskDetail` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Name |String |否 |`test` |要查詢的任務名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需填寫 <code>Name</code> 或 <code>ID</code> 任一項。</div><br> |
|ID |Long |否 |`cbxmc` |要查詢的任務 ID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需填寫 <code>Name</code> 或 <code>ID</code> 任一項。</div><br> |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參閱下表。更多詳情請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Task |[Task](https://docs.byteplus.com/en/docs/24/107430#task) 物件 |`-` |影片品質分析任務詳情。 |


<span id="task"></span>
### 任務


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|ID |Long |`1234567` |要查詢的任務 ID。 |
|Name |String |`test` |任務名稱。 |
|SrcURL |String |`https://live.example.com/video.flv` |測試串流的播放 URL。 |
|Interval |Integer |`5` |畫面品質評估標記點間隔。 |
|Duration |Integer |`300` |測試任務的持續時間（單位：秒）。 |
|ScoringResult |[ScoringResult](https://docs.byteplus.com/en/docs/24/107430#scoringresult) 物件 |`-` |影片品質分析結果。 |


<span id="scoringresult"></span>
### 評分結果


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|VQScoreLive |[VQScoreLive](https://docs.byteplus.com/en/docs/24/107430#vqscorelive) 陣列 |`-` |影片品質分析結果詳情。 |


<span id="vqscorelive"></span>
### VQScoreLive


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Timestamp |Integer |`1721621968` |分析點的時間戳，Unix 時間格式，精確到秒。 |
|Value |Float |`87.54` |測試點的品質分數，評分範圍為 0 到 100，分數越高，影片色彩品質越佳。不同評分區間對應不同的影片品質感知等級：<br><br><br>* 0\-60：主觀感受較差。<br><br>* 60\-70：主觀感受良好。<br><br>* 70\-100：主觀感受清晰。 |


<span id="Samples"></span>
## 樣本

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=GetLiveVideoQualityAnalysisTaskDetail&Version=2023-01-01
{
    "ID": "21312434***1234134134"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetLiveVideoQualityAnalysisTaskDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Task": {
            "TaskID": 21312434***1234134134,
            "Name": "test",
            "SrcURL": "https://pull.example.com/live/example_stream.flv",
            "Interval": 5,
            "Duration": 300,
            "ScoringResult": {
                "VQScoreLive": [
                    {
                        "Timestamp": 1721621968,
                        "Value": 87.54
                    }
                ]
            }
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107430#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.Empty |%s 為必填 |缺少參數。請檢查錯誤訊息中指定的參數是否有傳入。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定的參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.Length |%s 不得超過 %d |參數長度不正確。請檢查錯誤訊息中指定參數的長度是否超出限制。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 其中之一，%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出取值範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime 等 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：<br><br><br>* 開始時間晚於結束時間。<br><br>* 過期時間早於當前時間。 |
|400 |InvalidParam.DomainAndApp |domain 與 app 不能同時存在 |不可同時傳入 Domain 與 App。請修改輸入參數。 |
|400 |InvalidParam.VhostOrDomainEmpty |請輸入 vhost 或 domain |Vhost 或 Domain 必須至少傳入一個作為輸入參數。請修改輸入參數。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |錯誤訊息中指定的資源正在使用中，導致無法刪除。請釋放該資源後重試。 |
|403 |RequestForbidden |*  |因當前帳號下無請求的資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳號下無請求的資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未開通視頻直播服務或帳號已欠費，導致賬單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到域名空間（Vhost）。請檢查傳入的域名空間是否與實際使用的域名空間一致。 |
|404 |ResourceNotFound.DomainNotExist |未找到 domain |未找到域名（Domain）。請檢查傳入的域名是否與實際使用的域名一致。 |
|404 |ResourceNotFound.AppNotExist |未找到 app |未找到 App 名稱（App）。請檢查傳入的 App 名稱是否與實際使用的 App 名稱一致。 |
|404 |ResourceNotFound.PresetNotExist |未找到 preset |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|429 |RequestLimitExceeded |*  |請求建立的資源（包括域名空間、域名、App 名稱、配置、憑證）超出限制。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |請求建立的資源（包括域名空間、域名、App 名稱、配置、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與虛擬主機或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.ServicesOrBilling |發生與服務或帳單相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設值相關的內部錯誤，請聯絡管理員。 |發生與預設值相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Stream |發生與串流相關的內部錯誤，請聯絡管理員。 |發生與串流相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
