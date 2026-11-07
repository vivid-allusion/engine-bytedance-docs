---
title: "CreateDomainV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dj3h3u96xn-zh-TW"
---

調用 `CreateDomainV2` API 以新增一個或多個推流或拉流的網域名稱。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳號每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateDomainV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須同時帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateDomainV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domains |[Domains](https://docs.byteplus.com/en/docs/24/107296#domains) 陣列 |是 |`-` |網域名稱陣列。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">一個網域名稱空間最多可包含 10 個網域名稱。</div><br> |
|Vhost |String |是 |`vhost` |網域名稱空間是相關聯網域的集合，由字母（A\-Z, a\-z）、數字（0\-9）及連字號（\-）組成。您可以自訂新的網域名稱空間，或調用 ListDomainDetail 介面以獲取現有網域所使用的網域名稱空間。 |
|ProjectName |String |否 |`default` |與網域名稱空間關聯的專案。預設為空，表示屬於「default」專案。<br><br>網域名稱空間與專案關聯後，您可以依專案管理資源用量與計費。網域名稱空間建立後，無法變更專案設定。如需管理專案，請前往 BytePlus 控制台的 [Project](https://console.byteplus.com/iam/resourcemanage/project) 頁面。 |


<span id="domains"></span>
### Domains


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainName |String |是 |`push.example.com` |網域名稱由字母（A\-Z, a\-z）、數字（0\-9）及連字號（\-）組成，長度為 1 至 60 個字元。 |
|ChainID |String |否 |`93cb8cf3*******ece5600142` |SSL 憑證鏈 ID。預設為空，表示該網域未綁定 SSL 憑證。您可調用 [ListCertV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcertv2) 介面或前往直播控制台的 [憑證管理](https://console.byteplus.com/live/main/certificate)頁面以獲取待綁定的憑證鏈 ID。 |
|Type |String |是 |`push` |網域名稱類型：<br><br><br>* `push`：推流網域名稱。<br><br>* `pull-flv`：拉流網域名稱。 |
|Region |String |是 |`cn` |加速區域。有效值包括：<br><br><br>* `oversea`：中國大陸以外。<br><br>* `cn`：中國大陸。<br><br>* `global`：全球。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=CreateDomainV2&Version=2023-01-01
{
    "Vhost": "vhost",
    "Domains": [
        {
            "DomainName": "push.example.com",
            "Type": "push",
            "Region": "cn",
            "ChainID": "93cb8cf3*******ece5600142"
        },
        {
            "DomainName": "pull.example.com",
            "Type": "pull-flv",
            "Region": "cn",
            "ChainID": "93c56cf3*******ece522142"
        }
    ],
    "ProjectName": "default"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "CreateDomainV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107296#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定參數是否有非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出值域。 |
|400 |InvalidParameter.Tags.Key |指定的參數 Tags.Key 無效。 |參數 `Tags.Key` 驗證失敗。請檢查參數是否正確。 |
|400 |InvalidParameter.Tags.Value |指定的參數 Tags.Value 無效。 |參數 `Tags.Value` 驗證失敗。請檢查參數是否正確。 |
|400 |InvalidParameter.Tags |指定的參數 Tags 無效。 |參數 `Tags` 驗證失敗。請檢查參數是否正確。 |
|400 |Duplicate.Tags.Key |指定的 tags 物件包含重複的鍵值。 |參數 `Tags.Key` 的值重複。請檢查參數是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數。 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未開通計費狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
