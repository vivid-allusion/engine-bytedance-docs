---
title: "GetBucketRequestPayment"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/GetBucketRequestPayment"
---

<span id="8f8a086d"></span>
## Description

This interface is for viewing the bucket payment mode.

<span id="0de0bbc8"></span>
## Request syntax

```JSON
GET /?requestPayment HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string 
```


<span id="913c80c2"></span>
## Request parameters and headers

This request uses common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|requestPayment |Query |String |Yes |\- |Represents a special identifier for the PutBucketRequestPayment request. |


<span id="432a01a6"></span>
## Request body elements

This request does not require body elements.

<span id="3d97c7b4"></span>
## Response headers

This request returns common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<span id="da6a2043"></span>
## Response body elements


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Payer |String |Requester |Payment modes for buckets are explained as follows:<br><br><br>* `BucketOwner`: the owner pays all costs in this mode.<br><br>* `Requester`: in this mode, the requester pays for traffic and request fees during access, while the bucket owner only pays for storage and other costs. For details, see [Fee Description](https://docs.byteplus.com/docs/tos/Using-requester-pays#62b0c8f8). |


<span id="a961fe27"></span>
## Sample request

```JSON
GET /?requestPayment HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string 
```


<span id="480e99a2"></span>
## Sample response

```JSON
HTTP/1.1 204 No Content
Date: Thu, 19 Jun 2025 07:22:28 GMT
Server: TosServer
x-tos-id-2: 1e89f203b2d00006-a444ed0
x-tos-request-id: 1e89f203b2d00006-a444ed0
{
    "Payer": "Requester"
}
```
