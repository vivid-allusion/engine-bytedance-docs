---
title: "CopyObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-copyobject"
---

<span id=".5Yqf6IO95o-P6L-w"></span>
## Feature description

This API is used to copy an object within the same bucket or across buckets in the same region.

All copy requests must be authenticated. Besides, you must have read access to the source object and write access to the target bucket. When copying an object, you can preserve all metadata (the default) or specify new metadata. However, the ACL is not preserved and is set to private for the user making the request. To override the default ACL setting, specify a new ACL when generating a copy request.

To restore an earlier version of an object to the current version in a versioning\-enabled bucket, simply copy the earlier version to the same bucket. TOS will automatically designate this version as current.

<span id=".5pyN5Yqh56uv5Yqg5a-G"></span>
## **Server\-side encryption**

When you perform a CopyObject operation, you can choose to use server\-side encryption headers, such as TOS\-managed keys (SSE\-TOS), customer\-provided encryption keys (SSE\-C), or KMS\-managed keys (SSE\-KMS) for server\-side encryption. With server\-side encryption, TOS encrypts the data you upload at the file level, then stores the encrypted data persistently. When you download the file, TOS automatically decrypts the encrypted data and returns it to you. For more details about server\-side encryption, see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview).

<span id=".5L2_55So6ZmQ5Yi2"></span>
## **Usage restrictions**

CopyObject has the following object restrictions:


* The target object's size must be within [0, 5GiB]. If the source object exceeds 5GiB, use the [UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy) interface.

* Both CopyObject and UploadPartCopy require read permission on the source object.

* Before copying archive storage, cold archive storage, or deep cold archive storage objects with CopyObject, you must restore the objects first.


<span id="58a4f2f9"></span>
## Billing notes


