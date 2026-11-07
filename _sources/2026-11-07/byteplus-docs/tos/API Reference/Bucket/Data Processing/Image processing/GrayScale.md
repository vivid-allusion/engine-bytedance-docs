---
title: "GrayScale"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GrayScale"
---

<span id="a180eac4"></span>
## Description

This interface sets the image to grayscale.

<span id="4fa4202b"></span>
## Notes

Confirm the relevant restrictions before using this interface. For details, see [Usage restrictions](https://docs.byteplus.com/docs/tos/docs-overview_2?lang=en#usage-restrictions).

<span id="ab3b6e8f"></span>
## Request syntax

```TypeScript
GET /<ObjectKey>?x-tos-process=image/colorspace,gray HTTP/1.1
Host: examplebucket-1250000000.vol.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:
Content-Length: 64

[Object]
```


<span id="0f91f283"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Field name** |**Location** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-process |Query |String |Yes |image/colorspace,gray |Data processing type, values are image/colorspace,gray. |


<span id="2a64f58c"></span>
## Request body elements


|**Field name** |**Type** |**Required** |**Example value** |**Description** |
|---|---|---|---|---|
|gray |String |Yes |gray |Convert to grayscale, currently only supports the value `gray`. |


<span id="4f92bd58"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="ef4545b2"></span>
## Response body elements

Returns result image content.

<span id="dce26f64"></span>
## Sample request

```TypeScript
GET /<ObjectKey>?x-tos-process=image/colorspace,gray HTTP/1.1
Host: examplebucket-1250000000.vol.com
Date: Wed, 28 Oct 2015 20:32:00 GMT
Authorization:
Content-Length: 64

[Object]
```


<span id="7a0748ba"></span>
## Sample response

```TypeScript
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 1024

// Result image content
[Object]
```
