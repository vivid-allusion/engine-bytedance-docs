---
title: "ListTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023-zh-TW"
---

調用 `ListTimeShiftPresetV2` API 查詢指定網域名稱空間下所有 appName 的時移配置。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒 1 次查詢。

* 生效說明：新增、更新及刪除時移配置後，需在操作（3\-5 分鐘）後重新推流及拉流，方可使用變更後的配置。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListTimeShiftPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListTimeShiftPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |網域名稱空間。若未指定，則查詢所有網域名稱空間下的所有配置。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或於 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取網域所屬的網域名稱空間。 |
|Type |String |是 |`tos` |儲存類型。請始終設為 `tos`。 |


<span id="Response parameters"></span>
## 回應參數

API 專屬的唯一回應參數請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|列表 |[List](https://docs.byteplus.com/en/docs/24/107456#list) 陣列 |`-` |時移模板列表。 |


<span id="list"></span>
### 列表


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`live` |AppName 欄位。 |
|MaxShiftTime |Integer |`25920` |時移時長，將直播流的可用時間往後移動指定秒數。單位：秒。 |
|Domain |String |`pull.example.com` |拉流網域名稱。 |
|Name |String |`livedemo` |時移配置名稱。 |
|Bucket |String |`5cd18a3563**********cbe0aaf694` |BytePlus TOS 的 bucket。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=ListTimeShiftPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Type": "tos"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
  "ResponseMetadata": {
    "RequestId": "201806041104200100100232280022D30",
    "Action": "ListTimeShiftPresetV2",
    "Version": "2023-01-01",
    "Service": "live",
    "Region": "ap-singapore-1",
  }
  "Result": {
      "List": [
        {
          "Vhost": "push.example.com",
          "App": "live",
          "Bucket": "5cd18********f694",
          "Domain": "pull.example.com",
          "MaxShiftTime": 259200,
          "Name": "livedemo",
          "Type": "tos"

        }
      ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107456#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證未通過。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳戶下無所需資源（資源包括網域名稱空間、網域名稱、app 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因當前帳戶下無所需資源（資源包括網域名稱空間、網域名稱、app 名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致無法出帳。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重新嘗試。若仍然返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
