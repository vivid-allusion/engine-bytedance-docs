---
title: "UpdateRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcerewrite-zh-TW"
---

配置原始地址重寫規則。原始地址重寫功能可根據預設的匹配規則，從新的地址拉取串流。詳細資訊請參見[原始地址重寫](https://docs.byteplus.com/en/docs/24/origin-address-rewrite)。

<span id="Requirements"></span>
## 需求


* 前置條件：僅適用於按需拉源任務，以及使用 FLV、HLS 和 RTMP 協議的串流。

* 限制：重寫規則最多為 50 條。

* 頻率限制：每個帳戶每秒最多 10 次查詢。


<span id="HTTP request"></span>
## HTTP 請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=UpdateRelaySourceRewrite&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有 API 除了需帶入 API 專屬參數外，還必須帶入[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`UpdateRelaySourceRewrite` |API 操作名稱。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。你可以呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面取得該網域所屬的網域名稱空間。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">未帶入 Vhost 的請求可能導致網域名稱出現非預期變更。因此，強烈建議你指定 Vhost。</div><br> |
|Domain |String |否 |`pull.example.com` |拉流網域名稱。你可以呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面取得網域名稱。 |
|RewriteRule |[RewriteRule](https://docs.byteplus.com/en/docs/24/107379#rewriterule)物件 |否 |`N/A` |原始地址重寫配置 |


<span id="rewriterule"></span>
### RewriteRule


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Enable |Boolean |是 |`true` |是否啟用原始地址重寫<br><br><br>* `true`：啟用<br><br>* `false`：停用 |
|RewriteRuleList |[RewriteRuleList](https://docs.byteplus.com/en/docs/24/107379#rewriterulelist)陣列 |是 |`N/A` |重寫規則列表 |


<span id="rewriterulelist"></span>
### RewriteRuleList


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|TargetPath |String |否 |`/app/live/$1` |新路徑。你可以使用`${1}`、`${2}`、`${3}`、`${4}`和`${5}`分別代表第一到第五個萬用字元所匹配的內容。路徑必須符合以下要求：<br><br><br>* 路徑不得包含協議及網域名稱，例如`http://example.domain.com`。<br><br>* 路徑必須以`/`開頭。<br><br>* 路徑最多可包含 1,024 個字元。<br><br>* 路徑不得包含兩個連續的星號，即`**`。<br><br>* 路徑不得包含兩個連續的`${`，即`${${`。 |
|OriginPath |String |否 |`/example/(.\*) \|現有路徑。路徑最多可包含五個萬用字元。但請勿使用萬用字元來代表查詢參數。路徑必須符合以下要求： \| |* 路徑不得包含協議及網域名稱，例如`http://example.domain.com`。<br><br>* 路徑必須以`/`開頭。<br><br>* 路徑最多可包含 1,024 個字元。<br><br>* 路徑不得包含兩個連續的星號，即`**`。<br><br>* 路徑不得包含兩個連續的 ${，即`${${`。 |
|IncludeParams |Boolean |否 |`true` |是否將原始路徑的查詢參數包含於新路徑中。<br><br><br>* `true`：包含<br><br>* `false`：不包含 |


<span id="Response parameters"></span>
## 回應參數

此 API 僅在回應中返回[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=UpdateRelaySourceRewrite&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com",
    "RewriteRules": {
        "Enable": true,
        "RewriteRuleList": [
            {
                "TargetPath": "/app/live/$1",
                "OriginPath": "/example/(.*)$",
                "IncludeParams": true
            }
        ]
    }
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "UpdateRelaySourceRewrite",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
