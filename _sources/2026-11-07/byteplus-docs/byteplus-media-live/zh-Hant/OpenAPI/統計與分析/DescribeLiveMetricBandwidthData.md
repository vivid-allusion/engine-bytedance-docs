---
title: "DescribeLiveMetricBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata-zh-TW"
---

調用 `DescribeLiveMetricBandwidthData` API，以查詢指定時間範圍內的直播域名或直播流的頻寬監控數據。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 2025 年 2 月 18 日起，我們將不再維護此舊版 API。其文件將於 2025 年 5 月 18 日下線。建議遷移至新版 UpdateUser 介面。詳情請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata">DescribeLiveEdgeStatData</a> 文件。</div>


<span id="Requirements"></span>
## 要求


* 限制：

   * 支援查詢特定域名（包含已刪除的域名）或特定直播流所產生的頻寬監控數據。

   * 頻寬監控數據用於數據監控，其收集方式與頻寬用量數據不同。請使用 [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) 查詢直播頻寬用量數據。

* 速率限制：每個帳號每秒 100 次查詢

* 數據延遲：

   * 當聚合粒度為 60 秒時，數據延遲為 5 分鐘；

   * 其他時間粒度下，數據延遲為 15 分鐘。

* 數據度量：頻寬數據以 1000 為基數計算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveMetricBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了 API 專屬參數外，還必須傳入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveMetricBandwidthData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。預設為空，表示查詢 BytePlus MediaLive 下所有域名的頻寬用量數據。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取待查詢的域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">以流粒度查詢頻寬監控數據時，需同時指定 <code>App</code> 及 <code>Stream</code> 參數以指定直播流。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 100 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">以流粒度查詢頻寬監控數據時，需同時指定 <code>App</code> 及 <code>Stream</code> 參數以指定直播流。</div><br> |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設為所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸 FLV 格式的視頻。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸 TS 格式的視頻。<br><br>* `RTMP`：即時消息傳輸協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：Quick UDP Internet Connections，一種基於 UDP 的新型低延遲網際網路傳輸協議。<br><br>* `CMAF`：一種用於高效自適應 HTTP 視訊串流的協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢 <code>QUIC</code> 協議時，不能同時查詢其他協議。</div><br> |
|ISPList |字串陣列 |否 |`["telecom"]` |提供網路接入服務的運營商標識。預設情況下，表示全部運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。<br><br><br>如需獲取各運營商的標識，可呼叫 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107424#region) 陣列 |否 |`-` |CDN 節點 IP 所屬區域列表，預設表示全部區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不能在同一請求中同時使用。</div><br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107424#region) 陣列 |否 |`-` |用戶端 IP 所屬區域列表，預設表示全部區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不能在同一請求中同時使用。</div><br> |
|StartTime |字串 |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |否 |`300` |資料彙總的粒度，單位為秒，支援以下選項：<br><br><br>* `60`：1 分鐘。每 1 分鐘彙總一次時，單次查詢的最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天；<br><br>* `300`：（預設）5 分鐘。每 5 分鐘彙總一次時，單次查詢的最大時間跨度為 31 天，歷史查詢時間範圍為 366 天；<br><br>* `3600`：1 小時。每 1 小時彙總一次時，單次查詢的最大時間跨度為 93 天，歷史查詢時間範圍為 366 天。 |
|DetailField |字串陣列 |否 |`["Domain"]` |資料分割維度預設不進行拆分。支援的維度如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供商；<br><br>* `Protocol`：推拉流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當使用 <code>DetailField</code> 參數指定資料分割維度，且至少有一個參數（<code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code>）傳入多個值時，才會根據指定維度進行資料分割（如 Domain、ISP、Protocol）。</div><br> |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |可呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 獲取區域資訊中的大區標識。 |
|Country |字串 |否 |`CN` |可呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 獲取區域資訊中的國家標識。按國家篩選時，需同時傳入「Area」與「Country」。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份標識，目前不支援中國大陸、香港、澳門、台灣以外的國家或地區。可呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 獲取標識資訊。在按省份篩選時，需同時傳入`Area`、`Country`及`Province` |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多詳情請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com"]` |域名列表。 |
|App |字串 |`live` |查詢流量資料（以串流為粒度）時指定的 AppName 欄位。 |
|Stream |字串 |`example_stream` |查詢流量資料（以串流為粒度）時指定的 StreamName 欄位。 |
|ProtocolList |字串陣列 |`["HTTP-FLV", "RTMP"]` |推拉流協議，協議說明如下：<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸 FLV 格式的視頻。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸 TS 格式的視頻。<br><br>* `RTMP`：即時訊息協議（Real Time Message Protocol）。<br><br>* `RTM`：即時媒體（Real Time Media），超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議（Secure Reliable Transport protocol）。<br><br>* `QUIC`：快速 UDP 網際網路連線（Quick UDP Internet Connections），基於 UDP 的新型低延遲網際網路傳輸協議。<br><br>* `CMAF`：一種基於 HTTP 的高效自適應視頻串流協議。 |
|ISPList |字串陣列 |`["telecom"]` |用於標示網際網路服務提供者（ISP）識別碼的陣列。有效選項包括：<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107424#region) 陣列 |`-` |CDN 節點 IP 所屬區域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107424#region) 陣列 |`-` |用戶端 IP 所屬區域列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|DetailField |字串陣列 |`["Domain"]` |資料分維度拆分，維度及說明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網際網路服務提供者；<br><br>* `Protocol`：推拉流協議。 |
|PeakUpBandwidth |浮點數 |`20` |取得指定時間範圍內的上行峰值頻寬，單位為 Mbps。 |
|PeakDownBandwidth |浮點數 |`20` |取得指定時間範圍內的下行最大峰值頻寬，單位為 Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/107424#bandwidthdata) 陣列 |`-` |包含所有時間粒度頻寬資料的資料列表。 |
|BandwidthDetailDataList |[BandwidthDetailData](https://docs.byteplus.com/en/docs/24/107424#bandwidthdetaildata) 陣列 |`-` |按維度拆分的頻寬資料列表。 |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |區域資訊中的區域識別碼。 |
|Country |字串 |`CN` |區域資訊中的國家識別碼。 |
|Province |字串 |`beijing` |區域資訊中的省份識別碼。 |


<span id="bandwidthdata"></span>
### BandwidthData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |按時間粒度聚合資料時，每個時間粒度的起始時間，採 RFC3339 UTC 時間格式，精確到秒。 |
|UpBandwidth |浮點數 |`20` |當前資料聚合時間粒度內的上行峰值頻寬，單位為 Mbps。 |
|DownBandwidth |浮點數 |`20` |當前資料聚合時間粒度內的下行峰值頻寬，單位為 Mbps。 |


<span id="bandwidthdetaildata"></span>
### BandwidthDetailData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |按域名維度拆分資料時的域名資訊。 |
|Protocol |字串 |`HTTP-FLV` |按推拉流協議維度拆分資料時的協議資訊。 |
|ISP |字串 |`telecom` |按 ISP 維度拆分資料時的 ISP 資訊。 |
|PeakUpBandwidth |浮點數 |`20` |資料依維度切分後，目前維度的上行頻寬峰值，單位為 Mbps。 |
|PeakDownBandwidth |Float |`20` |資料依維度切分後，目前維度的下行頻寬峰值，單位為 Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/107424#bandwidthdata) 陣列 |`-` |資料切分後，目前維度下所有時間粒度的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveMetricBandwidthData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "App": "live",
    "Stream": "example_stream",
    "ProtocolList": [
        "HTTP-FLV",
        "RTMP"
    ],
    "ISPList": [
        "telecom"
    ],
    "RegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "UserRegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Domain"
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveMetricBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "App": "live",
        "Stream": "example_stream",
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "ISPList": [
            "telecom"
        ],
        "RegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "UserRegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "DetailField": [
            "Domain"
        ],
        "PeakUpBandwidth": 20,
        "PeakDownBandwidth": 20,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 20,
                "DownBandwidth": 20
            }
        ],
        "BandwidthDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "push.example.com",
                "ISP": "telecom",
                "PeakUpBandwidth": 20,
                "PeakDownBandwidth": 20,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00+08:00",
                        "UpBandwidth": null,
                        "DownBandwidth": null
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107424#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置與憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
