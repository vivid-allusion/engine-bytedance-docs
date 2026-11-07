---
title: "DeleteBucketInventory"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/DeleteBucketInventory"
---

<span id="9499e28a"></span>
## Description

This interface is used to delete an inventory rule specified in a bucket.

<span id="eb725e92"></span>
## **Request syntax**

```JSON
DELETE /?inventory&id=report HTTP/1.1
Host: BucketName.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:59:18 GMT
Authorization: authorization string
```


<span id="ddfa9065"></span>
## Request parameters and headers

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|inventory |Query |String |Yes |\- |Special identification representing DeleteBucketInventory requests. |
|id |Query |String |Yes |report |Bucket inventory name. |


<span id="1322f84a"></span>
## **Request body elements**

No elements are used.

<span id="9e16cd2b"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="ee67b395"></span>
## **Response body elements**

No elements are used.

<span id="11130ad1"></span>
## Request example

```JSON
DELETE /?inventory&id=report HTTP/1.1
Host: BucketName.tos-cn-beijing.bytepluses.com
Date: Fri, 30 Jul 2021 13:53:55 GMT
Authorization: authorization string
```


<span id="691815ae"></span>
## Response example

```JSON
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
