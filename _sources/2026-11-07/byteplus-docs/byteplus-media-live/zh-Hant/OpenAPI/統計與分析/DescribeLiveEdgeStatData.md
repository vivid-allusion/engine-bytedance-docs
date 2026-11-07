---
title: "DescribeLiveEdgeStatData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023-zh-TW"
---

調用 `DescribeLiveEdgeStatData` 介面以查詢指定協議、ISP、區域及時間範圍下，直播流所產生的上下行流量、上下行峰值頻寬，以及請求數等資料。

<span id="Usage scenario"></span>
## 使用場景


* 限制：

   * 頻寬資料用於數據監控，其收集方式與頻寬使用資料不同。請使用 [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) 查詢直播頻寬使用資料。

   * 流量資料用於數據監控，其收集方式與流量使用資料不同。請使用 [DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata) API 查詢直播流量使用資料。

* 頻率限制：每個帳戶每秒最多 30 次查詢。

* 資料延遲：

   * 當彙總粒度為 60 秒時，資料延遲為 5 分鐘；

   * 其他時間粒度下，資料延遲為 15 分鐘。

* 資料計量：

   * 頻寬資料以 1000 為基數計算，例如 1 Mbps = 1000 Kbps。

   * 流量資料以 1000 為基數計算，例如 1 GB = 1000 MB。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveEdgeStatData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了特定參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveEdgeStatData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com","pull.example.com"]` |域名列表。預設為空，表示會查詢您 BytePlus MediaLive 下的所有域名。您可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得需查詢的域名。 |
