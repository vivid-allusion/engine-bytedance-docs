---
title: "DeleteBucketRename"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletebucketrename"
---

<span id="d1fd76d4"></span>
## Description

Call the DeleteBucketRename interface to disable the RenameObject feature.

<span id="3843aa6e"></span>
## **Request syntax**

```JSON
DELETE /?rename HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="afa3b065"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|rename |Query |String |Yes |\- |Only the parameter name needs to be set, without setting the value, representing the special identifier for the DeleteBucketRename request. |


<span id="cd5cceac"></span>
## **Request body elements**

This request does not use message elements.

<span id="a2ca8019"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="30f85a2c"></span>
## **Response body elements**

There is no message element in this request response.

<span id="deb3af35"></span>
## **Sample request**

```JSON
DELETE /?rename HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="261c239a"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
