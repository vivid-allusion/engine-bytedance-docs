---
title: "DescribeRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-dakt2mfojk"
---

Queries origin address rewrite rules. The origin address rewrite feature enables fetching the stream from a new address based on predefined matching rules. For details, see [Origin address rewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite).

<span id="requirements"></span>
## Requirements

Rate limit：10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeRelaySourceRewrite&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeRelaySourceRewrite` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|Domain |String |No |`pull.example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RelaySourceRewriteList |Object of [RelaySourceRewriteList](https://docs.byteplus.com/en/docs/24/7743#relaysourcerewritelist) |`None` |Origin address rewrite configurations |


<span id="relaysourcerewritelist"></span>
### RelaySourceRewriteList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name apace. |
|Domain |String |`pull.example.com` |The domain name. |
|RewriteRule |Object of [RewriteRule](https://docs.byteplus.com/en/docs/24/7743#rewriterule) |`None` |The origin address rewrite configurations. |


<span id="rewriterule"></span>
### RewriteRule


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Enable |Boolean |`true` |Whether origin address rewrite is enabled. |
|RewriteRuleList |Array of [RewriteRuleList](https://docs.byteplus.com/en/docs/24/7743#rewriterulelist) |`None` |A list of rewrite rules. |


<span id="rewriterulelist"></span>
### RewriteRuleList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TargetPath |String |`/app/live/$1` |The new path. |
|OriginPath |String |`/example/$2` |The existing path. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeRelaySourceRewrite&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "Domain": "pull.example.com"
}
```


<span id="sample-response"></span>
### Sample response

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


&nbsp;
