---
title: "UpdateCustomLine"
product: "BytePlus DNS Suite"
product_code: "byteplus-dns-suite"
source: "https://docs.byteplus.com/en/docs/byteplus-dns-suite/reference-updatecustomline"
---

Updates an IP\-based line.

<span id="usage"></span>
## Usage


* Rate limit: Maximum 1 call per second.


<span id="request"></span>
## Request


* Method: POST

* URL: https://dns.byteplusapi.com/?Action=UpdateCustomLine&Version=2018\-08\-01


<span id="request-parameters"></span>
## Request parameters

In addition to the following parameters, you also need to include the [authentication parameters](https://docs.byteplus.com/byteplus-dns-suite/reference/calling-an-api-with-http-requests#includedinreqheader).

<span id="query"></span>
### Query


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`UpdateCustomLine` |The name of the API. The value of this parameter is `UpdateCustomLine`. |
|Version |String |Yes |`2018-08-01` |The version of the API. The value of this parameter is `2018-08-01`. |


<span id="body"></span>
### Body


|**Name** |**Type** |**Required** |Example |**Description** |
|---|---|---|---|---|
|Line |String |Yes |`custom-5040` |The ID of the IP\-based line. You can obtain the ID of the IP\-based line from the `Line` parameter returned by the [ListCustomLines API](https://docs.byteplus.com/docs/byteplus-dns-suite/reference-listcustomlines). |
|NameCN |String |No |`IP-based line 2` |The name of the IP\-based line. UTF\-8 format. Maximum length is 32 UTF\-8 characters. If you do not set this parameter, its value remains unchanged. |
|IPSegments |String[] |No |`["192.168.1.0/24"]` |One or more CIDR address blocks for the IP\-based line. Supports both IPv4 and IPv6 addresses. For example, `192.168.1.0/24` or `2001:db8::/103`. If you do not set this parameter, its value remains unchanged. |
|Remark |String |No |`Remark` |The remark for the IP\-based line. UTF\-8 format. Maximum length is 64 UTF\-8 characters. If you do not set this parameter, its value remains unchanged. |


<span id="e7393b5a"></span>
## Response body

<span id="90644f3f"></span>
### ResponseMetadata object


|**Name** |**Type** |**Description** |
|---|---|---|
|RequestId |String |The ID that identifies this request. |
|Action |String |The value of the Action query parameter. |
|Version |String |The version of the API. |
|Service |String |The type of service. |
|Region |String |The region where the service is located. |


<span id="c3707891"></span>
### Result object


|**Name** |**Type** |**Description** |
|---|---|---|
|Line |String |The ID of the IP\-based line. |


<span id="ea55885f"></span>
## Example

<span id="bba8b942"></span>
### Request example

```JSON
POST https://dns.byteplusapi.com/?Version=2018-08-01&Action=UpdateCustomLine

{
  "Line": "custom-5040",
  "NameCN": "mycustomline002",
  "Remark": "create a line",
  "IPSegments": [
       "1.0.0.0/24",
       "10.0.0.0/8"
  ]
}
```


<span id="4b7b4209"></span>
### Response example

```JSON
{
    "ResponseMetadata": {
        "RequestId": "2023041218201639D6CA012808E5147F83",
        "Action": "UpdateCustomLine",
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
