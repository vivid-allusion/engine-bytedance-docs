---
title: "DescribeLiveBatchStreamTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtrafficdata-2023-zh-TW"
---

呼叫 `DescribeLiveBatchStreamTrafficData` API，查詢指定時間範圍內的上行與下行流量資料及其詳細資料。

## 要求

* 限制：

   * 支援查詢指定網域名稱或協定下的流量資料。

   * 支援查詢已刪除網域名稱下產生的流量資料。

* 速率限制：每個帳戶每秒 30 次查詢。

* 資料延遲：資料延遲為 15 分鐘。

* 資料指標：流量資料以 1000 為基數計算，例如 1 GB = 1000 MB。

## HTTP 請求

* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTrafficData&Version=2023\-01\-01

## 請求參數

### 通用參數

除 API 特定參數外，所有 API 都必須使用[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)呼叫。

### 查詢

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLiveBatchStreamTrafficData` |API 操作。 |
|Version |String |Yes |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |

### 主體參數

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|DomainList |Array of String |No |`["push.example.com", "push2.example.com"]` |拉流網域清單。預設為空，表示查詢所有網域。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 主控台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，以取得要查詢的拉流網域。 |
|ProtocolList |Array of String |No |`["HTTP-FLV", "RTMP"]` |推拉流協定，協定說明如下：<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協定，以 FLV 格式傳輸影片格式。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協定，以 TS 格式傳輸影片格式。<br><br>* `RTMP`：即時訊息傳輸協定。<br><br>* `RTM`：即時媒體，超低延遲直播協定。<br><br>* `SRT`：安全可靠傳輸協定。<br><br>* `QUIC`：快速 UDP 網際網路連線，一種基於 UDP 的新型低延遲網際網路傳輸協定。<br><br>* `CMAF`：一種透過 HTTP 進行高效自適應影片串流的協定。<br><br><br>> **说明**<br><br><br><br>* > 如果查詢 QUIC 協定，則無法同時查詢其他協定。<br><br><br>* > 預設情況下，查詢的總流量資料是實際產生的上行與下行流量。<br><br><br>* > 如果傳入單一協定進行查詢，並加總各協定的流量，結果會大於實際總流量。<br> |
|ISPList |Array of String |No |`["telecom"]` |提供網路存取服務的電信業者識別碼。預設表示所有電信業者。支援的電信業者如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研計算機網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：中國廣電網路；<br><br>* `huashu`：華數傳媒。<br><br>   如果你需要取得各電信業者的識別碼，可以呼叫 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/107431#regionlist) |No |`-` |CDN 節點 IP 所屬區域清單，預設表示所有區域。<br><br>> **说明**<br><br><br>> 不支援同時使用參數 RegionList 和 UserRegionList。<br> |
|UserRegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/107431#regionlist) |No |`-` |用戶端 IP 所屬區域清單，預設表示所有區域。<br><br>> **说明**<br><br><br>> 不支援同時使用參數 RegionList 和 UserRegionList。<br> |
|StartTime |String |Yes |`2021-04-13T00:00:00Z` |查詢範圍的開始時間（UTC 時間，採用 RFC 3339 格式，精確到秒）。<br><br>> **说明**<br><br><br>> 單次查詢的最大時間跨度為 24 小時，歷史查詢時間範圍為 366 天。<br> |
|EndTime |String |Yes |`2021-04-14T00:00:00Z` |查詢範圍的結束時間（UTC 時間，採用 RFC 3339 格式，精確到秒）。 |
|PageNum |Integer |No |`1` |頁碼。值必須大於或等於 `1`。預設值：`1`。 |
|PageSize |Integer |No |`1000` |每頁的查詢結果數量。有效值：[100,1000]。預設值：`1000`。<br><br>> **说明**<br><br><br>> 如果將此參數設為 `0`，則使用預設值。<br> |

### RegionList

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Area |String |No |`CN` |區域資訊中的大區識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。 |
|Country |String |No |`CN` |區域資訊中的國家/地區識別碼可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得。依國家/地區篩選時，需要同時傳入 'Area' 和 'Country'。 |
|Province |String |No |`beijing` |目前不支援中國大陸、香港、澳門和台灣以外國家或地區的省份識別碼。你可以透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得識別碼資訊。依省份篩選時，需要同時傳入 `Area`、 `Country` 和 `Province` |

## 回應參數

關於唯一的 API 特定回應參數，請參閱下表。更多詳細資訊，請參閱[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com", "push2.example.com"]` |網域清單。 |
|ProtocolList |Array of String |`["RTMP"]` |推拉流協定，協定說明如下：<br><br><br>* `HTTP-FLV`：基於 HTTP 的推拉流協定，以 FLV 格式傳輸影片格式。<br><br>* `HTTP-HLS`：基於 HTTP 的推拉流協定，以 TS 格式傳輸影片格式。<br><br>* `RTMP`：即時訊息傳輸協定。<br><br>* `RTM`：即時媒體，超低延遲直播協定。<br><br>* `SRT`：安全可靠傳輸協定。<br><br>* `QUIC`：快速 UDP 網際網路連線，一種基於 UDP 的新型低延遲網際網路傳輸協定。<br><br>* `CMAF`：一種透過 HTTP 進行高效自適應影片串流的協定。 |
|ISPList |Array of String |`["telecom"]` |提供網路存取服務的電信業者識別碼。 |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/107431#regionlist-response) |`-` |CDN 節點 IP 所屬區域清單。 |
|UserRegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/107431#regionlist-response) |`-` |用戶端 IP 所屬區域清單。 |
|StartTime |String |`2022-11-10T00:00:00Z` |查詢開始時間，為 UTC 時間，依 RFC3339 格式化，精確到秒。 |
|EndTime |String |`2022-11-11T00:00:00Z` |查詢結束時間，為 UTC 時間，依 RFC3339 格式化，精確到秒。 |
|TotalUpTraffic |Float |`40` |查詢時間範圍內的總上行流量，以 GB 為單位。 |
|TotalDownTraffic |Float |`40` |查詢時間範圍內的總下行流量，以 GB 為單位。 |
|StreamInfoList |Array of [StreamInfoList](https://docs.byteplus.com/en/docs/24/107431#streaminfolist) |`-` |按串流分段的資料。 |
|Pagination |Object of [Pagination](https://docs.byteplus.com/en/docs/24/107431#pagination) |`-` |分頁資訊。 |

### RegionList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Area |String |`CN` |區域資訊中的區域識別碼。 |
|Country |String |`CN` |區域資訊中的國家/地區識別碼。 |
|Province |String |`beijing` |區域資訊中的省份識別碼。 |

### StreamInfoList

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Domain |String |`push.example.com` |網域名稱。 |
|App |String |`example_app` |串流位址的 AppName 欄位。 |
|Stream |String |`example_stream` |串流位址的 StreamName 欄位。 |
|UpTraffic |Float |`20` |目前串流的上行流量，單位為 GB。 |
|DownTraffic |Float |`20` |目前串流的下行流量，單位為 GB。 |

### Pagination

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNum |Integer |`1` |目前頁碼。 |
|PageSize |Integer |`1000` |每頁的結果數量。 |
|TotalCount |Integer |`2` |結果總數。 |

## 範例

### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTrafficData&Version=2023-01-01
{
    "StartTime": "2022-11-10T00:00:00Z",
    "EndTime": "2022-11-11T00:00:00Z"
}
```

### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveBatchStreamTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singpore-1"
    },
    "Result": {
        "StartTime": "2022-11-10T00:00:00Z",
        "EndTime": "2022-11-11T00:00:00Z",
        "TotalUpTraffic": 40,
        "TotalDownTraffic": 40,
        "StreamInfoList": [
            {
                "Domain": "push.example.com",
                "Stream": "example_stream",
                "App": "live",
                "UpTraffic": 20,
                "DownTraffic": 20
            },
            {
                "Domain": "push2.example.com",
                "Stream": "example_stream",
                "App": "live",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 1000,
            "TotalCount": 2
        }
    }
}
```

## 錯誤碼

以下是與目前操作相關的錯誤碼。關於其他錯誤碼，請參閱 [BytePlus OpenAPI 通用錯誤碼](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |未分類錯誤。建議重試。如果仍傳回此錯誤碼，請 [聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |\- |輸入參數無效或不符合要求。請參考 [請求參數](https://docs.byteplus.com/en/docs/24/107431#request-parameters) 說明進行檢查。 |
|400 |InvalidParam.BindError |請求參數錯誤，請檢查輸入資料 |參數驗證失敗。請檢查資料類型是否正確。 |
|403 |RequestForbidden |\- |請求遭拒，因為目前帳戶下沒有請求的資源（資源包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。 |
|404 |ResourceNotFound |\- |找不到資源（包括網域名稱空間、網域名稱、應用程式名稱、組態和憑證）。建議重試。如果仍傳回此錯誤碼，請 [聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請 [聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |內部服務逾時。請聯絡管理員。 |內部服務逾時。請 [聯絡支援](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
