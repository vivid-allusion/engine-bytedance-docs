---
title: "GeneratePlayURL"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023-zh-TW"
---

呼叫 `GeneratePlayURL` API，以產生指定串流的拉流地址。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 25 次查詢。

* 先決條件：

   * 要產生轉碼串流的拉流地址，必須先完成對應 [transcoding configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding) 的 `AppName` 設定。

   * 要產生 ABR 拉流地址，必須先完成對應 [ABR configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) 的 `AppName` 設定，並選擇相應的協議類型。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=GeneratePlayURL&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`GeneratePlayURL` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流用的網域名稱。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱。 |
|App |String |是 |`live` |推流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 30 字元。 |
|Stream |String |是 |`test` |拉流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 到 100 字元。 |
|Type |String |否 |`fcdn` |CDN 類型。有效值：<br><br><br>* `fcdn`：（預設）BytePlus MediaLive CDN。<br><br>* `3rd`：第三方 CDN。若使用 [relay](https://docs.byteplus.com/byteplus-media-live/docs/relay) 功能並需取得第三方拉流地址，請將 `Type` 設為 `3rd`。 |
|Suffix |String |否 |`5` |轉碼串流的後綴，預設為空。若設定不為空，則為產生轉碼串流的拉流地址。可呼叫 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) 查詢現有轉碼模板及其對應後綴。 |
|ValidDuration |Integer |否 |`5` |地址自產生時起，依 `ValidDuration` 設定的時長過期。單位：秒。有效範圍：\> 0。預設值：604800（七天）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">M3U8 拉流地址過期後，拉流將立即停止。其他類型地址過期時，已進行中的拉流不受影響。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時設定 <code>ValidDuration</code> 與 <code>ExpiredTime</code>，僅 <code>ExpiredTime</code> 的設定生效。</div><br> |
|ExpiredTime |String |否 |`2022-08-19T16:07:25+08:00` |地址的過期時間（RFC 3339 格式的本地時間，精確到秒），單位為秒。預設過期時間為地址產生後七天。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">M3U8 拉流地址過期後，拉流將立即停止。對於其他類型的地址，即使地址過期，持續的拉流操作也不會受到影響。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同時設置<code>ValidDuration</code>和<code>ExpiredTime</code>，僅<code>ExpiredTime</code>的設置會生效。</div><br> |
|StreamType |String |是 |`source` |生成的地址類型，具體值如下：<br><br><br>* `source`：生成源流地址。<br><br>* `transcode`：生成轉碼流地址。<br><br>* `abr`：生成 ABR 地址。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料類型** |**範例值** |**描述** |
|---|---|---|---|
|URLList |[URLList](https://docs.byteplus.com/en/docs/24/107309#urllist) 陣列 |`-` |拉流地址列表。 |
|AuthType |String |`TypeB` |用於生成拉流地址的 URL 驗證類型。若值為空，表示目前網域未配置 URL 驗證。<br><br><br>* `TypeA`：A 類型。<br><br>* `TypeB`：B 類型。<br><br>* `TypeC`：C 類型。<br><br>* `TypeCustom`：自定義類型。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">關於 A、B、C 類型的詳細資訊，請參閱<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>。</div><br> |


<span id="urllist"></span>
### URLList


|**參數** |**資料類型** |**範例值** |**描述** |
|---|---|---|---|
|URL |String |`https://pull.example.com/live/test.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70` |拉流地址。 |
|Type |String |`pull` |地址類型。<br><br><br>* `pull`：拉流地址<br><br>* `3rd_play(replay_source)`：第三方拉流地址（原始拉流）<br><br>* `3rd_play(relay_sink)`：第三方拉流地址（中繼拉流） |
|CDN |String |`fcdn` |CDN 類型。<br><br><br>* `fcdn`：（預設）BytePlus Video Cloud CDN；<br><br>* `3rd`：第三方 CDN。 |
|Protocol |String |`udp` |串流協議。有效值：<br><br><br>* `hls`：HLS 拉流地址。<br><br>* `flv`：FLV 拉流地址。<br><br>* `rtmp`：RTMP 拉流地址。<br><br>* `udp`：RTM 拉流地址，適用於客戶端 SDK（BytePlus MediaLive Player SDKs for iOS、Android、React Native 和 Flutter）及其他播放器。<br><br>* `udp_websdk`：RTM 拉流地址，適用於 BytePlus MediaLive Player SDK for Web。<br><br>* `cmaf`：CMAF 拉流地址。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">若無法取得 BytePlus MediaLive Player SDK for Web 的 RTM 拉流地址，請聯繫<a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a>。</div><br><br><br>* <div data-tips="true" data-tips-type="warning">BytePlus MediaLive Player SDK for Web 的 RTM 拉流地址支援自動轉碼，包括 B\-frame 移除及 AAC 轉 Opus 音訊轉換。更多資訊請參閱<a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses">Generating live\-stream addresses</a>。</div><br><br><br>* <div data-tips="true" data-tips-type="warning">當<code>StreamType</code>值為<code>abr</code>時，<code>Protocol</code>值為<code>udp</code>的 RTM\-ABR 拉流地址目前支援 BytePlus MediaLive Player SDKs for iOS 和 Android，以及其他播放器。</div><br> |
|SubStreamURL |[SubStreamURL](https://docs.byteplus.com/en/docs/24/107309#substreamurl) 陣列 |`-` |子流地址。僅當`StreamType`為`abr`時返回。 |


<span id="substreamurl"></span>
### SubStreamURL


|**參數** |**資料類型** |**範例值** |**描述** |
|---|---|---|---|
|Suffix |String |`_ld` |子流轉碼後綴。 |
|Tag |String |`LL-HLS` |地址標籤，例如`drm`、`hls encryption`。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=GeneratePlayURL&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "test",
    "StreamType": "source",
    "ExpiredTime": "2022-08-19T16:07:25Z"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GeneratePlayURL",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "URLList": [
            {
                "URL": "https://pull.example.com/live/test.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70",
                "CDN": "fcdn",
                "Protocol": "udp",
                "Type": "pull"
            }
        ],
        "AuthType": "TypeB"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[contact support](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107309#request-parameters)描述進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料類型是否正確。 |
|400 |InvalidParam.Format |%s 格式錯誤 |參數格式不正確。請檢查錯誤訊息中指定參數是否包含非法字元或 URL 格式錯誤。 |
|400 |InvalidParam.OutOfRange |%s 應為 {[%s]} 之一%s 應介於 %d 與 %d 之間 |參數超出允許範圍。請檢查錯誤訊息中指定參數的值是否超出取值範圍。 |
|400 |InvalidParam.TimeLogic |startTime 晚於 endTime，等等。 |傳入的時間參數不符合時間邏輯。請檢查是否存在以下問題：開始時間晚於結束時間。過期時間早於當前時間。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下不存在所請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |請求被拒絕，因為當前帳戶下不存在所請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或儲值。 |尚未啟用視訊直播服務或帳戶已欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |發生與 vhost 或網域名稱相關的內部錯誤，請聯絡管理員。 |發生與網域名稱空間（Vhost）或網域名稱（Domain）相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
