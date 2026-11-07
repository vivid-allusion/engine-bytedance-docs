---
title: "UpdateRegionAccessRule"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateregionaccessrule-zh-TW"
---

呼叫 `UpdateRegionAccessRule` API 以為指定的網域名稱建立地理限制。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateRegionAccessRule&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 呼叫時，除了 API 專屬參數外，還必須包含 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRegionAccessRule` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該網域所屬的網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |拉流網域名稱。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得用於建立地理限制的網域名稱。 |
|RegionAccessRule |[RegionAccessRule](https://docs.byteplus.com/en/docs/24/107329#regionaccessrule) 物件 |是 |`-` |地理限制。 |


<span id="regionaccessrule"></span>
### RegionAccessRule


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Type |String |是 |`allow` |存取控制類型。<br><br><br>* `allow`：僅允許指定地區的請求存取你的網域名稱。<br><br>* `deny`：禁止指定地區的請求存取你的網域名稱。 |
|Enable |String |是 |`true` |是否啟用此設定。<br><br><br>* `true`：啟用設定。<br><br>* `false`：停用設定。 |
|CountryList |Array of String |否 |`CN` |在允許清單或封鎖清單中的國家和地區。請使用 ISO 3166\-1 代碼表示國家和地區，例如 CN、SG 或 US。 |
|ProvinceList |Array of String |否 |`HK` |在允許清單或封鎖清單中的省份，目前僅支援中國的香港、澳門和台灣地區。對應的代碼分別為 HK、MO 和 TW。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateRegionAccessRule&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RegionAccessRule": [
        {
            "Type": "allow",
            "Enable": true,
            "CountryList": [
                "CN",
                "SG"
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
        "Action": "UpdateRegionAccessRule",
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
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107329#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.DomainAndApp |domain 和 app 不能同時存在 |不可同時傳入 Domain 和 App。請修改輸入參數。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、設定與憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、設定與憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的帳單狀態不可用，請啟用服務或充值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到域名 |未找到該域名（Domain）。請檢查傳入的域名是否與實際使用的域名一致。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯繫管理員。 |發生與資料庫相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
