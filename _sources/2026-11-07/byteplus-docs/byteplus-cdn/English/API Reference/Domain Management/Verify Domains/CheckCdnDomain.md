---
title: "CheckCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/CheckCdnDomain_en-us"
---

Verifies the ownership of a specified domain name. Before calling this API, make sure you have created the corresponding TXT record with your DNS provider as prompted in the CDN console.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `CheckCdnDomain`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Represents a domain name to be verified. It can be a wildcard domain. |`www.example.com` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Status |String |Represents the verification result. The parameter can have the following values:<br><br><br>* `fail`: Indicates that the verification failed.<br><br>* `success`: Indicates that the verification passed. |`fail` |
|ErrorMsg |String |Represents the reason for the verification failure. If `Status` is `success`, the parameter value is empty (""). |`some reason` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=CheckCdnDomain&Version=2021-03-01
{
    "Domain": "www.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20241206143123375BE43944CA95D1969A",
        "Action": "CheckCdnDomain",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "ErrorMsg": "some error",
        "Status": "fail"
    }
}
```


&nbsp;
