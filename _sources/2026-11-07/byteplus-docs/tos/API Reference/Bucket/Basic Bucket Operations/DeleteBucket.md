---
title: "DeleteBucket"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-deletebucket"
---

<span id="fec8c872"></span>
## **Description**

This API is used to delete a created bucket. Before deletion, make sure that all objects and parts are removed from the bucket.

<span id="9a6635db"></span>
## **Request syntax**

```Plain
DELETE / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="df839333"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="0fe40cc3"></span>
## **Request body elements**

No elements are used.

<span id="be441c5b"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="6ae5dcd3"></span>
## **Response body elements**

No elements are used.

<span id="9ba89d73"></span>
## **Sample request**

```Plain
DELETE / HTTP/1.1
Host: bucketName.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 06:45:39 GMT
Authorization: authorization string
```


<span id="9727a065"></span>
## **Sample response**

```Plain
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 08:05:36 GMT
x-tos-id-2: 7a049d0bb80c000a-a444ed0
x-tos-request-id: 7a049d0bb80c000a-a444ed0
Server: TosServer
```
