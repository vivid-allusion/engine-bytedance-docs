---
title: "DescribeClosedStreamInfoByPage"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclosedstreaminfobypage-2023-zh-TW"
---

調用 `DescribeClosedStreamInfoByPage` API，按頁獲取已結束直播流的資訊。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳號每秒 1 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* Endpoint：https://open.byteplusapi.com/?Action=DescribeClosedStreamInfoByPage&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeClosedStreamInfoByPage` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |
|PageNum |Integer |是 |`1` |頁碼。BytePlus MediaLive 會將查詢結果分頁，只返回指定頁面的結果。有效範圍：≥ 1。 |
|PageSize |Integer |是 |`10` |每頁返回的結果數量。有效範圍：1–1000。 |
|Vhost |String |否 |`push.example.net` |域名空間。若不指定，則查詢所有域名空間下已結束的直播流。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取域名所屬的域名空間。 |
|Domain |String |否 |`push.example.net` |域名。若不指定，則查詢結果不會過濾直播流的域名。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。若不指定，則查詢結果不會過濾直播流的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。 |
|Stream |String |否 |`stream001` |直播流 URL 中的 StreamName 欄位。若不指定，則查詢結果不會過濾直播流的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 100 個字元。 |
|Sort |String |否 |`desc` |依結束時間排序流。有效值包括：<br><br><br>* `asc`：升序。<br><br>* `desc`：（預設）降序。 |
|EndTimeFrom |String |是 |`2021-10-02T19:39:26Z` |查詢區間的起始時間（UTC，RFC 3339 格式）。會查詢結束時間晚於此時間的流。預設值為當前時間減去 24 小時。 |
|EndTimeTo |String |是 |`2021-10-02T19:39:26Z` |查詢區間的結束時間（UTC，RFC 3339 格式）。會查詢結束時間早於此時間的流。預設值為當前時間。 |
|SourceType |String |否 |`push` |欲查詢流的來源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 並從中拉取的流。<br><br>* `relay`：從第三方 CDN 拉取的流。 |
|QueryType |String |否 |`fuzzy` |查詢流的方式。<br><br><br>* `fuzzy`：模糊匹配<br><br>* `strict`：（預設）完全匹配 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/107253#streaminfolist) 陣列 |`-` |串流資訊列表。 |
|RoughCount |整數 |`1` |已結束串流的總數。 |


<span id="streaminfolist"></span>
### StreamInfoList


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |字串 |`push.example.com` |網域名稱空間。 |
|Domain |字串 |`push.example.com` |網域名稱。 |
|App |字串 |`live` |直播串流 URL 中的 AppName 欄位。 |
|Stream |字串 |`exampel_stream` |直播串流 URL 中的 StreamName 欄位。 |
|StartTime |字串 |`2021-10-29T00:55:50Z` |串流開始時間。 |
|EndTime |字串 |`2021-10-29T09:30:17Z` |串流結束時間。 |
|SourceType |字串 |`push` |欲查詢串流的來源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 並從其拉取的串流。<br><br>* `relay`：從第三方 CDN 拉取的串流。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
GET https://open.byteplusapi.com/?Action=DescribeClosedStreamInfoByPage&Version=2023-01-01&PageNum=1&PageSize=10&Vhost=push.example.com&Domain=push.example.com&App=live&Stream=example_stream&Sort=desc&EndTimeFrom=2021-10-02T19:39:26Z&EndTimeTo=2021-10-02T19:39:26Z&SourceType=push&QueryType=fuzzy
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202110291823170102250842170814F5D6",
        "Action": "DescribeClosedStreamInfoByPage",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "RoughCount": 1,
        "StreamInfoList": [
            {
                "App": "live",
                "Domain": "push.example.com",
                "EndTime": "2021-10-29 17:31:57",
                "StartTime": "2021-10-29 17:30:17",
                "Stream": "exampel_stream",
                "Vhost": "push.example.com"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107253#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料類型是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定參數是否包含非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime 等。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：開始時間晚於結束時間。到期時間早於目前時間。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未啟用計費狀態，請開通服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|403 |AccessDenied |使用者無權於資源 %s 執行操作：%s |請求被拒絕。目前帳戶下無請求資源（網域名稱空間、網域名稱、應用、配置模板、憑證）或介面權限。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與虛擬主機或網域相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
