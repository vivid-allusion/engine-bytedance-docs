---
title: "UploadPartCopy"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-uploadpartcopy"
---

<span id="fcc79ab1"></span>
## **Description**

This API is used to copy part or all of an uploaded object as a part. A request for this API can be created by adding a `x-tos-copy-source` header to a request for [UploadPart](https://docs.byteplus.com/en/tos/reference/uploadpart).

<span id="8c83d5e5"></span>
## **Instructions**


* You must have read access to the source object when using CopyObject or UploadPartCopy.

* You cannot copy data from an object uploaded using AppendObject.

* You must first call the CreateMultipartUpload API to initiate a multipart task and obtain an `UploadId`, and then include that ID in your UploadPartCopy request.

* If the target part already exists, it will be overwritten when you copy the source object. Therefore, make sure the target part is either nonexistent or no longer needed before calling this API to prevent data loss.

* Before using the UploadPartCopy interface to copy objects stored in Archive, Cold Archive, or Deep Cold Archive storage classes, you must first restore the objects to a readable state.


<span id="36d9d6ad"></span>
## **Versioning**

In a versioning\-enabled bucket, an object may have multiple versions. By default, `x-tos-copy-source` identifies the current version of the object to copy. If the current version is a delete marker and you do not specify a `versionId` in `x-tos-copy-source`, TOS returns a 404 Not Found error, because the object no longer exists. If you specify a `versionId` in `x-tos-copy-source` but it corresponds to a delete marker, TOS returns 400 Bad Request, because you are not allowed to specify the `versionId` of a delete marker in `x-tos-copy-source`.

<span id="577e22a5"></span>
## **Request syntax**

```JSON
PUT /objectName?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
x-tos-copy-source: /sourcebucketname/SourceObjectName
x-tos-copy-source-range: bytes=start-end
```


<span id="c874c366"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|partNumber |Query |Integer |Yes |1 |Number of the uploaded part. Value range: [1,10000]. |
|uploadId |Query |String |Yes |f93f6fc9da94371f321e1008 |Multipart upload task ID returned in the initialization response, which uniquely identifies the created object. |
|x\-tos\-copy\-source |Header |String |Yes |/sourcebucketname/SourceObjectName?versionId=xxx |Specifies the source bucket and object. Use versionId to specify the version of a multiversion source object. |
|x\-tos\-copy\-source\-if\-match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |Copies the source object only if it has a matching ETag. |
|x\-tos\-copy\-source\-if\-modified\-since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Copies the object if it has been modified since the specified time. Use GMT time in RFC 1123 format. |
|x\-tos\-copy\-source\-if\-none\-match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |Copies the source object only if it has a different ETag. |
|x\-tos\-copy\-source\-if\-unmodified\-since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Copies the object if it has not been modified since the specified time. Use GMT time in RFC 1123 format. |
|x\-tos\-copy\-source\-range |Header |String |No |bytes=0\-5242880 |Specifies the range of bytes to copy from the source object, allowing a lower limit down to 0 and an upper limit up to object length \- 1 in bytes. Syntax: bytes=start\-end. |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if the source object is SSE\-C encrypted. |AES256 |Specifies the algorithm used for decrypting an SSE\-C encrypted source object. Valid value:<br><br><br>* AES256 |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if the source object is SSE\-C encrypted. |1234567890abcdefghijklmnopqrstuv |Specifies the key used for decrypting an SSE\-C encrypted source object. This must be the same key used for creating the source object. |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if the source object is SSE\-C encrypted. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-traffic\-limit |Header |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm used for SSE\-C encrypting the object. Valid value:<br><br><br>* AES256: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |1234567890abcdefghijklmnopqrstuv |Used with x\-tos\-server\-side\-encryption\-customer\-algorithm to specify the key used for SSE\-C encrypting the object. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |


<span id="df4360b8"></span>
## **Request body elements**

No elements are used.

<span id="7addd23f"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-copy\-source\-version\-id |String |Version ID of the source object, which is returned when you copy a specific version of the source object. |
|x\-tos\-server\-side\-encryption |String |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |When SSE\-KMS encryption is used for the object, this header is returned, indicating the KMS master key ID used for SSE\-KMS encryption. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |Algorithm used for encrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-md5 |String |MD5 value of the SSE\-C encryption key, which is returned if the object is SSE\-C encrypted. |


<span id="1da40ac7"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|ETag |String |ETag of the target part, which is a unique identifier of the part content and is used for data consistency verification during part merge. |
|LastModified |String |Last modified time of the target part. |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response.</div><br> |


<span id="9ff9b4e5"></span>
## **Sample request**

```JSON
PUT /objectName?partNumber=PartNumber&uploadId=UploadId HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 00:12:21 GMT
Authorization: authorization string
x-tos-copy-source: /sourcebucketname/SourceObjectName
x-tos-copy-source-range: bytes=0-5242880
```


<span id="55db3144"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130c7e29003a-a444ed0
x-tos-request-id: 4fac130c7e29003a-a444ed0
x-tos-hash-crc64ecma: 6186290338114851376
Date: Fri, 30 Jul 2021 00:12:21 GMT
server: TosServer

{
    "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
    "LastModified": "2021-08-20T06:45:57.000Z"
}
```
