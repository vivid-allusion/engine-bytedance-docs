---
title: "DescribeLiveSourceTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata-zh-TW"
---

調用 `DescribeLiveSourceTrafficData` API，可查詢指定拉流域名或回源流在指定時間範圍內產生的回源流量與頻寬的監控數據。

<span id="Requirements"></span>
## 需求


* 限制：支援查詢指定拉流域名（包含已刪除域名）或指定回源流產生的流量用量數據。

* 頻率限制：每個帳號每秒最多查詢 30 次。

* 數據延遲：

   * 當聚合粒度為 60 秒時，數據延遲為 5 分鐘；

   * 其他時間粒度下，數據延遲為 15 分鐘。

* 數據計量：

   * 流量數據以 1000 為基數計算，例如 1 GB = 1000 MB。

   * 頻寬數據以 1000 為基數計算，例如 1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSourceTrafficData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSourceTrafficData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |String 陣列 |否 |`["pull.example.com", "pull2.example.com"]` |拉流域名列表。預設為空，表示查詢所有域名的回源流量及頻寬數據。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">應僅提供 <code>DomainList</code> 或 <code>Domain</code>，不可同時提供。</div><br> |
|Domain |String |否 |`pull.example.com` |查詢流粒度數據時需指定拉流域名，且必須同時提供 `App` 與 `Stream`。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) 介面或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的回源流監控數據時，需同時指定 <code>Domain</code>、<code>App</code> 與 <code>Stream</code> 以明確指定回源流。</div><br> |
|App |String |否 |`live` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的回源流監控數據時，需同時指定 <code>Domain</code>、<code>App</code> 與 <code>Stream</code> 以明確指定回源流。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 100 個字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的回源流監控數據時，需同時指定 <code>Domain</code>、<code>App</code> 與 <code>Stream</code> 以明確指定回源流。</div><br> |
|ISPList |字串陣列 |否 |`["telecom", "unicom"]` |提供網路接入服務的運營商識別碼。預設包含所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：中國廣播電視網絡；<br><br>* `huashu`：華數傳媒。<br><br><br>如需取得各運營商的識別碼，可呼叫[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107360#userregionlist) 陣列 |否 |`-` |用戶端 IP 所屬地區清單，預設表示所有地區。 |
|Aggregation |整數 |否 |`300` |資料彙總的粒度，單位為秒，支援以下選項：<br><br><br>* `60`：1 分鐘。<br><br>* `300`：（預設）5 分鐘。<br><br>* `3600`：1 小時。 |
|DetailField |字串陣列 |否 |`["Domain"]` |預設不提供資料分割的維度。支援的維度如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供者。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當使用<code>DetailField</code>參數指定資料分割維度，且<code>DomainList</code>或<code>ISPList</code>參數中至少有一個提供多個值時，回應中才會依維度分割資料。</div><br> |
|StartTime |字串 |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，需為 RFC 3339 格式，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">歷史查詢時間範圍為 366 天，單次查詢的最大時間跨度取決於 DetailField 與 Aggregation。關係說明如下。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">未進行維度分割或僅以一個維度分割資料時：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 60 秒彙總一次時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 300 秒彙總一次時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 3600 秒彙總一次時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">以兩個或以上維度分割資料時：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 60 秒彙總一次時，單次查詢的最大時間跨度為 3 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 300 秒彙總一次時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">資料每 3600 秒彙總一次時，單次查詢的最大時間跨度為 7 天。</div><br> |
|EndTime |字串 |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需為 RFC 3339 格式，精確到秒。 |


<span id="userregionlist"></span>
### UserRegionList


|**Parameter** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)取得區域資訊中的主要區域識別碼。 |
|Country |字串 |否 |`CN` |可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)取得區域資訊中的國家識別碼。按國家篩選時，需同時傳入`Area`與`Country`。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份識別碼，目前僅支援中國大陸、香港、澳門及台灣，其他國家或地區暫不支援。可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)取得識別碼資訊。當按省份篩選時，需要同時傳入`Area`、`Country`和`Province` |


<span id="Response parameters"></span>
## 回應參數

API 專屬的唯一回應參數請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com", "push2.example.com"]` |域名列表。 |
|Domain |字串 |`push.example.com` |查詢流級別流量資料時指定的域名。 |
|App |字串 |`live` |查詢流級別流量資料時指定的應用名稱。 |
|Stream |字串 |`example_stream` |查詢流級別流量資料時指定的串流名稱。 |
|ISPList |字串陣列 |`["telecom", "unicom"]` |提供網路接入服務的運營商標識。預設包含所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網絡；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信傳媒集團；<br><br>* `btvn`：廣播電視網絡（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107360#userregionlist) 陣列 |`-` |用戶端 IP 所屬地區列表。 |
|DetailField |字串陣列 |`["Domain"]` |資料分割維度及其說明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網際網路服務提供商。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，格式為 RFC 3339，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|TotalTraffic |浮點數 |`20` |指定查詢時間範圍內的回源總流量，單位為 GB。 |
|PeakBandwidth |浮點數 |`20` |指定時間範圍內的回源峰值頻寬，單位為 Mbps。 |
|TrafficDataList |[TrafficDataList](https://docs.byteplus.com/en/docs/24/107360#trafficdatalist) 陣列 |`-` |包含所有時間粒度的流量及頻寬資料列表。 |
|TrafficDetailDataList |[TrafficDetailDataList](https://docs.byteplus.com/en/docs/24/107360#trafficdetaildatalist) 陣列 |`-` |按維度分割後的流量及頻寬資料列表。 |


<span id="userregionlist"></span>
### UserRegionList


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |區域資訊中的區域標識。 |
|Country |字串 |`CN` |區域資訊中的國家標識。 |
|Province |字串 |`beijing` |區域資訊中的省份標識。 |


<span id="trafficdatalist"></span>
### TrafficDataList


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |按時間粒度聚合資料時，每個時間粒度的開始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|Traffic |浮點數 |`20` |當前資料聚合時間粒度內產生的回源流量，單位為 GB。 |
|Bandwidth |浮點數 |`20` |當前資料聚合時間粒度內的回源峰值頻寬，單位為 Mbps。 |


<span id="trafficdetaildatalist"></span>
### TrafficDetailDataList


|**參數** |**資料類型** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |按域名維度分割資料時的域名資訊。 |
|ISP |字串 |`telecom` |按運營商維度分割資料時的運營商資訊。 |
|TotalTraffic |浮點數 |`20` |資料分割後當前維度的回源總流量，單位為 GB。 |
|PeakBandwidth |浮點數 |`20` |資料分割後當前維度的回源峰值頻寬，單位為 Mbps。 |
|TrafficDataList |[TrafficDataList](https://docs.byteplus.com/en/docs/24/107360#trafficdatalist) 陣列 |`-` |資料分割後當前維度下所有時間粒度的流量資料列表。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceTrafficData&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ISPList": [
        "telecom",
        "unicom"
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
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveSourceTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "push.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ISPList": [
            "telecom",
            "unicom"
        ],
        "UserRegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "DetailField": [
            "Domain"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "TotalTraffic": 20,
        "TrafficDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Traffic": 20,
                "Bandwidth": 20
            }
        ],
        "TrafficDetailDataList": [
            {
                "Domain": "push.example.com",
                "ISP": "telecom",
                "TotalTraffic": 20,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Traffic": 20,
                        "Bandwidth": 10
                    }
                ],
                "PeakBandwidth": 20
            }
        ],
        "PeakBandwidth": 20
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107360#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、組態和憑證）。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡技術支援](https://console.byteplus.com/workorder/create)。 |
