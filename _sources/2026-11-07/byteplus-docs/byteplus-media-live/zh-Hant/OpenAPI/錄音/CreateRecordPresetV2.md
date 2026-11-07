---
title: "CreateRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createrecordpresetv2-2023-zh-TW"
---

調用 `CreateRecordPresetV2` API 以建立錄製配置。系統會根據您的錄製配置，對符合條件的直播流進行錄製。

<span id="Usage scenario"></span>
## 使用場景

`CreateRecordPresetV2` API 支援建立三層配置：Vhost（低優先級）、Vhost + App（中優先級）、以及 Vhost + App + Stream（高優先級）。當存在多層配置時，優先級依序提升。例如，若同時建立了 Vhost 和 Vhost + App 層級的配置，直播流將優先使用 Vhost + App 層級。

<span id="Requirements"></span>
## 需求


* 前置條件：

   * 當您選擇將錄製檔案儲存於 VOD 平台時，請先啟用 BytePlus VOD 服務，並參考 [Spaces](https://https://docs.byteplus.com/en/docs/byteplus-vod/docs-space-management) 建立空間。

   * 當錄製檔案儲存於 TOS 時，請先啟用 TOS 服務，並聯繫 [support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) 取得授權。

* 計費：使用錄製與儲存功能可能產生錄製費用，詳情請參考 [Transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding_2)。

* 頻率限制：單一用戶的操作頻率限制為每秒 10 次。

* 生效說明：若新增、更新或刪除錄製配置，需重新推流與拉流，並等待 3\-5 分鐘後變更才會生效。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=CreateRecordPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`CreateRecordPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢該網域所屬的名稱空間。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>App</code> 值為空，且 <code>Stream</code> 值也為空時，表示錄製配置為 Vhost 層級的全域配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>App</code> 值不為空時，請參見 <code>Stream</code> 參數說明以了解 Stream 值的含義。</div><br> |
|Stream |String |否 |`stream001` |流名稱。其值與直播流 URL 中的 StreamName 欄位一致。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 100 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當 <code>App</code> 值不為空，且 <code>Stream</code> 值為空時，表示錄製配置為 Vhost + App 層級的全域配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當<code>App</code>值不為空且<code>Stream</code>不為空時，表示錄製配置為 Vhost + App + Stream。</div><br> |
|RecordPresetConfig |[RecordPresetConfig](https://docs.byteplus.com/en/docs/24/107377#recordpresetconfig) 物件 |是 |`-` |直播錄製的詳細配置。 |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TranscodeRecord |整數 |否 |`1` |是否錄製轉碼串流。有效值：<br><br><br>* `0`（預設）：不錄製；<br><br>* `1`：錄製所有轉碼串流；<br><br>* `2`：錄製由 TranscodeSuffixList 指定的特定轉碼串流。若轉碼串流字尾清單為空，仍會錄製所有轉碼串流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需選擇<code>TranscodeRecord</code>或<code>OriginRecord</code>其中之一進行錄製。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 與 <code>OriginRecord</code> 不能同時為 <code>0</code></div><br> |
|OriginRecord |整數 |否 |`0` |是否錄製原始串流。有效值：<br><br><br>* `0`（預設）：不錄製原始串流。<br><br>* `1`：錄製原始串流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">需選擇<code>TranscodeRecord</code>或<code>OriginRecord</code>其中之一進行錄製。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 與 <code>OriginRecord</code> 不能同時為 <code>0</code>。</div><br> |
|SliceDuration |整數 |否 |`5` |單個 TS 檔案的時長，單位為秒。預設值為 10。有效範圍：2–100。當錄製檔案儲存為 HLS 格式時，此參數生效。 |
|FlvParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107377#recordparam) 物件 |否 |`-` |錄製檔案為 FLV 格式時的相關參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須透過設定<code>FlvParam</code>、<code>HlsParam</code>、<code>Mp4Param</code>三者之一的參數值，指定至少一種錄製格式。</div><br> |
|HlsParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107377#recordparam) 物件 |否 |`-` |錄製檔案為 HLS 格式時的相關參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須透過設定<code>FlvParam</code>、<code>HlsParam</code>、<code>Mp4Param</code>三者之一的參數值，指定至少一種錄製格式。</div><br> |
|Mp4Param |[RecordParam](https://docs.byteplus.com/en/docs/24/107377#recordparam) 物件 |否 |`-` |錄製檔案為 MP4 格式時的相關參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須透過設定<code>FlvParam</code>、<code>HlsParam</code>、<code>Mp4Param</code>三者之一的參數值，指定至少一種錄製格式。</div><br> |
|TranscodeSuffixList |字串陣列 |否 |`["_hd","_bd"]` |轉碼串流字尾清單。當指定的轉碼串流匹配時（`TranscodeRecord` 值為 `2`），轉碼串流錄製配置生效。`TranscodeSuffixList` 的預設配置為空，若為空則錄製所有轉碼串流。 |


<span id="recordparam"></span>
### RecordParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |布林值 |否 |`true` |是否啟用當前格式的錄製。有效值：<br><br><br>* `false`（預設）：停用<br><br>* `true`：啟用 |
|Duration |整數 |否 |`7200` |在錄製完成後儲存錄製檔案的場景下，單個檔案的錄製時長（單位：秒）預設為 7200，取值範圍為 \-1 及 300–86400。<br><br><br>* `-1`：錄製時長無限制。錄製完成後，會產生並儲存一個完整的錄製檔案。<br><br>* 當取值為 [300,86400] 區間時，錄製檔案時長達到時即產生錄製檔案，錄製完成後一併上傳。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅於錄製檔案為 HLS 格式，且需搭配分段錄製及即時儲存場景下的兩種配置之一時生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若錄製過程中發生斷線，對應產生的錄製檔案時長也會相應縮短。</div><br> |
|Splice |整數 |否 |`0` |在錄製完成後儲存錄製檔案的場景下，合併切片時間（單位為秒）的預設值為 0。其值及含義如下。<br><br><br>* `-1`：合併流片段。無論是否有暫停，所有內容都會合併為一個檔案，直到錄製達到最大時長。<br><br>* `0`（預設）：不合併流。生成新檔案。每次直播流暫停後恢復時都會重新錄製並生成新檔案。<br><br>* 大於 0 的任何值：設定生成新檔案前的最大等待時間（單位為秒）。若在設定時間內暫停並重新開始，錄製會繼續於同一檔案。在設定等待時間後恢復錄製會分割檔案。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在錄製檔案為 HLS 格式且需配置分段錄製及即時儲存場景的兩種選項之一時有效。</div><br> |
|RealtimeRecordDuration |整數 |否 |`300` |在即時儲存場景下，單檔錄製時長（單位為秒）預設為 `1800`，取值範圍為 300\-21600。當錄製時長達到設定的單檔錄製時長時，錄製檔案會立即生成並即時上傳儲存。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若錄製過程中發生斷線，對應生成的錄製檔案時長也會相應縮短。</div><br> |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107377#tosparam) 物件 |否 |`-` |TOS 儲存配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">錄製檔案僅能指定一個儲存位置，僅能選擇 <code>TOSParam</code> 或 <code>VODParam</code>，不可同時指定。</div><br> |
|VODParam |[VODParam](https://docs.byteplus.com/en/docs/24/107377#vodparam) 物件 |否 |`-` |VOD 儲存配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">錄製檔案僅能指定一個儲存位置，僅能選擇 <code>TOSParam</code> 或 <code>VODParam</code>，不可同時指定。</div><br> |
|ContinueDuration |整數 |否 |`180` |在分段錄製即時儲存場景下，設定連線中斷恢復等待時間（單位為秒），預設值為 180，取值範圍為 [0,3600]。<br><br>若連線中斷時長小於此值，錄製任務不會停止；若實際連線中斷時長大於此值，錄製任務將停止，恢復連線後會啟動新的錄製任務。 |


<span id="tosparam"></span>
### TOSParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |布林值 |否 |`true` |定義是否將錄製檔案儲存於 TOS 儲存。有效值：<br><br><br>* `false`（預設）：不將錄製檔案儲存於 TOS。<br><br>* `true`：將錄製檔案儲存於 TOS。 |
|Bucket |字串 |否 |`live-test-tos-example` |TOS 儲存的 bucket。例如，儲存位置為 live\-test\-tos\-example/live/liveapp 時，`Bucket` 的值為 `live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若使用 TOS 儲存，即在 <code>TOSParam</code> 中將 <code>Enable</code> 設為 <code>true</code>，則必須指定 <code>Bucket</code>。</div><br> |
|StorageDir |字串 |否 |`live/liveapp` |TOS 儲存 bucket 的目錄。預設為空。例如，儲存位置為 live\-test\-tos\-example/live/liveapp 時，`StorageDir` 的值為 `live/liveapp`。 |
|ExactObject |字串 |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |儲存路徑。預設值為<br><br>`"record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"`。<br><br>你可以刪除路徑中的固定片段，例如 `{App}/{Stream}`。<br><br>參數格式要求如下：<br><br><br>* 路徑不得以斜線 `/` 或反斜線 `\` 開頭；<br><br>* 路徑不得包含 `//` 或 `/./`；<br><br>* 路徑不得包含轉義序列，例如 `\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最後一個片段會作為檔案名稱，且必須遵循檔案命名規則。例如，檔案名稱不能為 `..`。<br><br><br>若保留 `ExactObject` 的預設值，生成的儲存目錄將類似於：`record/your_domain_name.com/app1/stream1/1683357987_1683358299.mp4`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若將 ExactObject 設為無法保證儲存路徑唯一性的自訂值，則有可能因儲存路徑相同而導致舊錄製檔案被新檔案覆蓋。</div><br> |


<span id="vodparam"></span>
### VODParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |布林值 |否 |`true` |是否使用 BytePlus VOD 儲存錄製檔案。有效值：<br><br><br>* `false`（預設）：不使用 BytePlus VOD 儲存錄製檔案。<br><br>* `true`：使用 BytePlus VOD 儲存錄製檔案。 |
|VodRegion |字串 |否 |`ap-singapore-1` |VOD 區域。有效值：<br><br><br>* `ap-singapore-1`：亞太區（新加坡）。<br><br>* `ap-southeast-1`：亞太區（柔佛）。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>VODParam</code> 中的 <code>Enable</code> 設為 <code>true</code>，此參數為必填。</div><br> |
|VodNamespace |字串 |否 |`Snapshot` |BytePlus VOD 空間名稱，必須屬於指定的 `VodRegion`。你可以登入 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/totalOverview/)查詢空間名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>VODParam</code> 中的 <code>Enable</code> 設為 <code>true</code>，此參數為必填。</div><br> |
|WorkflowID |字串 |否 |`25524a2d891d7daf4b9` |工作流 ID。若指定工作流 ID，則會將對應工作流套用於儲存至 VOD 的錄製檔案。你可以登入 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/totalOverview/)取得工作流 ID。預設值為空。 |
|ClassificationID |整數 |否 |`1234` |直播錄製檔案儲存至 VOD 時的影片分類 ID。你可以透過點播的 [ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications) 介面查詢影片分類 ID 等資訊。預設值為空。 |
|StorageClass |整數 |否 |`1` |直播錄製檔案儲存至 VOD 時的儲存類型。預設值為 `1`。支援的值及其含義如下：<br><br><br>* `1`：標準儲存；<br><br>* `2`：歸檔儲存。 |
|ExactObject |字串 |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |設定錄製檔案儲存至 VOD 時的儲存規則。預設值為 `record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。你可以刪除路徑中的固定片段，例如 `{App}/{Stream}`。<br><br><br>* 路徑不得以斜線 `/` 或反斜線 `\` 開頭；<br><br>* 路徑不得包含 `//` 或 `/./`；<br><br>* 路徑不得包含轉義序列，例如 `\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最後一個片段會作為檔案名稱，且必須遵循檔案命名規則。例如，檔案名稱不能為 `..`。<br><br><br>若保留預設值，生成的儲存目錄將類似於：`record/your_domain_name/app1/stream1/1683357987_1683358299.mp4`。 |


<span id="Response parameters"></span>
## 回應參數

如需查詢 API 專屬回應參數，請參見下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|PresetName |字串 |`abcdabcdab` |錄製配置 ID。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=CreateRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "RecordPresetConfig": {
        "OriginRecord": 1,
        "HlsParam": {
            "Enable": "true",
            "RealtimeRecordDuration": 7200,
            "Splice": 0,
            "TOSParam": {
                "Enable": true,
                "Bucket": "live-test-tos-example",
                "StorageDir": "",
                "RecordObject": "record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"
            }
        }
    }
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PresetName": "abc****dab"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。如果仍然返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107377#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因當前帳號下無請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳號下無請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 未開通計費狀態，請開通服務或儲值。 |尚未啟用視訊直播服務或帳號欠費，導致無法取得帳單。請檢查服務啟用狀態及帳號欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。建議重試。如果仍然返回錯誤碼，請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |請求建立的資源（包括網域名稱空間、網域名稱、應用名稱、配置、憑證）已存在。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
