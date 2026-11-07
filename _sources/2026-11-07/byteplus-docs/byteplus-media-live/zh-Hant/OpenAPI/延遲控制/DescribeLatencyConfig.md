---
title: "DescribeLatencyConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig-zh-TW"
---

調用 `DescribeLatencyConfig` API 以查詢 GOP 的伺服器快取配置。

<span id="Requirements"></span>
## 需求

速率限制：每個帳戶每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeLatencyConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳遞 API 專屬參數外，還必須帶上 [通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLatencyConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。當前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空間。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面以獲取該域所屬的域名空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須至少配置 <code>Vhost</code> 或 <code>Domain</code> 其中之一。</div><br> |
|Domain |String |否 |`pull.example.com` |拉流用的域名。可調用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面以獲取域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">必須至少配置 <code>Vhost</code> 或 <code>Domain</code> 其中之一。</div><br> |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。如需更多詳情，請參閱 [請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|LatencyConfigList |[LatencyConfigList](https://docs.byteplus.com/en/docs/24/107427#latencyconfiglist) 陣列 |`-` |延遲配置列表。 |


<span id="latencyconfiglist"></span>
### LatencyConfigList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空間。 |
|Domain |String |`pull.example.com` |域名。 |
|GopCacheSize |String |`2000` |邊緣伺服器用於暫存視訊內容的快取大小。快取大小以毫秒為單位。 |
|CreateTime |String |`2024-03-25T11:20:47Z` |配置建立時的 UTC 時間，格式為 RFC 3339。 |
|UpdateTime |String |`2024-03-25T11:20:47Z` |配置最後更新時的 UTC 時間，格式為 RFC 3339。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DescribeLatencyConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404120143108F3D78593F7AFFF41F99",
        "Action": "DescribeLatencyConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "LatencyConfigList": [
            {
                "CreateTime": "2024-03-25T11:20:47Z",
                "Domain": "example.com",
                "GopCacheSize": 2000,
                "UpdateTime": "2024-03-25T11:20:47Z",
                "Vhost": "example"
            }
        ]
    }
}
```
