---
title: "DeleteBucketLifecycle"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-deletebucketlifecycle"
---

<span id="1894066e"></span>
## **Description**

This API is used to delete the lifecycle rules of a bucket.

<span id="274d3255"></span>
## **Request syntax**

```JSON
DELETE /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="6a2c4144"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|lifecycle |Query |String |Yes |\- |Identifies a DeleteBucketLifecycle request. |


<span id="0bcfadef"></span>
## **Request body elements**

No elements are used.

<span id="d4188b49"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="c886c4a0"></span>
## **Response body elements**

No elements are used.

<span id="da865b09"></span>
## **Sample request**

```JSON
DELETE /?lifecycle HTTP/1.1
Host: bucket-name.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
```


<span id="0aa3d5fb"></span>
## **Sample response**

```JSON
HTTP/1.1 204 OK
Date: Fri, 30 Jul 2021 13:53:55 GMT
Server: TosServer
x-tos-id-2: 1e89f203jld00006-a444fd0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a nonexistent lifecycle rule is deleted, a 204 status code is also returned.</div>