* Calling the CopyObject interface equals performing one GET Object request on the source bucket and one PUT Object request on the target bucket. Therefore, the source bucket incurs a read request fee, and the target bucket incurs a write request fee. For details, see [Request fees](https://docs.byteplus.com/docs/tos/docs-request-fee).

* Calling the CopyObject API will increase the storage capacity of the destination bucket.

* Calling the CopyObject API to change the object's storage class involves data overwriting. For example, if you call the CopyObject API to change a 15\-day IA object to standard storage, you will incur insufficient duration capacity charges for the 15\-day IA storage. For detailed billing information, see [Storage capacity fees](https://docs.byteplus.com/docs/tos/docs-storage-fee).


<span id=".6K-35rGC5raI5oGv5qC35byP"></span>
## Request syntax

```JSON
PUT /DestObjectName HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
x-tos-copy-source: /sourcebucketname/SourceObjectName
```


<span id=".6K-35rGC5Y-C5pWw5ZKM5raI5oGv5aS0"></span>
## Request parameters and headers


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|x\-tos\-acl |Header |String |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: private, default.<br><br>* `public-read`: public read.<br><br>* `public-read-write`: public read and write.<br><br>* `authenticated-read`: authenticated user read.<br><br>* `bucket-owner-read`: bucket owner read.<br><br>* `bucket-owner-full-control`: bucket owner full control.<br><br>* `bucket-owner-entrusted`: controlled by bucket policy, bucket owner full control.<br><br>* `default`: inherits bucket ACL; object ACL matches bucket ACL policy. |
|x\-tos\-copy\-source |Header |String |Yes |/sourcebucketname/SourceObjectName?versionId=xxx |Specifies the source bucket and object. The source object name must be URL\-encoded, following the application/x\-www\-form\-urlencoded standard.<br><br>Use versionId to specify the version of a multiversion source object. |
|x\-tos\-copy\-source\-if\-match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |Copies the source object only if it has a matching ETag. |
|x\-tos\-copy\-source\-if\-modified\-since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Copies the object if it has been modified since the specified time. Use GMT time in RFC 1123 format. |
|x\-tos\-copy\-source\-if\-none\-match |Header |String |No |8a36be0d764367db4eea2deb16b71543 |Copies the source object only if its ETag differs from the specified value. |
|x\-tos\-copy\-source\-if\-unmodified\-since |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Copies the object if it has not been modified since the specified time. Use GMT time in RFC 1123 format. |
|x\-tos\-server\-side\-encryption |Header |String |No |AES256 |Specifies the method used for encrypting the object. If this parameter is unset, the object is not encrypted by default. Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS.<br><br>   For detailed explanations of SSE\-TOS and SSE\-KMS encryption methods, see [Server-side encryption](https://docs.byteplus.com/docs/tos/reference-copyobject).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Using SSE\-KMS for server\-side encryption incurs API call fees. Creating KMS keys incurs key management fees charged by KMS. For more information, see <a href="https://docs.byteplus.com/docs/kms/BytePlus_KMS_Pricing">KMS billing details</a>.</div><br> |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |Header |String |No, but YES if SSE\-KMS is used. |trn:kms:cn\-beijing:20000111:keyrings/ring\-test/keys/key\-test |Specify the master key for the SSE\-KMS encrypted object. The format is as follows:<br><br>`trn:kms:<region>:<accountID>:keyrings/<keyring>/keys/<key>`: The TRN of the KMS master key, where `region` is the Region ID of the key, `accountID` is the account ID of the key owner, `keyring` is the keyring alias, and `key` is the master key alias.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The default master key is currently not supported. If SSE\-KMS encryption is specified without this header, the server returns a <code>400 InvalidRequest</code> error.</div><br> |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm used for SSE\-C encrypting the object. Valid value:<br><br><br>* AES256: Use the AES\-256 algorithm. For details, see [Server-side encryption](https://docs.byteplus.com/docs/tos/reference-copyobject). |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |YWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWFhYWE= |Used with `x-tos-server-side-encryption-customer-algorithm` to specify the SSE\-C encryption key for the target object. The key must be a base64\-encoded 256\-bit encryption key. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4+A== |Used together with `x-tos-server-side-encryption-customer-key`, this header represents the MD5 value of the key used to encrypt the target object. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if the source object is SSE\-C encrypted. |AES256 |Specifies the algorithm used for decrypting an SSE\-C encrypted source object. Valid value:<br><br><br>* `AES256`: SSE\-TOS encryption method. For detailed information, see [Server-side encryption](https://docs.byteplus.com/docs/tos/reference-copyobject). |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key |Header |String |No, but yes if the source object is SSE\-C encrypted. |1234567890abcdefghijklmnopqrstuv |Specifies the key used for decrypting an SSE\-C encrypted source object. This must be the same key used when creating the source object. |
|x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if the source object is SSE\-C encrypted. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-copy\-source\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-grant\-full\-control |Header |String |No |id=123,id=456 |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object. Format: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |String |No |id=123,id=456 |Allows the grantee to read the object and its metadata. Format: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |String |No |id=123,id=456 |Allows the grantees to read the object ACL. Format: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |String |No |id=123,id=456 |Allows the grantees to modify the object ACL. Format: id=account1,id=account2. |
|x\-tos\-metadata\-directive |Header |String |No |COPY |Specifies whether to copy metadata from the source object or replace metadata with that provided in the request. The options are as follows:<br><br><br>* `COPY`: Copies metadata from the source object, default value.<br><br>* `REPLACE`: Replaces metadata using the metadata provided in the request. |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key: value |If the x\-tos\-metadata\-directive header is set to REPLACE, you can specify custom metadata through HTTP request headers prefixed with "x\-tos\-meta\-". |
|x\-tos\-website\-redirect\-location |Header |String |No |/anotherObjectName |For buckets with a Website configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata. |
|x\-tos\-storage\-class |Header |String |No |STANDARD |Specifies the storage type of the object. If this parameter is unset, the object inherits the default storage type of its containing bucket. Valid values:<br><br><br>* `STANDARD`: Standard storage.<br><br>* `IA`: Infrequent access storage.<br><br>* `INTELLIGENT_TIERING`: Intelligent tiered storage.<br><br>* `ARCHIVE_FR`: Archive flash recovery storage.<br><br>* `ARCHIVE`: Archive storage.<br><br>* `COLD_ARCHIVE`: Cold archive storage.<br><br>* `DEEP_COLD_ARCHIVE`: deep cold archive storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou) support cold archive storage.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Currently, only North China 2 (Beijing), East China 2 (Shanghai), and South China 1 (Guangzhou) support deep cold archive storage, all in invited testing. Contact your account manager if you need to use this storage type.   </div><br>    |
|x\-tos\-tagging |Header |String |No |Key1=Value1&Key2=Value2 |Set the tag information for the object in the format `{Key}={Value}`. Multiple tags can be set simultaneously, separated by`&`a separator.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The tag keys and values need to be URL\-encoded.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a certain object does not use<code>=</code>setting the Value, TOS treats the tag’s Value as an empty string.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more restrictions on object tags, see <a href="https://docs.byteplus.com/docs/tos/docs-managing-file-labels">Object tags</a>.</div><br> |
|x\-tos\-tagging\-directive |Header |String |No |Copy |Specifies whether the object tags are copied from the source object or replaced with those provided in the request. Valid values:<br><br><br>* `Copy` (default): Copy the tags from the source object.<br><br>* `Replace`: Do not copy tags from the source object; use the tags provided in the request instead. |
|x\-tos\-traffic\-limit |Header |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. The options are as follows:<br><br><br>* Value range: 245760\-838860800, unit: bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-forbid\-overwrite |Header |String |No |false |Whether to allow overwriting objects with the same name. The options are as follows:<br><br><br>* Not specified or set to `false`: indicates overwriting objects with the same name is allowed.<br><br>* Set to `true`: indicates overwriting objects with the same name is prohibited.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the target bucket is under enabled or suspended versioning status, the <code>x-tos-forbid-overwrite</code> parameter is ineffective, allowing overwriting objects with the same name.</div><br> |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. The options are as follows:<br><br><br>* Value range: 245760\-838860800, unit: bit/s.<br><br>* This parameter cannot be specified in the header and the query simultaneously. |
|x\-tos\-object\-expires |Header |String |No |3 |Set the object's expiration time. After expiration, TOS will automatically delete the object. The unit is days. You can set a positive integer to specify when the object will expire, starting from the object's Last\-Modified time. The deletion task will begin at midnight after reaching the expiration time.<br><br>For example, set the value of the `x-tos-object-expires` parameter to`3`, if the object's Last\-Modified time is 2024\-09\-26 12:00, the object will expire at 2024\-09\-30 00:00.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The expiration time is not inherited from the source object by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The object's expiration time takes precedence over lifecycle deletion rules. For example, if the object expiration time is set to 5 days but the lifecycle rule deletes the object after 3 days, the object will ultimately be deleted after 5 days according to the expiration time.</div><br> |
|x\-tos\-object\-lock\-mode |Header |String |No |COMPLIANCE |The mode of the retention policy can only be set to `COMPLIANCE`, indicating compliance mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To configure a retention policy for an object, you must first enable the retention policy feature. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Putbucketobjectlockconfiguration">PutBucketObjectLockConfiguration</a>.</div><br> |
|x\-tos\-object\-lock\-retain\-until\-date |Header |String |No |2025\-01\-01T00:00:00Z |Until the lock expiration date, the object cannot be deleted or overwritten. Follow the ISO 8601 time format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>x-tos-object-lock-retain-until-date</code> parameter must be used together with the <code>x-tos-object-lock-mode</code> parameter.</div><br> |
|if\-match |Header |String |No |d41d8cd98f00b204e9800998ecf8427e |ETag condition controlling upload behavior: the object uploads only if the specified ETag matches the ETag of an existing object in the bucket. If the specified ETag does not exist or does not match, the upload will fail and return a 412 status code. |
|if\-none\-match |Header |String |No |d41d8cd98f00b204e9800998ecf8427e |ETag condition controlling upload behavior: the object uploads only if the specified ETag does not match the ETag of the existing object in the bucket. If the ETag of the existing object in the bucket matches the specified ETag, the upload fails and returns status code 412.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>if-none-match</code> supports setting to<code>*</code>, indicating that the upload fails and returns status code 412 if an object with the same name exists in the target bucket regardless of its ETag.</div><br> |


<span id=".6K-35rGC5YWD57Sg"></span>
## Request body elements

No elements are used.

<span id=".5ZON5bqU5raI5oGv5aS0"></span>
## Response headers

This request returns common response headers. See [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|x\-tos\-copy\-source\-version\-id |String |57AF1A32CECB56721267 |Version ID of the source object, which is returned when copying a specific version of the source object. |
|x\-tos\-version\-id |String |43D62700044343044833 |Version ID of the target object. |
|x\-tos\-server\-side\-encryption |String |kms |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |trn:kms:cn\-beijing:20000111:keyrings/ring\-test/keys/key\-test |ID of the primary key for SSE\-KMS encryption, which is returned if the object is encrypted this way. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |AES256 |Algorithm used for SSE\-C encryption, which is returned if the object is encrypted this way. |
|x\-tos\-server\-side\-encryption\-customer\-key\-md5 |String |0gYVWExOAz67jX5A6qY4+A== |MD5 value of the key used for SSE\-C encryption, which is returned if the object is encrypted this way. |
|x\-tos\-qos\-delay\-time |Integer |10 |This header indicates the duration of request throttling, in milliseconds. Upload requests return the exact throttled duration; copy or download requests return an estimated throttled duration based on the throttling level and file size. |


<span id=".5ZON5bqU5YWD57Sg"></span>
## Response body elements


|**Name** |**Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ETag |String |8a36be0d764367db4eea2deb16b71543 |ETag of the target object. |
|LastModified |String |2021\-08\-20T06:38:52.000Z |Last modified time of the target object. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```JSON
PUT /DestObjectName HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 13:55:03 +0000
Authorization: authorization string
x-tos-copy-source: /sourcebucketname/SourceObjectName
```


<span id=".5ZON5bqU56S65L6L"></span>
## Sample response

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130bedb6002c-a444ed0
x-tos-request-id: 4fac130bedb6002c-a444ed0
x-tos-hash-crc64ecma: 6186290338114851376
Date: Fri, 30 Jul 2021 13:55:03 GMT
server: TosServer

{
    "ETag": "\"8a36be0d764367db4eea2deb16b71543\"",
    "LastModified": "2021-08-20T06:38:52.000Z"
}
```
