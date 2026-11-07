---
title: "DeleteBucketCustomDomain"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletebucketcustomdomain"
---

<span id="7d31112c"></span>
## **Feature Description**

This interface is used to delete a single custom domain configuration for a specified storage bucket (Bucket).

<span id="f6b57a73"></span>
## Precautions

To invoke this interface, you must be the bucket owner or be authorized the DeleteBucketCustomDomain permission for the current bucket.

<span id="3cc4f65e"></span>
## **Request syntax**

```JSON
DELETE /?customdomain=example.com HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="93c8a721"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|customdomain |Query |String |Yes |customdomain=example.com |Represents a special identifier for the DeleteBucketCustomDomain request, setting the custom domain to be deleted. |


<span id="4983142a"></span>
## **Request body elements**

This request does not use message elements.

<span id="daba774f"></span>
## **Response headers**

This request returns the common response message headers, please see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="9e2f94ce"></span>
## **Response body elements**

This interface does not use response elements

<span id="4758519b"></span>
## **Sample request**

```JSON
DELETE /?customdomain=example.com HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="f8535af2"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
