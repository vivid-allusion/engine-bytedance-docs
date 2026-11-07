---
title: "DescribeLiveBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata-zh-TW"
---

調用 `DescribeLiveBandwidthData` API，以查詢指定直播域名在指定時間範圍內的頻寬使用情況，包括推流域名的上行峰值頻寬及拉流域名的下行峰值頻寬。

<span id="Requirements"></span>
## 需求


* 計費：關於頻寬價格，請參閱 [Live-streaming service fees](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees)。

* 限制：

   * 支援查詢已刪除域名產生的頻寬使用數據。

   * 頻寬使用數據用於計費與對帳，與頻寬數據監控的收集方式不同。請使用 [DescribeLiveMetricBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata) 查詢直播頻寬監控數據。

* 頻率限制：每個帳戶每秒最多查詢 30 次

* 數據延遲：15 分鐘

* 數據指標：頻寬數據以 1000 為基數計算，例如 1 Mbps = 1000 Kbps。

* 統計規則：頻寬使用數據每 5 分鐘計算一次。根據查詢時間及粒度設定，返回時間範圍內的最大值及粒度內的最大值。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBandwidthData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。預設為空，表示查詢您 BytePlus MediaLive 下所有域名的頻寬使用數據。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取待查詢的域名。 |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設包含所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸視頻格式為 FLV。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸視頻格式為 TS。<br><br>* `RTMP`：即時消息協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：Quick UDP Internet Connections，基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種高效、適應性強的 HTTP 視頻串流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若查詢 <code>QUIC</code> 協議時，不能同時查詢其他協議。</div><br> |
|ISPList |Array of String |否 |`["telecom", "unicom"]` |提供網路接入服務的運營商標識。預設表示所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。<br><br><br>如需獲取各運營商標識，可調用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107454#region) |否 |`-` |CDN節點IP所屬的區域列表，預設表示全部區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code>不可在同一請求中同時使用。</div><br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107454#region) 陣列 |否 |`-` |用戶端IP所屬的區域列表，預設表示全部區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code>不可在單一請求中同時使用。</div><br> |
|StartTime |字串 |是 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採RFC 3339格式，精確到秒。 |
|EndTime |字串 |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採RFC 3339格式，精確到秒。 |
|Aggregation |整數 |否 |`300` |資料彙總的粒度（單位：秒），支援以下選項：<br><br><br>* `300`（預設）：5分鐘。以5分鐘為彙總粒度時，單次查詢最大時間跨度為31天，歷史查詢最大時間範圍為366天。<br><br>* `3600`：1小時。以1小時為彙總粒度時，單次查詢最大時間跨度為93天，歷史查詢最大時間範圍為366天。<br><br>* `86400`：1天。以1天為彙總粒度時，單次查詢最大時間跨度為93天，歷史查詢最大時間範圍為366天。 |
|DetailField |字串陣列 |否 |`["Domain"]` |資料分割維度預設不分割。支援的分割維度如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供者；<br><br>* `Protocol`：推拉流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只有在回應中使用 <code>DetailField</code> 參數指定資料分割維度，且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 其中至少一個參數傳入多個值時，才會根據維度進行資料分割。</div><br> |


<span id="region"></span>
### Region


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |區域資訊中的主要區域識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。 |
|Country |字串 |否 |`CN` |區域資訊中的國家識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。以國家為篩選條件時，需同時傳入 'Area' 與 'Country'。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份識別碼，目前不支援中國大陸、香港、澳門、台灣以外的國家或地區。可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得識別碼資訊。以省份為篩選條件時，需同時傳入 `Area`、`Country` 與 `Province` |


<span id="Response parameters"></span>
## 回應參數

