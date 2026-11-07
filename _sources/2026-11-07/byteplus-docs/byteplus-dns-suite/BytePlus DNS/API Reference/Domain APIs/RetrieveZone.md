---
title: "RetrieveZone"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-retrievezone"
---

Generates domain verification information.

This information is required when BytePlus DNS verifies the ownership of your domain.

<span id="usage"></span>
## Usage


* Rate limit: 1 call per second.


<span id="request"></span>
## Request


* Method: POST

* Address: https://dns.byteplusapi.com/?Action=RetrieveZone?Version=2018\-08\-01


<span id="af0b7d9f"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`RetrieveZone` |The name of the API. The value of this parameter is `RetrieveZone`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|ZoneName |String |Yes |`example.com` |The domain to be verified. The domain must be a second\-level domain and cannot be a wildcard domain. |


<span id="e5a2189f"></span>
## Response body

<span id="d6c6d083"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="20236efe"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|Host |String |The domain prefix in the TXT record. |
|Txt |String |The value of the TXT record. |
|ZoneName |String |The domain name to be verified. |
|IsOwnedByDomain |String |This parameter is not used. Please ignore this parameter. |


<span id="7b441dc3"></span>
## Example

<span id="4f6038df"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=RetrieveZone
{
  "ZoneName": "example.com"
}
```


<span id="3b984c61"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20221101140621010210025044055EEFFA",
        "Action": "RetrieveZone",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "Host": "byteplus-retrieval",
        "Txt": "verify-4ea49976-59ab-11ed-b66f-00163e12d591",
        "ZoneName": "example.com",
        "IsOwnedByDomain": true
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
