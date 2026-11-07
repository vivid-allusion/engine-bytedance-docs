---
title: "DescribeRecordTaskFileHistory"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describerecordtaskfilehistory-2023-zh-TW"
---

查詢指定網域名稱空間的歷史錄製資訊，例如錄製時長、檔案格式、開始時間與結束時間。進行中的錄製不會被檢索。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多可查詢 10 次。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeRecordTaskFileHistory&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeRecordTaskFileHistory` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |網域名稱空間。預設為空，表示將查詢你 BytePlus MediaLive 下所有網域名稱空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該網域所屬的網域名稱空間。 |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。預設為空，表示將查詢該網域名稱空間下所有 AppName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 30 字元。 |
|Stream |String |否 |`stream-123` |直播串流 URL 中的 StreamName 欄位。預設為空，表示將查詢該 AppName 下所有 StreamName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 100 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若指定 <code>Stream</code>，則必須同時指定 <code>App</code>。</div><br> |
|DateFrom |String |是 |`2023-11-01T00:00:00Z` |查詢範圍的開始時間（本地時間，RFC 3339 格式，精確到秒）。查詢指定錄製任務詳細資訊時，DateFrom 應設為錄製任務開始時間之前的任意時間。 |
|DateTo |String |是 |`2023-11-07T23:59:59Z` |查詢範圍的結束時間（本地時間，RFC 3339 格式，精確到秒）。DateTo 必須晚於 DateFrom，且 DateTo 與 DateFrom 的間隔不得超過 7 天。 |
|PageNum |Integer |是 |`1` |頁碼。BytePlus MediaLive 將查詢結果分頁，僅返回指定頁面的結果。 |
|PageSize |Integer |是 |`30` |每頁查詢結果數量。 |
|Type |String |否 |`tos` |儲存類型。<br><br><br>* `tos`：BytePlus TOS；<br><br>* `vod`：BytePlus VOD。 |


<span id="Response parameters"></span>
## 回應參數

專屬於 API 的回應參數請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Data |[Data](https://docs.byteplus.com/en/docs/24/107334#data) 陣列 |`-` |錄製紀錄列表。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107334#pagination) 物件 |`-` |分頁資訊。 |


<span id="data"></span>
### 資料


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`live` |AppName 欄位。 |
|Stream |String |`stream-123` |StreamName 欄位。 |
|儲存桶 |字串 |`live-record-test` |儲存桶名稱或 BytePlus TOS。 |
|路徑 |字串 |`est6/record/push.example.org/live/testStream413` |錄製檔案的儲存路徑，格式為 `/record/{vhost}/{app}/{stream}`。 |
|時長 |字串 |`01:34` |錄製檔案的長度。 |
|格式 |字串 |`m3u8` |錄製檔案的格式。 |
|開始時間 |字串 |`2023-11-01 00:49:17` |錄製開始的時間。 |
|結束時間 |字串 |`2023-11-01 00:45:44` |錄製結束的時間。 |
|檔案名稱 |字串 |`1630331125_16303312***.m3u8` |錄製檔案的名稱。 |
|Vid |字串 |`v03713g100**********bob16pnh65g` |錄製檔案在 BytePlus VOD 中的 ID。 |
|開始時間 UTC |字串 |`2023-10-31T16:49:17Z` |錄製開始的時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|結束時間 UTC |字串 |`2023-10-31T00:45:44Z` |錄製結束的時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |


<span id="pagination"></span>
### 分頁


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PageCur |整數 |`1` |目前頁碼。 |
|PageSize |整數 |`10` |每頁結果數量。 |
|PageTotal |整數 |`1` |總頁數。 |
|TotalCount |整數 |`1` |檢索到的錄製檔案總數。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST
{
    "Vhost": "push.example.com",
    "App": "live",
    "Stream": "stream-123",
    "DateFrom": "2023-11-01T00:00:00Z",
    "DateTo": "2023-11-07T23:59:59Z",
    "PageNum": 1,
    "PageSize": 30,
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "202108302155380102252431000500BC2E",
        "Action": "DescribeRecordTaskFileHistory",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "Vhost": "push.example.com",
                "App": "live",
                "Stream": "testStream413",
                "Bucket": "live-test6",
                "Path": "est6/record/push.example.com/live/testStream413",
                "Duration": "01:34",
                "StartTime": "2021-08-16 00:00:00",
                "EndTime": "2021-08-17 00:00:00",
                "StartTimeUTC": "2021-08-16T00:00:00Z",
                "EndTimeUTC": "2021-08-17T00:00:00Z",
                "Format": "",
                "FileName": "1630331125_16303312***.m3u8"
            }
        ],
        "Pagination": {
            "PageCur": 1,
            "PageSize": 10,
            "PageTotal": 1,
            "TotalCount": 1
        }
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107334#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
