---
title: "DeleteHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/deletehlsconfig-zh-TW"
---

呼叫 `DeleteHLSConfig` API，可將特定網域空間的 HLS 設定恢復為預設值，包括分段大小、分段數量等。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多 10 次查詢

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteHLSConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 呼叫時，必須同時包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) 及 API 專屬參數。

<span id="Query"></span>
### 查詢


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteHLSConfig` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型態** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。可呼叫 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 頁面取得該網域所屬的網域名稱空間。 |
|App |String |否 |`live` |直播串流 URL 中的 AppName 欄位。必須與新增設定時填寫的值一致。可包含大寫字母（A\-Z）、小寫字母（a\-z）、數字（0\-9）、底線（_）、連字號（\-）及句點（.），長度為 1 至 30 字元。 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅於回應中返回 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DeleteHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202404120112128186EFFADE3658DF0DB2",
        "Action": "DeleteHLSConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
