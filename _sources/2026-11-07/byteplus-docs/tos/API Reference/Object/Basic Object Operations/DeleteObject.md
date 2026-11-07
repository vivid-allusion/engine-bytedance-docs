---
title: "DeleteObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-deleteobject"
---

<span id="6b1408b5"></span>
## **Description**

This API is used to delete a specified object from a bucket.

If versioning is enabled for the bucket, calling this API without specifying a version ID creates a delete marker with a newly generated version ID. If versioning is `suspended` for the bucket, calling this API deletes the `null` version of the object and replaces it with a delete marker whose version ID is also `null`. In a versioning\-enabled bucket, specifying a version ID while deleting an object deletes that particular version.

<span id="da8d3191"></span>
## **Request syntax**

```JSON
DELETE /ObjectName HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="f739141b"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|versionId |Query |String |No |123 |ID of the object version to delete. |


<span id="3424457a"></span>
## **Request body elements**

No elements are used.

<span id="46fb85e1"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-delete\-marker |Bool |Indicates whether the object has been marked as deleted. If not, the header will not appear in the response. |
|x\-tos\-version\-id |String |Version ID of the object. It will not appear in the response if the object has no version ID. |


<span id="c013a236"></span>
## **Response body elements**

No elements are used.

<span id="d6122cc0"></span>
## **Sample request**

```JSON
DELETE /objectName HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id="353a4033"></span>
## **Sample response**

```JSON
HTTP/1.1 204 No Content
Date: Fri, 30 Jul 2021 08:05:36 GMT
Server: TosServer
x-tos-id-2: 1e89f203b2d00006-a444ed0
x-tos-request-id: 1e89f203b2d00006-a444ed0
```
