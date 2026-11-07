---
title: "DeleteBucketEncryption"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletebucketencryption"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface deletes the server\-side encryption configuration of a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Only North China 2 (Beijing), East China 2 (Shanghai), Asia Pacific Southeast (Johor), and Asia Pacific Southeast (Jakarta) regions support the DeleteBucketEncryption interface.

* Only users with `tos:DeleteBucketEncryption` permission can call the DeleteBucketEncryption interface. By default, the bucket owner has `tos:DeleteBucketEncryption` permission directly, and the owner can grant this permission to other users.

* HNS buckets do not support the DeleteBucketEncryption interface yet.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
DELETE /?encryption HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses the public request headers. See [Public Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|encryption |Query |String |Yes |\- |Represents a special identifier for the DeleteBucketEncryption request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## **Request body elements**

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## **Response headers**

This request returns the public response headers. See [Public Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## **Response body elements**

No elements are used.

<span id=".6K-35rGC56S65L6L"></span>
## **Sample request**

```JSON
DELETE /?encryption HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## **Sample response**

```JSON
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
