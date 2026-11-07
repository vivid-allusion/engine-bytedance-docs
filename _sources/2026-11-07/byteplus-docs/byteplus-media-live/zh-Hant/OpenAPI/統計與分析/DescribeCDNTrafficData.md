---
title: "DescribeCDNTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdntrafficdata-zh-TW"
---

調用 `DescribeCDNTrafficData` API 以查詢在指定時間範圍內存取直播錄製與快照時所使用的 CDN 流量。

<span id="Requirements"></span>
## 需求


* 頻率限制：每個帳戶每秒 1 次查詢。

* 數據延遲：4 分鐘。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeCDNTrafficData&Version=2020\-08\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCDNTrafficData` |API 操作名稱。 |
|Version |String |是 |`2020-08-01` |本 API 操作的版本。當前版本：2020\-08\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|StartTime |String |是 |`2022-04-08T00:00:00Z` |查詢範圍的開始時間，需符合 RFC 3339 格式，精確到秒。 |
|EndTime |String |是 |`2022-04-08T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式，精確到秒。 |
|DomainList |Array of String |否 |`["push.example.com"]` |欲查詢的網域名稱清單。如未指定，將查詢帳戶下所有網域名稱。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面獲取網域名稱。 |
|Interval |Integer |是 |`300` |數據粒度。單位：秒。僅可設為 300。 |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/107449#regionlist) |是 |`-` |區域清單。 |


<span id="regionlist"></span>
### RegionList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |String |是 |`Global` |支援值：<br><br><br>* `AsiaPacific-1`<br><br>* `AsiaPacific-2`<br><br>* `AsiaPacific-3`<br><br>* `NorthAmerica`<br><br>* `SouthAmerica`<br><br>* `Europe`<br><br>* `MiddleEast`<br><br>* `Global`：非中國大陸地區 |
|Country |String |否 |`-` |預留作未來用途。 |
|Province |String |否 |`-` |預留作未來用途。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多詳情請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"` |欲查詢的網域名稱清單。 |
|Interval |Integer |`300` |數據粒度。 |
|StartTime |String |`2022-04-08T00:00:00Z` |查詢範圍的開始時間，需符合 RFC 3339 格式，精確到秒。 |
|EndTime |String |`2022-04-08T00:00:00Z` |查詢範圍的結束時間，需符合 RFC 3339 格式，精確到秒。 |
|TrafficTotalData |Array of [CDNTrafficData](https://docs.byteplus.com/en/docs/24/107449#cdntrafficdata) |`-` |依時間區間彙總的數據。 |
|TrafficDetailDataList |Array of [TrafficDetailDataList](https://docs.byteplus.com/en/docs/24/107449#trafficdetaildatalist) |`-` |依時間區間及網域名稱彙總的數據。 |


<span id="cdntrafficdata"></span>
### CDNTrafficData


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |String |`2022-04-08T00:00:00Z` |每個區間的開始時間（UTC 時間，RFC 3339 格式）。 |
|Traffic |Float |`22` |CDN 流量數據，單位為 GB。 |


<span id="trafficdetaildatalist"></span>
### TrafficDetailDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |String |`push.example.com` |網域名稱。 |
|TrafficDataList |Array of [CDNTrafficData](https://docs.byteplus.com/en/docs/24/107449#cdntrafficdata) |`-` |依時間區間彙總的數據。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeCDNTrafficData&Version=2020-08-01
{
    "StartTime": "2022-04-08T00:00:00Z",
    "EndTime": "2022-04-08T00:00:00Z",
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "Interval": 300
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
  "ResponseMetadata":{
    "RequestId":"202207130928130102511970410745B8DC",
    "Action":"DescribeCDNTrafficData",
    "Version":"2020-08-01",
    "Service":"live",
    "Region":"ap-singapore-1"
  },
  "Result":{
    "StartTime": "2022-04-08T00:00:00Z",
    "EndTime": "2022-04-08T00:00:00Z",
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "Interval": 300,
    "TrafficTotalData": [
        {
            "Timestamp": "2022-04-08T00:00:00Z",
            "Traffic": 276.00
        },
        {
            "Timestamp": "2022-04-08T01:00:00Z",
            "Traffic": 276.00
        }
    ],
    "TrafficDetailDataList": [
        {
            "Domain": "push.example.com",
            "TrafficDataList": [
                {
                    "TimeStamp": "2022-04-08T00:00:00Z",
                    "Traffic": 138.00
                },
                {
                    "TimeStamp": "2022-04-08T01:00:00Z",
                    "Traffic": 138.00
                }
            ]
        },
        {
            "Domain": "push.example2.com",
            "TrafficDataList": [
                {
                    "TimeStamp": "2022-04-08T00:00:00Z",
                    "Traffic": 138.00
                },
               {
                    "TimeStamp": "2022-04-08T01:00:00Z",
                    "Traffic": 138.00
                }
            ]
        }
    ]
}
```


<span id="Error codes"></span>
## 錯誤碼

以下為與本次操作相關的錯誤碼。其他錯誤碼請參見 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**說明** |
|---|---|---|---|
|200 |CommonErr |*  |未分類錯誤。建議重試。若仍返回錯誤碼，請 [聯繫客服](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107449#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料型別是否正確。 |
|403 |RequestForbidden |*  |因目前帳戶下無請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求已被拒絕。 |
|403 |RequestForbidden.AccountIDNotAllow |此 AccountID 無權存取相應資源，請檢查請求參數。 |因目前帳戶下無請求的資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求已被拒絕。 |
|403 |RequestForbidden.BillingStatus |該 AccountID 的計費狀態不可用，請啟用服務或儲值。 |尚未啟用視訊直播服務或帳戶欠費，導致帳單不可用。請檢查服務啟用狀態及帳戶欠費狀態。 |
|404 |ResourceNotFound |*  |未找到資源（包括網域名稱空間、網域名稱、應用名稱、配置及憑證）。建議重新嘗試。若仍返回錯誤碼，請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |發生與資料庫相關的內部錯誤，請聯絡管理員。 |發生與資料庫相關的內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請[聯絡客服](https://console.byteplus.com/workorder/create)。 |
