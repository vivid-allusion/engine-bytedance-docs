---
title: "DeleteVideoConvertTemplate"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteVideoConvertTemplate"
---

<span id="beff0f82"></span>
## Description

This API deletes video transcode templates.

<span id="5be149b3"></span>
## Notes

When using a sub\-account, the `DeleteDataProcessTemplate` permission must be granted for the current bucket.

<span id="08c51a53"></span>
## Request syntax

```JSON
DELETE /?process_template&id={ID} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="b2a06388"></span>
## Request parameters and headers


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|ID |String |No |34333938323062333934611901\*\*\*\*\*\*\*\*\*\* |Audio and video task ID. If no ID is specified, all audio and video tasks will be listed. |


<span id="364b84c8"></span>
## Request body elements

No elements are used.

<span id="5c0949d3"></span>
## Response headers

The response contains common headers. For more information, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="2dd008b2"></span>
## Response body elements

This request does not use response body elements.

<span id="eb39ba2d"></span>
## Sample request

```JSON
DELETE /?process_template&id={ID} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="43421667"></span>
## Sample response

```JSON
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
