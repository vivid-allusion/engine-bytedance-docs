---
title: "DeleteTranscodePresetBatch"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023-zh-TW"
---

調用 `DeleteTranscodePresetBatch` API，以批次刪除 ABR 子流的轉碼配置。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteTranscodePresetBatch&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteTranscodePresetBatch` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Type |String |是 |`hls-abr` |請選擇要刪除的 ABR 配置的協議類型。有效值：<br><br><br>* `hls-abr`：HLS\-ABR<br><br>* `dash-abr`：DASH\-ABR<br><br>* `rtm-abr`：RTM\-ABR<br><br>* `abr`：HLS\-ABR 和 DASH\-ABR<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">刪除啟用多種協議類型的 ABR 配置時，請使用以下<code>Type</code>值：</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">對於啟用 HLS\-ABR 和 RTM\-ABR 的配置，請使用<code>hls-abr</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">對於啟用 DASH\-ABR 和 RTM\-ABR 的配置，請使用<code>dash-abr</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">對於啟用 HLS\-ABR、DASH\-ABR 和 RTM\-ABR 的配置，請使用<code>abr</code>。</div><br> |
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/107330#presetlist) 陣列 |是 |`-` |要刪除 ABR 子流轉碼配置資訊，可呼叫[ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)，查看需要刪除的 ABR 類型轉碼配置。 |


<span id="presetlist"></span>
### PresetList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Preset |String |是 |`asdq12ed` |刪除配置中的 Preset 值。 |
|Vhost |String |是 |`push.example.com` |要刪除配置中的 Vhost 值。 |
|App |String |是 |`live` |刪除配置中的 App 值。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteTranscodePresetBatch&Version=2023-01-01
{
    "Type": "hls-abr",
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "Preset": "asdq12ed"
        },
        {
            "Vhost": "push.example.com",
            "App": "live",
            "Preset": "d2asda2e"
        }
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteTranscodePresetBatch",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下是與目前操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107330#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，無法刪除 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權訪問對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |尚未開通視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、應用名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |內部錯誤 |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
