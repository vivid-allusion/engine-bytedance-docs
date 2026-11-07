---
title: "GetObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference--getobject"
---

## **Description**

This API is used to download a specified object from a bucket. You must be either the bucket owner or an authorized user to use this API. For versioning\-enabled buckets, if the version to download is unspecified, this API returns the current version of the object; if a `versionId` is provided, the corresponding version is returned.

## Server\-side encryption

If the object to download is encrypted with SSE\-TOS, do not include encryption\-related headers, such as `x-tos-server-side-encryption`, in the GET request; otherwise, you will receive an HTTP 400 BadRequest error.

If the requested object was SSE\-C encrypted when it was uploaded, your request must include the following headers:

* x\-tos\-server\-side\-encryption\-customer\-algorithm

* x\-tos\-server\-side\-encryption\-customer\-key

* x\-tos\-server\-side\-encryption\-customer\-key\-MD5

## **Request syntax**

```JSON
GET /objectName HTTP/1.1
Host: destbucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```

## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|Range |Header |String |No |bytes=0\-4 |Specifies the byte range of the object to return. If this parameter is unset, the server returns the entire object. This parameter accepts a range as its value, allowing a lower limit down to 0 and an upper limit up to object length \- 1 in bytes. The lower limit of the range is required. If only the lower limit is indicated, the server returns the object content from the lower limit to the end. Syntax: bytes=start\-end.<br><br>> **tip**<br><br><br>> The ETag in the response is the ETag for the object, not the range, even if the Range header is specified.<br> |
|If\-Match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |The object is returned only if it has a matching ETag; otherwise, 412 Precondition Failed is returned. |
|If\-Modified\-Since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |The object is returned only if it has been modified since the specified time; otherwise, 304 Not Modified is returned. Use GMT time in RFC 1123 format. |
|If\-None\-Match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |The object is returned only if it has a different ETag; otherwise, 304 Not Modified is returned. |
|If\-Unmodified\-Since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |The object is returned only if it has not been modified since the specified time; otherwise, 412 Precondition Failed is returned. Use GMT time in RFC 1123 format. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm used for decrypting an SSE\-C encrypted object. Valid value:<br><br><br>* AES256: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |1234567890abcdefghijklmnopqrstuv |Used with x\-tos\-server\-side\-encryption\-customer\-algorithm to specify the key used for decrypting an SSE\-C encrypted object. |
|x\-tos\-server\-side\-encryption\-customer\-key\-md5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-traffic\-limit |Header |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|response\-content\-disposition |Query |String |No |attachment; filename=123.txt |Specifies the value of the Content\-Disposition response header returned by the server. |
|response\-content\-encoding |Query |String |No |gzip |Specifies the value of the Content\-Encoding response header returned by the server. |
|response\-content\-language |Query |String |No |en\-US |Specifies the value of the Content\-Language response header returned by the server. |
|response\-content\-type |Query |String |No |text/plain |Specifies the value of the Content\-Type response header returned by the server. |
|response\-expires |Query |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Specifies the value of the Expires response header returned by the server. |
|versionId |Query |String |No |123 |ID of the desired object version. |

## **Request body elements**

No elements are used.

## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

