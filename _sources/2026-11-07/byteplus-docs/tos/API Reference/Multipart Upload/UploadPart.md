---
title: "UploadPart"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-uploadpart"
---

<span id="650c3f3b"></span>
## **Description**

This API is used to upload part data. Before calling this API, you need to initialize a multipart upload task using the [CreateMultipartUpload](https://docs.byteplus.com/en/tos/reference/createmultipartupload) API and obtain the `UploadId` for the task. The part `ETag` is returned after each successful upload. Each uploaded part in a multipart upload task has a unique `partNumber`. If you upload a new part using the same `partNumber` that was used with a previous part, the previously uploaded part is overwritten. You can upload multiple parts simultaneously in one upload task of an object, and the upload order does not affect the final merge outcome.

All except the last part must be at least 5 MB in size. Part numbers can be any number from 1 to 10,000, inclusive.

<span id="a9634697"></span>
## Server\-side encryption

With server\-side encryption enabled, TOS encrypts the data you upload at the file level and stores the encrypted data permanently. When you download a file, TOS automatically decrypts and returns the data to you. If server\-side encryption with customer\-provided keys (SSE\-C) is used, the request must carry the same SSE\-C headers as in the `CreateMultiPartUpload` request.

TOS supports server\-side encryption for multipart uploads. Unless you use SSE\-C encryption, you don't need to include encryption parameters in each `UploadPart` request. Instead, you only need to specify the server\-side encryption parameters in the initial `CreateMultiPartUpload` request. For more information, see [CreateMultipartUpload](https://docs.byteplus.com/en/tos/reference/createmultipartupload).

If you specify to use SSE\-C in the `CreateMultiPartUpload` request, you must include the following headers in each `UploadPart` request:


* x\-tos\-server\-side\-encryption\-customer\-algorithm

* x\-tos\-server\-side\-encryption\-customer\-key

* x\-tos\-server\-side\-encryption\-customer\-key\-MD5


<span id="4d77c459"></span>
## **Request syntax**

```JSON
PUT /objectName?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-Length: length

<part content>
```


<span id="117e46e2"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|partNumber |Query |Integer |Yes |1 |Number of the uploaded part. Value range: [1,10000]. |
|uploadId |Query |String |Yes |f93f6fc9da94371f321e1008 |Multipart upload task ID returned in the initialization response, which uniquely identifies the created object. |
|Content\-Length |Header |Integer |Yes |100 |Length of the message body. |
|Content\-MD5 |Header |String |No |XrY7u+Ae7tCTyyK7j1rNww== |Base64\-encoded MD5 digest of the message body. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm used for SSE\-C encrypting the object. Valid value:<br><br><br>* AES256: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |1234567890abcdefghijklmnopqrstuv |Used with x\-tos\-server\-side\-encryption\-customer\-algorithm to specify the key used for SSE\-C encrypting the object. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-traffic\-limit |Header |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |


<span id="ad0688ae"></span>
## **Request body elements**

No elements are used.

<span id="cc2c7a83"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-server\-side\-encryption |String |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |When SSE\-KMS encryption is used for the object, this header is returned, indicating the KMS master key ID used for SSE\-KMS encryption. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |Algorithm used for encrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |MD5 value of the encryption key, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br>If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response. |


<span id="c54e6592"></span>
## **Response body elements**

No elements are used.

<span id="8438976d"></span>
## **Sample request**

```JSON
PUT /objectName?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 00:09:01 GMT
Authorization: authorization string
Content-Length: 102400

<102400 Byte part content>
```


<span id="6d52d768"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130c7d9d0036-a444ed0
x-tos-request-id: 4fac130c7d9d0036-a444ed0
x-tos-hash-crc64ecma: 6186290338114851376
Date: Fri, 30 Jul 2021 00:09:01 GMT
server: TosServer
ETag: "ef176a6c424f954fa42d4cde03949897"
Content-Length: 0
```
