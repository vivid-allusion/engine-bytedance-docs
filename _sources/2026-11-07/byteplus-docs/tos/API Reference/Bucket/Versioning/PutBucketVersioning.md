---
title: "PutBucketVersioning"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Putbucketversioning"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This interface sets the versioning feature for a bucket. The versioning feature allows multiple versions of the same object within a bucket to be retained simultaneously, preventing accidental deletion or overwriting of objects, and can also be used to archive historical versions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Notes


* Only users with `PutBucketVersioning` permission can invoke the `PutBucketVersioning` interface. By default, the bucket owner directly holds the `PutBucketVersioning` permission, and the bucket owner can grant this permission to other users. For detailed instructions on permission control via bucket policy, refer to [Bucket Authorization Policy Management](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

* The versioning feature of a bucket is disabled by default. For detailed information on the bucket versioning feature, see [Versioning Overview](https://docs.byteplus.com/docs/tos/docs-overview).

* HNS buckets do not support the PutBucketVersioning interface.


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
PUT /?versioning HTTP/1.1 
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string

{ 
    "Status":"Enabled"
}
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers

This request uses common request headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|---|
|versioning |Query |String |Yes |\- |Represents a special identifier for the PutBucketVersioning request. |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements


|**Name** |**Type** |**Required** |**Sample value** |**Note** |
|---|---|---|---|---|
|Status |String |Yes |Enabled |Enable or disable bucket versioning with the following values:<br><br><br>* `Enabled`: enable versioning.<br><br>* `Suspended`: suspend versioning. |


<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns common response headers. See [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements

No elements are used in the response for this request.

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
PUT /?versioning HTTP/1.1 
Host: bucketname.tos-cn-beijing.volces.com
Date: GMT Date
Authorization: authorization string

{ 
    "Status":"Enabled"
}
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 1874010a59fb053f650a59fb-be4a38d-1qin1v-PuO-cb-tos-front-azc-1        
x-tos-request-id: 1874010a59fb053f650a59fb-be4a38d-1qin1v-PuO-cb-tos-front-azc-1            
Date: Wed, 20 Sep 2023 02:28:54 GMT
server: TosServer
Content-Length: 0
```
