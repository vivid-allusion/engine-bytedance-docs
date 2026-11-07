---
title: "DeleteBucketMirrorBack"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletebucketmirrorback"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface deletes a bucket's mirror back\-to\-origin rule.

<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
DELETE /?mirror HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers; see [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|mirror |Query |String |Yes |\- |Special identifier representing the DeleteBucketMirrorBack request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns the common response message header. See [common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

This response does not use message elements.

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
DELETE /?mirror HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
