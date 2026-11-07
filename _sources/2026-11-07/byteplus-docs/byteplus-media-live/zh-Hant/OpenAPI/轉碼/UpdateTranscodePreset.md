---
title: "UpdateTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1-zh-TW"
---

呼叫 `UpdateTranscodePreset` API 以更新已新增的轉碼配置。若未填寫非必填參數，對應的參數配置將不會變更。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次查詢。

* 生效說明：新增、更新及刪除轉碼配置後，需在操作完成（3\-5 分鐘）後重新推流及拉流，才能使用已變更的配置。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateTranscodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateTranscodePreset` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Preset |String |是 |`PresetName` |配置名稱。可呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API 取得欲更新的配置名稱。 |
|Vhost |String |是 |`push.example.com` |網域名稱空間。可呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API 取得欲更新配置的網域名稱空間。 |
|App |String |否 |`live` |AppName 欄位。可呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API 取得欲更新配置的 AppName 欄位。 |
|SuffixName |String |否 |`hd` |轉碼串流的後綴。可包含大小寫字母、底線（_）及連字號（\-）。最大長度：10 字元。常見後綴包括 _sd、_hd 及 _uhd。例如，若設定 _hd 為後綴，則轉碼串流名稱為 streamName_hd。 |
|VideoBitrate |Integer |否 |`0` |影片位元率（bps）。預設值為 1,000,000。0 表示保持原始影片位元率。<br><br>有效範圍依 Vcodec 值而異：<br><br><br>* h264 與 h265 為 0–30,000,000<br><br>* h266 為 0–60,000,000 |
|Vcodec |String |否 |`h265` |影片編碼格式。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `h266`：H.266。<br><br>* `copy`：不轉碼影片串流。且所有影片配置皆無法套用。 |
|AudioBitrate |Integer |否 |`30` |音訊位元率（Kbps）。有效範圍：0\-1000。預設值為 128。0 表示保持原始位元率。 |
|Acodec |String |否 |`aac` |音訊編碼格式。<br><br><br>* `aac`：AAC。<br><br>* `copy`：不轉碼音訊串流。且所有音訊配置皆無法套用。<br><br>* `opus`：OPUS。 |
|FPS |Integer |否 |`60` |影片幀率（fps）。預設值為 25。0 表示保持原始幀率。<br><br>有效範圍依 Vcodec 值而異：<br><br><br>* h264 與 h265 為 0–60<br><br>* h266 為 0–35 |
|GOP |Integer |否 |`2` |IDR 幀之間的最大間隔。單位：秒。有效範圍：1–30。 |
|Width |Integer |否 |`1366` |影片寬度（像素 px）。當 Vcodec 設為 h264 或 h265 且 As 設為 0 時有效。<br><br>有效範圍為 {0,[150–1920]}。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">影片將依據 Width 與 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 Width 或 Height 任一設為 0 時，將保留原始影片尺寸。</div><br> |
|Height |整數 |否 |`768` |影片高度，以像素（px）為單位。當 Vcodec 設為 h264 或 h265 且 As 設為 0 時有效。<br><br>有效範圍為 {0,[150–1920]}。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">影片將依 Width 與 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 Width 或 Height 任一設為 0 時，將保留原始影片尺寸。</div><br> |
|As |字串 |否 |`1` |是否自動調整影片尺寸。<br><br><br>* `0`: 關閉自動調整，影片將依 Width 與 Height 拉伸。請確保 Width 與 Height 在有效範圍內。<br><br>* `1`: 開啟自動調整，影片將依 ShortSide 或 LongSide 等比例縮放。請確保 ShortSide 與 LongSide 在有效範圍內。 |
|ShortSide |整數 |否 |`500` |影片的短邊。當 As 設為 1 時有效。<br><br>有效範圍依 Roi 與 Vcodec 值而異：<br><br><br>* 當 Roi 為 false 時。<br><br>   * h264 為 150\-2160<br><br>   * h265 為 150\-4096<br><br>   * h266 為 150\-720<br><br>* 當 Roi 為 true 時，範圍為 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為 0，將保留原始影片尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為非 0 值，影片將依 ShortSide 的值拉伸。</div><br> |
|LongSide |整數 |否 |`600` |影片的長邊。當 As 設為 1 時有效。<br><br>有效範圍依 Roi 與 Vcodec 值而異：<br><br><br>* 當 Roi 為 false 時。<br><br>   * h264 為 150\-4096<br><br>   * h265 為 150\-7680<br><br>   * h266 為 150\-1280<br><br>* 當 Roi 為 true 時，範圍為 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為 0，將保留原始影片尺寸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 與 ShortSide 均設為非 0 值，影片將依 ShortSide 的值拉伸。</div><br> |
|BFrames |整數 |否 |`3` |兩個參考幀之間最多可有的 B 幀數。預設值為 3。0 表示移除 B 幀。<br><br>有效值依 Vcodec 值而異：<br><br><br>* h264 為 [0–7]。<br><br>* h265 與 h266 為 {0, 1, 2, 3, 7, 15}。 |
|Roi |布林值 |否 |`true` |是否以低碼率高清模式轉碼。<br><br><br>* `true`: 低碼率高清模式。<br><br>* `false`:（預設）標準模式。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">當 Vcodec 為 H.266 時，轉碼不支援低碼率高清模式。</div><br> |
|AbrMode |整數 |否 | |當 IsHlsAbr 設為 true 時，是否對每個轉碼串流對齊 I 幀：<br><br><br>* `1`: 是<br><br>* `0`:（預設）否 |
|AutoTransResolution |整數 |否 |`1` |是否限制轉碼解析度不得超過原始串流解析度。<br><br><br>* `0`: 允許<br><br>* `1`:（預設）限制 |
|AutoTransVb |整數 |否 |`1` |是否限制轉碼碼率不得超過原始串流碼率。<br><br><br>* `0`: 允許<br><br>* `1`:（預設）限制 |
|AutoTransVr |整數 |否 |`1` |是否限制轉碼幀率不得超過原始幀率。<br><br><br>* `0`: 允許<br><br>* `1`:（預設）限制 |
|StopInterval |整數 |否 |`60` |轉碼任務的暫停時長，單位為秒。<br><br>當 TransType 設為 Pull 時有效。有效值範圍為 \-1 或 0 到 300 之間的整數。\-1 表示當拉流停止時，任務不會暫停。預設值為 60。 |
|TransType |String |否 |`Pull` |當以下情況發生時，轉碼任務啟動：<br><br><br>* `Push`：直播流啟動時。<br><br>* `Pull`：（預設）請求轉碼後的流時。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateTranscodePreset&Version=2023-01-01
{
    "Preset": "PresetName",
    "Vhost": "push.example.com",
    "App": "live",
    "SuffixName": "hd"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateTranscodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107301#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳號下無請求的資源（資源包括網域命名空間、網域名稱、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為當前帳號下無請求的資源（資源包括網域命名空間、網域名稱、App 名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 的計費狀態不可用，請開通服務或充值。 |尚未啟用視訊直播服務或帳號欠費，導致帳單不可用。請檢查服務開通狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域名稱、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
