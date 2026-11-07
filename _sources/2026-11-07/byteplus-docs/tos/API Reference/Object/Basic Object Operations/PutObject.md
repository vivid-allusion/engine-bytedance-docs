---
title: "PutObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putobject"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## **Introduction**

This API is used to add an object to a bucket. To add an object to a bucket, you must have write permission on the bucket.

TOS is a distributed system. If it receives multiple write requests for the same object concurrently, it overwrites all but the last object written. You can supply the expected MD5 value using the `Content-MD5` header for comparison with the uploaded object's MD5 value; if they do not match, an error is returned.

<span id=".5pyN5Yqh56uv5Yqg5a-G"></span>
## Server\-side encryption

With server\-side encryption enabled, TOS encrypts the data you upload at the object level and stores the encrypted data permanently. When you download an object, TOS automatically decrypts and returns the data to you. For more details on server\-side encryption, see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).

<span id="acl"></span>
## ACL

You can set an object's ACL through headers. All objects are private by default. You can grant specific permissions to an account or predefined group. For more details about ACL, see [ACL policy overview](https://docs.byteplus.com/docs/tos/docs-overview_4).

<span id=".5a2Y5YKo57G75Z6L"></span>
## Storage type

TOS stores objects in Standard Storage by default. This storage type features high availability, reliability, and performance. You can also choose another storage type according to the use case. For more information, see [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type).

<span id=".5aSa54mI5pys"></span>
## Versioning

When an object is uploaded to a versioning\-enabled bucket, a unique version ID is generated for the object and returned in the x\-tos\-version\-id header of the response.

For an object uploaded to a versioning\-suspended bucket, the object version ID is "null", and only the latest version will be retained after repeated uploads with the same key.

<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## **Request syntax**

