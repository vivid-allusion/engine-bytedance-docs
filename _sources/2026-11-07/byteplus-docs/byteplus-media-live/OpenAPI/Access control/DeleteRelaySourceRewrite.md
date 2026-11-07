---
title: "DeleteRelaySourceRewrite"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-3nf0nln2b2"
---

Deletes origin address rewrite rules. The origin address rewrite feature enables fetching the stream from a new address based on predefined matching rules. For details, see [Origin address rewrite](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-origin-address-rewrite).

<span id="requirements"></span>
## Requirements

Rate limit：10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DeleteRelaySourceRewrite&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DeleteRelaySourceRewrite` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |No |`example` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A request without Vhost might match and delete the domain names unintentionally. Consequently, we strongly recommend you specify Vhost.</div><br> |
|Domain |String |No |`example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Items |Array of [Items](https://docs.byteplus.com/en/docs/24/7744#items) |`-` |A list of rewrite rules deleted. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DeleteRelaySourceRewrite&Version=2023-01-01
{
    "Domain": "push.example.com",
    "Vhost": "pull.example.com"
}
```


<span id="sample-response"></span>
### Sample response

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


&nbsp;
