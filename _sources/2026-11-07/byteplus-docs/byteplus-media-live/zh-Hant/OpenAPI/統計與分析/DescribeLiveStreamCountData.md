---
title: "DescribeLiveStreamCountData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata-zh-TW"
---

獲取特定推流、回源拉流或轉碼流在指定時間範圍內的峰值數量。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒 30 次請求

* 數據延遲：5 分鐘


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveStreamCountData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 調用必須同時傳遞[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)和 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStreamCountData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**數據類型** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|StartTime |String |是 |`2021-08-16T00:00:00+08:00` |查詢範圍的開始時間（UTC 時間，RFC 3339 格式，精確到秒）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">最大歷史查詢範圍為 366 天。單次查詢的最大時間跨度取決於數據聚合的時間粒度。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當數據每 60 秒聚合一次，即<code>Aggregation</code>設為<code>60</code>時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當數據每 300 秒聚合一次，即<code>Aggregation</code>設為<code>300</code>時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當數據每 3600 秒聚合一次，即<code>Aggregation</code>設為<code>3600</code>時，單次查詢的最大時間跨度為 31 天。</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59+08:00` |查詢範圍的結束時間（UTC 時間，RFC 3339 格式，精確到秒）。 |
|DomainList |Array of String |否 |`["push.exmaple.com","push2.example.com"]` |用於直播的域名列表。預設情況下，此列表為空，表示返回所有域名的峰值流數。可調用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)，或前往[BytePlus MediaLive 控制台](https://console.byteplus.com/live/main/domain/list)的**Domains**頁面，獲取直播使用的域名。 |
|StreamType |Array of String |否 |`["push"]` |流類型。預設情況下，返回所有流類型的峰值流數。可選值：<br><br><br>* `push`：推流。<br><br>* `relay-source`：回源拉流。<br><br>* `transcode`：轉碼流。 |
|ISPList |Array of String |否 |`["telecom"]` |網際網路服務提供商（ISP）標識。預設情況下，返回所有 ISP 的峰值流數。可選值：<br><br><br>* `unicom`：中國聯通。<br><br>* `telecom`：中國電信。<br><br>* `mobile`：中國移動。<br><br>* `cernet`：中國教育和科研網（CERNET）。<br><br>* `drpeng`：鵬博士。鵬博士電信傳媒集團<br><br>* `btvn`：廣播電視網（BTVN）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">僅當<code>StreamType</code>設為<code>push</code>時，此參數才生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">你也可以調用<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata">DescribeLiveISPData</a>獲取 ISP 標識。</div><br> |
|UserRegionList |Array of [UserRegionList](https://docs.byteplus.com/en/docs/24/107402#userregionlist) |否 |`-` |客戶端 IP 所屬地區列表。預設情況下，返回所有地區的峰值流數。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當<code>StreamType</code>設為<code>push</code>時，此參數才生效。</div><br> |
|Aggregation |Integer |否 |`60` |數據彙總的時間粒度，以秒為單位。預設值：`300`。可用值：<br><br><br>* `60`：1 分鐘。<br><br>* `300`：5 分鐘。<br><br>* `3600`：1 小時。 |
|DetailField |字串陣列 |否 |`["Domain"]` |數據分割的維度。預設情況下，數據不按維度分割。<br><br>目前，此參數僅有值 `Domain`，表示數據按網域分割。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當你為 <code>DomainList</code> 參數設置多個值時，此參數才會生效。</div><br> |


<span id="userregionlist"></span>
### UserRegionList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`AP1` |區域識別碼。你可以呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得區域識別碼。 |
|Country |字串 |否 |`CN` |國家識別碼。你可以呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得國家識別碼。若需依據國家篩選，需同時傳入 `Area` 與 `Country` 參數。 |
|Province |字串 |否 |`HK` |省份識別碼。你可以呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得省份識別碼。若需依據省份篩選，必須同時傳入 `Area`、`Country` 及 `Province` 參數。 |


<span id="Response parameters"></span>
## 響應參數

有關唯一的 API 專屬響應參數，請參見下表。更多詳情請參考[請求響應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com","push2.example.com"]` |網域清單。 |
|StartTime |字串 |`2021-08-16T00:00:00+08:00` |查詢範圍的開始時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|EndTime |字串 |`2021-08-16T00:01:59+08:00` |查詢範圍的結束時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|Aggregation |整數 |`60` |數據彙總的時間粒度，以秒為單位。可用值：<br><br><br>* `60`：1 分鐘。<br><br>* `300`：5 分鐘。<br><br>* `3600`：1 小時。 |
|DetailField |字串陣列 |`["Domain"]` |數據分割的維度。目前，此參數僅有值 `Domain`，表示數據按網域分割。 |
|StreamType |字串陣列 |`["push"]` |串流類型。可用值：<br><br><br>* `push`：推流。<br><br>* `relay-source`：回源拉流。<br><br>* `transcode`：轉碼流。 |
|PeakCount |整數 |`100` |當前查詢條件下的串流峰值數，即在特定時間範圍內推流、回源拉流或轉碼流的最大併發數。 |
|TotalStreamDataList |[TotalStreamDataList](https://docs.byteplus.com/en/docs/24/107402#totalstreamdatalist) 陣列 |`-` |所有時間粒度的數據。 |
|StreamDetailDataList |[StreamDetailDataList](https://docs.byteplus.com/en/docs/24/107402#streamdetaildatalist) 陣列 |`-` |按網域分割的數據。 |
|ISPList |字串陣列 |`["telecom"]` |網際網路服務供應商（ISP）識別碼。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107402#userregionlist) 陣列 |`-` |用戶端 IP 所屬的地區清單。 |


<span id="totalstreamdatalist"></span>
### TotalStreamDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2021-08-16T00:00:00+08:00` |按時間粒度彙總數據時，每個粒度的開始時間（RFC 3339 格式的 UTC 時間，精確到秒）。 |
|PeakCount |整數 |`100` |當前時間粒度內數據彙總的最大串流數。 |


<span id="streamdetaildatalist"></span>
### StreamDetailDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`push.example.com` |數據按網域分割時的網域資訊。 |
|TotalStreamDataList |[TotalStreamDataList](https://docs.byteplus.com/en/docs/24/107402#totalstreamdatalist) 陣列 |`-` |數據按網域分割後，當前網域下所有時間粒度的數據。 |


<span id="userregionlist"></span>
### UserRegionList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Area |字串 |`AP1` |區域識別碼。 |
|Country |字串 |`CN` |國家識別碼。 |
|Province |字串 |`HK` |省份識別碼。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStreamCountData&Version=2023-01-01
{
    "DomainList": [
        "example1.com",
        "example2.com"
    ],
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 60,
    "DetailField": [
        "Domain"
    ],
    "StreamType": [
        "pull",
        "relay-source"
    ]
}
```


<span id="Sample response"></span>
### 響應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveSourceStreamCountData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "example1.com",
            "example2.com"
        ],
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 60,
        "DetailField": [
            "Domain"
        ],
        "StreamType": [
            "pull",
            "relay-source"
        ],
        "PeakCount": 100,
        "TotalStreamDataList": [
            {
                "TimeStamp": "2021-08-16T00:00:00Z",
                "PeakCount": 100
            }
        ],
        "StreamDetailDataList": [
            {
                "Domain": "example1.com",
                "TotalStreamDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "PeakCount": 100
                    }
                ]
            },
            {
                "Domain": "example2.com",
                "TotalStreamDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "PeakCount": 100
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本操作相關的錯誤碼。其他錯誤碼請參見[BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**狀態碼** |**錯誤碼** |**錯誤訊息** |**說明** |
|---|---|---|---|
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [request parameters](https://docs.byteplus.com/en/docs/24/107402#request-parameters) 說明進行驗證。 |
|403 |RequestForbidden |*  |請求被拒絕，因為當前帳戶下沒有請求的資源（資源包括網域命名空間、網域名稱、應用程式、配置範本和憑證）。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
