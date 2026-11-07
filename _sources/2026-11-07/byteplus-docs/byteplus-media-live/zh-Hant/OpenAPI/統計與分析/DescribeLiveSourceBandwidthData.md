---
title: "DescribeLiveSourceBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcebandwidthdata-zh-TW"
---

調用 `DescribeLiveSourceBandwidthData` API 以查詢指定拉流域名或源流在指定時間範圍內產生的源站頻寬監控數據。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自 2025 年 2 月 18 日起，我們將不再維護此舊版 API。其文檔將於 2025 年 5 月 18 日下線。我們建議遷移至新版 UpdateUser 介面。詳情請參見 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata">DescribeLiveSourceTrafficData</a> 文檔。</div>


<span id="Requirements"></span>
## 需求


* 限制：支持查詢指定拉流域名（包括已刪除域名）或指定源流產生的頻寬使用數據。

* 頻率限制：每個帳號每秒最多 30 次查詢

* 數據延遲：

   * 當聚合粒度為 60 秒時，數據延遲為 5 分鐘；

   * 其他時間粒度下，數據延遲為 15 分鐘。

* 數據度量：頻寬數據以 1000 為基數計算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSourceBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用時，除需傳入 API 專屬參數外，還需傳入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSourceBandwidthData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本號。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["pull.example.com", "pull2.example.com"]` |拉流域名列表。預設為空，表示查詢所有域名的源站頻寬使用數據。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>DomainList</code> 和 <code>Domain</code> 僅需擇一傳入，不可同時傳入。</div><br> |
|Domain |String |否 |`pull.example.com` |查詢流粒度數據時需傳入拉流域名，且需同時傳入 `App` 和 `Stream`。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) 介面或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取需查詢的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的源站頻寬監控數據時，需同時指定 <code>Domain</code>、<code>App</code> 和 <code>Stream</code> 以明確源流。</div><br> |
|App |String |否 |`live` |源流的 AppName 欄位支持字母（A\-Z, a\-z）、數字（0\-9）、下劃線（_）、連字符（\-）及點（.），長度為 1~30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的源流頻寬監控數據時，需同時指定 <code>Domain</code>、<code>App</code> 和 <code>Stream</code> 以明確源流。</div><br> |
|Stream |String |否 |`example_stream` |源流的 StreamName 欄位支持字母（A\-Z, a\-z）、數字（0\-9）、下劃線（_）、連字符（\-）及點（.），長度為 1~100 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢源流在流粒度下的帶寬監控數據時，需同時指定<code>Domain</code>、<code>App</code>及<code>Stream</code>以明確源流。</div><br> |
|ISPList |字串陣列 |否 |`["telecom"]` |提供網路接入服務的運營商識別碼。預設情況下，表示所有運營商。支持的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒；<br><br><br>如需獲取各運營商的識別碼，可調用[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107389#userregionlist)陣列 |否 |`-` |用戶端 IP 所屬區域列表，預設表示所有區域。 |
|StartTime |字串 |是 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，需採用 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，需採用 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |否 |`300` |數據聚合粒度（以秒為單位），支持以下選項：<br><br><br>* `60`：1 分鐘。每 1 分鐘聚合時，單次查詢的最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天；<br><br>* `300`：（預設）5 分鐘。每 5 分鐘聚合時，單次查詢的最大時間跨度為 31 天，歷史查詢時間範圍為 366 天；<br><br>* `3600`：1 小時。每 1 小時聚合時，單次查詢的最大時間跨度為 93 天，歷史查詢時間範圍為 366 天。 |
|DetailField |字串陣列 |否 |`["Domain"]` |預設情況下，數據不按維度分割。支持的維度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網際網路服務提供商。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當使用<code>DetailField</code>參數指定數據分割維度，且<code>DomainList</code>或<code>ISPList</code>中至少有一個參數傳入多個值時，回應中才會按維度分割數據。</div><br> |


<span id="userregionlist"></span>
### UserRegionList


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |區域資訊中的主要區域識別碼可透過調用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)獲取。 |
|Country |字串 |否 |`CN` |區域資訊中的國家識別碼可透過調用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)獲取。按國家過濾時，需同時傳入`Area`及`Country`。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份識別碼，目前不支持中國大陸、香港、澳門、台灣以外的國家或地區。可透過調用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)獲取識別碼資訊。按省份過濾時，需同時傳入`Area`、`Country`及`Province` |


<span id="Response parameters"></span>
## 響應參數

有關唯一的 API 專屬響應參數，請參見下表。更多詳情請參見 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["pull.example.com", "pull2.example.com"]` |域名列表。 |
|Domain |字串 |`pull.example.com` |查詢流粒度流量數據時指定的域名。 |
|App |字串 |`live` |查詢流粒度流量數據時指定的應用名稱。 |
|Stream |字串 |`example_stream` |在以串流粒度查詢流量數據時所指定的串流名稱。 |
|ISPList |字串陣列 |`["telecom"]` |用於標示網際網路服務提供商（ISP）識別碼的陣列。有效選項包括：<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107389#userregionlist) 陣列 |`-` |用於標示用戶端 IP 所屬區域的列表。 |
|DetailField |字串陣列 |`["Domain"]` |數據分割維度及其說明如下：<br><br><br>* `Domain`：網域名稱；<br><br>* `ISP`：網際網路服務提供商。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的起始時間，採 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |`300` |數據粒度，單位為秒。 |
|PeakBandwidth |浮點數 |`20` |指定時間範圍內的源站峰值頻寬，單位為 Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107389#bandwidthdatalist) 陣列 |`-` |包含所有時間粒度頻寬數據的列表。 |
|BandwidthDetailDataList |[BandwidthDetailDataList](https://docs.byteplus.com/en/docs/24/107389#bandwidthdetaildatalist) 陣列 |`-` |按維度分割後的頻寬數據列表。 |


<span id="userregionlist"></span>
### UserRegionList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |區域資訊中的區域識別碼。 |
|Country |字串 |`CN` |區域資訊中的國家識別碼。 |
|Province |字串 |`beijing` |區域資訊中的省份識別碼。 |


<span id="bandwidthdatalist"></span>
### BandwidthDataList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |以時間粒度聚合數據時，每個時間粒度的起始時間，採 RFC3339 UTC 時間格式，精確到秒。 |
|Bandwidth |浮點數 |`20` |當前數據聚合時間粒度內的源站峰值頻寬，單位為 Mbps。 |


<span id="bandwidthdetaildatalist"></span>
### BandwidthDetailDataList


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`pull.example.com` |按網域維度分割數據時的網域資訊。 |
|ISP |字串 |`telecom` |按 ISP 維度分割數據時的 ISP 資訊。 |
|PeakBandwidth |浮點數 |`20` |分割後當前維度的源站峰值頻寬，單位為 Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107389#bandwidthdatalist) 陣列 |`-` |分割後當前維度下所有時間粒度的頻寬數據列表。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceBandwidthData&Version=2023-01-01
{
    "DomainList": [
        "pull.example.com",
        "pull2.example.com"
    ],
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ISPList": [
        "telecom"
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
### 響應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveSourceBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "pull.example.com",
            "pull2.example.com"
        ],
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ISPList": [
            "telecom"
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
        "PeakBandwidth": 20,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bandwidth": 20
            }
        ],
        "BandwidthDetailDataList": [
            {
                "Domain": "pull.example.com",
                "ISP": "telecom",
                "PeakBandwidth": 20,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Bandwidth": 20
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [Request Parameters](https://docs.byteplus.com/en/docs/24/107389#request-parameters) 說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳戶下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [contact support](https://console.byteplus.com/workorder/create)。 |
