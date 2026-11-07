---
title: "CreateCustomLine"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-createcustomline"
---

Creates an IP\-based line.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=CreateCustomLine&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request Parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`CreateCustomLine` |The name of the API. The value of this parameter is `CreateCustomLine`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|NameCN |String |Yes |`IP-based line 1` |The name of the IP\-based line. UTF\-8 format. Maximum length is 32 UTF\-8 characters. |
|IPSegments |String[] |Yes |`["192.168.1.0/24"]` |One or more CIDR address blocks for the IP\-based line. Supports both IPv4 and IPv6 addresses. For example, `192.168.1.0/24` or `2001:db8::/103`. You can add up to 1000 CIDR address blocks. |
|Remark |String |No |`Remark` |The remark for the IP\-based line. UTF\-8 format. Maximum length is 64 UTF\-8 characters. Default is an empty string. |


<span id="response-body"></span>
## Response body

<span id="responsemetadata-object"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="result-object"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|Line |String |The ID of the IP\-based line. |


<span id="example"></span>
## Example

<span id="request-example"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=CreateCustomLine

{
  "NameCN": "customline001",
  "Remark": "create a line",
  "IPSegments": [
       "1.0.0.0/24",
       "10.0.0.0/8"
  ]
}
```


<span id="response-example"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230412181301EDC68E183B4E891214D0",
        "Action": "CreateCustomLine",
        "Version": "2018-08-01",
        "Service": "dns",
        "Region": "singapore"
    },
    "Result": {
        "Line": "custom-5040"
    }
}
```


<span id="common-error-codes"></span>
## Common error codes

Refer to [Common Error Codes](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-handling-the-response).
