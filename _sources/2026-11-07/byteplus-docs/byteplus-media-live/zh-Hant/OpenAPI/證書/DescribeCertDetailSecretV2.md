---
title: "DescribeCertDetailSecretV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdetailsecretv2-2023-zh-TW"
---

調用 `DescribeCertDetailSecretV2` API，可透過憑證 ID 或憑證鏈 ID 查看憑證的詳細資訊。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeCertDetailSecretV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCertDetailSecretV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|CertID |String |否 |`812******1` |憑證 ID。可調用 [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API 取得 CertID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">應僅提供 <code>ChainID</code> 或 <code>CertID</code>，不可同時提供兩者。</div><br> |
|ChainID |String |否 |`188b5c6f6b3c47728418932*******d2` |憑證的 ChainID。可調用 [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) API 取得 ChainID。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">應僅提供 <code>ChainID</code> 或 <code>CertID</code>，不可同時提供兩者。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參閱下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|CertDomainList |String 陣列 |`["live.example.com"]` |憑證所保護的網域名稱列表。 |
|ChainID |String |`188b5c6f6b3c47728418932*******d2` |憑證鏈 ID。 |
|SSL |[SSL](https://docs.byteplus.com/en/docs/24/107440#ssl) 物件 |`-` |憑證鏈資訊。 |
|CertName |String |`live.example.com` |憑證名稱。 |
|NotBefore |String |`2019-09-05T00:00:00Z` |憑證生效時間（UTC 時間，RFC 3339 格式，時間戳精確到秒）。 |
|NotAfter |String |`2020-09-04T12:00:00Z` |憑證到期時間（UTC 時間，RFC 3339 格式，時間戳精確到秒）。 |
|Status |String |`OK` |憑證狀態，各值與含義的對應關係如下。<br><br><br>* `OK`：正常；<br><br>* `Expire`：已過期；<br><br>* `30days`：有效期剩餘 30 天；<br><br>* `15days`：有效期剩餘 15 天；<br><br>* `7days`：有效期剩餘 7 天；<br><br>* `1days`：有效期剩餘 1 天。 |


<span id="ssl"></span>
### SSL


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|KeyType |String |`rsa` |憑證所使用的加密演算法，目前預設為 RSA 演算法。 |
|Chain |String 陣列 |`[ "-----BEGIN CERTIFICATE-----MIIFa**********5S98-----END CERTIFICATE-----", "-----BEGIN CERTIFICATE-----MIIEk**********0UiB-----END CERTIFICATE-----", "-----BEGIN CERTIFICATE-----MIIEN**********B5==-----END CERTIFICATE-----" ]` |憑證鏈，包括葉子憑證（伺服器憑證）、中間憑證（中間 CA 憑證）以及根憑證（根 CA 憑證）。憑證鏈中的憑證採用 PEM 編碼格式。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeCertDetailSecretV2&Version=2023-01-01
{
    "ChainID": "188b5c6f6b3c47728418932*******d2"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeCertDetailV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertDomainList": [
        "pull.example.xyz"
        ],
        "CertName": "pull.example.xyz",
        "ChainID": "37a***b22d554a3b8785f111d51a2b88",
        "NotAfter": "2024-08-03T23:59:59Z",
        "NotBefore": "2024-05-06T00:00:00Z",
        "SSL": {
        "Chain": [
            "-----BEGIN CERTIFICATE-----\nMIIF+TCCBOG***UrNyWlJ7\n-----END CERTIFICATE-----\n",
            "-----BEGIN CERTIFICATE-----\nMIIEqjCCA5K***QjJNSg==\n-----END CERTIFICATE-----\n",
            "-----BEGIN CERTIFICATE-----\nMIIDjjCCAna***Zl\nMrY=\n-----END CERTIFICATE-----\n"
        ]
        "KeyType": "rsa",
        },
        "Status": "OK"
    }
    }
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107440#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 沒有權限存取對應資源，請檢查請求參數 |請求已被拒絕。目前帳戶下不存在所請求的資源（域名空間、域名、應用、配置模板、憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 無法取得計費狀態，請啟用服務或儲值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單無法取得。請檢查服務啟用狀態及帳戶欠費狀態。 |
|403 |AccessDenied |使用者未被授權執行：%s 在資源：%s 上 |請求已被拒絕。目前帳戶下不存在所請求的資源（域名空間、域名、應用、配置模板、憑證）或介面權限。 |
|404 |ResourceNotFound |*  |未找到資源（包含域名空間、域名、應用名稱、配置及憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