如需專屬 API 回應參數，請參見下表。更多細節請參閱 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com"]` |網域名稱列表。 |
|ProtocolList |字串陣列 |`["HTTP-FLV", "RTMP"]` |推拉流協議，協議說明如下：<br><br><br>* `HTTP-FLV`：基於HTTP的推拉流協議，傳輸FLV格式的視訊。<br><br>* `HTTP-HLS`：基於HTTP的推拉流協議，傳輸TS格式的視訊。<br><br>* `RTMP`：即時訊息協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：基於UDP的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種基於HTTP的高效、適應性視訊串流協議。 |
|ISPList |字串陣列 |`["telecom"]` |用於表示網際網路服務提供者（ISP）識別碼的陣列。有效選項包括：<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107454#region) 陣列 |`-` |CDN 節點 IP 所屬地區的列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107454#region) 陣列 |`-` |用戶端 IP 所屬地區的列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|DetailField |字串陣列 |`["Domain"]` |資料分維度展示，維度及說明如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供者；<br><br>* `Protocol`：推拉流協議。 |
|PeakUpBandwidth |浮點數 |`20` |獲取指定時間範圍內的上行頻寬峰值，單位為 Mbps。 |
|PeakDownBandwidth |浮點數 |`20` |獲取指定時間範圍內的下行頻寬最大峰值，單位為 Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/107454#bandwidthdata) 陣列 |`-` |每個時間粒度的所有資料。 |
|BandwidthDetailDataList |[BandwidthDetailData](https://docs.byteplus.com/en/docs/24/107454#bandwidthdetaildata) 陣列 |`-` |按維度分割的資料。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只有在 <code>DetailField</code> 參數指定資料分維度展示，且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 這三個參數中至少有一個傳入多個值時，回應中才會出現按維度分割的資料。</div><br> |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |地區資訊中的地區標識。 |
|Country |字串 |`CN` |地區資訊中的國家標識。 |
|Province |字串 |`beijing` |地區資訊中的省份標識。 |


<span id="bandwidthdata"></span>
### BandwidthData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |當資料按時間粒度聚合時，每個時間粒度的起始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|UpBandwidth |浮點數 |`20` |當前資料聚合時間粒度內的上行頻寬峰值，單位為 Mbps。 |
|DownBandwidth |浮點數 |`20` |當前資料聚合時間粒度內的下行頻寬峰值，單位為 Mbps。 |


<span id="bandwidthdetaildata"></span>
### BandwidthDetailData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |當資料按網域名稱維度分割時的網域資訊。 |
|Protocol |字串 |`RTMP` |當資料按推拉流協議維度分割時的協議資訊。 |
|ISP |字串 |`telecom` |當資料按運營商維度分割時的運營商資訊。 |
|PeakUpBandwidth |浮點數 |`20` |資料分維度後，當前維度的上行頻寬峰值，單位為 Mbps。 |
|PeakDownBandwidth |浮點數 |`20` |資料分維度後，當前維度的下行頻寬峰值，單位為 Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/107454#bandwidthdata) 陣列 |`-` |資料分維度後，當前維度下所有時間粒度的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBandwidthData&Version=2023-01-01
{
    "DomainList": [
        "example.com"
    ],
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
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Protocol"
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "example.com"
        ],
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
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "PeakUpBandwidth": 20,
        "PeakDownBandwidth": 20,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 20,
                "DownBandwidth": 20
            },
            {
                "TimeStamp": "2022-04-13T00:05:00Z",
                "UpBandwidth": 20,
                "DownBandwidth": 20
            }
        ],
        "BandwidthDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "PeakUpBandwidth": 20,
                "PeakDownBandwidth": 20,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 20,
                        "DownBandwidth": 20
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpBandwidth": 20,
                        "DownBandwidth": 20
                    }
                ]
            },
            {
                "Protocol": "RTMP",
                "PeakUpBandwidth": 0,
                "PeakDownBandwidth": 0,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 0,
                        "DownBandwidth": 0
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpBandwidth": 0,
                        "DownBandwidth": 0
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


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數不合法或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107454#request-parameters) 說明進行檢查。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置和憑證）。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
