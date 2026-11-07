---
title: "UpdateCMAFConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig-zh-TW"
---

在動態自適應串流（DASH）及低延遲 DASH（LL\-DASH）中，直播串流會被切分為 Common Media Application Format（CMAF）片段。透過呼叫 `UpdateCMAFConfig` API，您可以調整片段時長及片段數量設定，有效降低延遲並提升指定網域名稱空間（Vhost）下直播的相容性。

<span id="Requirements"></span>
## 需求


* 先決條件：

   * 需使用支援 DASH 的播放器。

   * iOS 10.0、macOS 10.12 及 tvOS 10.0 或更高版本的作業系統皆支援 CMAF 內容。

* 限制：

   * DASH 封裝適用於推流、使用 HLS、FLV 及 Real\-Time Messaging Protocol（RTMP）進行源站拉流，以及使用 DASH over CMAF 進行拉流。

   * DASH 封裝設定不僅適用於此網域名稱，亦適用於同一網域名稱空間（Vhost）下的其他網域名稱。

   * 封裝設定於 3 至 5 分鐘內生效。

* 頻率限制：每個帳戶每秒最多 10 次查詢


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateCMAFConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，亦必須帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateCMAFConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`Arctic` |網域名稱空間。您可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或於 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面查詢該網域所屬的網域名稱空間。 |
|App |String |否 |`Far` |直播串流 URL 中的 AppName 欄位。若未指定，則設定將套用至所有 AppName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。 |
|Interval |Float |否 |`2` |CMAF 片段時長可設定為 `1` 至 `60` 秒。預設值為 `2`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建議直播串流的畫面組（GOP）大小保持穩定，且片段時長等於或為 GOP 大小的整數倍。</div><br> |
|PlaylistLength |Integer |否 |`6` |播放列表中包含的媒體片段數量。可輸入 `3` 至 `10` 的整數，預設值為 `3`。 |
|DisableLowLatency |Boolean |否 |`true` |是否停用低延遲 DASH。低延遲 DASH 擴展協議以實現低延遲影片串流，同時維持可擴展性。預設值為 `false`。<br><br><br>* `true`：停用；<br><br>* `false`：啟用。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateCMAFConfig&Version=2023-01-01
{
    "Vhost": "example",
    "App": "liveShow",
    "Interval": 3,
    "PlaylistLength": 6,
    "DisableLowLatency": true
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "2024041105461468A8B53B2CE41BAA7E87",
        "Action": "UpdateCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
