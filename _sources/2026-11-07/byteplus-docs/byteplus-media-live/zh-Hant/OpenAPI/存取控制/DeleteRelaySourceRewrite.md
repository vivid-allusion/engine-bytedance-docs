---
title: "DeleteRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-3nf0nln2b2-zh-TW"
---

刪除來源位址重寫規則。來源位址重寫功能可根據預先定義的匹配規則，從新的位址拉取串流。詳情請參見[來源位址重寫](https://docs.byteplus.com/en/byteplus-media-live/docs/origin-address-rewrite)。

<span id="Requirements"></span>
## 需求

速率限制：每個帳號每秒 10 次查詢。

<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DeleteRelaySourceRewrite&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需傳入 API 專屬參數外，還必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteRelaySourceRewrite` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |否 |`example` |網域名稱空間。可呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面取得該網域所屬的網域名稱空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">未指定 Vhost 的請求可能會不小心匹配並刪除網域名稱。因此，我們強烈建議您指定 Vhost。</div><br> |
|Domain |String |否 |`example.com` |拉流用的網域名稱。可呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面取得網域名稱。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的 API 專屬回應參數，請參見下表。更多資訊請參考[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Items |[Items](https://docs.byteplus.com/en/docs/24/107426#items) 陣列 |`-` |已刪除的重寫規則清單。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 請求範例

```json
POST https://open.byteplusapi.com/?Action=DeleteRelaySourceRewrite&Version=2023-01-01
{
    "Domain": "push.example.com",
    "Vhost": "pull.example.com"
}
```


<span id="Sample response"></span>
### 回應範例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DeleteRelaySourceRewrite",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
