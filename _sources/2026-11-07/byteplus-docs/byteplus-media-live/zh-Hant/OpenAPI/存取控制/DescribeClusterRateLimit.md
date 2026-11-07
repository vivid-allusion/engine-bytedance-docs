---
title: "DescribeClusterRateLimit"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeclusterratelimit-zh-TW"
---

呼叫 `DescribeClusterRateLimit` API 查詢拉流請求的頻率限制。

## 要求

速率限制：每個帳號每秒 1 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeClusterRateLimit&Version=2023\-01\-01

## 請求參數

### 公共參數

除 API 特定參數外，所有 API 都必須搭配[公共參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`DescribeClusterRateLimit` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面以取得域名空間。 |
|Domain |String |否 |`pull.example.com` |用於拉流的域名。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或造訪 BytePlus MediaLive 控制台中的[網域](https://console.byteplus.com/live/main/domain/list)頁面以取得域名。 |

## 回應參數

如需唯一的 API 特定回應參數，請參閱下表。如需更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|ClusterRateLimitItemList |[ClusterRateLimitItemList](https://docs.byteplus.com/en/docs/24/107262#clusterratelimititemlist) 陣列 |`-` |限速設定。 |

### ClusterRateLimitItemList

|參數 |資料類型 |範例值 |說明 |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空間。 |
|Domain |String |`pull.example.com` |域名。 |
|Status |Integer |`0` |是否啟用限速。<br><br><br>* `0`：已啟用。<br><br>* `2`：已停用。 |
|Type |String |`ipToAll` |限速類型：<br><br><br>* `ipToAll`：限制從單一 IP 位址傳送的請求頻率。<br><br>* `url`：限制傳送到單一 URL 的請求頻率。<br><br>* `queryParam`：限制傳送到包含指定查詢參數之 URL 的請求頻率。<br><br>* `ipToUrl`：限制從單一 IP 位址傳送到相同 URL 的請求頻率。 |
|Param |String |`param1` |您要套用限速的查詢參數。 |
|RejectDuration |Integer |`60` |超過速率限制時，所有傳入請求都會遭拒絕的拒絕期間，單位為秒。 |
|RejectCode |Integer |`429` |請求遭拒絕時，客戶端收到的狀態碼。 |
|AggregationPeriod |Integer |`1` |統計期間，單位為秒，在此期間計算請求頻率。例如，如果您將 `AggregationPeriod` 設為 `10`，則每 10 秒計算一次請求頻率。 |
|Limit |Integer |`101` |在 `AggregationPeriod` 內允許的請求數上限。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeClusterRateLimit&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "DescribeClusterRateLimit",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "ClusterRateLimitItemList": [
            {
                "AggregationPeriod": 1,
                "Domain": "pull.example.com",
                "Limit": 101,
                "Param": "param1",
                "RejectCode": 429,
                "RejectDuration": 60,
                "Status": 0,
                "Type": "queryParam",
                "Vhost": "push.example.com"
            }
        ]
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 的常見錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107262#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |因目前帳號下沒有請求的資源，請求遭拒絕。資源包括域名空間、域名、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳號下沒有請求的資源，請求遭拒絕。資源包括域名空間、域名、應用程式名稱、設定和憑證。 |
|403 |RequestForbidden.BillingStatus |AccountID 的帳單狀態不可用，請啟用服務或儲值。 |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源。資源包括域名空間、域名、應用程式名稱、設定和憑證。建議重試。如果仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
