---
title: "GetBucketCustomDomainToken"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketCustomDomainToken"
---

<span id="2c214813"></span>
## Description

This API retrieves the ownership verification token information for a specified custom domain under a storage bucket.

<span id="f2638418"></span>
## Notes


* To call this API, you must be the bucket owner or have been granted `GetBucketCustomDomainToken` permission for the current bucket.

* If the specified domain has never created an ownership verification token, the API will return `NoSuchBucketCustomDomainToken`.


<span id="ed9f9952"></span>
## Request syntax

```Plain Text
GET /?customdomain=example.com&token HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="38a57bca"></span>
## Request parameters and headers 

For common request headers, see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |Type |Required |Sample value |Description |
|---|---|---|---|---|---|
|customdomain |Query |String |Yes |example.com |Custom domain name for the Token to be queried. |
|token |Query |String |Yes |\- |Obtains the unique token for verifying ownership of a custom domain request. |


<span id="a636d529"></span>
## Request body elements

No elements are used.

<span id="47bb6fe0"></span>
## Response headers

The response contains common headers. For more information, see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="28433267"></span>
## Response body elements


| **Name** |Type |Example value |Description |
|---|---|---|---|
|CustomDomainToken |Object |\- |Token information for custom domain ownership verification. |
|Domain |String |example.com |Custom domain pending ownership validation. |
|Token |String |csdafkjadsifjdsf |Domain ownership verification token. |
|ExpireTime |Int64 |1768292477445 |Token expiration timestamp. |
|Verified |Bool |false |Whether the domain ownership has been verified. The options are as follows:<br><br><br>* `true`: Verified.<br><br>* `false`: verification failed. |


<span id="b29a511a"></span>
## Sample request

```Plain Text
GET /?customdomain=example.com&token HTTP/1.1
Host: bucketname.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="1f89fbf5"></span>
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


<span id="ea7f9d96"></span>
## Error code


|Error codes |HTTP status code |Description |
|---|---|---|
|AccessDenied |403 |No operation permission. |
|InvalidParams |400 |`customdomain` parameter is empty or invalid. |
|NoSuchBucketCustomDomainToken |404 |The specified custom domain token does not exist. |
