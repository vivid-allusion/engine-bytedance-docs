---
title: "UpdateSnapshotPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatesnapshotpresetv2-zh-TW"
---

更新截圖配置。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒最多 10 次請求。

* 生效說明：若要使截圖配置的新增、更新或刪除操作生效，請在修改後 3\-5 分鐘重新推流。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateSnapshotPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須傳遞[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateSnapshotPresetV2` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名命名空間。可調用[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2)獲取更新截圖配置所需的`Vhost`值。 |
|App |String |是 |`live` |應用名稱。可調用[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2)獲取更新截圖配置所需的`App`值。 |
|Status |Integer |否 |`1` |截圖配置是否生效。可選值：<br><br><br>* `1`：生效。<br><br>* `0`：不生效。 |
|SnapshotPresetConfig |[SnapshotPresetConfig](https://docs.byteplus.com/en/docs/24/107433#snapshotpresetconfig) 對象 |是 |`-` |截圖配置的詳細參數。 |
|Preset |String |是 |`preset-123` |截圖配置名稱。可調用[ListVhostSnapshotPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/listvhostsnapshotpresetv2)獲取更新截圖配置所需的 `Name` 值。 |


<span id="snapshotpresetconfig"></span>
### SnapshotPresetConfig


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|JpegParam |[JpegParam](https://docs.byteplus.com/en/docs/24/107433#jpegparam) 對象 |否 |`-` |啟用 JPEG 截圖時設置的 JPEG 格式截圖參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須啟用 JPEG 或 JPG 截圖其中之一，不能同時啟用。</div><br> |
|JpgParam |[JpgParam](https://docs.byteplus.com/en/docs/24/107433#jpgparam) 對象 |否 |`-` |啟用 JPG 截圖時設置的 JPG 格式截圖參數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須啟用 JPEG 或 JPG 截圖其中之一，不能同時啟用。</div><br> |
|Interval |Integer |否 |`10` |截圖的時間間隔，單位為秒。預設值：`10`。該值必須為正整數。 |


<span id="jpegparam"></span>
### JpegParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否啟用當前格式的截圖。預設值：`false`。可選值：<br><br><br>* `true`：啟用。<br><br>* `false`：不啟用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107433#tosparam) 對象 |否 |`-` |用於截圖存儲至 TOS 的配置。 |


<span id="jpgparam"></span>
### JpgParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否啟用當前格式的截圖。預設值：`false`。可選值：<br><br><br>* `true`：啟用。<br><br>* `false`：不啟用。 |
|TOSParam |[TOSParam](https://docs.byteplus.com/en/docs/24/107433#tosparam) 對象 |否 |`-` |用於截圖存儲至 TOS 的配置。 |


<span id="tosparam"></span>
### TOSParam


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |否 |`true` |是否使用 TOS 進行存儲。預設值：`false`。可選值：<br><br><br>* `true`：使用 TOS。<br><br>* `false`：不使用 TOS。 |
|Bucket |String |否 |`live-test-tos-example` |TOS 存儲桶名稱。例如，若存儲路徑為`live-test-tos-example/live/liveapp`，則該參數值為`live-test-tos-example`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">使用 TOS 存儲時，此參數為必填。</div><br> |
|StorageDir |String |否 |`live/liveapp` |TOS 存儲桶下的存儲目錄。預設為空。例如，若存儲路徑為`live-test-tos-example/live/liveapp`，則該參數值為`live/liveapp`。 |
|ExactObject |字串 |否 |`{Domain}/{App}/{Stream}/{UnixTimestamp}` |當截圖類型為非覆蓋時的儲存規則。您可以按照 {Domain}/{App}/{Stream}/{UnixTimestamp} 格式配置規則。支援以下字元：<br><br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 數字（0\-9）<br><br>* 連字號（\-）<br><br>* 驚嘆號（!）<br><br>* 底線（_）<br><br>* 句點（.）<br><br>* 星號（\*）<br><br>* 佔位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您必須傳入 <code>ExactObject</code> 或 <code>OverwriteObject</code>。</div><br> |
|OverwriteObject |字串 |否 |`{Domain}/{App}/{Stream}` |當截圖類型為覆蓋時的儲存規則。您可以按照 {Domain}/{App}/{Stream} 格式配置規則。支援以下字元：<br><br><br>* 小寫字母（a\-z）<br><br>* 大寫字母（A\-Z）<br><br>* 數字（0\-9）<br><br>* 連字號（\-）<br><br>* 驚嘆號（!）<br><br>* 底線（_）<br><br>* 句點（.）<br><br>* 星號（\*）<br><br>* 佔位符<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">您必須傳入 <code>ExactObject</code> 或 <code>OverwriteObject</code>。</div><br> |


<span id="Response parameters"></span>
## 回應參數

本 API 僅在回應中返回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=UpdateSnapshotPresetV2&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "SnapshotPresetConfig": {
        "JpegParam": {
            "Enable": true,
            "TOSParam": {
                "Enable": true,
                "Bucket": "live-test-tos-example",
                "StorageDir": "live/liveapp",
                "ExactObject": "{Domain}/{App}/{Stream}/{UnixTimestamp}"
            }
        },
        "Interval": 10
    },
    "Preset": "preset-123"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "UpdateSnapshotPresetV2",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考請求參數說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型態是否正確。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域命名空間、網域、App、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取對應資源，請檢查請求參數 |因當前帳戶下無請求資源（資源包括網域命名空間、網域、App、配置及憑證），請求被拒絕。 |
|403 |RequestForbidden.BillingStatus |AccountID 的計費狀態不可用，請開通服務或充值。 |BytePlus MediaLive 服務尚未開通或帳戶欠費，導致帳單不可用。請檢查服務開通狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域命名空間、網域、App、配置及憑證）。建議重試。若仍返回錯誤碼，請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到預設 |未找到配置。請檢查所提供的配置是否與已建立的配置一致。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |發生與預設相關的內部錯誤，請聯絡管理員。 |發生與功能配置相關的內部錯誤。請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請 [聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
