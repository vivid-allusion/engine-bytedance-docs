---
title: "HeadObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-headobject"
---

<span id="3279e92c"></span>
## **Description**

This API retrieves metadata from an object without returning the object itself. It is particularly useful if you are only interested in an object's metadata. To use this API, you must have read permission for the object.

HEAD requests have the same options as GET requests on objects and will get the identical response except that there will be no response body. Therefore, if a HEAD request generates an error, TOS returns a generic 404 Not Found or 403 Forbidden status code.

<span id="844622b2"></span>
## Server\-side encryption

If the object is encrypted with SSE\-TOS , do not include encryption\-related headers, such as `x-tos-server-side-encryption`, in the HEAD request; otherwise, you will receive an HTTP 400 BadRequest error.

If the requested object was SSE\-C encrypted when it was uploaded, your request must include the following headers:


* x\-tos\-server\-side\-encryption\-customer\-algorithm

* x\-tos\-server\-side\-encryption\-customer\-key

* x\-tos\-server\-side\-encryption\-customer\-key\-MD5


<span id="ff059e1d"></span>
## **Request syntax**

```JSON
HEAD /objectName HTTP/1.1
Host: destbucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="01b40016"></span>
## **Request parameters and headers**

For common request headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|If\-Match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |The object metadata is returned only if the object has a matching ETag; otherwise, 412 Precondition Failed is returned. |
|If\-Modified\-Since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |The object metadata is returned only if the object has been modified since the specified time; otherwise, 304 Not Modified is returned. Use GMT time in RFC 1123 format. |
|If\-None\-Match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |The object metadata is returned only if the object has a different ETag; otherwise, 304 Not Modified is returned. |
|If\-Unmodified\-Since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |The object metadata is returned only if the object has not been modified since the specified time; otherwise, 412 Precondition Failed is returned. Use GMT time in RFC 1123 format. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No |AES256 |Specifies the algorithm used for decrypting an SSE\-C encrypted object. Valid value:<br><br><br>* AES256: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No |1234567890abcdefghijklmnopqrstuv |Used with x\-tos\-server\-side\-encryption\-customer\-algorithm to specify the key used for decrypting an SSE\-C encrypted object. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|versionId |Query |String |No |123 |Version ID of the object. Use this to get the metadata of a specific version of the object. |


<span id="d36d2d54"></span>
## **Request body elements**

No elements are used.

<span id="c07fd632"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If the object type is "Appendable", the response will not contain the ETag header.</div>



|**Name** |**Type** |**Description** |
|---|---|---|
|Last\-Modified |String |Last modified time of the object. |
|x\-tos\-delete\-marker |Bool |Indicates whether the object has been marked as deleted. If not, the header will not appear in the response. |
|x\-tos\-server\-side\-encryption |String |Server\-side encryption method of the object, which is returned if the object is SSE\-TOS encrypted. Valid values:<br><br><br>* `AES256`: Use SSE\-TOS. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |Algorithm used for decrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |MD5 value of the decryption key, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-version\-id |String |Version ID of the object. This header will not appear in the response if the object has no version ID. |
|x\-tos\-website\-redirect\-location |String |For buckets with a Website configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata. |
|x\-tos\-object\-type |String |This header is returned for non\-Normal objects. Valid value:<br><br><br>* Appendable: The object is uploaded using the AppendObject API. |
|x\-tos\-storage\-class |String |Storage type of the object. For detailed information, please refer to [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type). |
|x\-tos\-storage\-tier |String |The access level of the intelligent tiered object, with values described as follows:<br><br><br>* `FREQUENT`: Frequent Access tier of Intelligent Tiered Storage<br><br>* `INFREQUENT`: Infrequent Access tier of Intelligent Tiered Storage<br><br>* `ARCHIVEFR`: Flashback Archive tier of Intelligent Tiered Storage<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>x-tos-storage-tier</code> parameter is returned only for intelligent tiered objects.</div><br> |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br>If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response. |
|x\-tos\-tagging\-count |String |Number of the object tags, which is returned only if you have read permission for the tags. |
|X\-Tos\-Expiration |String |The expiration date of the object exists in two situations:<br><br><br>* If the object matches the deletion rules of the lifecycle, the following parameters will be returned:<br><br>   * `expiry-date`: Expiration date of the object.<br><br>   * `rule-id`: Lifecycle rule ID.<br><br>* If the object has an expiration time set, the expiry\-date parameter will be returned, indicating the expiration date of the object, while the rule\-id parameter will be empty. |
|x\-tos\-replication\-status |String |There are two scenarios for the replication status of objects, whether across regions or within the same region:<br><br><br>* If the object is in the source bucket, the parameter value is as follows:<br><br>   * `COMPLETE`: The object has been successfully copied to the destination bucket.<br><br>   * `PENDING`: The object is currently being copied.<br><br>   * `FAILED`: The object failed to copy.<br><br>* If the object belongs to the destination bucket, this parameter has only one value, which is REPLICA, indicating that the object has been synchronized through cross\-region replication or intra\-region replication functionality.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The function of querying the cross\-region replication or same\-region replication status (i.e. x\-tos\-replication\-status parameter) is currently in the invitation testing phase. If you need to use this function, please contact your account manager.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This parameter will only be returned when the object is part of a cross\-region replication or same\-region replication rule with the source or destination bucket.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Only supports querying the replication status of objects from a source bucket that has been configured with either a cross\-region replication rule or an intra\-region replication rule. For example, if there are multiple replication rules set up in the source bucket to replicate object A to buckets B, C, and D, querying the replication status of object A is not supported. There is no such limitation for objects in the destination bucket.</div><br> |
|x\-tos\-restore |String |If the storage type of the object is ARCHIVE and the Restore Object operation has been performed, the following header will be returned to indicate the status:<br><br><br>* If the replica generation is in progress, the return value will be ongoing\-request="true".<br><br>* If a copy has been generated, return the expiration date of the copy, for example ongoing\-request="false", expiry\-date="Sat, 1 Jan 2022 00:00:00 GMT". |
|x\-tos\-restore\-request\-date |String |If the object is of storage class ARCHIVE and a Restore Object operation has been performed, the x\-amz\-restore header will be returned in the copy response, indicating the time when the Restore Object operation was executed. For example, Sat, 1 Jan 2022 00:00:00 GMT. |
|x\-tos\-restore\-expiry\-days |Integer |If the object is of the ARCHIVE storage class and a Restore Object operation has been performed, in the copy generation, this header will be returned to indicate the number of days the copy is valid. |
|x\-tos\-restore\-tier |String |The recovery priority for archived storage objects can only be Standard, which means archived storage objects will be recovered within 1 minute. |
|x\-tos\-directory |Bool |This header field is returned when the bucket type is hierarchical bucket and the file type is directory. |
|x\-tos\-create\-time |String |Creation date of the object. |
|x\-tos\-object\-lock\-mode |String |The mode of the object retention policy can only be set to `COMPLIANCE`, which indicates compliance mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Your account must have the <code>GetObjectRetention</code> permission for the <code>x-tos-object-lock-mode</code> parameter to be returned.</div><br> |
|x\-tos\-object\-lock\-retain\-until\-date |String |The lock expiration date of the object is the date during which the object cannot be deleted or overwritten.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Your account must have the <code>GetObjectRetention</code> permission for the <code>x-tos-object-lock-retain-until-date</code> parameter to be returned.</div><br> |


<span id="e02f57ac"></span>
## **Response body elements**

No elements are used.

<span id="76c8a5e0"></span>
## **Sample request**

```JSON
HEAD /objectName HTTP/1.1
Host: destbucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id="d52e71f3"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
Content-Type: text/plain
Content-Length: 120
Date: Fri, 30 Jul 2021 08:05:36 GMT
ETag: "900150983cd24fb0d6963f7d28e17f72"
Last-Modified: Mon, 02 Jul 2021 10:29:28 GMT
server: TosServer
x-tos-id-2: ea2ceb08a4e30021-a444ed0
x-tos-request-id: ea2ceb08a4e30021-a444ed0
x-tos-storage-class: STANDARD
x-tos-hash-crc64ecma: 6186290338114851376
```
