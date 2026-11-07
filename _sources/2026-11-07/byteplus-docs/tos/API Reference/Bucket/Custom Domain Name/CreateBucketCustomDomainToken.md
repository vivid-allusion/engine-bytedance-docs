---
title: "CreateBucketCustomDomainToken"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/CreateBucketCustomDomainToken"
---

<span id="31eee243"></span>
## Description

This API creates an ownership verification token for a specified bucket’s custom domain. After obtaining the token, add a TXT record to the domain’s DNS to verify domain ownership.

<span id="1c4376d5"></span>
## Notes


* You must be the bucket owner or have the `CreateBucketCustomDomainToken` permission authorized for the current bucket to call this API.

* The token is valid for 72 hours by default and expires afterward.

* The corresponding ownership verification record will be cleared when deleting the custom domain.


<span id="6a79c613"></span>
## Request syntax

```Plain Text
PUT /?customdomain&token HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Type: application/json

{
  "CustomDomainRule": {
    "Domain": "example.com"
  }
}
```


<span id="e3a7e8d0"></span>
## Request parameters and headers 

For common request headers, see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|customdomain |Query |String |Yes |\- |Special identifier for custom domain requests. |
|token |Query |String |Yes |\- |Special identifier for creating custom domain ownership verification token request. |


<span id="e834d003"></span>
## Request body elements


| **Name** |Type |Required |Sample value |Description |
|---|---|---|---|---|
|CustomDomainRule |Object |Yes |\- |Custom domain rule. |
|Domain |String |Yes |example.com |Custom domain pending ownership verification. |


<span id="54cdc41e"></span>
## Response headers

The response contains common headers. For more information, see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="a3c328f5"></span>
## Response body elements


| **Name** |Type |Sample value |Description |
|---|---|---|---|
|CustomDomainToken |Object |\- |Token information for custom domain ownership verification. |
|Domain |String |example.com |Custom domain pending ownership verification |
|Token |String |csdafkjadsifjdsf |Domain ownership verification token. |
|ExpireTime |Int64 |1768292477445 |Token expiration time. |
|Verified |Bool |false |Whether domain ownership has been verified. The options are as follows:<br><br><br>* `true`: verified.<br><br>* `false`: not verified. |


<span id="4d443683"></span>
## Sample request

```Plain Text
PUT /?customdomain&token HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
Content-Type: application/json

{
  "CustomDomainRule": {
    "Domain": "example.com"
  }
}
```


<span id="a0c796af"></span>
## Sample response

```Plain Text
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 128

{
  "CustomDomainToken": {
    "Domain": "example.com",
    "Token": "csdafkjadsifjdsf",
    "ExpireTime": 1768292477445,
    "Verified": false
  }
}
```


<span id="44b95472"></span>
## Error code


|Error codes |Status code |Description |
|---|---|---|
|AccessDenied |403 |No operation permission. |
|InvalidParams |400 |Invalid request body format. |
|TooManyCustomDomainTokens |400 |The number of custom domain tokens exceeds the limit. |
