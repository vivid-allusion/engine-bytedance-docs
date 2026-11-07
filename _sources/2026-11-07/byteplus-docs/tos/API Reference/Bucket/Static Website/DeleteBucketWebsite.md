---
title: "DeleteBucketWebsite"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Deletebucketwebsite"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This API deletes the website configuration of the specified storage bucket (Bucket).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes

You must be the bucket owner or have the DeleteBucketWebsite permission for the current bucket to call this API.

<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
DELETE /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|website |Query |String |Yes |\- |Special identifier representing the DeleteBucketWebsite request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns public response headers. See [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

No elements are used.

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
DELETE /?website HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
