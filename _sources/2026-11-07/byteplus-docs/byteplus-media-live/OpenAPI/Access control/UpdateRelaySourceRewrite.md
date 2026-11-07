---
title: "UpdateRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updaterelaysourcerewrite"
---

Configures origin address rewrite rules. The origin address rewrite feature enables fetching the stream from a new address based on predefined matching rules. For details, see [Origin address rewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite).

<span id="requirements"></span>
## Requirements


* Prerequisites：Applicable to on\-demanded origin\-pull task and streams that use the FLV, HLS, and RTMP protocols only.

* Limitations：The maximum of rewrite rules is 50.

* Rate limit：10 queries per second per account.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateRelaySourceRewrite&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateRelaySourceRewrite` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A request without Vhost might lead to unintended changes to the domain names. Consequently, we strongly recommend you specify Vhost.</div><br> |
|Domain |String |No |`pull.example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|RewriteRule |Object of [RewriteRule](https://docs.byteplus.com/en/docs/24/7742#rewriterule) |No |`N/A` |The origin address rewrite configurations |


<span id="rewriterule"></span>
### RewriteRule


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Enable |Boolean |Yes |`true` |Whether to enable origin address rewrite<br><br><br>* `true`: Enable<br><br>* `false`: Disable |
|RewriteRuleList |Array of [RewriteRuleList](https://docs.byteplus.com/en/docs/24/7742#rewriterulelist) |Yes |`N/A` |A list of rewrite rules |


<span id="rewriterulelist"></span>
### RewriteRuleList


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TargetPath |String |No |`/app/live/$1` |The new path. You can use `${1}`, `${2}`, `${3}`, `${4}`, and `${5}` to represent the content matched by the first to the fifth wildcards respectively. The path must satisfy the following requirements:<br><br><br>* The path must not contain the protocol and domain name, such as `http://example.domain.com`.<br><br>* The path must start with `/`.<br><br>* The path can contain a maximum of 1,024 characters.<br><br>* The path cannot contain two consecutive asterisks, i.e. `**`.<br><br>* The path cannot contain two consecutive instances of `${`, i.e. `${${`. |
|OriginPath |String |No |`/example/(.\*) \| The existing path. The path may include a maximum of five wildcards. However, do not use wildcards to represent query parameters. The path must satisfy the following requirements: \| |* The path must not contain the protocol and domain name, such as `http://example.domain.com`.<br><br>* The path must start with `/`.<br><br>* The path can contain a maximum of 1,024 characters.<br><br>* The path cannot contain two consecutive asterisks, i.e. `**`.<br><br>* The path cannot contain two consecutive instances of ${, i.e. `${${`. |
|IncludeParams |Boolean |No |`true` |Whether to include the query parameters of the original path in the new path.<br><br><br>* `true`: Include<br><br>* `false`: Exclude |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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


&nbsp;
