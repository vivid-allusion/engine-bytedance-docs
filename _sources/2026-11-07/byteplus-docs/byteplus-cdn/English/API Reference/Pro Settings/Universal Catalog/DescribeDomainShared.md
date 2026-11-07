---
title: "DescribeDomainShared"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDomainShared_en"
---

Specify a universal catalog to get the domain names associated with the universal catalog.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeDomainShared`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConfigName |String |No |Indicates the name of a universal catalog and queries the domain names associated with the universal catalog. |`my_list` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|ConfigName |String |Indicates the name of the universal catalog. |`my_list` |
|Domain |String[] |Indicates a list of domain names associated with the universal catalog. If the universal catalog is not associated with any domain names, the parameter value will be an empty array.<br><br>When calling this API, if the IAM account does not have permission to access a domain name associated with the universal catalog, that domain name will not appear in the `Domain` list. |`["example.com","www.example.com"]` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDomainShared&Version=2021-03-01
{
    "ConfigName":"test11"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241209063311CB50419F0326B7CA55A4",
        "Action": "DescribeDomainShared",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ConfigName": "test11",
        "Domain": [
            "www.example.com"
        ]
    }
}
```


&nbsp;
