---
title: "UpdateRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterecordpresetv2-2023-zh-TW"
---

調用 `UpdateRecordPresetV2` API 以更新已建立的錄製配置。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次查詢。

* 生效說明：新增、更新或刪除錄製配置後，需在操作完成後（3\-5 分鐘）重新推流及拉流，才能使用變更後的配置。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateRecordPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRecordPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待更新配置的網域名稱空間。 |
|App |String |否 |`live` |AppName 欄位。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待更新配置的 AppName 欄位。 |
|Stream |String |否 |`example_stream` |StreamName 欄位。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待更新配置的 StreamName 欄位。 |
|Preset |String |是 |`liverecord` |配置名稱。可調用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 取得待更新配置的名稱。 |
|RecordPresetConfig |[RecordPresetConfig](https://docs.byteplus.com/en/docs/24/107385#recordpresetconfig) 物件 |否 |`-` |錄製的詳細配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">以下參數若未傳入值，則表示與更新前的配置相同。</div><br> |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TranscodeRecord |Integer |否 |`1` |是否錄製轉碼流。有效值：<br><br><br>* `0`（預設）：不錄製；<br><br>* `1`：錄製所有轉碼流；<br><br>* `2`：錄製由 TranscodeSuffixList 指定的轉碼流。若轉碼流後綴列表為空，仍會錄製所有轉碼流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">錄製時需選擇 <code>TranscodeRecord</code> 或 <code>OriginRecord</code> 其中之一。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 與 <code>OriginRecord</code> 不可同時為 <code>0</code>。</div><br> |
|OriginRecord |Integer |否 |`1` |是否錄製原始流。有效值：<br><br><br>* `0`（預設）：不錄製；<br><br>* `1`：錄製原始流。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">錄製時需選擇 <code>TranscodeRecord</code> 或 <code>OriginRecord</code> 其中之一。</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>TranscodeRecord</code> 與 <code>OriginRecord</code> 不可同時為 <code>0</code>。</div><br> |
|SliceDuration |Integer |否 |`5` |單個 TS 檔案的時長（秒）。預設值為 `10`。有效範圍：5–30。此參數僅在錄製檔案存為 HLS 格式時生效。 |
|FlvParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107385#recordparam) 物件 |否 |`-` |錄製檔案存為 FLV 格式時的錄製配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須至少指定一種錄製格式，需設定 <code>FlvParam</code>、<code>HlsParam</code> 或 <code>Mp4Param</code> 其中之一的參數值。</div><br> |
|HlsParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107385#recordparam) 物件 |否 |`-` |錄製檔案存為 HLS 格式時的錄製配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須至少指定一種錄製格式，需設定 <code>FlvParam</code>、<code>HlsParam</code> 或 <code>Mp4Param</code> 其中之一的參數值。</div><br> |
|Mp4Param |[RecordParam](https://docs.byteplus.com/en/docs/24/107385#recordparam) 物件 |否 |`-` |當你以 MP4 格式儲存錄製檔案時的錄製配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">你必須透過設定其中一個參數值，<code>FlvParam</code>、<code>HlsParam</code> 和 <code>Mp4Param</code>，指定至少一種錄製格式。</div><br> |
|TranscodeSuffixList |字串陣列 |否 |`["_hd"]` |轉碼串流後綴清單。當指定的轉碼串流匹配時（`TranscodeRecord` 值為 `2`），轉碼串流錄製配置生效，`TranscodeSuffixList` 的預設配置為空值，若為空值則錄製所有轉碼串流。 |


<span id="recordparam"></span>
### RecordParam


|**參數** |**資料型態** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Enable |布林值 |否 |`true` |是否啟用當前格式的錄製。有效值：<br><br><br>* `false`（預設）：停用<br><br>* `true`：啟用 |
|Duration |整數 |否 |`7200` |在錄製完成後儲存錄製檔案的場景下，單一檔案的錄製時長（單位：秒）預設為 7200，值域為 \-1 及 300\-86400。<br><br><br>* `-1`：錄製時間無限制。錄製完成後會產生並儲存完整的錄製檔案。<br><br>* 當值介於 [300,86400] 時，表示錄製檔案時長達到設定值時立即產生錄製檔案，並於錄製完成後一併上傳。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅於錄製檔案為 HLS 格式時生效，並需於分段錄製及即時儲存場景下配置為兩種選項之一。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若錄製過程中發生斷線，對應產生的錄製檔案時長也會相應縮短。</div><br> |
|Splice |整數 |否 |`0` |在錄製完成後儲存錄製檔案的場景下，合併拼接時間（單位：秒）預設為 0。其值及含義如下。<br><br><br>* `-1`：合併串流片段。無論任何暫停，所有內容都會合併為一個檔案，直到錄製達到最大時長。<br><br>* `0`（預設）：不合併串流。產生新檔案。每次直播串流暫停後重新開始，皆會重新錄製一個新檔案。<br><br>* 任何大於 0 的值：設定產生新檔案前的最大等待時間（單位：秒）。若於定義時間內暫停並重新開始，錄製會持續於同一檔案。超過定義等待時間後重新開始，則會分割檔案。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅於錄製檔案為 HLS 格式時生效，並需於分段錄製及即時儲存場景下配置為兩種選項之一。</div><br> |
|RealtimeRecordDuration |整數 |否 |`7200` |於分段錄製及即時儲存場景下，設定分段錄製檔案的時長（單位：秒）。預設值為 1800，值域為 `300-21600`。當錄製時長達到設定的單檔錄製時長時，錄製檔案會立即產生並即時上傳儲存。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若錄製過程中發生斷線，對應產生的錄製檔案時長也會相應縮短。</div><br> |
|ContinueDuration |整數 |否 |`180` |在分段錄製即時存儲場景下，設定連線中斷恢復等待時間（單位：秒），預設值為180，取值範圍為[0,3600]。<br><br>若連線中斷時長小於此值，錄製任務不會停止；若實際連線中斷時長大於此值，錄製任務將停止，並在連線恢復後啟動新的錄製任務。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107385#tosparam)的物件 |否 |`-` |TOS存儲配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只能指定一個錄製檔案的存儲位置，僅能選擇<code>TOSParam</code>或<code>VODParam</code>，不可同時選擇。</div><br> |
|VODParam |[VODParam](https://docs.byteplus.com/en/docs/24/107385#vodparam)的物件 |否 |`-` |VOD存儲配置。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只能指定一個錄製檔案的存儲位置，僅能選擇<code>TOSParam</code>或<code>VODParam</code>，不可同時選擇。</div><br> |


<span id="tosparam"></span>
### TOSParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |定義是否將錄製檔案存儲於TOS。有效值：<br><br><br>* `false`：不將錄製檔案存儲於TOS。<br><br>* `true`：將錄製檔案存儲於TOS。 |
|Bucket |String |否 |`live-test-tos-example` |BytePlus TOS存儲的bucket。例如，當存儲位置為live\-test\-tos\-example/live/liveapp時，`Bucket`的值為`live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若使用TOS存儲，即在<code>TOSParam</code>中將<code>Enable</code>設為<code>true</code>，則必須指定<code>Bucket</code>。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS存儲bucket的目錄。預設為空。例如，當存儲位置為live\-test\-tos\-example/live/liveapp時，`StorageDir`的值為`live/liveapp`。 |
|ExactObject |String |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |存儲路徑。預設值為<br><br>`"record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}"`。<br><br>可刪除路徑中的固定片段，例如`{App}/{Stream}`。<br><br>參數格式要求如下：<br><br><br>* 路徑不得以斜線`/`或反斜線`\`開頭；<br><br>* 路徑不得包含`//`或`/./`；<br><br>* 路徑不得包含跳脫序列，例如`\b`、`\t`、`\n`、`\v`、`\f`、`\r`；<br><br>* 最後一段將作為檔案名稱，且必須符合檔案命名規則。例如，不可為`..`。<br><br><br>若保持`ExactObject`的預設值，最終存儲目錄將類似於：`record/your_domain_name.com/app1/stream1/1683357987_1683358299.mp4`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若將ExactObject設為自訂值且無法保證存儲路徑唯一性，則有可能因存儲路徑相同而導致舊錄製檔案被新檔案覆蓋。</div><br> |


<span id="vodparam"></span>
### VODParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否使用BytePlus VOD存儲錄製檔案。有效值：<br><br><br>* `false`：不使用BytePlus VOD存儲錄製檔案。<br><br>* `true`：使用BytePlus VOD存儲錄製檔案。 |
|VodRegion |String |否 |`ap-singapore-1` |VOD區域。有效值：<br><br><br>* `ap-singapore-1`：亞太區（新加坡）。<br><br>* `ap-southeast-1`：亞太區（柔佛）。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若<code>VODParam</code>中的<code>Enable</code>設為<code>true</code>，則此參數為必填。</div><br> |
|VodNamespace |String |否 |`Snapshot` |BytePlus VOD空間名稱，必須屬於指定的`VodRegion`。可登入[BytePlus VOD控制台](https://console.byteplus.com/vodpaas/totalOverview/)查詢空間名稱。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若<code>VODParam</code>中的<code>Enable</code>設為<code>true</code>，則此參數為必填。</div><br> |
|WorkflowID |字串 |否 |`25524a2d*********891d7daf4b9` |工作流 ID。若指定工作流 ID，則相應的工作流將應用於儲存在 VOD 的錄製檔案。您可以登入 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/totalOverview/)以取得工作流 ID。預設值為空。 |
|ClassificationID |整數 |否 |`12**34` |錄製檔案儲存至點播時的影片分類 ID。您可以透過點播的 [ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications)介面查詢影片分類 ID 等資訊。預設為空。 |
|StorageClass |整數 |否 |`1` |錄製檔案儲存至 VOD 時的儲存類型。預設值為`1`。支援的值及其含義如下。<br><br><br>* `1`：標準儲存；<br><br>* `2`：歸檔儲存。 |
|ExactObject |字串 |否 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |設定錄製檔案儲存至 VOD 時的儲存規則。預設值為`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}`。您可以刪除路徑中的固定片段，例如`{App}/{Stream}`。<br><br><br>* 路徑不得以斜線`/`或反斜線`\`開頭；<br><br>* 路徑不得包含`//`或`/./`；<br><br>* 路徑不得包含如`\b`、`\t`、`\n`、`\v`、`\f`、`\r`等跳脫序列；<br><br>* 最後一段將作為檔案名稱，必須遵循檔案命名規則。例如，不得為`..`。<br><br><br>若保留預設值，最終儲存目錄將類似於：`record/your_domain_name/app1/stream1/1683357987_1683358299.mp4`。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Preset": "liverecord",
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
        "RequestId": "20220726*******************051B513A",
        "Action": "UpdateRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107385#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取相應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |此 AccountID 未開通計費狀態，請開通服務或充值。 |尚未啟用影片直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設 |未找到配置。請檢查傳入的配置是否與已建立的配置一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與預設相關的內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
