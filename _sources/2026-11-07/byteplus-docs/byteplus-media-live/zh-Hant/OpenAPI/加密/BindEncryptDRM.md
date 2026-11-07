---
title: "BindEncryptDRM"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecertdrm_1-zh-TW"
---

調用 `BindEncryptDRM` API 以新增或更新直播流的 DRM 加密配置。

<span id="Requirements"></span>
## 需求


* 計費：對轉碼流進行加密將產生轉碼費用。有關詳細費用資訊，請參閱 [轉碼計費](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* 頻率限制：每個帳號每秒 1 次查詢。

* 生效時間：配置新增或更新後約 3 至 5 分鐘生效。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=BindEncryptDRM&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須傳入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`BindEncryptDRM` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |該網域所屬的網域命名空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取網域命名空間。 |
|App |String |是 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。 |
|DRMSystems |Array of String |是 |`["FairPlay","Widevine"]` |加密類型。支援的值如下。<br><br><br>* `FairPlay`：使用 FairPlay 技術的商業 DRM 加密；<br><br>* `Widevine`：使用 Widevine 技術的商業 DRM 加密；<br><br>* `PlayReady`：使用 PlayReady 技術的商業 DRM 加密；<br><br>* `ClearKey`：HLS 標準加密。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">DRM 加密與 HLS 標準加密不可同時配置。</div><br> |
|EncryptOriginStream |Boolean |是 |`true` |是否啟用源流加密，值及其含義如下。<br><br><br>* `true`：啟用；<br><br>* `false`：未啟用。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">源流與轉碼流至少需有一項啟用錄製。</div><br> |
|EncryptTranscodeStream |Boolean |是 |`true` |是否啟用轉碼流加密，值及其含義如下。<br><br><br>* `true`：啟用；<br><br>* `false`：未啟用。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">源流與轉碼流至少需有一項啟用錄製。</div><br> |
|EncryptTranscodeSuffix |Array of String |否 |`["_uhd","hd"]` |啟用轉碼流加密時，配置需加密的轉碼流後綴。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=BindEncryptDRM&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Enable": true,
    "EncryptTranscodeSuffix": [
        "_uhd",
        "hd"
    ],
    "EncryptTranscodeStream": true,
    "EncryptOriginStream": true,
    "DRMSystems": [
        "FairPlay",
        "Widevine"
    ]
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "BindEncryptDRM",
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
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107328#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳號下無請求資源（資源包括網域命名空間、網域、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 沒有權限存取對應資源，請檢查請求參數 |請求被拒絕，因為目前帳戶下沒有所需資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |AccountID 無法取得帳單狀態，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單無法取得。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
