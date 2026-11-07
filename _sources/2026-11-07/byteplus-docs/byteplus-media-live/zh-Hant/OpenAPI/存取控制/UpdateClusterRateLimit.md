---
title: "UpdateClusterRateLimit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updateclusterratelimit-zh-TW"
---

呼叫 `UpdateClusterRateLimit` API，以新增或修改拉流請求的頻率限制。

## 使用場景

您可以透過此操作執行以下任一項：

* 限制來自單一 IP 位址的請求頻率。

* 限制來自單一 IP 位址且傳送至相同 URL 的請求頻率。

* 限制傳送至單一 URL 的請求頻率。

* 限制傳送至包含指定查詢參數之 URL 的請求頻率。

> **说明**

> 頻率限制會依邊緣叢集套用，而非套用於整個網路。舉例來說，假設來自特定 IP 位址的請求頻率限制設定為每秒 50 次。若叢集 A 和叢集 B 在一秒內都收到來自某個 IP 位址的 50 個請求，則不會發生錯誤。不過，若叢集 A 收到 101 個請求，而叢集 B 在同一秒內仍收到 50 個請求，則在拒絕期間，該 IP 位址後續傳送且由叢集 A 收到的任何請求都會遭到封鎖。另一方面，叢集 B 不會受到影響。

## 要求

速率限制：每個帳號每秒 1 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateClusterRateLimit&Version=2023\-01\-01

## 請求參數

### 公共參數

除了 API 特定參數外，呼叫所有 API 時都必須使用[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`UpdateClusterRateLimit` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### Body 參數

|參數 |資料類型 |必填 |範例值 |描述 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |用於拉流的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的[網域](https://console.byteplus.com/live/main/domain/list)頁面，以取得網域名稱。 |
|Status |Integer |否 |`0` |是否啟用速率限制。<br><br><br>* `0`：啟用速率限制。<br><br>* `2`：停用速率限制。 |
|Type |String |是 |`ipToAll` |您要設定的速率限制類型：<br><br><br>* `ipToAll`：限制來自單一 IP 位址的請求頻率。<br><br>* `url`：限制傳送至單一 URL 的請求頻率。<br><br>* `queryParam`：限制傳送至包含指定查詢參數之 URL 的請求頻率。<br><br>* `ipToUrl`：限制來自單一 IP 位址且傳送至相同 URL 的請求頻率。 |
|Param |String |否 |`param1` |您要套用速率限制的查詢參數。<br><br>> **说明**<br><br><br>> 此參數僅在同時符合以下條件時為必填且生效：<br><br><br><br>* > `Type` 設定為 `queryParam`。<br><br><br>* > [技術支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)已為您的帳號啟用查詢參數速率限制。<br> |
|RejectDuration |Integer |否 |`1` |超過速率限制時，所有傳入請求都會被拒絕的拒絕期間，以秒為單位。值範圍為 [1, 10080]。預設值為 `1`。 |
|RejectCode |Integer |否 |`429` |請求遭拒絕時，客戶端收到的狀態碼。預設值為 `429`。 |
|AggregationPeriod |Integer |否 |`1` |統計期間，以秒為單位，在此期間會計算請求頻率。例如，若您將 `AggregationPeriod` 設定為 `10`，則每 10 秒計算一次請求頻率。值範圍為 [1, 3600]。預設值為 `1`。 |
|Limit |Integer |是 |`101` |在 `AggregationPeriod` 內允許的最大請求數。值範圍為 [0, 100,000]。 |

## 回應參數

此 API 只會在回應中傳回[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateClusterRateLimit&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Type": "ipToAll",
    "Limit": 101
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateClusterRateLimit",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 公共錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107269#request-parameters)描述進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |由於目前帳號下沒有請求的資源，因此請求遭拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 沒有存取對應資源的權限，請檢查請求參數 |由於目前帳號下沒有請求的資源，因此請求遭拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請啟用服務或儲值。 |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、設定和憑證）。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |Internal Service 逾時。請聯絡管理員。 |Internal Service 逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
