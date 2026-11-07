---
title: "DeleteVideoWatermarkTemplate"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteVideoWatermarkTemplate"
---

<span id="faa67e2b"></span>
## Description

This interface deletes a clear watermark template.

<span id="87450004"></span>
## Notes

When using a sub\-account, grant the `DeleteDataProcessTemplate` permission on the current bucket.

<span id="0549a6bb"></span>
## Request syntax

```Python
DELETE /?process_template&id={ID} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="9bce43e9"></span>
## Request parameters and headers 


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|ID |String |No |\- |Watermark template ID. If no ID is specified, all watermark templates will be deleted. |


<span id="37d42870"></span>
## Request body elements

No elements are used.

<span id="6995b3f6"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="909d0aaa"></span>
## Response body elements

This request does not use response body elements.

<span id="4469e5b4"></span>
## Sample request

```Python
DELETE /?process_template&id={ID} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="e28c0c7d"></span>
## Sample response

```Python
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
