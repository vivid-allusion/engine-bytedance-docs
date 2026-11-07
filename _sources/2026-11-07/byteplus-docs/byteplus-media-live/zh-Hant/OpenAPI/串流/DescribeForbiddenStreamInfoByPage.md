---
title: "DescribeForbiddenStreamInfoByPage"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeforbiddenstreaminfobypage-2023-zh-TW"
---

調用 `DescribeForbiddenStreamInfoByPage` API，按頁獲取已禁用串流的資訊。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多查詢 1 次。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* 端點：https://open.byteplusapi.com/?Action=DescribeForbiddenStreamInfoByPage&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了特定參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeForbiddenStreamInfoByPage` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |
|PageNum |Integer |是 |`1` |頁碼。BytePlus MediaLive 將查詢結果分頁，只返回指定頁碼的結果。有效範圍：≥ 1。 |
|PageSize |Integer |是 |`10` |每頁返回的結果數量。有效範圍：1–1000。 |
|Vhost |String |否 |`push.example.com` |域名空間。若未指定，表示查詢所有域名空間下的禁用串流。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢域名所屬的域名空間。 |
|Domain |String |否 |`push.example.com` |域名。若未指定，表示查詢結果不過濾串流的域名。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢域名。 |
|App |String |否 |`live` |串流 URL 中的 AppName 欄位。若未指定，表示查詢結果不過濾串流的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。 |
|Stream |String |否 |`example_stream` |串流 URL 中的 StreamName 欄位。若未指定，表示查詢結果不過濾串流的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 100 字元。 |
|Sort |String |否 |`desc` |依結束時間排序串流。有效值包括：<br><br><br>* `asc`：升序。<br><br>* `desc`：（預設）降序。 |
|QueryType |String |否 |`fuzzy` |查詢串流的方式。<br><br><br>* `fuzzy`：模糊匹配<br><br>* `strict`：（預設）精確匹配 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/107297#streaminfolist) 陣列 |`-` |串流資訊列表。 |
|RoughCount |Integer |`1` |已結束串流的總數。 |


<span id="streaminfolist"></span>
### StreamInfoList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空間。 |
|Domain |String |`push.example.com` |推流用的域名。 |
|App |String |`live` |串流 URL 中的 AppName 欄位。 |
|Stream |String |`example_stream` |直播串流中的 StreamName 欄位。 |
|CreateTime |String |`2021-10-19T08:16:14Z` |直播串流被禁止推流的時間（UTC 時間，RFC 3339 格式，精確到秒）。 |
|EndTime |字串 |`2022-01-08T21:00:36Z` |直播流停止被禁止推流的時間。（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|狀態 |布林值 |`true` |定義流是否被禁用。<br><br><br>* `true`：已禁用。<br><br>* `false`：已啟用。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
GET https://open.byteplusapi.com/?Action=DescribeClosedStreamInfoByPage&Version=2023-01-01&PageNum=1&PageSize=10&Vhost=push.example.com&Domain=push.example.com&App=live&Stream=example_stream&Sort=desc&QueryType=fuzzy
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2021102918431901022508421700164AA1",
        "Action": "DescribeForbiddenStreamInfoByPage",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RoughCount": 1,
        "StreamInfoList": [
            {
                "App": "live",
                "CreateTime": "2021-10-19T16:16:14Z",
                "Domain": "push.example.com",
                "EndTime": "2022-01-19T05:00:36Z",
                "Status": true,
                "Stream": "example_stream",
                "Vhost": "push.example.com"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107297#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未開通計費狀態，請開通服務或充值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|403 |AccessDenied |用戶無權執行操作：%s於資源：%s |請求被拒絕。當前帳戶下無請求資源（域名空間、域名、應用、配置模板、憑證）或介面權限。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
