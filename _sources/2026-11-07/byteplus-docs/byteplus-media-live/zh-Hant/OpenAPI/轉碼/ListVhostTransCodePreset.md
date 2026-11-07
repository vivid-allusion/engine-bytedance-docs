---
title: "ListVhostTransCodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1-zh-TW"
---

調用 `ListVhostTransCodePreset` API 以查詢轉碼配置列表。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListVhostTransCodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostTransCodePreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空間。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢該域名所屬的域名空間。 |
|IsHlsAbr |Boolean |否 |`true` |是否查詢 DASH 協議 ABR 子流的轉碼配置，預設為空。<br><br><br>* `true`：是<br><br>* `false`：否<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>IsHlsAbr</code> 與 <code>IsDashAbr</code> 均為 <code>true</code> 時，表示查詢基於 HLS 協議與 DASH 協議的 ABR 子流轉碼配置。</div><br> |
|IsDashAbr |Boolean |否 | |是否查詢 DASH 協議 ABR 子流的轉碼配置，預設為空。<br><br><br>* `true`：是<br><br>* `false`：否<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 <code>IsHlsAbr</code> 與 <code>IsDashAbr</code> 均為 <code>true</code> 時，表示查詢基於 HLS 協議與 DASH 協議的 ABR 子流轉碼配置。</div><br> |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 專屬回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CommonPresetList |[TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/107411#transcodepresetvhostapp) 陣列 |`-` |預設轉碼配置列表。 |
|CustomizePresetList |[TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/107411#transcodepresetvhostapp) 陣列 |`-` |自定義轉碼配置列表。 |
|AllPresetList |[TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/107411#transcodepresetvhostapp) 陣列 |`-` |全部轉碼配置列表。 |


<span id="transcodepresetvhostapp"></span>
### TranscodePresetVhostAPP


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空間。 |
|App |String |`live` |AppName 欄位。 |
|TranscodePreset |[TranscodePreset](https://docs.byteplus.com/en/docs/24/107411#transcodepreset) 物件 |`-` |模板詳細資訊。 |


<span id="transcodepreset"></span>
### TranscodePreset


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|AbrMode |Integer |`1` |當 `IsHlsAbr` 設為 `true` 時，是否對每個轉碼流的 I 幀進行對齊：<br><br><br>* `1`：是<br><br>* `0`：否 |
|Acodec |String |`aac` |音訊編碼器。<br><br><br>* `aac`：AAC。<br><br>* `copy`：不轉碼音訊流。<br><br>* `opus`：OPUS。 |
|As |String |`0` |是否自動調整視訊尺寸。<br><br><br>* `0`：禁用自動調整，並根據 `Width` 和 `Height` 拉伸視訊。<br><br>* `1`：啟用自動調整，並根據 `ShortSide` 或 `LongSide`縮放視訊。 |
|AudioBitrate |Integer |`30` |音訊碼率。單位：Kbps。 |
|AutoTransResolution |Integer |`1` |是否限制轉碼解析度不得超過原始流解析度。<br><br><br>* `0`：允許<br><br>* `1`：限制 |
|AutoTransVb |Integer |`1` |是否限制轉碼碼率不得超過原始流碼率。<br><br><br>* `0`：允許<br><br>* `1`：限制 |
|AutoTransVr |Integer |`1` |是否限制轉碼幀率不得超過原始幀率。<br><br><br>* `0`：允許<br><br>* `1`：限制 |
|BFrames |Integer |`3` |兩個參考幀之間最多的 B 幀數。0 表示移除 B 幀。 |
|FPS |Integer |`60` |視訊幀率。單位：fps。 |
|GOP |整數 |`2` |IDR 幀之間的最大間隔。單位：秒。 |
|Height |整數 |`100` |影片高度（像素 px）。當 Vcodec 設為 h264 或 h265 且 As 設為 0 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">影片會根據 Width 和 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 Width 或 Height 任一設為 0 時，會保留原始影片尺寸。</div><br> |
|LongSide |整數 |`200` |影片的長邊。當 As 設為 1 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均設為 0，則保留原始影片尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均設為非 0 值，影片會根據 ShortSide 的值拉伸。</div><br> |
|Preset |字串 |`preset1` |轉碼配置的名稱。 |
|Roi |布林值 |`true` |是否以低碼率高清模式進行轉碼。<br><br><br>* `true`：低碼率高清模式。<br><br>* `false`：（預設）標準模式。 |
|ShortSide |整數 |`100` |影片的短邊。當 As 設為 1 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均設為 0，則保留原始影片尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均設為非 0 值，影片會根據 ShortSide 的值拉伸。</div><br> |
|StopInterval |整數 |`60` |轉碼任務的暫停時長，單位為秒。<br><br>當 TransType 設為 Pull 時有效。有效值範圍為 \-1 或 0 到 300 之間的整數。\-1 表示拉流停止時任務不會暫停。預設值為 60。 |
|SuffixName |字串 |`hd` |轉碼流的後綴。 |
|Vcodec |字串 |`h265` |影片編碼格式。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `copy`：不轉碼影片流。 |
|VideoBitrate |整數 |`30` |影片碼率。單位：Kbps。 |
|Width |整數 |`200` |影片寬度（像素 px）。當 Vcodec 設為 h264 或 h265 且 As 設為 0 時有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">影片會根據 Width 和 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 Width 或 Height 任一設為 0 時，會保留原始影片尺寸。</div><br> |
|TransType |字串 |`Pull` |轉碼任務啟動時機：<br><br><br>* `Push`：直播流啟動時。<br><br>* `Pull`：請求轉碼流時。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestID": "2021072818053901022706413520787",
        "Action": "ListVhostTransCodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "CommonPresetList": [],
        "CustomizePresetList": []
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107411#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.Empty |%s 為必填項 |缺少參數。請檢查錯誤訊息中指定的參數是否已傳入。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置和憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權訪問對應資源，請檢查請求參數 |請求被拒絕，因為當前帳戶下沒有所需的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 無法取得帳單狀態，請啟用服務或充值。 |尚未啟用視頻直播服務或帳戶欠費，導致帳單無法取得。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
