---
title: "CreateTranscodePresetBatch"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023-zh-TW"
---

調用 `CreateTranscodePresetBatch` API 以批量建立 ABR 子流轉碼配置。

<span id="Requirements"></span>
## 需求


* 子流是通過將原始流轉碼為不同解析度和碼率來創建的，此過程會產生轉碼費用。有關價格詳情，請參閱[轉碼](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding)。

* 更新轉碼配置後，將於 3 至 5 分鐘內生效。

* 更新或移除轉碼配置不會影響正在進行的流。您必須停止並重新啟動流以套用變更。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateTranscodePresetBatch&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須傳入[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |字串 |是 |`CreateTranscodePresetBatch` |API 操作名稱。 |
|Version |字串 |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|類型 |字串 |是 |`hls-abr` |選擇批量創建 ABR 配置的協議類型。有效值：<br><br><br>* `hls-abr`：啟用 HLS\-ABR 創建 ABR 配置。<br><br>* `dash-abr`：啟用 DASH\-ABR 創建 ABR 配置。<br><br>* `rtm-abr`：啟用 RTM\-ABR 創建 ABR 配置。<br><br>* `abr`：同時啟用 HLS\-ABR 和 DASH\-ABR 創建 ABR 配置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數可與<code>IsRtmAbr</code>搭配使用，以同時啟用 RTM\-ABR 與其他 ABR 協議類型：</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">將此參數設為<code>hls-abr</code>，並將<code>IsRtmAbr</code>設為<code>true</code>，即可同時啟用 HLS\-ABR 和 RTM\-ABR。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">將此參數設為<code>dash-abr</code>，並將<code>IsRtmAbr</code>設為<code>true</code>，即可同時啟用 DASH\-ABR 和 RTM\-ABR。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">將此參數設為<code>abr</code>，並將<code>IsRtmAbr</code>設為<code>true</code>，即可同時啟用 HLS\-ABR、DASH\-ABR 和 RTM\-ABR。</div><br> |
|CopyParams |布林值 |否 |`true` |將用戶請求的 URL 參數複製到子流請求的 URL。<br><br><br>* `true`：是；<br><br>* `false`：否。 |
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/107361#presetlist) 陣列 |是 |`-` |子流轉碼配置的詳細參數。 |


<span id="presetlist"></span>
### PresetList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |字串 |是 |`push.example.com` |域名空間。你可以呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面，以獲取該域名所屬的域名空間。 |
|App |字串 |是 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。 |
|SuffixName |字串 |是 |`hd` |轉碼流的字尾，支援由大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）及連字號（\-）組成，長度為 1 至 10 個字元。<br><br>轉碼字尾通常用於串流名稱的字尾形式。常見標識包括 `sd`、`hd`、`uhd`。例如，若轉碼配置的標識為 `hd`，則拉流時轉碼後的串流名稱為 `原始流名稱_hd`。 |
|VideoBitrate |整數 |是 |`1000000` |視訊碼率，單位為 bps，取值範圍為 [0,30000000]。 |
|Vcodec |字串 |是 |`h265` |視訊編碼格式：<br><br><br>* `h264`：使用 H.264 編碼格式；<br><br>* `h265`：使用 H.265 編碼格式；<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一串流下的所有 ABR 子流應配置相同的視訊編碼格式。</div><br> |
|AudioBitrate |整數 |否 |`50` |音訊碼率，單位為 kbps。 |
|Acodec |字串 |否 |`acc` |音訊編碼格式。預設格式為 AAC，支援以下 3 種：<br><br><br>* `aac`：使用 AAC 編碼格式；<br><br>* `copy`：不進行轉碼，所有音訊編碼參數均無效；<br><br>* `opus`：採用 Opus 編碼格式。 |
|FPS |整數 |否 |`25` |影片幀率，以 fps（每秒幀數）為單位，範圍為 [0,60]，預設值為 25fps。幀率越高，影片播放越流暢。 |
|GOP |整數 |是 |`2` |IDR 幀之間的最大間隔，以秒為單位，範圍為 [1,30]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一串流下所有 ABR 子串流的 GOP 配置必須一致。</div><br> |
|寬度 |整數 |是 |`1000` |影片寬度，範圍為 [150, 1920]。 |
|高度 |整數 |是 |`500` |影片高度，值的範圍為 [150,1920]。 |
|Roi |布林值 |否 |`true` |是否以低碼率高清模式進行轉碼。<br><br><br>* `true`：低碼率高清模式。<br><br>* `false`：（預設）標準模式。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一串流下所有 ABR 子串流應配置相同的轉碼方式。</div><br> |
|AutoTransResolution |整數 |否 |`1` |是否啟用轉碼不超過來源串流解析度，預設值 `1` 表示啟用。啟用後，若來源串流解析度低於轉碼配置解析度（即來源串流的寬度和高度均低於轉碼配置），則以來源串流影片解析度進行轉碼。<br><br><br>* `0`：停用；<br><br>* `1`：啟用。 |
|AutoTransVb |整數 |否 |`1` |僅在不超過來源串流碼率時啟用轉碼。預設值 `1` 表示此功能已啟用。啟用後，若來源串流碼率低於配置的轉碼碼率，則以來源串流影片碼率進行轉碼。<br><br><br>* `0`：停用；<br><br>* `1`：啟用。 |
|AutoTransVr |整數 |否 |`1` |啟用轉碼幀率不超過來源串流幀率，預設值為 `1` 表示啟用。啟用後，若來源串流幀率低於轉碼配置幀率，則依來源串流影片幀率進行轉碼。<br><br><br>* `0`：停用；<br><br>* `1`：啟用。 |
|TranscodeStruct |[TranscodeStruct](https://docs.byteplus.com/en/docs/24/107361#transcodestruct) 物件 |否 |`-` |轉碼資訊。 |


<span id="transcodestruct"></span>
### TranscodeStruct


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|類型 |字串 |否 |`Pull` |轉碼任務於以下情況啟動：<br><br><br>* `Push`：直播串流啟動時。<br><br>* `Pull`：（預設）請求轉碼串流時。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一串流下所有 ABR 子串流的類型應配置一致。</div><br> |
|IsRtmAbr |布林值 |否 |`false` |創建 ABR 配置時是否啟用 RTM\-ABR。預設值：`false`。有效值：<br><br><br>* `true`：啟用 RTM\-ABR。<br><br>* `false`：不啟用 RTM\-ABR。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=CreateTranscodePresetBatch&Version=2023-01-01
{
    "Type": "hls-abr",
    "CopyParams": true,
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SuffixName": "hd",
            "VideoBitrate": 1000000,
            "Vcodec": "h265",
            "FPS": 25,
            "GOP": 2,
            "Width": 1000,
            "Height": 500,
            "AudioBitrate": 50,
            "Acodec": "acc",
            "AutoTransResolution": 1,
            "AutoTransVb": 1,
            "AutoTransVr": 1,
            "Roi": true,
            "TranscodeStruct": {
                "Type": "Pull"
            },
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SuffixName": "ld",
            "VideoBitrate": 500000,
            "Vcodec": "h265",
            "FPS": 25,
            "GOP": 2,
            "Width": 1000,
            "Height": 500,
            "AudioBitrate": 50,
            "Acodec": "acc",
            "AutoTransResolution": 1,
            "AutoTransVb": 1,
            "AutoTransVr": 1,
            "Roi": true,
            "TranscodeStruct": {
                "Type": "Pull"
            }
        }
    ]
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateTranscodePresetBatch",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與當前操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107361#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證未通過。請檢查資料型別是否正確。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出範圍。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下沒有所需的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 沒有權限存取相應資源，請檢查請求參數。 |請求被拒絕，因為當前帳戶下沒有所需的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 的計費狀態不可用，請啟用服務或充值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置和憑證）。建議重試。若仍返回錯誤碼，請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與服務或帳單相關的內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯繫客服](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
