---
title: "DeleteBucketTagging"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletebuckettagging"
---

<span id="3845da29"></span>
## Feature Description

This interface is used to delete the tag information of a specified bucket.

<span id="7752eaef"></span>
## Precautions

Only the bucket owner and users with DeleteBucketTagging permission can delete bucket tags.

<span id="3148f083"></span>
## **Request syntax**

```JSON
DELETE /?tagging HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="ae1bf9f4"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|tagging |Query |String |Yes |\- |Represents the special identifier for the DeleteBucketTagging request. |


<span id="169af421"></span>
## **Request body elements**

This request does not use message elements.

<span id="35ad0088"></span>
## **Response headers**

This request returns the common response message headers, please see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="21150571"></span>
## **Response body elements**

This interface does not use response elements.

<span id="2679260c"></span>
## **Sample request**

```JSON
DELETE /?tagging HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="9e39992f"></span>
## **Sample response**

```JSON
HTTP/1.1 204 OK
Date: Sat, 07 Oct 2023 09:02:23 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
Content-Length: 0
```
