---
title: "UpdateIPAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateipaccessrule-zh-TW"
---

調用 `UpdateIPAccessRule` API，為指定的網域名稱配置 IP 阻擋清單或允許清單。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateIPAccessRule&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateIPAccessRule` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱空間。 |
|Domain |String |是 |`push.example.com` |拉流或推流用的網域名稱。您可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱。 |
|IPAccessRule |[IPAccessRule](https://docs.byteplus.com/en/docs/24/107313#ipaccessrule) 物件 |是 |`-` |IP 限制規則。 |


<span id="ipaccessrule"></span>
### IPAccessRule


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Type |String |是 |`deny` |IP 存取規則類型。值及含義如下。<br><br><br>* `allow`：允許清單。只有允許清單中的 IP 位址才可存取資源。<br><br>* `deny`：阻擋清單。阻擋清單中的 IP 位址無法存取資源。 |
|Enable |Boolean |是 |`true` |是否啟用目前的 IP 存取規則配置。值及含義如下。<br><br><br>* `true`：啟用；<br><br>* `false`：停用。 |
|IPList |Array of String |是 |`["1.1.1.2","192.168.0.1/24"]` |允許清單或阻擋清單中的 IP 位址列表。僅支援 IPv4 位址。允許 CIDR 標記法。例如，您可以指定 192.168.0.0 或 192.168.0.0/24。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateIPAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "push.example.com",
    "IPAccessRule": [
        {
            "Type": "deny",
            "Enable": true,
            "IPList": [
                "192.168.1.1",
                "192.168.1.2"
            ]
        }
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "202011121850010102250920591B011F85",
        "Action": "UpdateIPAccessRule",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107313#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Empty |%s 為必填 |缺少參數。請檢查錯誤訊息中指定的參數是否有傳入。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未開通計費狀態，請開通服務或充值。 |尚未啟用視頻直播服務或帳戶有欠費，導致帳單無法取得。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置及憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到該域名（Domain）。請檢查傳入的域名是否與實際使用的域名一致。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯繫管理員。 |發生與資料庫相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
