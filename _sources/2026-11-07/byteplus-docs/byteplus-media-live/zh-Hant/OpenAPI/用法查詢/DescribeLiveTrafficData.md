---
title: "DescribeLiveTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata-zh-TW"
---

呼叫 `DescribeLiveTrafficData` API，以查詢指定直播串流網域在指定時間範圍內的流量使用情況。此外，還包含推流網域的上行流量資料以及拉流網域的下行流量資料。

<span id="Requirements"></span>
## 需求


* 計費：有關價格資訊，請參閱 [直播服務費用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees)。

* 限制：

   * 支援查詢流量使用資料（包含已刪除的網域名稱）；

   * 流量使用資料用於計費對帳，其收集方式與流量資料監控不同。請使用 [DescribeLiveMetricTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivemetrictrafficdata) 查詢直播流量監控資料。

* 頻率限制：每個帳戶每秒最多 30 次查詢。

* 資料延遲：15 分鐘。

* 資料度量：流量資料以 1000 為基數計算，例如，1 GB = 1000 MB。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveTrafficData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTrafficData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["example.com"]` |網域名稱清單。預設為空，表示將查詢您 BytePlus MediaLive 下所有網域名稱的流量使用資料。您可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或前往 BytePlus MediaLive 控制台的 [網域管理](https://console.byteplus.com/live/main/domain/list)頁面，取得要查詢的網域名稱。 |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設包含所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸影片格式為 FLV。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸影片格式為 TS。<br><br>* `RTMP`：即時訊息協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：快速 UDP 網際網路連線協議，基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種基於 HTTP 的高效自適應影片串流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若查詢 <code>QUIC</code> 協議時，無法同時查詢其他協議。</div><br> |
|ISPList |Array of String |否 |`["telecom"]` |提供網路接入服務的運營商識別碼。預設表示所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數媒體。<br><br><br>若需取得各運營商識別碼，可呼叫 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107366#region) |否 |`-` |CDN 節點 IP 所屬區域清單，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可在同一次請求中同時使用。</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107366#region) |否 |`-` |用戶端 IP 所屬的區域列表，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可在同一個請求中同時使用。</div><br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，需使用 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需使用 RFC 3339 格式，精確到秒。 |
|Aggregation |Integer |否 |`300` |資料彙總的粒度（單位：秒），支援以下選項：<br><br><br>* `300`（預設）：5 分鐘。以 5 分鐘為彙總區間時，單次查詢的最大時間跨度為 31 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `3600`：1 小時。以 1 小時為彙總區間時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。<br><br>* `86400`：1 天。以 1 天為彙總區間時，單次查詢的最大時間跨度為 93 天，歷史查詢的最大時間範圍為 366 天。 |
|DetailField |Array of String |否 |`["Domain"]` |資料分割的維度預設不進行分割。支援的維度如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供者；<br><br>* `Protocol`：推拉流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只有在回應中，若 <code>DetailField</code> 參數用於指定資料分割維度，且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 中至少有一個參數傳入多個值時，才會依維度進行資料分割。</div><br> |


<span id="region"></span>
### Region


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Area |String |否 |`CN` |區域資訊中的主要區域識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。 |
|Country |String |否 |`CN` |區域資訊中的國家識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。以國家進行篩選時，需同時傳入 `Area` 與 `Country`。 |
|Province |String |否 |`beijing` |區域資訊中的省份識別碼，目前不支援中國大陸、香港、澳門、台灣以外的國家或地區。可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得識別碼資訊。以省份進行篩選時，需同時傳入 `Area`、`Country` 與 `Province` |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參閱下表。更多細節請參閱 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|DomainList |Array of String |`["example.com"]` |網域名稱列表。 |
|ProtocolList |Array of String |`["HTTP-FLV", "RTMP"]` |推拉流協議，協議說明如下：<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸 FLV 格式的視訊。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸 TS 格式的視訊。<br><br>* `RTMP`：即時訊息協議（Real Time Message Protocol）。<br><br>* `RTM`：即時媒體（Real Time Media），超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議（Secure Reliable Transport protocol）。<br><br>* `QUIC`：快速 UDP 網路連線（Quick UDP Internet Connections），基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種高效、可調適的 HTTP 視訊串流協議。 |
|ISPList |Array of String |`["telecom"]` |用於表示網際網路服務提供者（ISP）識別碼的陣列。有效選項包括：<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：廣播電視網絡（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107366#region)陣列 |`-` |CDN節點IP所屬的區域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107366#region)陣列 |`-` |客戶端IP所屬的區域列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採用RFC 3339格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用RFC 3339格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|DetailField |字串陣列 |`["Domain"]` |資料分割維度及其說明如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供者；<br><br>* `Protocol`：推拉流協議。 |
|TotalUpTraffic |浮點數 |`20` |查詢時間範圍內的總上行流量，單位為GB。 |
|TotalDownTraffic |浮點數 |`20` |查詢時間範圍內的總下行流量，單位為GB。 |
|TrafficDataList |[TrafficData](https://docs.byteplus.com/en/docs/24/107366#trafficdata)陣列 |`-` |每個資料粒度的所有資料。 |
|TrafficDetailDataList |[TrafficDetailData](https://docs.byteplus.com/en/docs/24/107366#trafficdetaildata)陣列 |`-` |依維度分割的資料。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當使用<code>DetailField</code>參數指定資料分割維度，且<code>DomainList</code>、<code>ProtocolList</code>或<code>ISPList</code>中至少有一個參數提供多個值時，回應中才會進行依維度分割資料。</div><br> |


<span id="region"></span>
### Region


|**Parameter** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |區域資訊中的區域識別碼。 |
|Country |字串 |`CN` |區域資訊中的國家識別碼。 |
|Province |字串 |`beijing` |區域資訊中的省份識別碼。 |


<span id="trafficdata"></span>
### TrafficData


|**Parameter** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |資料按時間粒度聚合時，每個時間粒度的起始時間，採用RFC3339 UTC時間格式，精確到秒。 |
|UpTraffic |浮點數 |`20` |當前資料聚合時間粒度內產生的總上行流量，單位為GB。 |
|DownTraffic |浮點數 |`20` |當前資料聚合時間粒度內產生的總下行流量，單位為GB。 |


<span id="trafficdetaildata"></span>
### TrafficDetailData


|**Parameter** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`example.com` |資料按網域維度分割時的網域資訊。 |
|Protocol |字串 |`HTTP-FLV` |資料按推拉流協議維度分割時的協議資訊。 |
|ISP |字串 |`telecom` |資料按運營商維度分割時的運營商資訊。 |
|TotalUpTraffic |浮點數 |`0` |資料分割後當前維度的總上行流量，單位為GB。 |
|TotalDownTraffic |浮點數 |`0` |資料分割後當前維度的總下行流量，單位為GB。 |
|TrafficDataList |[TrafficData](https://docs.byteplus.com/en/docs/24/107366#trafficdata)陣列 |`-` |資料分割後當前維度下所有時間粒度的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTrafficData&Version=2023-01-01
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
        "Action": "DescribeLiveTrafficData",
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
        "TotalUpTraffic": 20,
        "TotalDownTraffic": 20,
        "TrafficDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            },
            {
                "TimeStamp": "2022-04-13T00:05:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "TrafficDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "TotalUpTraffic": 20,
                "TotalDownTraffic": 20,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20
                    }
                ]
            },
            {
                "Protocol": "RTMP",
                "TotalUpTraffic": 0,
                "TotalDownTraffic": 0,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 0,
                        "DownTraffic": 0
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpTraffic": 0,
                        "DownTraffic": 0
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107366#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
