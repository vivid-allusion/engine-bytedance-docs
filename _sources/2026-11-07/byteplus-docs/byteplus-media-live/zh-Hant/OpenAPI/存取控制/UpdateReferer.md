---
title: "UpdateReferer"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatereferer-2023-zh-TW"
---

呼叫 `UpdateReferer` API，建立網域層級的 Referer 封鎖清單或允許清單組態。

## 要求

* 限制：依預設，您最多可為同一個網域建立 100 條 Referer 規則。如需建立更多規則，請聯絡[技術支援](https://console.byteplus.com/workorder/create)取得協助。

* 速率限制：每個帳號每秒 1 次查詢。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateReferer&Version=2023\-01\-01

## 請求參數

### 通用參數

呼叫所有 API 時，除 API 特定參數外，還必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查詢

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Action |String |是 |`UpdateReferer` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |此組態套用的網域名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱空間。 |
|Domain |String |是 |`pull.example.com` |拉流的網域名稱。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱。 |
|RefererInfoList |[RefererInfoList](https://docs.byteplus.com/en/docs/24/107255#refererinfolist) 的陣列 |是 |`-` |Referer 資訊清單。<br><br>在同一個 `Domain` 內，您最多可設定 100 條 Referer 規則，且單一請求最多可設定 100 條 Referer 規則。 |

### RefererInfoList

|參數 |資料類型 |必填 |範例值 |說明 |
|---|---|---|---|---|
|Key |String |是 |`referer` |Referer 組態的關鍵字。只能設定為 `referer`。 |
|Type |String |是 |`deny` |Referer 限制類型。可取以下值：<br><br><br>* `deny`：封鎖清單組態。若拉流請求符合 Referer 規則，則會被拒絕。<br><br>* `allow`：允許清單組態。若拉流請求符合 Referer 規則，則會被允許。<br><br><br>> **说明**<br><br><br>> 在同一次 API 呼叫中，`RefererInfoList` 內的所有規則都必須使用相同的 `Type` 值。<br> |
|Value |String |否 |`live.example1.net` |Referer 限制規則，即要驗證的拉流請求 Referer 值。可新增完整網域名稱或萬用字元網域名稱。最多可輸入 300 個字元。 |

## 回應參數

此 API 在回應中僅傳回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateReferer&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RefererInfoList": [
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example1.net"
        },
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example2.net"
        },
        {
            "Type": "allow",
            "Key": "referer",
            "Value": "live.example3.net"
        }
    ]
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "UpdateReferer",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。如需其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|狀態碼 |錯誤碼 |錯誤訊息 |說明 |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。若仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參閱[請求參數](https://docs.byteplus.com/en/docs/24/107255#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料類型是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一，%s 應介於 %d 和 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出取值範圍。 |
|400 |InvalidParam.Length |%s 不應長於 %d |參數長度不正確。請檢查錯誤訊息中指定參數的長度是否超出限制。 |
|403 |RequestForbidden |\- |由於目前帳號下沒有請求的資源，請求遭到拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |由於目前帳號下沒有請求的資源，請求遭到拒絕（資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請啟用服務或儲值。 |視訊直播服務尚未啟用，或帳號欠費，導致帳單不可用。請檢查服務啟用狀態和帳號欠費狀態。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。建議重試。若仍傳回此錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生資料庫相關內部錯誤，請聯絡管理員。 |發生資料庫相關內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生 vhost 或 domain 相關內部錯誤，請聯絡管理員。 |發生與網域名稱空間 (Vhost) 或網域名稱 (Domain) 相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
