---
title: "DescribeCMAFConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig-zh-TW"
---

調用 `DescribeCMAFConfig` API，以查詢指定網域名稱空間下串流的持續時間與分段數設定。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeCMAFConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 呼叫時，除了 API 專屬參數外，還必須帶上 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCMAFConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。您可以調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面，取得該網域所屬的網域名稱空間。 |


<span id="Response parameters"></span>
## 回應參數

有關 API 專屬回應參數，請參見下表。更多細節請參考 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|CMAFConfigList |[CMAFConfigList](https://docs.byteplus.com/en/docs/24/107319#cmafconfiglist) 陣列 |`-` |CMAF 設定列表。 |


<span id="cmafconfiglist"></span>
### CMAFConfigList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`Arctic` |網域名稱空間。 |
|App |String |`Far` |AppName 欄位。 |
|Interval |Float |`2.6` |CMAF 分段持續時間，範圍為 1 至 60。 |
|PlaylistLength |Integer |`6` |播放清單中包含的媒體分段數。整數，範圍為 3 至 10。 |
|DisableLowLatency |Boolean |`true` |是否停用低延遲 DASH。低延遲 DASH 擴展協議以實現低延遲影片串流，同時維持可擴展性。<br><br><br>* `true`：停用；<br><br>* `false`：啟用。 |
|CreateTime |String |`2024-02-23T07:51:15Z` |建立設定時的 UTC 時間（RFC 3339 格式）。 |
|UpdateTime |String |`2024-02-23T07:51:15Z` |最後更新設定時的 UTC 時間（RFC 3339 格式）。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeCMAFConfig&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "20240411060546FAFDB99137DFD66F1D02",
        "Action": "DescribeCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CMAFConfigList": [
            {
                "Vhost": "example.com",
                "App": "",
                "DefaultLatency": 3,
                "DisableLowLatency": false,
                "Interval": 2,
                "PlaylistLength": 3,
                "CreateTime": "2024-03-18T05:47:44Z",
                "UpdateTime": "2024-03-18T05:47:44Z"
            }
        ]
    }
}
```
