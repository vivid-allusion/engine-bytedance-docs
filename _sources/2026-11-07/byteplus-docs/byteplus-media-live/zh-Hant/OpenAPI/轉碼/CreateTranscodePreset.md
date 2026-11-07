---
title: "CreateTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023-zh-TW"
---

呼叫 `CreateTranscodePreset` API 以建立轉碼配置，系統將根據您的轉碼配置，對符合條件的直播流進行即時轉碼。

<span id="Usage scenario"></span>
## 使用場景

`CreateTranscodePreset` API 支援建立多個 `Vhost + App` 層級的轉碼配置，且不同的轉碼配置需透過轉碼後綴（SuffixName）來區分。建立轉碼配置後，您可以在拉流地址的串流名稱中加入轉碼後綴來使用該轉碼配置。

<span id="Requirements"></span>
## 需求


* 計費：有關轉碼價格，請參閱 [Transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* 頻率限制：每個帳戶每秒最多 10 次查詢。

* 生效說明：新增、更新及刪除轉碼配置後，需重新推流及拉流（3\-5 分鐘）才能使用變更後的配置。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateTranscodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateTranscodePreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |名稱空間。您可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢該網域所屬的名稱空間。 |
|App |String |是 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。 |
|SuffixName |String |是 |`hd` |轉碼流的後綴。可包含大寫及小寫字母（A\-Z、a\-z）、底線（_）及連字號（\-）。最大長度：10 字元。常見後綴包含 `_sd`、`_hd` 及 `_uhd`。例如，若您設定 `_hd` 為後綴，則轉碼流名稱為 `streamName_hd`。 |
|VideoBitrate |Integer |否 |`1000000` |視訊位元率（bps）。預設值為 1,000,000。0 表示保留原始視訊位元率。<br><br>視訊位元率範圍依視訊編碼格式（`Vcodec`）而異。<br><br>不同 Vcodec 值的有效範圍如下：<br><br><br>* h264 與 h265 為 0–30,000,000 |
|Vcodec |String |是 |`h265` |視訊編碼器。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `copy`：不轉碼視訊流。且所有視訊配置皆無法套用，包括視訊幀率（`FPS`）、視訊位元率（`VideoBitrate`）、解析度設定（`As`、`Width`、`Height`、`ShortSide`、`LongSide`）、`GOP` 及 `BFrames` 等。 |
|AudioBitrate |Integer |否 |`50` |音訊位元率（Kbps）。有效範圍：0\-1000。預設值為 128。0 表示保留原始位元率。 |
|Acodec |String |否 |`aac` |音訊編碼器。預設值為 `aac`。可設定以下值：<br><br><br>* `aac`：AAC。<br><br>* `opus`：OPUS。<br><br>* `copy`：不會轉碼音訊流。且所有音訊設定皆無法套用。音訊編解碼器參數包含音訊位元率（`AudioBitrate`）等。 |
|FPS |整數 |否 |`25` |影片幀率（fps）。預設值為 25。0 表示保持原始幀率。<br><br>有效範圍依 Vcodec 值而異：<br><br><br>* h264 與 h265 為 0–60 |
|GOP |整數 |否 |`2` |IDR 幀之間的最大間隔。單位：秒。有效範圍：1–30。 |
|Width |整數 |否 |`400` |影片的寬度（像素 px）。當 `Vcodec` 設為 h264 或 h265 且 `As` 設為 `0` 時有效。<br><br>影片寬度範圍依 Vcodec 值而異：<br><br><br>* h264 與 h265 為 150\-1920。<br><br>* h266 不支援設定 Width 與 Height。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整關閉（<code>As</code> 值為 0）時，影片會依 Width 與 Height 的值拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整關閉（<code>As</code> 值為 0）時，若 Width 或 Height 任一設為 0，則保留原始影片尺寸。</div><br> |
|Height |整數 |否 |`200` |影片的高度（像素 px）。當 Vcodec 設為 h264 或 h265 且 `As` 設為 0 時有效。<br><br>影片寬度範圍依 Vcodec 值而異：<br><br><br>* h264 與 h265 為 150–1920<br><br>* h266 不支援設定 Width 與 Height。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整關閉（<code>As</code> 值為 0）時，影片會依 Width 與 Height 的值拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整關閉（<code>As</code> 值為 0）時，若 Width 或 Height 任一設為 0，則保留原始影片尺寸。</div><br> |
|As |字串 |否 |`1` |是否自動調整影片尺寸。預設值為 0，可設定以下值：<br><br><br>* `0`：關閉自動調整；<br><br>* `1`：開啟自動調整。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整關閉（<code>As</code> 值為 <code>0</code>）時，影片會依 Width 與 Height 的值拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整開啟（<code>As</code> 值為 <code>1</code>）時，轉碼後的影片解析度會依短邊長度（<code>ShortSide</code>）、長邊長度（<code>LongSide</code>）、影片寬度（<code>Width</code>）、影片高度（<code>Height</code>）的優先順序決定，另一邊按比例縮放。</div><br> |
|ShortSide |整數 |否 |`768` |影片短邊長度。配置不同轉碼類型（`Roi`）與影片編解碼器（`Vcodec`）時，短邊長度的值範圍如下。<br><br><br>* 當轉碼類型為標準模式（`Roi` 值為 `false`）時，有效範圍依 `Roi` 與 `Vcodec` 值而異：<br><br>   * h264 為 150\-2160<br><br>   * h265 為 150\-4096<br><br>* 當轉碼類型為低碼率高清模式（`Roi` 為 `true`）<br><br>   * h264 或 h265 為 0 或 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當影片解析度自動調整開啟（<code>As</code> 值為 <code>1</code>）時，此參數有效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時將 <code>LongSide</code> 與 <code>ShortSide</code> 設為 0，則保留原始影片尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時將 LongSide 與 <code>ShortSide</code> 設為非 0 的值，影片會依據 <code>ShortSide</code> 的值進行拉伸。</div><br> |
|LongSide |整數 |否 |`500` |影片的長邊長度。配置不同的轉碼類型（Roi）及影片編碼（Vcodec）時，長邊長度的取值範圍如下。<br><br><br>* 當轉碼類型為標準模式（Roi 值為 false）時，合法範圍依 Roi 與 Vcodec 值而異：<br><br>   * h264：150\-4096<br><br>   * h265：150\-7680<br><br>* 當轉碼類型為低碼率高清模式（`Roi` 為 `true`）<br><br>   * h264 與 h265：0 與 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當啟用影片解析度自動調整（<code>As</code> 值為 <code>1</code>）時，此參數有效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時將 <code>LongSide</code> 與 <code>ShortSide</code> 設為 0，則保留原始影片尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時將 <code>LongSide</code> 與 <code>ShortSide</code> 設為非 0 的值，影片會依據 <code>ShortSide</code> 的值進行拉伸。</div><br> |
|BFrames |整數 |否 |`3` |兩個參考幀之間的最大 B 幀數。預設值為 3。0 表示移除 B 幀。<br><br>合法值依 Vcodec 值而異：<br><br><br>* h264：[0–7]<br><br>* h265： |
|Roi |布林值 |否 |`true` |是否使用低碼率高清模式進行轉碼。<br><br><br>* `true`：低碼率高清模式。<br><br>* `false`：（預設）標準模式。 |
|AbrMode |整數 |否 |`1` |當 IsHlsAbr 設為 true 時，是否對每個轉碼流的 I 幀進行對齊：<br><br><br>* `1`：是<br><br>* `0`：（預設）否 |
|AutoTransResolution |整數 |否 |`1` |是否啟用轉碼解析度不超過來源流解析度。啟用後，若原始流解析度低於轉碼解析度，則依來源流解析度進行轉碼。<br><br><br>* `0`：停用<br><br>* `1`：（預設）啟用 |
|AutoTransVb |整數 |否 |`1` |是否啟用限制轉碼碼率不超過來源流碼率。啟用後，若來源流碼率低於轉碼碼率，則依來源流碼率進行轉碼。<br><br><br>* `0`：停用<br><br>* `1`：（預設）啟用 |
|AutoTransVr |整數 |否 |`1` |是否限制轉碼幀率不超過來源幀率。啟用後，若來源幀率低於轉碼幀率，則依來源幀率進行轉碼。<br><br><br>* `0`：停用<br><br>* `1`：（預設）啟用 |
|StopInterval |整數 |否 |`60` |轉碼任務的暫停時長（秒）。<br><br>當 TransType 設為 Pull 時有效。合法值範圍為 \-1 或 0 到 300 之間的整數。\-1 表示拉流停止時任務不暫停。預設值為 60。 |
|TransType |字串 |否 |`Pull` |轉碼任務啟動時機：<br><br><br>* `Push`：直播流啟動時。<br><br>* `Pull`：（預設）請求轉碼流時。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參閱 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|PresetName |字串 |`preset` |轉碼模板名稱。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=CreateTranscodePreset&Version=2023-01-01
{
    "Vhost":"push.example.com",
    "App":"live",
    "SuffixName":"hd",
    "Vcodec"："h264"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "Action": "CreateTranscodePreset",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "PresetName": "preset"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107386#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證未通過。請檢查資料型別是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 和 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因目前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 未啟用計費狀態，請開通服務或充值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
