---
title: "DescribeLiveMetricTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivemetrictrafficdata-zh-TW"
---

調用 `DescribeLiveMetricTrafficData` API，以查詢指定時間範圍內直播域名或直播流的流量監控數據。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 2025 年 2 月 18 日起，我們將不再維護此舊版 API。其文件將於 2025 年 5 月 18 日下架。建議您轉向新版 UpdateUser 介面。詳情請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023">DescribeLiveEdgeStatData</a> 文件。</div>


<span id="Requirements"></span>
## 需求


* 限制：

   * 支持查詢指定直播域名（包含已刪除域名）或直播流產生的流量監控數據。

   * 流量監控數據用於數據監控，其收集方式與流量使用數據不同。請使用 [DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata) API 查詢直播流量使用數據。

* 頻率限制：每個帳戶每秒最多 100 次查詢

* 數據延遲：

   * 當聚合粒度為 60 秒時，數據延遲為 5 分鐘；

   * 其他時間粒度下，數據延遲為 15 分鐘。

* 數據度量：流量數據以 1000 為基數計算，例如，1 GB = 1000 MB。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveMetricTrafficData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)，並包含 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveMetricTrafficData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。預設為空，表示將查詢您 BytePlus MediaLive 下所有域名的流量數據。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或進入 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，獲取需查詢的域名。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度數據時，App 與 Stream 參數皆為必填。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 100 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度數據時，<code>App</code> 與 <code>Stream</code> 參數皆為必填。</div><br> |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設包含所有協議類型。支持的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸視頻格式為 FLV。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸視頻格式為 TS。<br><br>* `RTMP`：即時消息協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：Quick UDP Internet Connections，一種基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種用於高效、自適應 HTTP 視訊串流的協定。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢 <code>QUIC</code> 協定時，無法同時查詢其他協定。</div><br> |
|ISPList |字串陣列 |否 |`["telecom"]` |提供網路接入服務的業者識別碼。預設情況下，表示所有業者。支援的業者如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。<br><br><br>如需取得各業者的識別碼，可呼叫 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107418#region) 陣列 |否 |`-` |CDN 節點 IP 所屬地區列表，預設表示所有地區。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不能在同一請求中同時使用。</div><br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107418#region) 陣列 |否 |`-` |用戶端 IP 所屬地區列表，預設表示所有地區。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不能在同一請求中同時使用。</div><br> |
|StartTime |字串 |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，格式為 RFC 3339，精確到秒。 |
|EndTime |字串 |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精確到秒。 |
|Aggregation |整數 |否 |`300` |資料彙總的粒度，單位為秒，支援以下選項：<br><br><br>* `60`：1 分鐘。每 1 分鐘彙總一次時，單次查詢的最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天；<br><br>* `300`：（預設）5 分鐘。每 5 分鐘彙總一次時，單次查詢的最大時間跨度為 31 天，歷史查詢時間範圍為 366 天；<br><br>* `3600`：1 小時。每 1 小時彙總一次時，單次查詢的最大時間跨度為 93 天，歷史查詢時間範圍為 366 天。 |
|DetailField |字串陣列 |否 |`["Domain"]` |資料分割維度預設不分割。支援的分割維度如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供者；<br><br>* `Protocol`：推拉流協定。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">只有在 <code>DetailField</code> 參數用於指定資料分割維度，且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 其中至少一個參數提供多個值時，回應中才會根據維度進行資料分割。</div><br> |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得區域資訊中的主要區域識別碼。 |
|Country |字串 |否 |`CN` |可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得區域資訊中的國家識別碼。依國家篩選時，需同時傳入 `Area` 與 `Country`。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份識別碼，目前不支援中國大陸、香港、澳門、台灣以外的國家或地區。可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得識別碼資訊。依省份篩選時，需同時傳入 `Area`、`Country` 與 `Province` |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參見 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com"]` |網域名稱列表。 |
|App |字串 |`live` |查詢流級別流量數據時指定的 AppName 欄位。 |
|Stream |字串 |`example_stream` |查詢流級別流量數據時指定的 StreamName 欄位。 |
|ProtocolList |字串陣列 |`["HTTP-FLV", "RTMP"]` |推拉流協議。可用協議說明如下：<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸 FLV 格式的視頻。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸 TS 格式的視頻。<br><br>* `RTMP`：即時消息傳輸協議（Real Time Message Protocol）。<br><br>* `RTM`：即時媒體（Real Time Media），超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議（Secure Reliable Transport protocol）。<br><br>* `QUIC`：快速 UDP 網際連線協議（Quick UDP Internet Connections），一種基於 UDP 的新型低延遲網際網路傳輸協議。<br><br>* `CMAF`：一種高效自適應的 HTTP 視頻串流協議。 |
|ISPList |字串陣列 |`["telecom"]` |表示網際網路服務提供商（ISP）標識的陣列。有效選項包括：<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107418#region) 陣列 |`-` |CDN 節點 IP 所屬地區列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107418#region) 陣列 |`-` |用戶端 IP 所屬地區列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |`300` |數據粒度，單位為秒。 |
|DetailField |字串陣列 |`[Domain]` |數據分割維度及其說明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網際網路服務提供商；<br><br>* `Protocol`：推拉流協議。 |
|TotalUpTraffic |浮點數 |`20` |查詢時間範圍內的上行總流量，單位為 GB。 |
|TotalDownTraffic |浮點數 |`20` |查詢時間範圍內的下行總流量，單位為 GB。 |
|TrafficDataList |[TrafficData](https://docs.byteplus.com/en/docs/24/107418#trafficdata) 陣列 |`-` |所有時間粒度的流量數據。 |
|TrafficDetailDataList |[TrafficDetailData](https://docs.byteplus.com/en/docs/24/107418#trafficdetaildata) 陣列 |`-` |按維度分割的數據。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當使用 <code>DetailField</code> 參數指定數據分割維度，且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 這三個參數中至少有一個傳入多個值時，回應中才會出現按維度分割的數據。</div><br> |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |地區資訊中的地區標識。 |
|Country |字串 |`CN` |地區資訊中的國家標識。 |
|Province |字串 |`beijing` |地區資訊中的省份標識。 |


<span id="trafficdata"></span>
### TrafficData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |按時間粒度聚合數據時，每個時間粒度的開始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|UpTraffic |浮點數 |`20` |當前數據聚合時間粒度內產生的上行總流量，單位為 GB。 |
|DownTraffic |浮點數 |`20` |當前數據聚合時間粒度內產生的下行總流量，單位為 GB。 |


<span id="trafficdetaildata"></span>
### TrafficDetailData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |按域名維度分割數據時的域名資訊。 |
|Protocol |字串 |`HTTP-FLV` |按推拉流協議維度分割數據時的協議資訊。 |
|ISP |字串 |`telecom` |當資料依據業者維度分割時的業者資訊。 |
|TotalUpTraffic |Float |`20` |資料分割後當前維度的總上行流量，單位為 GB。 |
|TotalDownTraffic |Float |`20` |資料分割後當前維度的總下行流量，單位為 GB。 |
|TrafficDataList |[TrafficData](https://docs.byteplus.com/en/docs/24/107418#trafficdata) 陣列 |`-` |資料分割後當前維度下所有時間粒度的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveMetricTrafficData&Version=2023-01-01
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
        "Action": "DescribeLiveMetricTrafficData",
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
            ""
        ],
        "TotalUpTraffic": 20,
        "TotalDownTraffic": 20,
        "TrafficDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "TrafficDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "push.example.com",
                "ISP": "telecom",
                "TotalUpTraffic": 20,
                "TotalDownTraffic": 20,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00+08:00",
                        "UpTraffic": null,
                        "DownTraffic": null
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**描述** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107418#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create)。 |
