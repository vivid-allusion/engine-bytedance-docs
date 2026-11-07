---
title: "UpdateLatencyConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig-zh-TW"
---

呼叫 `UpdateLatencyConfig` API，透過為指定用於拉流的域名下的流配置伺服器 GOP 快取，以降低直播延遲。

<span id="Requirements"></span>
## 需求


* 限制：此功能僅適用於通過 Flash Video (FLV) 和 Real\-Time Messaging Protocol (RTMP) 進行拉流。

* 頻率限制：每個帳戶每秒最多 10 次查詢。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateLatencyConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 在帶入 API 專屬參數的同時，必須帶入 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateLatencyConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流用的域名。你可以呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面以取得域名。 |
|GopCacheSize |Integer |是 |`2000` |邊緣伺服器的快取大小是指分配給暫存畫面組（GOP）的儲存空間量。<br><br><br>* 快取大小以毫秒為單位。<br><br>* 有效範圍：500\-20,000。<br><br>* 預設值為 `2000`。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateLatencyConfig&Version=2023-01-01
{
    "GopCacheSize": 2000,
    "Domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "20240412014133DA1BD20A355B07FE66F5",
        "Action": "UpdateLatencyConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
