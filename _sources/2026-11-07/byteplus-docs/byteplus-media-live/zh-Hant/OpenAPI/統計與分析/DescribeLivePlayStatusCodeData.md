---
title: "DescribeLivePlayStatusCodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata-zh-TW"
---

調用 `DescribeLivePlayStatusCodeData` API，以查詢在指定時間範圍內對該網域發出的請求狀態碼比例，包括推流請求、拉流請求及源流請求。

<span id="Requirements"></span>
## 需求


* 限制：支援查詢由特定網域（包含已刪除網域）產生的推拉流請求或源站請求的狀態碼分布。

* 頻率限制：每個帳戶每秒最多 30 次查詢

* 資料延遲：15 分鐘


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLivePlayStatusCodeData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePlayStatusCodeData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com", "pull.example.com"]` |網域列表。預設為空，表示查詢所有網域的請求狀態碼百分比資料。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或至 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，取得查詢請求狀態碼百分比資料所需的網域。 |
|ISPList |Array of String |否 |`["telecom"]` |提供網路接入服務的運營商識別碼。預設表示所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：Dr.鵬電信與媒體集團；<br><br>* `btvn`：中國廣播網絡；<br><br>* `huashu`：華數傳媒。<br><br><br>如需取得各運營商的識別碼，可調用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107453#region) |否 |`-` |CDN 節點 IP 所屬區域列表，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可於同一請求中同時使用。</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107453#region) |否 |`-` |用戶端 IP 所屬區域列表，預設表示所有區域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 與 <code>UserRegionList</code> 不可於同一請求中同時使用。</div><br> |
|StartTime |String |是 |`2024-04-28T14:00:00Z` |查詢範圍的起始時間，格式為 RFC 3339，精確到秒。 |
|EndTime |String |是 |`2024-04-28T14:00:00Z` |查詢範圍的結束時間，格式為 RFC 3339，精確到秒。 |
|Aggregation |Integer |否 |`300` |資料彙總粒度（單位：秒），支援以下選項：<br><br><br>* `60`：1 分鐘。每 1 分鐘彙總時，單次查詢最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天；<br><br>* `300`：（預設）5 分鐘。每 5 分鐘彙總時，單次查詢最大時間跨度為 31 天，歷史查詢時間範圍為 366 天；<br><br>* `3600`：1 小時。當以每1小時聚合時，單次查詢的最長時間跨度為93天，歷史查詢的時間範圍為366天。 |
|DetailField |字串陣列 |否 |`["Domain"]` |資料分維度預設不拆分。支援的維度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網際網路服務提供商；<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>DetailField</code>參數指定了分維度，且下列參數之一有多個值時，回應中才會進行分維度資料分割：<code>DomainList</code>或<code>ISPList</code>。</div><br> |
|類型 |字串 |否 |`Access` |請求類型，對應值及含義如下：<br><br><br>* `Access`：（預設）推流與拉流請求。<br><br>* `Source`：回源請求。 |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)獲取區域資訊中的大區識別碼。 |
|Country |字串 |否 |`CN` |可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)獲取區域資訊中的國家識別碼。按國家篩選時，需同時傳入`Area`與`Country`。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份識別碼目前僅支援中國大陸、香港、澳門及台灣，其他國家或地區暫不支援。可透過呼叫[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)獲取識別碼資訊。按省份篩選時，需同時傳入`Area`、`Country`及`Province`。 |


<span id="Response parameters"></span>
## 回應參數

如需 API 專屬回應參數，請參閱下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com", "pull.example.com"]` |域名清單。 |
|ISPList |字串陣列 |`["telecom"]` |提供網路接入服務的運營商識別碼。預設為全部運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數傳媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107453#region)陣列 |`-` |CDN節點IP所屬區域清單。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107453#region)陣列 |`-` |用戶端IP所屬區域清單。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採RFC 3339格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採RFC 3339格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|類型 |字串 |`Access` |請求類型，對應值及含義如下：<br><br><br>* `Access`：推流與拉流請求。<br><br>* `Source`：回源請求。 |
|DetailField |字串陣列 |`["Domain"]` |資料分維度及其說明如下：<br><br><br>* `Domain`：域名。<br><br>* `ISP`：網際網路服務提供商。 |
|StatusSummaryDataList |[StatusSummaryData](https://docs.byteplus.com/en/docs/24/107453#statussummarydata)陣列 |`-` |當前查詢條件下的狀態碼占比。 |
|StatusDataList |[StatusData](https://docs.byteplus.com/en/docs/24/107453#statusdata)陣列 |`-` |所有時間粒度的資料。 |
|StatusDetailDataList |[StatusDetailData](https://docs.byteplus.com/en/docs/24/107453#statusdetaildata)陣列 |`-` |按維度拆分的資料。 |


<span id="region"></span>
### Region


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`CN` |區域資訊中的區域識別碼。 |
|Country |字串 |`CN` |區域資訊中的國家識別碼。 |
|Province |字串 |`beijing` |區域資訊中的省份識別碼。 |


<span id="statussummarydata"></span>
### StatusSummaryData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|StatusCode |整數 |`400` |請求狀態碼。 |
|Value |整數 |`67` |目前狀態碼的出現次數。 |
|百分比 |浮點數 |`67` |目前狀態碼在所有狀態碼總數中的出現百分比。 |


<span id="statusdata"></span>
### StatusData


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2021-08-16T00:00:00Z` |當資料依時間粒度聚合時，每個時間粒度的起始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|StatusSummaryDataList |[StatusSummaryData](https://docs.byteplus.com/en/docs/24/107453#statussummarydata) 陣列 |`-` |目前資料聚合時間粒度內的狀態碼詳細資料。 |


<span id="statusdetaildata"></span>
### StatusDetailData


|**參數** |**資料型態** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`pull.example.com` |拉流域名。 |
|ISP |字串 |`unicom` |網際網路服務提供商。 |
|StatusDataList |[StatusData](https://docs.byteplus.com/en/docs/24/107453#statusdata) 陣列 |`-` |每個時間戳的粒度資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePlayStatusCodeData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "pull.example.com"
    ],
    "UserRegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2024-04-28T14:00:00Z",
    "EndTime": "2024-04-28T14:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Domain"
    ],
    "Type": "Access"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLivePlayStatusCodeData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "pull.example.com"
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
            "Domain"
        ],
        "StatusSummaryDataList": [
            {
                "StatusCode": 400,
                "Value": 67,
                "Percent": 67
            }
        ],
        "StatusDataList": [
            {
                "TimeStamp": "2021-08-16T00:00:00Z",
                "StatusSummaryDataList": [
                    {
                        "StatusCode": 400,
                        "Value": 67,
                        "Percent": 67
                    }
                ]
            }
        ],
        "StatusDetailDataList": [
            {
                "Domain": "pull.example.com",
                "ISP": "unicom",
                "StatusDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "StatusSummaryDataList": [
                            {
                                "StatusCode": 400,
                                "Value": 67,
                                "Percent": 67
                            }
                        ]
                    }
                ]
            }
        ],
        "Type": "Access"
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為本操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107453#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求資源（資源包括域名空間、域名、App 名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
