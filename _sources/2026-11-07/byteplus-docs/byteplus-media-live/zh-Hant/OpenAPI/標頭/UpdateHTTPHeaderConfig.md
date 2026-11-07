---
title: "UpdateHTTPHeaderConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatehttpheaderconfig-zh-TW"
---

調用 `UpdateHTTPHeaderConfig` API，可在邊緣伺服器回應給用戶端時新增額外的 HTTP 標頭，或在回源任務中向第三方源站伺服器發送請求時新增額外的 HTTP 標頭。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateHTTPHeaderConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateHTTPHeaderConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |該網域所屬的網域名稱空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取此資訊。 |
|Domain |String |否 |`pull.example.com` |拉流網域名稱。如未指定，則配置將套用於該網域名稱空間下的所有拉流網域名稱。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取網域名稱。 |
|Phase |Integer |是 |`0` |要更新的 HTTP 標頭類型：<br><br><br>* `0`：邊緣伺服器回應給用戶端時；<br><br>* `1`：回源任務中向第三方源站伺服器發送請求時。 |
|HeaderConfigList |[HeaderConfigList](https://docs.byteplus.com/en/docs/24/107337#headerconfiglist) 陣列 |是 |`無` |要新增的 HTTP 標頭清單。<br><br>最多可新增 20 個標頭。 |
|BlockOriginal |Integer |否 |`0` |是否移除原有標頭。<br><br><br>* `0`：保留；<br><br>* `1`：移除。 |
|Enable |Boolean |是 |`true` |是否啟用該網域的配置。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。 |


<span id="headerconfiglist"></span>
### HeaderConfigList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|HeaderKey |String |否 |`Content-Type` |標頭名稱，必須唯一且不得超過 1024 個字元。 |
|HeaderValue |String |否 |`text/plain` |標頭值。可將常數或變數指定為標頭值。<br><br>對於回應中的標頭，標頭值可為以下變數：<br><br><br>* `${domain}`：用戶端請求中的網域名稱。範例：`example.com`<br><br>* `${uri}`：用戶端請求的路徑（不含查詢參數）。若用戶端請求被重寫，該變數表示重寫後的路徑。範例：`/dir/sample.php`<br><br>* `${args}`：用戶端請求中的查詢參數。若用戶端請求被重寫，該變數表示重寫後的參數。範例：`color=red&n=10`<br><br>* `${remote_addr}`：發送請求的用戶端 IP 位址。範例：`10.10.10.10`<br><br>* `${server_addr}`：回應用戶端請求的邊緣伺服器 IP 位址。範例：`10.10.10.10`<br><br><br>對於請求中的標頭，標頭值可為以下變數：<br><br><br>* `${upstream_host}`：回源請求中的網域名稱。範例：`example.com`<br><br>* `${upstream_uri}`：回源請求的路徑（不含查詢參數）。若請求已被重寫，此變數表示重寫後的路徑。範例：`/dir/sample.php`<br><br>* `${upstream_args}`：源站拉取請求中的查詢參數。若請求已被重寫，此變數表示重寫後的參數。範例：`color=red&n=10`<br><br>* `${remote_addr}`：發送請求的客戶端 IP 位址。範例：`10.10.10.10` |
|HeaderFieldType |整數 |是 |`0` |標頭值的類型：<br><br><br>* `0`：常數；<br><br>* `1`：變數。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateHTTPHeaderConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Phase": 0,
    "HeaderConfigList": [
        {
            "HeaderKey": "Content-Type",
            "HeaderValue": "text/plain",
            "HeaderFieldType": 0
        }
    ],
    "BlockOriginal": 0,
    "Enable": true
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UpdateHTTPHeaderConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107337#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包含網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包含網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請啟用服務或儲值。 |尚未啟用影音直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包含網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到網域名稱 |未找到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