```JSON
PUT /objectName HTTP/1.1
Host: destbucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
Content-length: length

<put data>
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## **Request parameters and headers**

This request uses common request headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|Content\-Length |Header |Integer |Yes |100 |Length of the message body. |
|Content\-MD5 |Header |String |No |XrY7u+Ae7tCTyyK7j1rNww== |Base64\-encoded MD5 digest of the message body. |
|Content\-Type |Header |String |No |text/plain |Object content type. |
|Cache\-Control |Header |String |No |no\-cache, no\-store, must\-revalidate |Specifies the caching behavior when the object is downloaded. |
|Expires |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Specifies the cache expiration time as defined in RFC 2616. |
|Content\-Disposition |Header |String |No |attachment; filename=123.txt |Specifies the name of the object when downloaded. |
|Content\-Encoding |Header |String |No |gzip |Specifies the content encoding of the object when downloaded. |
|Content\-Language |Header |String |No |en\-US |Specifies the content language of the object when downloaded. |
|x\-tos\-acl |Header |String |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: Private.<br><br>* `public-read`: Public read.<br><br>* `public-read-write`: Public read\-write.<br><br>* `authenticated-read`: Authenticated user read.<br><br>* `bucket-owner-read`: Bucket owner read.<br><br>* `bucket-owner-full-control`: Bucket owner full control.<br><br>* `bucket-owner-entrusted`: Controlled by bucket policy, bucket owner full control.<br><br>* `default`: Inherits the bucket ACL, meaning the object's ACL policy matches the bucket's ACL policy. |
|x\-tos\-grant\-full\-control |Header |String |No |id=123,id=456 |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object during object creation. Format: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |String |No |id=123,id=456 |Allows the grantees to read the object and its metadata. Format: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |String |No |id=123,id=456 |Allows the grantees to read the object ACL. Format: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |String |No |id=123,id=456 |Allows the grantees to modify the object ACL. Format: id=account1,id=account2. |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key: value |When creating an object, you can specify custom metadata through HTTP request headers prefixed with "x\-tos\-meta\-" to tailor object management. Your custom metadata will appear in the response headers when others retrieve this object or query the object metadata. |
|x\-tos\-server\-side\-encryption |Header |String |No |AES256 |Specifies the method used for encrypting the object. If this parameter is unset, the object is not encrypted by default. Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS.<br><br>   For details on SSE\-TOS and SSE\-KMS encryption methods, see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/reference-putobject).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using SSE\-KMS for server\-side encryption incurs API call charges. Creating KMS keys generates key management fees charged by KMS. For more information, see <a href="https://docs.byteplus.com/en/docs/6476/71331">KMS billing details</a>.</div><br> |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |Header |String |No, but YES if SSE\-KMS is used. |trn:kms:cn\-beijing:20000111:keyrings/ring\-test/keys/key\-test |Specify the master key for SSE\-KMS encrypted target objects, with the following format:<br><br>`trn:kms:<region>:<accountID>:keyrings/<keyring>/keys/<key>`: TRN of the KMS master key, where `region` is the region ID where the key is used, `accountID` is the account ID that owns the key, `keyring` is the keyring alias, and `key` is the master key alias.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default master key is not supported. If SSE\-KMS encryption is specified without this header, the server returns a <code>400 InvalidRequest</code> error.</div><br> |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm for SSE\-C encrypting the object. Valid value:<br><br><br>* AES256: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |YWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWE= |Used with `x-tos-server-side-encryption-customer-algorithm`, specifies the SSE\-C encrypted target object's key in base64 encoded 256\-bit format. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-website\-redirect\-location |Header |String |No |/anotherObjectName |For buckets with a Website configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata. |
|x\-tos\-storage\-class |Header |String |Not supported |STANDARD |Specifies the storage type of the destination object. If unset, the destination object's storage type follows the default storage type of its bucket. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent Tiering.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive.<br><br>* `COLD_ARCHIVE`: Cold Archive.<br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only China (Beijing), China (Shanghai), and China (Guangzhou) support Cold Archive.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only China (Beijing), China (Shanghai), and China (Guangzhou) support Deep Cold Archive. All are in the invitation testing phase. Please contact your account manager if you need to use this storage type.   </div><br>    |
|x\-tos\-tagging |Header |String |No |Key1=Value1&Key2=Value2 |Set object tag information in the format `{Key}={Value}`. Multiple tags can be set simultaneously, separated by `&`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The tag keys and values need to be URL\-encoded.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a tag is set without using <code>=</code> to specify a tag value, TOS treats the tag value as an empty string.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more tag restrictions, see <a href="https://docs.byteplus.com/docs/tos/docs-managing-file-labels">Object tags</a>.</div><br> |
|x\-tos\-traffic\-limit |Header |String |No |819200 |TOS supports per\-link rate limiting of object uploads and downloads, ensuring ample bandwidth for other applications. The options are as follows:<br><br><br>* Range: 245760\-838860800, unit: bit/s.<br><br>* This parameter can be specified in either the header or the query, but not both simultaneously. |
|x\-tos\-forbid\-overwrite |Header |String |No |false |Allows overwriting objects with the same name; the values are explained below:<br><br><br>* Not specified or set to `false`: Allows overwriting objects with the same name.<br><br>* Set to `true`: Prohibits overwriting objects with the same name.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the target bucket has versioning enabled or suspended, the <code>x-tos-forbid-overwrite</code> parameter is ignored, allowing overwriting of objects with the same name.</div><br> |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS supports per\-link rate limiting during object upload and download operations to ensure network bandwidth for other applications. Valid values:<br><br><br>* Range: 245760\-838860800, unit: bit/s.<br><br>* This parameter cannot be specified in both the header and query simultaneously. |
|x\-tos\-object\-expires |Header |String |No |3 |Set the object's expiration time. After expiration, TOS will delete the object automatically. The unit is days, supporting positive integers. This means the object will expire after the specified time, counted from the object's Last\-Modified time. The deletion task starts at midnight on the expiration day.<br><br>For example, if you set the `x-tos-object-expires` parameter to `3`, and the object's last modified time is 2024\-09\-26 12:00, the object will expire at 2024\-09\-30 00:00.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The object expiration time takes precedence over lifecycle delete rules. For example, if the object expiration time is set to 5 days and the lifecycle rule deletes the object after 3 days, the object will be deleted after 5 days according to the expiration time.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TOS supports querying an object's expiration time via <a href="https://docs.byteplus.com/docs/tos/reference--getobject">GetObject</a> or <a href="https://docs.byteplus.com/docs/tos/reference-headobject">HeadObject</a>.</div><br> |
|x\-tos\-object\-lock\-mode |Header |String |No |COMPLIANCE |The mode of the retention policy can only be `COMPLIANCE`, which indicates compliance mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To configure a retention policy for an object, you must first enable the retention policy feature. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Putbucketobjectlockconfiguration">PutBucketObjectLockConfiguration</a>.</div><br> |
|x\-tos\-object\-lock\-retain\-until\-date |Header |String |No |2025\-01\-01T00:00:00Z |The object's locked deadline is the date during which the object cannot be deleted or overwritten. Follow the ISO 8601 time format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The <code>x-tos-object-lock-retain-until-date</code> parameter must be used together with the <code>x-tos-object-lock-mode</code> parameter.</div><br> |
|if\-match |Header |String |No |d41d8cd98f00b204e9800998ecf8427e |Control upload behavior with the ETag condition; the object uploads only if the specified ETag matches the ETag of an existing object in the bucket. If the specified ETag is missing or does not match, the upload fails and returns a 412 status code. |
|if\-none\-match |Header |String |No |d41d8cd98f00b204e9800998ecf8427e |Control upload behavior with the ETag condition: the object uploads only if the specified ETag does not match the ETag of the existing object in the bucket. If the specified ETag matches the ETag of the existing object in the bucket, the upload fails and returns a 412 status code.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>if-none-match</code> supports setting to <code>*</code>, meaning the upload fails and returns a 412 status code as long as an object with the same name exists in the target bucket (regardless of its ETag).</div><br> |


<span id=".6K-35rGC5YWD57Sg"></span>
## **Request body elements**

The request uses no body elements. The message body is the uploaded object data.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## **Response headers**

This request returns common response headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|x\-tos\-server\-side\-encryption |String |kms |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |trn:kms:cn\-beijing:\*\*\*\*:keyrings/ring\-test/keys/key\-test |ID of the KMS master key, which is returned if the object is SSE\-KMS encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |AES256 |Algorithm used for encrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |0gYVWExOAz67jX5A6qY4+A== |MD5 value of the encryption key, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-version\-id |String |57AF1A32CECB56721267 |Version ID of the object. This header will not appear in the response if the object has no version ID. |
|x\-tos\-hash\-crc64ecma |Integer |6186290338114851376 |CRC\-64 value of the object, which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This is the CRC\-64 value of the unencrypted object content when server\-side encryption is enabled for object upload.</div><br> |
|x\-tos\-qos\-delay\-time |Integer |10 |This header indicates the duration of flow control on the request, in ms. Upload requests return the exact duration under flow control; copy or download requests return an estimated duration based on flow control level and object size. |


<span id=".5ZON5bqU5YWD57Sg"></span>
## **Response body elements**

No elements are used.

<span id=".6K-35rGC56S65L6L"></span>
## **Sample request**

```JSON
PUT /objectName HTTP/1.1
Host: destbucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
Content-Length: 100

[100 Byte data content]
```


<span id=".5ZON5bqU56S65L6L"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 367be10900210004-a444ed0
x-tos-request-id: 367be10900210004-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0
ETag: "1c06e540e11d65a51aeb724e72fa641a"
x-tos-hash-crc64ecma: 6186290338114851376
```
