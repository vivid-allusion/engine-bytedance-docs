---
title: "ListCacheSharedDomains"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/ListCacheSharedDomains_en-us"
---

Retrieves created shared cache configurations. You can specify filtering conditions to filter the configurations returned by the API.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `ListCacheSharedDomains`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|PrimaryDomain |String |No |Represents a domain name. Retrieves shared cache configurations where this domain name is the target domain.<br><br>If this parameter is not specified, this filtering condition is not applied.<br><br>Only one of `PrimaryDomain` or `SecondaryDomain` can be specified. |`example` |
|SecondaryDomain |String |No |Represents a domain name. Retrieves shared cache configurations that include this domain name in the shared cache domain list.<br><br>If this parameter is not specified, this filtering condition is not applied. |`example.net` |
|ExactMatch |Boolean |No |Indicates whether CDN uses exact matching when matching `PrimaryDomain` or `SecondaryDomain` with domains in the configurations. The parameter has the following values:<br><br><br>* `true`: Indicates exact matching.<br><br>* `false`: Indicates fuzzy matching.<br><br><br>The default value is `false`. |`false` |
|PageSize |Long |No |This API paginates the retrieved configurations. This parameter indicates the number of configurations per page. The value can range from 1 to 100, and the default value is `10`. |`10` |
|PageNum |Long |No |Indicates which page of configurations to display. The default value is `1`. |`1` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Data |Object[] |Represents the list of shared cache configurations returned by this API. | |
|CacheSharedOn |String |Represents a list of configured domains. Multiple domains are separated by commas (,). |`www.example.com,abc.example.com` |
|TargetHost |String |Represents the target domain name. |`www.example.com` |
|UpdateTime |Long |Represents the last update time of the configuration, in Unix timestamp format with seconds as the unit. |`1755831922` |
|PageNumber |Long |Represents the `PageNumber` you specified. |`1` |
|PageSize |Long |Represents the `PageSize` you specified. |`10` |
|Total |Long |Represents the number of configurations that meet the filtering conditions. |`3` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=ListCacheSharedDomains&Version=2021-03-01
{
    "ExactMatch": false,
    "PrimaryDomain": "example"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250910102143FC1FDB61C3CFED0130C4",
        "Action": "ListCacheSharedDomains",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CacheSharedOn": "www.example.com,abc.example.com",
                "TargetHost": "www.example.net",
                "UpdateTime": 1755831922
            },
            {
                "CacheSharedOn": "docs.example.com",
                "TargetHost": "docs.example.net",
                "UpdateTime": 1749631703
            }
        ],
        "PageNumber": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
