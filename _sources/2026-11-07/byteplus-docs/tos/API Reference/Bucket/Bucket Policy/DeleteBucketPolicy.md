---
title: "DeleteBucketPolicy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-deletebucketpolicy"
---

<span id="33337d75"></span>
## **Description**

This API is used to delete the bucket policy of a bucket.

<span id="08e8e273"></span>
## Note

This API must be called by the bucket owner or subaccounts of the bucket owner with the DeleteBucketPolicy permission for the bucket. For detailed instructions on how to achieve access control using bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/en/tos/docs/overview_5).

<span id="108c8011"></span>
## **Request syntax**

```JSON
DELETE /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="a98e173f"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|policy |Query |String |Yes |\- |Identifies a DeleteBucketPolicy request. |


<span id="dc1100f2"></span>
## **Request body elements**

No elements are used.

<span id="a899e643"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="89c2f33d"></span>
## **Response body elements**

No elements are used.

<span id="ad05ac9e"></span>
## **Sample request**

```JSON
DELETE /?policy HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="1d92cb28"></span>
## **Sample response**

```JSON
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
