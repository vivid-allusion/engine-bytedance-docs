---
title: "ListVhostRecordPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023-zh-TW"
---

呼叫 `ListVhostRecordPresetV2` API 以查詢某個 Vhost 下的所有錄製配置，包括 Vhost、Vhost + App、Vhost + App + Stream 三個層級的所有配置。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=ListVhostRecordPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了特定 API 參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostRecordPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得網域名稱空間。 |
|Type |String |否 |`tos` |你要查詢的儲存類型。有效值包括：<br><br><br>* `tos`（預設）：BytePlus TOS。<br><br>* `vod`：BytePlus VOD。 |


<span id="Response parameters"></span>
## 回應參數

如需唯一的 API 特定回應參數，請參見下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/107409#presetlist) 陣列 |`-` |錄製配置列表。 |


<span id="presetlist"></span>
### PresetList


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|App |String |`live` |AppName 欄位。 |
|Stream |String |`example_stream` |StreamName 欄位。 |
|SlicePresetV2 |[SlicePresetV2](https://docs.byteplus.com/en/docs/24/107409#slicepresetv2) 物件 |`-` |配置資訊。 |


<span id="slicepresetv2"></span>
### SlicePresetV2


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|ID |Long |`8` |配置 ID。 |
|Name |String |`RecordPresetexample` |配置名稱。 |
|RecordPresetConfig |[RecordPresetConfig](https://docs.byteplus.com/en/docs/24/107409#recordpresetconfig) 物件 |`-` |錄製參數。 |


<span id="recordpresetconfig"></span>
### RecordPresetConfig


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|TranscodeRecord |Integer |`1` |是否錄製轉碼串流。有效值包括：<br><br><br>* `0`（預設）：不錄製；<br><br>* `1`：錄製所有轉碼串流；<br><br>* `2`：錄製由 TranscodeSuffixList 指定的轉碼串流。若轉碼串流後綴列表為空，仍然表示錄製所有轉碼串流。 |
|TranscodeSuffixList |String 陣列 |`["_hd"]` |轉碼串流後綴列表。當轉碼串流錄製配置根據指定的轉碼串流（`TranscodeRecord` 值為 `2`）生效時，`TranscodeSuffixList` 的預設配置為空，效果等同於錄製所有轉碼串流。 |
|OriginRecord |Integer |`1` |是否錄製原始串流。有效值包括：<br><br><br>* `0`（預設）：不錄製原始串流。<br><br>* `1`：錄製原始串流。 |
|SliceDuration |Integer |`5` |單個 TS 檔案的時長（秒）。預設值為 `10`。有效範圍：5–30。當錄製檔案儲存為 HLS 格式時，此參數生效。 |
|FlvParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107409#recordparam) 物件 |`-` |錄製檔案儲存為 FLV 格式時的錄製配置。 |
|HlsParam |[RecordParam](https://docs.byteplus.com/en/docs/24/107409#recordparam) 物件 |`-` |錄製檔案儲存為 HLS 格式時的錄製配置。 |
|Mp4Param |[RecordParam](https://docs.byteplus.com/en/docs/24/107409#recordparam) 物件 |`-` |錄製檔案儲存為 MP4 格式時的錄製配置。 |


<span id="recordparam"></span>
### RecordParam


|**參數** |**資料型別** |**範例值** |**描述** |
|---|---|---|---|
|Enable |Boolean |`true` |是否啟用當前格式的錄製。有效值包括：<br><br><br>* `false`：停用<br><br>* `true`：啟用 |
|時長 |整數 |`7200` |在錄製完成後儲存錄製檔案的場景下，錄製檔案的最長時長及其值與含義如下。<br><br><br>* `-1`：表示完整錄製。錄製完成後，會生成並儲存完整的錄製檔案。<br><br>* 當值在 [300, 86400] 範圍內時，表示錄製檔案會根據設定的時長分段生成。錄製完成後，錄製檔案會一併上傳並儲存。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此參數僅在錄製檔案為 HLS 格式且需配置為分段錄製及即時儲存場景的兩種選項之一時有效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">錄製過程中若發生斷線，對應生成的錄製檔案時長也會相應縮短。</div><br> |
|RealtimeRecordDuration |整數 |`7200` |在分段錄製及即時儲存場景下，設定分段錄製檔案的時長（單位：秒）。預設值為 1800。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">錄製過程中若發生斷線，對應生成的錄製檔案時長也會相應縮短。</div><br> |
|Splice |整數 |`0` |在錄製完成後儲存錄製檔案的場景下，決定直播流斷線時錄製內容的合併方式。其值與含義如下。<br><br><br>* `-1`：合併流片段。無論是否有暫停，所有內容都會合併為一個檔案，直到錄製達到最大時長。<br><br>* `0`（預設）：生成新檔案。每次直播流暫停後重新開始，會重新錄製並生成新檔案。<br><br>* 大於 0 的任何值：設定生成新檔案前的最大等待時間（單位：秒）。若在定義時間內暫停並重新開始，錄製會繼續在同一檔案中。超過定義等待時間後重新開始，則會分割檔案。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">此參數僅在錄製檔案為 HLS 格式且需配置為分段錄製及即時儲存場景的兩種選項之一時有效。</div><br> |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107409#tosparam) 物件 |`-` |TOS 儲存配置。 |
|VODParam |[VODParam](https://docs.byteplus.com/en/docs/24/107409#vodparam) 物件 |`-` |VOD 儲存配置。 |


<span id="tosparam"></span>
### TOSParam


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Enable |布林值 |`true` |定義是否將錄製檔案儲存至 TOS 儲存。有效值包括：<br><br><br>* `false`：不將錄製檔案儲存至 TOS。<br><br>* `true`：將錄製檔案儲存至 TOS。 |
|Bucket |字串 |`live-test-tos-example` |TOS 儲存的 bucket。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若 <code>Enable</code> 在 <code>TOSParam</code> 中設為 <code>true</code>，則必須指定 <code>Bucket</code>。</div><br> |
|StorageDir |字串 |`live/liveapp` |錄製檔案在 bucket 中的目錄，預設為空。 |
|ExactObject |字串 |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |錄製檔案的儲存規則。 |


<span id="vodparam"></span>
### VODParam


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Enable |布林值 |`true` |是否使用 BytePlus VOD 儲存錄製檔案。有效值包括：<br><br><br>* `false`：不使用 BytePlus VOD 儲存錄製檔案。<br><br>* `true`：使用 BytePlus VOD 儲存錄製檔案。 |
|VodRegion |字串 |`ap-singapore-1` |VOD 區域。有效值：<br><br><br>* `ap-singapore-1`：亞太區（新加坡）。<br><br>* `ap-southeast-1`：亞太區（柔佛）。 |
|VodNamespace |字串 |`SnapShot` |BytePlus VOD 空間的名稱，屬於 `VodRegion`。您可以登入 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/totalOverview/)查詢空間名稱。 |
|WorkflowID |String |`25524a2d*********891d7daf4b9` |工作流 ID。若指定工作流 ID，則會將相應的工作流應用於儲存在 VOD 的錄製檔案。您可以登入 [BytePlus VOD 控制台](https://console.byteplus.com/vodpaas/totalOverview/)取得工作流 ID。 |
|ClassificationID |Integer |`12***45` |直播錄製檔案儲存至點播時的影片分類 ID。您可以透過點播的 [ListVideoClassifications](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listvideoclassifications) 介面查詢影片分類 ID 等資訊。預設為空。 |
|StorageClass |Integer |`1` |直播錄製檔案儲存至 VOD 時的儲存類型。預設值為 `1`。支援的值如下。<br><br><br>* `1`：標準儲存；<br><br>* `2`：歸檔儲存。 |
|ExactObject |String |`record/{PubDomain}/{App}/{Stream}/{StartTime}_{EndTime}` |設定錄製檔案儲存至 VOD 時的儲存規則。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=ListVhostRecordPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20220726*******************051B513A",
        "Action": "ListVhostRecordPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SlicePresetV2": {
                "ID": 8,
                "Name": "RecordPresetexample",
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
        }
    ]
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllowed |此 AccountID 無權訪問相應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |尚未開通影片直播服務或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括域名空間、域名、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯繫管理員。 |發生與預設相關的內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
