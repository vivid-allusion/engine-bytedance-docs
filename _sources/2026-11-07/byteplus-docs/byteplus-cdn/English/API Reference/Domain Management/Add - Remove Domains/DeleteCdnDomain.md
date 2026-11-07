---
title: "DeleteCdnDomain"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-deletecdndomain"
---

Delete the specified domain name. After the domain name is deleted, you will not be able to view the configuration or historical data of the domain name.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DeleteCdnDomain&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DeleteCdnDomain`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Indicates the domain name you want to delete. |`www.example.com` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DeleteCdnDomain&Version=2021-03-01
{
  "Domain": "www.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202109152017370101941000541800CE83",
    "Action": "DeleteCdnDomain",
    "Version": "2021-03-01",
    "Service": "CDN",
    "Region": "ap-singapore-1"
  }
}
```


&nbsp;
