---
title: "DeleteAccessPoint"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteAccessPoint"
---

<span id="ed8189ef"></span>
## Description

`DeleteAccessPoint` interface deletes a specified access point under your account. After deleting an access point, its associated domain names will become invalid.

<span id="776796fe"></span>
## Request syntax

```HTTP
DELETE /accesspoint/{AccessPointName} HTTP/1.1
Host: {BucketName}.tos-cn-beijing.volces.com
Date: GMT Date
Authorization: authorization string
x-tos-account-id: AccountId
```


<span id="c09808d5"></span>
## Request parameters and headers 

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).


|Field name | Location |Type |Required |Example value |Description |
|---|---|---|---|---|---|
|AccessPointName |Path |String |Yes |ap\-test |Name of the access point you want to delete. |
|x\-tos\-account\-id |Header |String |Yes |200\*\*\*\*\*\*\*\* |Specifies the ID of the BytePlus account being reported. |


<span id="c5741106"></span>
## Request body elements

No elements are used.

<span id="98f79b17"></span>
## Response headers

The response contains common headers. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/tos/reference-common-parameters).

<span id="127cbf96"></span>
## Response body elements

The response body of this request is empty.

<span id="732a4241"></span>
## Sample request

```HTTP
DELETE /accesspoint/ap-test HTTP/1.1
Host: tos-control.cn-beijing.volces.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: TOS4-HMAC-SHA256 Credential=AKLT**********/20210730/cn-beijing/tos/request, SignedHeaders=host;x-tos-account-id;x-tos-date, Signature=...
x-tos-account-id: 200********
```


<span id="f2d495e4"></span>
## Sample response

A successful request will return the status code `HTTP/1.1 204 No Content`, and the response body will be empty.
