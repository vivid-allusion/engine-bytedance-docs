---
title: "DeleteAudioConvertTemplates"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteAudioConvertTemplates"
---

<span id="0cbd839e"></span>
## Description

This interface deletes audio transcoding templates.

<span id="881b5d12"></span>
## Notes

The primary account has full permissions by default, while IAM sub\-users have no permissions by default. If you need to use a sub\-user to perform this operation, the primary account must grant the sub\-user the `DeleteDataProcessTemplate `permission via IAM policy or bucket policy.

<span id="31239f5f"></span>
## Request syntax

```Python
DELETE /?process_template&id={ID} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="e704fb7f"></span>
## Request parameters and headers


|Name |Type |Required |Example value |Description |
|---|---|---|---|---|
|ID |String |No |39316134376136663339611901\*\*\*\*\*\*\*\*\*\* |Audio transcoding template ID. If no ID is specified, all audio transcoding templates will be deleted. |


<span id="d540c52a"></span>
## Request body elements

No elements are used.

<span id="495c64b9"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="1a8389c0"></span>
## Response body elements

This request does not use response body elements.

<span id="605d46fa"></span>
## Sample request

```Python
DELETE /?process_template&id={ID} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="1a63a6ee"></span>
## Sample response

```Python
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
