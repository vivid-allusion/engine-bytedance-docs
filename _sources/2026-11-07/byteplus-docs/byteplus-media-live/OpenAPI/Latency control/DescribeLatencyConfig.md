---
title: "DescribeLatencyConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelatencyconfig"
---

Call the `DescribeLatencyConfig` API to query the server cache config of the GOP.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeLatencyConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeLatencyConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |No |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Vhost</code> and <code>Domain</code> must be configured at least one.</div><br> |
|Domain |String |No |`pull.example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>Vhost</code> and <code>Domain</code> must be configured at least one.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|LatencyConfigList |Array of [LatencyConfigList](https://docs.byteplus.com/en/docs/24/20104#latencyconfiglist) |`-` |The list of the latency configuration. |


<span id="latencyconfiglist"></span>
### LatencyConfigList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|Domain |String |`pull.example.com` |The domain name. |
|GopCacheSize |String |`2000` |The cache size of an edge server for temporarily storing video content. The cache size is measured in milliseconds. |
|CreateTime |String |`2024-03-25T11:20:47Z` |The UTC time in RFC 3339 format when the configuration was created. |
|UpdateTime |String |`2024-03-25T11:20:47Z` |The UTC time in RFC 3339 format when the configuration was last updated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeLatencyConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "domain": "pull.example.com"
}
```


<span id="sample-response"></span>
### Sample response

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


&nbsp;