|**Name** |**Type** |**Description** |
|---|---|---|
|Content\-Range |String |Range of the object data returned. |
|Last\-Modified |String |Last modified date of the object. |
|x\-tos\-delete\-marker |Bool |Indicates whether the object has been marked as deleted. If not, the header will not appear in the response. |
|x\-tos\-server\-side\-encryption |String |Server\-side encryption method of the object, which is returned if the object is SSE\-TOS encrypted. Valid values:<br><br>`AES256`: Use SSE\-TOS. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |Algorithm used for decrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |MD5 value of the decryption key, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-version\-id |String |Version ID of the object. This header will not appear in the response if the object has no version ID. |
|x\-tos\-website\-redirect\-location |String |For buckets with a Website configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata. |
|x\-tos\-object\-type |String |This header is returned for non\-Normal objects. Valid value:<br><br>Appendable: The object is uploaded using the AppendObject API. |
|x\-tos\-storage\-class |String |Storage type of the object. For detailed information, please refer to [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type). |
|x\-tos\-storage\-tier |String |The access level of the intelligent tiered object, with values described as follows:<br><br><br>* `FREQUENT`: Frequent Access tier of Intelligent Tiered Storage<br><br>* `INFREQUENT`: Infrequent Access tier of Intelligent Tiered Storage<br><br>* `ARCHIVEFR`: Flashback Archive tier of Intelligent Tiered Storage<br><br><br>> **tip**<br><br><br>> The `x-tos-storage-tier` parameter is returned only for intelligent tiered objects.<br> |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br>> **tip**<br><br><br>> If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response.<br> |
|x‑tos‑tagging‑count |String |Number of the object tags,which is returned only if you have read permission for the tags. |
|X\-Tos\-Expiration |String |The expiration date of the object exists in two situations:<br><br><br>* If the object matches the deletion rules of the lifecycle, the following parameters will be returned:<br><br>   * `expiry-date`: Expiration date of the object.<br><br>   * `rule-id`: Lifecycle Rule ID.<br><br>* If the object has an expiration time set, the expiry\-date parameter will be returned, indicating the expiration date of the object, while the rule\-id parameter will be empty. |
|x\-tos\-replication\-status |String |There are two scenarios for the replication status of objects, whether across regions or within the same region:<br><br><br>* If the object is in the source bucket, the parameter value is as follows:<br><br>   * `COMPLETE`: The object has been successfully copied to the destination bucket.<br><br>   * `PENDING`: The object is currently being copied.<br><br>   * `FAILED`: The object failed to copy.<br><br>* If the object belongs to the destination bucket, this parameter has only one value, which is REPLICA, indicating that the object has been synchronized through cross\-region replication or intra\-region replication functionality.<br><br><br>> **warning**<br><br><br><br>* > The function of querying the cross\-region replication or same\-region replication status (i.e. x\-tos\-replication\-status parameter) is currently in the invitation testing phase. If you need to use this function, please contact your account manager.<br><br><br>* > This parameter will only be returned when the object is part of a cross\-region replication or same\-region replication rule with the source or destination bucket.<br><br><br>* > Only supports querying the replication status of objects from a source bucket that has been configured with either a cross\-region replication rule or an intra\-region replication rule. For example, if there are multiple replication rules set up in the source bucket to replicate object A to buckets B, C, and D, querying the replication status of object A is not supported. There is no such limitation for objects in the destination bucket.<br> |
|x\-tos\-restore |String |If the object has a storage class of ARCHIVE, it will return the copy deletion time, for example ongoing\-request="false", expiry\-date="Sat, 1 Jan 2022 00:00:00 GMT". |
|x\-tos\-qos\-delay\-time |Integer |This header field indicates the duration of the request being rate\-limited, in milliseconds. Upload requests will return the exact duration of being rate\-limited; copy or download requests will return an estimated duration of being rate\-limited based on the degree of rate limiting and file size. |
|x\-tos\-directory |Bool |This header field will be returned if the bucket type is hierarchical bucket and the file type is directory. |
|x\-tos\-create\-time |String |Creation date of the object. |
|x\-tos\-object\-lock\-mode |String |The mode of the object retention policy can only be `COMPLIANCE`, which indicates compliance mode.<br><br>> **tip**<br><br><br>> Your account must have the `GetObjectRetention` permission for the `x-tos-object-lock-mode` parameter to be returned.<br> |
|x\-tos\-object\-lock\-retain\-until\-date |String |The lock expiration date of the object specifies the period during which the object cannot be deleted or overwritten.<br><br>> **tip**<br><br><br>> Your account must have the `GetObjectRetention` permission for the `x-tos-object-lock-retain-until-date` parameter to be returned.<br> |

## **Response body elements**

No elements are used.

## **Sample request**

```JSON
GET /objectName HTTP/1.1
Host: destbucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```

## **Sample response**

```JSON
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 120
Date: Fri, 30 Jul 2021 08:05:36 GMT
ETag: "900150983cd24fb0d6963f7d28e17f72"
Last-Modified: Mon, 02 Jul 2021 10:29:28 GMT
server: TosServer
x-tos-id-2: d604607e63b001f-a444ed0
x-tos-request-id: d604607e63b001f-a444ed0
x-tos-hash-crc64ecma: 6186290338114851376

[ 120 Bytes object content]
```
