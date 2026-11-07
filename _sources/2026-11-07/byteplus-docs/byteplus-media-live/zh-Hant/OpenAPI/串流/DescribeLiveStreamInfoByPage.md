---
title: "DescribeLiveStreamInfoByPage"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreaminfobypagev2023-zh-TW"
---

調用 `DescribeLiveStreamInfoByPage` API，按頁獲取正在進行中的直播流資訊。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 1 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：GET

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveStreamInfoByPage&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStreamInfoByPage` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |
|PageNum |Integer |是 |`1` |頁碼。BytePlus MediaLive 會將查詢結果分頁，只返回指定頁面的結果。有效範圍：≥ 1。 |
|PageSize |Integer |是 |`10` |每頁返回的結果數量。有效範圍：1–1000。 |
|Vhost |String |否 |`push.example.com` |域名空間。如未指定，表示查詢所有域名空間下正在進行的所有直播流。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取域名所屬的域名空間。 |
|Domain |String |否 |`push.example.com` |域名。如未指定，表示查詢結果不篩選直播流的域名。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。如未指定，表示查詢結果不篩選直播流的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 30 個字元。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。如未指定，表示查詢結果不篩選直播流的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 100 個字元。 |
|StreamType |String |否 |`origin` |要查詢的流類型。如未指定，則查詢結果會包含兩種流類型。<br><br><br>* `origin`：原始流。<br><br>* `trans`：轉碼流。 |
|SourceType |String |否 |`push` |要查詢的流來源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 並拉取的流。<br><br>* `relay`：從第三方 CDN 拉取的流。 |
|QueryType |String |否 |`fuzzy` |查詢流的方式。<br><br><br>* `fuzzy`：模糊匹配<br><br>* `strict`：（預設）精確匹配 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/107375#streaminfolist) 陣列 |`-` |流資訊列表。 |
|RoughCount |Integer |`1` |流的總數。 |


<span id="streaminfolist"></span>
### StreamInfoList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|ID |Long |`1005002` |流 ID。 |
|Vhost |String |`push.example.com` |域名空間。 |
|Domain |String |`push.example.com` |域名。 |
|App |String |`live` |AppNmae 欄位。 |
|Stream |字串 |`example_stream` |StreamName 欄位。 |
|SessionStartTime |字串 |`2021-10-29T00:55:50.186Z` |直播串流會話開始的時間。 |
|SourceType |字串 |`push` |查詢的串流來源。<br><br><br>* `push`：直接推送至 BytePlus MediaLive 並從中拉取的串流。<br><br>* `relay`：從第三方 CDN 拉取的串流。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```JSON
GET https://open.byteplusapi.com/?Action=DescribeLiveStreamInfoByPage&Version=2023-01-01&PageNum=1&PageSize=10&Vhost=push.example.com&Domain=push.example.com&App=live&Stream=example_stream&StreamType=origin&SourceType=push&QueryType=fuzzy
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202110291811420102250842170013F8D2",
        "Action": "DescribeLiveStreamInfoByPage",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RoughCount": 1,
        "StreamInfoList": [
            {
                "App": "live",
                "Domain": "push.example.com",
                "ID": 1005002,
                "SessionStartTime": "2021-10-29T08:55:50.186Z",
                "Stream": "example_stream\t",
                "SourceType": "push",
                "Vhost": "push.example.com"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107375#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一 %s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未開通視頻直播服務或帳號欠費，導致無法取得帳單。請檢查服務開通狀態及帳號欠費狀態。 |
|403 |AccessDenied |使用者未獲授權執行：%s 於資源：%s |請求被拒絕。當前帳號下無請求資源（網域名稱空間、網域名稱、應用、配置範本、憑證）或介面權限。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置與憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到 vhost |未找到網域名稱空間（Vhost）。請檢查傳入的網域名稱空間是否與實際使用的網域名稱空間一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域名稱相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
