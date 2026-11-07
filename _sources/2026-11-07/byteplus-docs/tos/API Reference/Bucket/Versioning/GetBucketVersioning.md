---
title: "GetBucketVersioning"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Getbucketversioning"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface retrieves the versioning status of a bucket.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Only users with `GetBucketVersioning` permission can call the `GetBucketVersioning` interface. By default, the bucket owner has direct `GetBucketVersioning` permission; the owner can also grant this permission to other users. For detailed instructions on managing permissions using bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

* HNS buckets do not support the GetBucketVersioning interface.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
GET /?versioning HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

The public request headers used by this request; see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|versioning |Query |String |Yes |\- |Special identifier representing the GetBucketVersioning request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

The public response headers returned by this request; see [public parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements


|**Name** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |Enabled |Versioning status of the bucket, with the following values:<br><br><br>* `Enabled`: Versioning is enabled.<br><br>* `Suspended`: Versioning is suspended.<br><br>* Empty: Versioning is not enabled. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
GET /?versioning HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Wed, 20 Sep 2023 02:39:48 GMT
Authorization: authorization string
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
x-tos-id-2: ef60010a5b74f967650a5b74-ac1a2718-1qin80-GBV-cb-tos-front-aza-1        
x-tos-request-id: ef60010a5b74f967650a5b74-ac1a2718-1qin80-GBV-cb-tos-front-aza-1          
Date: Wed, 20 Sep 2023 02:28:54 GMT
Content-Length: 20
server: TosServer

{
    "Status": "Enabled"
}
```
