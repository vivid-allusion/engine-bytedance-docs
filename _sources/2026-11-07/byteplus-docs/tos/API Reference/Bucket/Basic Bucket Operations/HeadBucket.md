---
title: "HeadBucket"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-headbucket"
---

<span id="5236641f"></span>
## **Description**

This API is used to determine whether a bucket exists and whether the requesting user has access to it.

It returns a `200 OK` status code if both answers are yes. If the bucket does not exist or the user does not have access, `404 Not Found` or `403 Forbidden` is returned.

<span id="6f96f9ba"></span>
## **Request syntax**

```Plain
HEAD / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="d1db7c28"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="9122b112"></span>
## **Request body elements**

No elements are used.

<span id="2ebafe21"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-bucket\-region |String |The bucket region. |
|x\-tos\-storage\-class |String |The default storage type of the bucket. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`:Cold Archive Storage.<br><br>* `DEEP_COLD_ARCHIVE`:Deep Cold Archive Storage. |


<span id="eeea3ebf"></span>
## **Response body elements**

No elements are used.

<span id="7fdd440a"></span>
## **Sample request**

```Plain
HEAD / HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id="b4f057b4"></span>
## **Sample response**

```Plain
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 08:05:36 GMT
Server: TosServer
x-tos-id-2: d242440bbb9b000e-a444ed0
x-tos-request-id: d242440bbb9b000e-a444ed0
x-tos-bucket-region: ap-southeast-1
x-tos-storage-class: STANDARD
```