|AppList |Array of String |否 |`["live","vodlive"]` |AppName 列表，為直播流 URL 中的欄位。預設為空，表示會查詢所有 AppName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 30 字元。 |
|StreamList |Array of String |否 |`["stream001","stream002"]` |StreamName 列表，為直播流 URL 中的欄位。預設為空，表示會查詢所有 StreamName。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及點（.），長度為 1 至 100 字元。 |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設包含所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協議，傳輸視頻格式為 FLV。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協議，傳輸視頻格式為 TS。<br><br>* `RTMP`：即時訊息傳輸協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：Quick UDP Internet Connections，一種基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種用於 HTTP 高效且自適應的視頻串流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若查詢 <code>QUIC</code> 協議時，無法同時查詢其他協議。</div><br> |
|ISPList |字串陣列 |否 |`["unicom", "telecom"]` |提供網路接入服務的運營商識別碼。預設情況下，表示所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。<br><br>   如需獲取各運營商的識別碼，可呼叫 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107393#region) 陣列 |否 |`-` |CDN 節點 IP 所屬區域列表，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可在同一請求中同時使用。</div><br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107393#region) 陣列 |否 |`-` |用戶端 IP 所屬區域列表，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可在同一請求中同時使用。</div><br> |
|DetailField |字串陣列 |否 |`["Domain"]` |資料分割維度預設不分割。支援的維度如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網路服務提供商；<br><br>* `Protocol`：推拉流協議。<br><br>* `Area`：CDN 節點 IP 所屬區域。<br><br>* `Country`：用戶端 IP 所屬國家。<br><br>* `UserArea`：用戶端 IP 所屬區域。<br><br>* `UserCountry`：用戶端 IP 所屬國家。 |
|Aggregation |整數 |否 | |資料彙總粒度（以秒為單位），支援以下選項：<br><br><br>* `60`：1 分鐘。<br><br>* `300`：（預設）5 分鐘。<br><br>* `3600`：1 小時。 |
|StartTime |字串 |是 |`2024-12-12T00:00:00Z` |查詢範圍的起始時間，採 RFC 3339 格式，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">歷史查詢時間範圍為 366 天，單次查詢的最大時間跨度取決於 DetailField 與 Aggregation。相關關係說明如下。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當未進行維度分割或僅以一個維度分割資料時：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 60 秒彙總時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 300 秒彙總時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 3600 秒彙總時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當以兩個或以上維度分割資料時：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 60 秒彙總時，單次查詢的最大時間跨度為 3 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 300 秒彙總時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 3600 秒彙總時，單次查詢的最大時間跨度為 7 天。</div><br> |
|EndTime |字串 |是 |`2024-12-12T00:00:00Z` |查詢範圍的結束時間，採 RFC 3339 格式，精確到秒。 |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |區域資訊中的主要區域識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 獲取。 |
|Country |字串 |否 |`CN` |區域資訊中的國家識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 獲取。在以國家為篩選條件時，需同時傳入`Area`與`Country`。 |
|省份 |字串 |否 |`beijing` |區域資訊中的省份識別碼目前不支援中國大陸、香港、澳門、台灣以外的國家或地區。可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)取得識別碼資訊。在以省份為篩選條件時，需同時傳入`Area`、`Country`及`Province`。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 特定回應參數，請參考下表。更多詳情請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com","pull.example.com"]` |域名列表。 |
|AppList |字串陣列 |`["live","livevod"]` |AppName列表。 |
|StreamList |字串陣列 |`["stream001","stream002"]` |StreamName列表。 |
|ProtocolList |字串陣列 |`["HTTP-FLV", "RTMP"]` |推拉流協議。可用協議說明如下：<br><br><br>* `HTTP-FLV`：基於HTTP的推拉流協議，傳輸視頻格式為FLV。<br><br>* `HTTP-HLS`：基於HTTP的推拉流協議，傳輸視頻格式為TS。<br><br>* `RTMP`：即時消息協議。<br><br>* `RTM`：即時媒體，超低延遲直播協議。<br><br>* `SRT`：安全可靠傳輸協議。<br><br>* `QUIC`：Quick UDP Internet Connections，基於UDP的新型低延遲網路傳輸協議。<br><br>* `CMAF`：一種基於HTTP的高效自適應視頻串流協議。 |
|ISPList |字串陣列 |`["unicom",telecom"]` |用於標示網際網路服務提供商（ISP）識別碼的陣列。有效選項包括：<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|RegionList |[ResponseRegion](https://docs.byteplus.com/en/docs/24/107393#responseregion)陣列 |`-` |CDN節點IP所屬區域列表。 |
|UserRegionList |[ResponseRegion](https://docs.byteplus.com/en/docs/24/107393#responseregion)陣列 |`-` |用戶端IP所屬區域列表。 |
|DetailField |字串陣列 |`[Domain]` |資料分割維度及其說明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網際網路服務提供商；<br><br>* `Protocol`：推拉流協議。<br><br>* `Area`：CDN節點IP所屬區域。<br><br>* `Country`：用戶端IP所屬國家。<br><br>* `UserArea`：用戶端IP所屬區域。<br><br>* `UserCountry`：用戶端IP所屬國家。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|StartTime |字串 |`2024-12-12T00:00:00Z` |查詢範圍的起始時間，採RFC 3339格式，精確到秒。 |
|EndTime |字串 |`2024-12-12T01:00:00Z` |查詢範圍的結束時間，採RFC 3339格式，精確到秒。 |
|PeakUpBandwidth |浮點數 |`10` |查詢時間範圍內的上行峰值頻寬，單位為Mbps。 |
|PeakDownBandwidth |浮點數 |`10` |查詢時間範圍內的下行峰值頻寬，單位為Mbps。 |
|TotalUpTraffic |浮點數 |`20` |查詢時間範圍內的上行總流量，單位為GB（Gigabyte）。 |
|TotalDownTraffic |浮點數 |`20` |查詢時間範圍內的下行總流量，單位為GB（Gigabyte）。 |
|TotalRequest |浮點數 |`5` |請求數量。 |
|EdgeStatDataList |[EdgeStatDataList](https://docs.byteplus.com/en/docs/24/107393#edgestatdatalist)陣列 |`-` |所有時間粒度的資料。 |
|EdgeStatDetailDataList |[EdgeStatDetailDataList](https://docs.byteplus.com/en/docs/24/107393#edgestatdetaildatalist)陣列 |`-` |依維度分割的資料。 |


<span id="responseregion"></span>
### ResponseRegion


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |區域資訊中的區域識別碼。 |
|Country |字串 |`CN` |區域資訊中的國家識別碼。 |
|Province |字串 |`beijing` |區域資訊中的省份識別碼。 |


<span id="edgestatdatalist"></span>
### EdgeStatDataList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |當資料依時間粒度彙總時，每個時間粒度的開始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|UpTraffic |Float |`20` |當前資料彙總時間粒度內產生的上行總流量，單位為 GB（Gigabyte）。 |
|DownTraffic |Float |`20` |當前資料彙總時間粒度內產生的下行總流量，單位為 GB（Gigabyte）。 |
|UpBandwidth |Float |`10` |當前資料彙總時間粒度內的上行帶寬峰值，單位為 Mbps。 |
|DownBandwidth |Float |`10` |當前資料彙總時間粒度內的下行帶寬峰值，單位為 Mbps。 |
|Request |Float |`5` |當前資料彙總時間粒度內的請求數。 |


<span id="edgestatdetaildatalist"></span>
### EdgeStatDetailDataList


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Domain |String |`push.example.com` |當資料按網域維度分割時的網域資訊。 |
|Protocol |String |`HTTP-FLV` |當資料按推拉流協議維度分割時的協議資訊。 |
|ISP |String |`telecom` |當資料按運營商維度分割時的運營商資訊。 |
|Area |String |`CN` |當資料按 CDN 節點 IP 所在區域分割時的區域資訊。 |
|Country |String |`CN` |當資料按 CDN 節點 IP 所在國家分割時的國家資訊。 |
|UserArea |String |`CN` |當資料按用戶端 IP 所在區域分割時的區域資訊。 |
|UserCountry |String |`CN` |當資料按用戶端 IP 所在國家分割時的國家資訊。 |
|PeakUpBandwidth |Float |`10` |資料分割後當前維度的上行帶寬峰值，單位為 Mbps。 |
|PeakDownBandwidth |Float |`10` |資料分割後當前維度的下行帶寬峰值，單位為 Mbps。 |
|TotalUpTraffic |Float |`20` |資料分割後當前維度的上行總流量，單位為 GB。 |
|TotalDownTraffic |Float |`20` |資料分割後當前維度的下行總流量，單位為 GB。 |
|TotalRequest |Float |`5` |資料分割後當前維度的請求數。 |
|EdgeStatDataList |[EdgeStatDataList](https://docs.byteplus.com/en/docs/24/107393#edgestatdatalist) 陣列 |`-` |資料分割後當前維度下所有時間粒度的資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveEdgeStatData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "pull.example.com"
    ],
    "ProtocolList": [
        "HTTP-FLV",
        "RTMP"
    ],
    "ISPList": [
        "unicom",
        "telecom"
    ],
    "RegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2024-12-12T00:00:00Z",
    "EndTime": "2024-12-12T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Domain"
    ],
    "AppList": [
        "live",
        "vodlive"
    ],
    "StreamList": [
        "stream001",
        "stream002"
    ]
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveEdgeStatData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "pull.example.com"
        ],
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "RegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "StartTime": "2024-12-12T00:00:00Z",
        "EndTime": "2024-12-12T01:00:00Z",
        "Aggregation": 300,
        "TotalUpTraffic": 20,
        "TotalDownTraffic": 20,
        "AppList": [
            "live",
            "livevod"
        ],
        "StreamList": [
            "stream001",
            "stream002"
        ],
        "PeakUpBandwidth": 10,
        "PeakDownBandwidth": 10,
        "TotalRequest": 5,
        "EdgeStatDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20,
                "UpBandwidth": 10,
                "DownBandwidth": 10,
                "Request": 5
            }
        ],
        "EdgeStatDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "push.example.com",
                "ISP": "telecom",
                "TotalUpTraffic": 20,
                "TotalDownTraffic": 20,
                "PeakUpBandwidth": 10,
                "PeakDownBandwidth": 10,
                "TotalRequest": 5,
                "EdgeStatDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20,
                        "UpBandwidth": 10,
                        "DownBandwidth": 10,
                        "Request": 5
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參考 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**Description** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請[聯繫支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[請求參數](https://docs.byteplus.com/en/docs/24/107393#request-parameters)說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證未通過。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |請求被拒絕，因當前帳號下無請求資源（資源包括網域空間、網域、App 名稱、配置及憑證）。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域空間、網域、App 名稱、配置及憑證）。建議重試。若仍返回錯誤碼，請[聯繫支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯繫管理員。 |發生內部錯誤。請[聯繫支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯繫管理員。 |內部服務逾時。請[聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
