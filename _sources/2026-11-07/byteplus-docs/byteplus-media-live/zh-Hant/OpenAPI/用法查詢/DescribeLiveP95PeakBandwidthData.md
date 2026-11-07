---
title: "DescribeLiveP95PeakBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata-zh-TW"
---

調用 `DescribeLiveP95PeakBandwidthData` API，可查詢指定直播域名在指定時間範圍內的第 95 百分位峰值頻寬使用情況，包括推流域名的上行第 95 百分位峰值頻寬和拉流域名的下行第 95 百分位峰值頻寬。

<span id="Requirements"></span>
## 需求


* 限制：支援查詢指定域名（包含已刪除域名）產生的第 95 百分位峰值頻寬使用數據。

* 頻率限制：每個帳號每秒最多查詢 30 次

* 數據延遲：15 分鐘

* 數據度量：頻寬數據以 1000 為基數計算，例如 1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveP95PeakBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用時，除 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveP95PeakBandwidthData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。預設為空，表示查詢您 BytePlus MediaLive 下所有域名的頻寬使用數據。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [域名](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的域名。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，需符合 RFC 3339 格式，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">單次查詢的最大時間跨度為 31 天，歷史查詢的最大時間範圍為 366 天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`300` |數據聚合的時間粒度，單位為秒，目前介面預設且僅支援以 `300` 秒為間隔進行數據分段。 |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "HTTP-HLS"]` |推拉流協議。預設表示所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 協議的推拉流協議，採用 FLV 格式進行視訊傳輸。<br><br>* `HTTP-HLS`：基於 HTTP 協議的推拉流協議，採用 TS 格式進行視訊傳輸。<br><br>* `RTMP`：即時訊息傳輸協議，用於實時訊息傳輸。<br><br>* `RTM`：即時媒體協議，用於超低延遲直播。<br><br>* `SRT`：安全可靠傳輸協議，用於安全可靠的串流。<br><br>* `QUIC`：Quick UDP Internet Connections，一種基於 UDP 的新型低延遲網際網路傳輸協議。<br><br>* `CMAF`：通用媒體應用格式，一種多功能串流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢 <code>QUIC</code> 協議時，不能同時查詢其他協議。</div><br> |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107407#region) |否 |`-` |CDN 節點 IP 所屬的區域列表，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">RegionList 與 UserRegionList 不能在同一請求中同時使用。</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107407#region) |否 |`-` |客戶端 IP 所屬區域列表，預設表示全部區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可於同一請求中同時使用。</div><br> |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |String |否 |`CN` |區域資訊中的主要區域識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。 |
|Country |String |否 |`CN` |區域資訊中的國家識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。以國家進行篩選時，需同時傳入 'Area' 與 'Country'。 |
|Province |String |否 |`beijing` |區域資訊中的省份識別碼，目前不支援中國大陸、香港、澳門、台灣以外的國家或地區。可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得識別碼資訊。以省份進行篩選時，需同時傳入 `Area`、`Country` 及 `Province`。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"]` |網域名稱列表。 |
|StartTime |String |`2022-04-18T20:00:00Z` |查詢範圍的起始時間（RFC 3339 格式 UTC 時間，精確到秒）。 |
|EndTime |String |`2022-04-18T22:00:00Z` |查詢範圍的結束時間（RFC 3339 格式 UTC 時間，精確到秒）。 |
|Aggregation |Integer |`300` |資料粒度，單位為秒。 |
|ProtocolList |Array of String |`["HTTP-FLV", "HTTP-HLS"]` |推拉流協議。預設表示全部協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 協議的推拉流協議，採用 FLV 格式進行視頻傳輸。<br><br>* `HTTP-HLS`：基於 HTTP 協議的推拉流協議，採用 TS 格式進行視頻傳輸。<br><br>* `RTMP`：即時訊息傳輸協議，用於即時訊息傳輸。<br><br>* `RTM`：即時媒體協議，用於超低延遲直播。<br><br>* `SRT`：安全可靠傳輸協議，用於安全可靠的串流。<br><br>* `QUIC`：Quick UDP Internet Connections，基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：Common Media Application Format，通用串流協議。 |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107407#region) |`-` |CDN 節點 IP 所屬區域列表。 |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107407#region) |`-` |客戶端 IP 所屬區域列表。 |
|P95PeakBandwidth |Float |`100` |指定時間範圍內，第 95 百分位上行與下行峰值頻寬之總和。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若請求時於 <code>RegionList</code> 指定多個區域，則會回傳這些區域的第 95 百分位上行與下行峰值頻寬總和。</div><br> |
|P95PeakTimestamp |String |`2022-04-18T22:00:00Z` |第 95 百分位峰值頻寬的時間戳，RFC 3339 格式 UTC 時間，精確到秒。 |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Area |String |`CN` |區域資訊中的區域識別碼。 |
|Country |String |`CN` |區域資訊中的國家識別碼。 |
|Province |String |`beijing` |區域資訊中的省份識別碼。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveP95PeakBandwidthData&Version=2023-01-01
{
    "StartTime": "2022-04-18T20:00:00Z",
    "EndTime": "2022-04-18T22:00:00Z",
    "Aggregation": 300
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveP95PeakBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StartTime": "2022-04-18T20:00:00Z",
        "EndTime": "2022-04-18T22:00:00Z",
        "Aggregation": 300,
        "P95PeakBandwidth": 100,
        "P95PeakTimestamp": "2022-04-18T22:00:00Z"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107407#request-parameters) 說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、App 名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
