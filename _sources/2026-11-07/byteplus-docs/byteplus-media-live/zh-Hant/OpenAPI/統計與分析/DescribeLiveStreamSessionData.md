---
title: "DescribeLiveStreamSessionData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata-zh-TW"
---

調用 `DescribeLiveStreamSessionData` API，以查詢指定網域下所有直播流或指定直播流在指定時間範圍內的請求數量及最大線上觀眾數。

<span id="Requirements"></span>
## 需求


* 限制：支援查詢特定直播網域（包含已刪除網域）的請求數量及最大同時線上觀眾數。

* 頻率限制：每個帳戶每秒最多 30 次查詢

* 資料延遲：

   * 當彙總粒度為 60 秒時，資料延遲為 5 分鐘；

   * 其他時間粒度下，資料延遲為 15 分鐘。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLiveStreamSessionData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStreamSessionData` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|DomainList |String 陣列 |否 |`["pull.example.com"]` |拉流網域列表。預設為空，表示將查詢所有網域的請求數及線上觀眾資料。你可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得欲查詢的拉流網域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅需提供 <code>DomainList</code> 或 <code>Domain</code>，不可同時提供。</div><br> |
|Domain |String |否 |`pull.example.com` |查詢流粒度資料時，需提供拉流網域，且必須同時帶入 `App` 及 `Stream` 參數。你可以透過調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) 接口或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得欲查詢的拉流網域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的請求數及線上用戶資料時，需同時指定 <code>Domain</code>、<code>App</code> 及 <code>Stream</code> 參數，以明確指定直播流。</div><br> |
|App |String |否 |`example_app` |直播流 URL 中的 AppName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的源站流量監控資料時，必須指定 <code>Domain</code>、<code>App</code> 及 <code>Stream</code>，以識別特定源站流。</div><br> |
|Stream |String |否 |`example_stream` |直播流 URL 中的 StreamName 欄位。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 100 字元。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢流粒度的源站流量監控資料時，必須指定 <code>Domain</code>、<code>App</code> 及 <code>Stream</code>，以識別源站流。</div><br> |
|ProtocolList |String 陣列 |否 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設表示所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：一種基於 HTTP 協議的推拉流協議，採用 FLV 格式進行視頻傳輸。<br><br>* `HTTP-HLS`：一種基於 HTTP 協議的推拉流協議，採用 TS 格式進行視頻傳輸。<br><br>* `RTMP`：即時消息傳輸協議，用於實時消息傳輸。<br><br>* `RTM`：即時媒體協議，用於超低延遲直播。<br><br>* `SRT`：安全可靠傳輸協議，用於安全可靠的流媒體傳輸。<br><br>* `QUIC`：快速 UDP 網際網路連接協議，一種基於 UDP 的新型低延遲網際網路傳輸協議。<br><br>* `CMAF`：通用媒體應用格式，一種多功能流媒體協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查詢 QUIC 協議時，不能同時查詢其他協議。</div><br> |
|ISPList |Array of String |否 |`["telecom"]` |提供網路接入服務的運營商標識。預設情況下，表示所有運營商。支持的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網（CERNET）；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信傳媒集團；<br><br>* `btvn`：中國廣播電視網絡；<br><br>* `huashu`：華數傳媒。<br><br><br>如需獲取各運營商的標識，可調用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [RegionList](https://docs.byteplus.com/en/docs/24/107404#regionlist) |否 |`-` |CDN 節點 IP 所屬地區列表，預設表示所有地區。 |
|Aggregation |Integer |否 | |數據聚合的粒度，單位為秒，支持以下選項：<br><br><br>* `60`：1 分鐘。<br><br>* `300`：（預設）5 分鐘。<br><br>* `3600`：1 小時。 |
|DetailField |Array of String |否 |`["Domain"]` |數據明細的維度預設不拆分。支持的維度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：網路服務提供商；<br><br>* `Protocol`：推拉流協議。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">僅當 <code>DetailField</code> 參數指定了拆分維度，且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 中至少有一項傳入多個值時，響應結果才會根據維度進行數據拆分。</div><br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，需使用 RFC 3339 格式，精確到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">歷史查詢時間範圍為 366 天，單次查詢的最大時間跨度取決於 DetailField 和 Aggregation。關係說明如下。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">當不拆分維度或僅按一個維度拆分數據時：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">數據每 60 秒聚合一次時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">數據每 300 秒聚合一次時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">數據每 3600 秒聚合一次時，單次查詢的最大時間跨度為 31 天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">當按兩個及以上維度拆分數據時：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">數據每 60 秒聚合一次時，單次查詢的最大時間跨度為 3 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">數據每 300 秒聚合一次時，單次查詢的最大時間跨度為 24 小時。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">數據每 3600 秒聚合一次時，單次查詢的最大時間跨度為 7 天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |


<span id="regionlist"></span>
### RegionList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Area |字串 |否 |`CN` |可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得區域資訊中的主要區域識別碼。 |
|Country |字串 |否 |`CN` |可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得區域資訊中的國家識別碼。以國家為篩選條件時，需同時傳入「Area」與「Country」。 |
|Province |字串 |否 |`beijing` |區域資訊中的省份識別碼，目前僅支援中國大陸、香港、澳門及台灣，其他國家或地區暫不支援。可透過呼叫 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 取得識別碼資訊。以省份為篩選條件時，需同時傳入 `Area`、`Country` 及 `Province`。 |


<span id="Response parameters"></span>
## 回應參數

如需瞭解 API 專屬回應參數，請參閱下表。更多細節請參考 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|DomainList |字串陣列 |`["push.example.com"]` |域名列表。 |
|Domain |字串 |`pull.example.com` |拉流域名。 |
|App |字串 |`live` |直播串流 URL 中的 AppName 欄位。 |
|Stream |字串 |`example_stream` |直播串流 URL 中的 StreamName 欄位。 |
|ProtocolList |字串陣列 |`["HTTP-FLV", "RTMP"]` |推拉流協議。預設表示所有協議類型。支援的協議如下。<br><br><br>* `HTTP-FLV`：基於 HTTP 協議的推拉流協議，採用 FLV 格式進行視訊傳輸。<br><br>* `HTTP-HLS`：基於 HTTP 協議的推拉流協議，採用 TS 格式進行視訊傳輸。<br><br>* `RTMP`：即時訊息傳輸協議，用於即時訊息傳輸。<br><br>* `RTM`：即時媒體協議，適用於超低延遲直播。<br><br>* `SRT`：安全可靠傳輸協議，用於安全且可靠的串流。<br><br>* `QUIC`：Quick UDP Internet Connections，一種基於 UDP 的新型低延遲網路傳輸協議。<br><br>* `CMAF`：通用媒體應用格式，一種多功能串流協議。 |
|ISPList |字串陣列 |`["telecom", "unicom"]` |提供網路接入服務的運營商識別碼。預設包含所有運營商。支援的運營商如下。<br><br><br>* `unicom`：中國聯通；<br><br>* `railcom`：中國鐵通；<br><br>* `telecom`：中國電信；<br><br>* `mobile`：中國移動；<br><br>* `cernet`：中國教育和科研網；<br><br>* `tianwei`：中國天威；<br><br>* `alibaba`：阿里巴巴集團；<br><br>* `tencent`：騰訊控股；<br><br>* `drpeng`：鵬博士電信與媒體集團；<br><br>* `btvn`：廣播電視網（BTVN）；<br><br>* `huashu`：華數媒體。 |
|RegionList |[RegionList](https://docs.byteplus.com/en/docs/24/107404#regionlist) 陣列 |`-` |CDN 節點 IP 所屬區域列表。 |
|StartTime |字串 |`2021-04-13T00:00:00Z` |查詢範圍的開始時間，採用 RFC 3339 格式，精確到秒。 |
|EndTime |字串 |`2021-04-14T00:00:00Z` |查詢範圍的結束時間，採用 RFC 3339 格式，精確到秒。 |
|Aggregation |整數 |`300` |資料粒度，單位為秒。 |
|DetailField |字串陣列 |`["Domain"]` |資料分割維度：<br><br><br>* `Domain`：域名。<br><br>* `ISP`：網路服務提供商。<br><br>* `Protocol`：推拉流協議。 |
|TotalRequest |整數 |`20` |指定查詢時間範圍內的請求總數。 |
|PeakOnlineUser |整數 |`20` |指定查詢時間範圍內的同時在線用戶峰值。 |
|TotalHitRate |雙精度 |`13.45` |指定時間範圍內所有域名及協議的整體邊緣請求命中率。用於評估邊緣請求快取機制在減輕源站負載方面的效果。 |
|SessionDataList |[SessionDataList](https://docs.byteplus.com/en/docs/24/107404#sessiondatalist) 陣列 |`-` |所有時間粒度的資料。 |
|SessionDetailDataList |[SessionDetailDataList](https://docs.byteplus.com/en/docs/24/107404#sessiondetaildatalist) 陣列 |`-` |依特定維度分割的資料。 |


<span id="regionlist"></span>
### RegionList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|地區 |字串 |`CN` |區域資訊中的區域識別碼。 |
|國家 |字串 |`CN` |區域資訊中的國家識別碼。 |
|省份 |字串 |`beijing` |區域資訊中的省份識別碼。 |


<span id="sessiondatalist"></span>
### SessionDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TimeStamp |字串 |`2022-04-13T00:00:00Z` |依時間粒度彙總資料時，每個時間粒度的起始時間，格式為 RFC3339 UTC 時間，精確到秒。 |
|Request |整數 |`10` |當前資料彙總時間粒度內的請求數。 |
|OnlineUser |整數 |`20` |當前資料彙總時間粒度內的線上用戶峰值數。 |
|HitRate |雙精度 |`13.45` |指定粒度下的邊緣請求命中率（例如每 60 秒或每 5 分鐘）。 |


<span id="sessiondetaildatalist"></span>
### SessionDetailDataList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Domain |字串 |`pull.example.com` |按網域維度分割資料時的網域資訊。 |
|Protocol |字串 |`HTTP-FLV` |依串流協議分割資料時的協議資訊。 |
|ISP |字串 |`telecom` |按 ISP 維度分割資料時的 ISP 資訊。 |
|TotalRequest |整數 |`20` |資料分割後當前維度的請求數。 |
|PeakOnlineUser |整數 |`20` |資料分割後當前維度的線上用戶峰值數。 |
|TotalHitRate |浮點數 |`13.45` |資料依特定維度（如`Domain`）分割後，在指定查詢時間範圍內各維度的整體邊緣請求命中率。此指標用於評估不同資料分段的快取效率。 |
|SessionDataList |[SessionDataList](https://docs.byteplus.com/en/docs/24/107404#sessiondatalist) 陣列 |`-` |資料分割後當前維度的所有時間粒度資料。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStreamSessionData&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "example_app",
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
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
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
        "Action": "DescribeLiveStreamSessionData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "ISPList": [
            "telecom",
            "unicom"
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
        "TotalRequest": 20,
        "PeakOnlineUser": 20,
        "TotalHitRate": 13.41,
        "SessionDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Request": 10,
                "OnlineUser": 20,
                "HitRate": 13.41
            }
        ],
        "SessionDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "pull.example.com",
                "ISP": "telecom",
                "TotalRequest": 20,
                "PeakOnlineUser": 20,
                "SessionDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Request": 20,
                        "OnlineUser": 20,
                        "HitRate": 13.41
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
|400 |InvalidParam |*  |輸入參數無效或不符合要求。請參考[Request Parameters](https://docs.byteplus.com/en/docs/24/107404#request-parameters)說明進行檢查。 |
|403 |RequestForbidden |*  |因當前帳號下無請求資源（資源包括網域名稱空間、網域名稱、應用名稱、配置及憑證），請求被拒絕。 |
|500 |InternalError |發生內部錯誤，請聯絡管理員。 |發生內部錯誤。請[聯絡支援](https://console.byteplus.com/workorder/create)。 |
