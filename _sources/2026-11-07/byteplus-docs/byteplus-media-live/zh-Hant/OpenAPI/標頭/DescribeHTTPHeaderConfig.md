---
title: "DescribeHTTPHeaderConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describehttpheaderconfig-zh-TW"
---

調用 `DescribeHTTPHeaderConfig` API 查詢指定網域名稱的 HTTP 標頭配置。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeHTTPHeaderConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeHTTPHeaderConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取該網域所屬的網域名稱空間。 |
|Domain |String |否 |`pull.example.com` |拉流網域名稱。如未指定，查詢結果將包含該網域名稱空間下所有拉流網域名稱。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取網域名稱。 |
|Phase |Integer |是 |`0` |要查詢的 HTTP 標頭配置類型：<br><br><br>* `0`：回應標頭。<br><br>* `1`：請求標頭。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求與回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|HeaderConfigList |[HeaderConfigList](https://docs.byteplus.com/en/docs/24/107290#headerconfiglist) 陣列 |`無` |網域名稱的標頭配置清單。 |


<span id="headerconfiglist"></span>
### HeaderConfigList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`example` |網域名稱空間。 |
|Domain |String |`example.com` |網域名稱。 |
|HeaderDetailList |[HeaderDetailList](https://docs.byteplus.com/en/docs/24/107290#headerdetaillist) 陣列 |`無` |要查詢的 HTTP 標頭清單。 |
|BlockOriginal |Integer |`0` |是否排除原始標頭。<br><br><br>* `0`：包含。<br><br>* `1`：排除。 |
|Enable |Boolean |`true` |是否啟用該配置。<br><br><br>* `true`：已啟用。<br><br>* `false`：未啟用。 |


<span id="headerdetaillist"></span>
### HeaderDetailList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|HeaderKey |String |`Content-Type` |標頭名稱。 |
|HeaderValue |String |`text/plain` |標頭值。標頭值可為常數或下列變數之一：<br><br>對於回應中的標頭，標頭值可為下列變數：<br><br><br>* `${domain}`：用戶端請求中的網域名稱。範例：`example.com`<br><br>* `${uri}`：用戶端請求中不含查詢參數的路徑。若用戶端請求經過重寫，該變數表示重寫後的路徑。範例：`/dir/sample.php`<br><br>* `${args}`：用戶端請求中的查詢參數。若用戶端請求經過重寫，該變數表示重寫後的參數。範例：`color=red&n=10`<br><br>* `${remote_addr}`：發送請求的用戶端 IP 位址。範例：`10.10.10.10`<br><br>* `${server_addr}`：回應用戶端請求的邊緣伺服器 IP 位址。範例：`10.10.10.10`<br><br><br>對於請求中的標頭，標頭值可為下列變數：<br><br><br>* `${upstream_host}`：回源請求中的網域名稱。範例：`example.com`<br><br>* `${upstream_uri}`：回源請求中不含查詢參數的路徑。若請求經過重寫，該變數表示重寫後的路徑。範例：`/dir/sample.php`<br><br>* `${upstream_args}`：回源請求中的查詢參數。如果請求被重寫，此變數表示重寫後的參數。範例：`color=red&n=10`<br><br>* `${remote_addr}`：發送請求的客戶端 IP 位址。範例：`10.10.10.10` |
|HeaderFieldType |整數 |`0` |標頭值的類型：<br><br><br>* `0`：常數<br><br>* `1`：變數 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeHTTPHeaderConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "Phase": 0
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeHTTPHeaderConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "HeaderConfigList": [
            {
                "Vhost": "push.example.com",
                "Domain": "pull.example.com",
                "BlockOriginal": 0,
                "Enable": false,
                "HeaderDetailList": [
                    {
                        "HeaderKey": "Content-Key",
                        "HeaderValue": "text/plain",
                        "HeaderFieldType": 0
                    }
                ]
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
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107290#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|400 |InvalidParam.DomainAndApp |domain 和 app 不可同時存在 |不可同時傳入 Domain 與 App。請修改輸入參數。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.DomainNotExist |未找到網域名稱 |未找到網域名稱（Domain）。請檢查傳入的網域名稱是否與實際使用的網域名稱一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
