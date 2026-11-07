---
title: "AbortMultipartUpload"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-abortmultipartupload"
---

<span id="26f9cb64"></span>
## **Description**

This API is used to abort a multipart upload task,after which any subsequent upload or listing becomes impossible. Once an upload task is aborted, all related part data is cleared.

<span id="b19e2a6d"></span>
## **Request syntax**

```JSON
DELETE /objectName?uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="93380af7"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|uploadId |Query |String |Yes |f93f6fc9da94371f321e1008 |Identifies a multipart upload task. |


<span id="c53e6d61"></span>
## **Request body elements**

No elements are used.

<span id="1554bd59"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="86e26084"></span>
## **Response body elements**

No elements are used.

<span id="e86027c7"></span>
## **Sample request**

```JSON
DELETE /objectName?uploadId=7fffca8a0509feb42dc5489183bde769 HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 00:09:58 GMT
Authorization: authorization string
```


<span id="86c04346"></span>
## **Sample response**

```JSON
HTTP/1.1 204 No Content
x-tos-id-2: 4fac130c7dd60038-a444ed0
x-tos-request-id: 4fac130c7dd60038-a444ed0
Date: Fri, 30 Jul 2021 00:09:58 GMT
server: TosServer
```
