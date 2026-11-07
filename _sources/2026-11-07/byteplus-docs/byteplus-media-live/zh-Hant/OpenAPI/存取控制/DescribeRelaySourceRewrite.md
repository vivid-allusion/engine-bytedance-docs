---
title: "DescribeRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dakt2mfojk-zh-TW"
---

查詢源地址重寫規則。源地址重寫功能可根據預設的匹配規則，從新的地址拉取串流。詳情請參見[源地址重寫](https://docs.byteplus.com/en/byteplus-media-live/docs/origin-address-rewrite)。

<span id="Requirements"></span>
## 需求

頻率限制：每個帳戶每秒最多查詢10次。

<span id="HTTP request"></span>
## HTTP請求


* 方法：POST

* 端點：https://open.byteplusapi.com/?Action=DescribeRelaySourceRewrite&Version=2023\-01\-01


<span id="Request parameters"></span>
## 請求參數

<span id="Common parameters"></span>
### 通用參數

所有API除了專屬參數外，還必須帶上[通用參數](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查詢


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Action |String |是 |`*DescribeRelaySourceRewrite*` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。目前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body參數


|**參數** |**資料型別** |**是否必填** |**範例值** |**說明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |網域名稱空間。你可以呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面取得該網域所屬的名稱空間。 |
|Domain |String |否 |`pull.example.com` |拉流網域名稱。你可以呼叫[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)頁面取得網域名稱。 |


<span id="Response parameters"></span>
## 回應參數

有關唯一的API專屬回應參數，請參見下表。更多詳情請參見[請求回應](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章節。


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|RelaySourceRewriteList |[RelaySourceRewriteList](https://docs.byteplus.com/en/docs/24/107374#relaysourcerewritelist)物件 |`無` |源地址重寫設定 |


<span id="relaysourcerewritelist"></span>
### RelaySourceRewriteList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Vhost |String |`push.example.com` |網域名稱空間。 |
|Domain |String |`pull.example.com` |網域名稱。 |
|RewriteRule |[RewriteRule](https://docs.byteplus.com/en/docs/24/107374#rewriterule)物件 |`無` |源地址重寫設定。 |


<span id="rewriterule"></span>
### RewriteRule


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|Enable |Boolean |`true` |是否啟用源地址重寫。 |
|RewriteRuleList |[RewriteRuleList](https://docs.byteplus.com/en/docs/24/107374#rewriterulelist)陣列 |`無` |重寫規則列表。 |


<span id="rewriterulelist"></span>
### RewriteRuleList


|**參數** |**資料型別** |**範例值** |**說明** |
|---|---|---|---|
|TargetPath |String |`/app/live/$1` |新路徑。 |
|OriginPath |String |`/example/$2` |現有路徑。 |


<span id="Samples"></span>
## 範例

<span id="Sample request"></span>
### 範例請求

```json
POST https://open.byteplusapi.com/?Action=DescribeRelaySourceRewrite&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```


<span id="Sample response"></span>
### 範例回應

```json
{
    "ResponseMetadata": {
        "RequestId": "202306041104200100100232280022D31",
        "Action": "DescribeRelaySourceRewrite",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "RelaySourceRewriteList": {
            "Domain": "push.example.com",
            "Vhost": "pull.example.com",
            "RewriteRules": {
                "Enable": true,
                "RewriteRuleList": [
                    {
                        "TargetPath": "/app/live/$1",
                        "OriginPath": "/app/live/$2"
                    }
                ]
            }
        }
    }
}
```
