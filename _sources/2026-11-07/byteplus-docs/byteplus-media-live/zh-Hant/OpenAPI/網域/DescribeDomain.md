---
title: "DescribeDomain"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describedomain-2023-zh-TW"
---

呼叫 `DescribeDomain` API 以查詢指定域名的資訊，包括域名空間、CNAME 地址及域名狀態等。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒僅可查詢 1 次。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeDomain&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeDomain` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |String 陣列 |是 |`["push.example.com","pull.example.com"]` |欲查詢的域名清單。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |[DomainList](https://docs.byteplus.com/en/docs/24/107287#domainlist) 陣列 |`-` |域名相關資訊。 |


<span id="domainlist"></span>
### DomainList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |對應的域名空間。 |
|Domain |String |`push.example.com` |域名。 |
|Status |Integer |`0` |域名狀態。有效值包括：<br><br><br>* `0`：啟用。<br><br>* `1`：審核中。<br><br>* `2`：停用。注意，停用的域名無法使用。<br><br>* `3`：已刪除。<br><br>* `4`：審核未通過。您需重新提交域名進行審核。<br><br>* `5`：因帳戶逾期付款而凍結。<br><br>* `6`：因未備案而封鎖域名。 |
|Type |String |`push` |域名類型。有效值包括：<br><br><br>* `push`：推流域名。<br><br>* `pull-flv`：拉流域名。 |
|Region |String |`cn` |加速區域。有效值包括：<br><br><br>* `oversea`：（預設）中國大陸以外。<br><br>* `cn`：中國大陸。<br><br>* `global`：全球。<br><br><br>您必須先取得域名的互聯網內容提供者（ICP）許可證。 |
|CNAME |String |`push.example.com.c.byteplusfcdn.com` |分配給域名的 CNAME 地址。 |
|CnameCheck |Integer |`0` |域名的 CNAME 狀態。<br><br><br>* `0`：未配置。<br><br>* `1`：已配置。 |
|DomainCheck |Integer |`0` |域名可用性。<br><br><br>* `0`：正常。域名可用且已配置。<br><br>* `1`：配置中。域名可用且正在配置。<br><br>* `2`：不可用。域名不可用。 |
|ICPCheck |Integer |`0` |域名是否已完成 ICP 登記。當域名加速區域包含中國大陸時，會驗證此參數。若域名加速區域不包含中國大陸，請忽略此參數。 |
|CreateTime |String |`2006-01-02T15:04:05Z` |域名建立時間。 |
|CertDomain |String |`push.example.com` |由憑證保護的萬用域名。 |
|HTTP2 |Boolean |`false` |是否啟用 HTTP/2 協議。值如下：<br><br><br>* `false`：未啟用<br><br>* `true`：已啟用 |
|ChainID |String |`21614` |憑證的鏈 ID。 |
|PushDomain |String |`push.example.com` |推流關聯域名。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeDomain&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ]
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeDomain",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            {
                "Domain": "push.example.com",
                "Status": 0,
                "Type": "push",
                "Region": "cn",
                "CName": "push.example.com.c.byteplusfcdn.com",
                "PushDomain": "push.example.com",
                "Vhost": "push.example.com",
                "CnameCheck": 0,
                "DomainCheck": 0,
                "CreateTime": "2006-01-02T15:04:05Z"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107287#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證未通過。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
