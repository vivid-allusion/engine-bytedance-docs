---
title: "CreateMultipartUpload"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-createmultipartupload"
---

<span id="794aad72"></span>
## **Introduction**

This API is used to initialize a multipart upload task. Before uploading part data, you need to initialize the UploadId of a multipart upload task through this API. The subsequent operations of uploading parts, merging parts, aborting part uploads, and listing uploaded parts all require the UploadId. Initializing a multipart upload task does not affect the existing object with the same name.

If you have set up a lifecycle rule for the bucket to abort incomplete multipart uploads, the uploaded parts must be merged within the number of days specified in the bucket lifecycle configuration. Otherwise, the incomplete multipart upload becomes eligible for an abort action, and TOS aborts the multipart upload and clears the unmerged parts.

Initialized multipart upload tasks can be listed using the ListMultipartUploads API before they are completed or aborted.

<span id="eff479a5"></span>
## Server\-side encryption

With server\-side encryption enabled, TOS encrypts the data you upload at the file level and stores the encrypted data permanently. When you download a file, TOS automatically decrypts and returns the data to you.

<span id="899b7f76"></span>
## **Request syntax**

```JSON
POST /objectName?uploads HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string
```


<span id="b0c81acd"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|---|
|uploads |Query |String |Yes |\- |Identifies a CreateMultipartUpload request. |
|encoding\-type |Query |String |No |url |Specifies the encoding of the returned content. Valid value:<br><br><br>* url: Use URL encoding. |
|Content\-Type |Header |String |No |text/plain |Object content type. |
|Cache\-Control |Header |String |No |no\-cache, no\-store, must\-revalidate |Specifies the caching behavior when the object is downloaded. |
|Expires |Header |String |No |Mon, 04 Jul 2022 02:57:31 GMT |Specifies the cache expiration time as defined in RFC 2616. |
|Content\-Disposition |Header |String |No |attachment; filename=123.txt |Specifies the default filename of the object when downloaded. |
|Content\-Encoding |Header |String |No |gzip |Specifies the content encoding of the object when downloaded. |
|Content\-Language |Header |String |No |en\-US |Specifies the content language of the object when downloaded. |
|x\-tos\-acl |Header |String |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: Private permission.<br><br>* `public-read`: Publicly readable.<br><br>* `public-read-write`: Publicly readable and writable.<br><br>* `authenticated-read`: Authenticated users have read access.<br><br>* `bucket-owner-read`: The bucket owner has read access.<br><br>* `bucket-owner-full-control`: The bucket owner has full control.<br><br>* `bucket-owner-entrusted`: Controlled by the bucket policy, with the bucket owner having full control.<br><br>* `default`：Inherit bucket ACL, that is, the ACL policy of the object remains consistent with the bucket ACL policy. |
|x\-tos\-grant\-full\-control |Header |String |No |id=accountID |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object at object creation. Syntax: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |String |No |id=accountID |Allows the grantees to read the object and its metadata. Syntax: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |String |No |id=accountID |Allows the grantees to read the object ACL. Syntax: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |String |No |id=accountID |Allows the grantees to modify the object ACL. Syntax: id=account1,id=account2. |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key: value |When creating an object, you can specify custom metadata through HTTP request headers prefixed with "x\-tos\-meta\-" to tailor object management. Your custom metadata will appear in the response headers when others retrieve this object or query the object metadata. |
|x\-tos\-server\-side\-encryption |Header |String |No |AES256 |Specifies the method used for encrypting the object. If this parameter is unset, the object is not encrypted by default. Valid values:<br><br><br>* `AES256`: Use SSE\-TOS. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |Header |String |No, but YES if SSE\-C is used. |AES256 |Specifies the algorithm used for SSE\-C encrypting the object. Valid value:<br><br><br>* `AES256`: Use the AES\-256 algorithm. |
|x\-tos\-server\-side\-encryption\-customer\-key |Header |String |No, but YES if SSE\-C is used. |1234567890abcdefghijklmnopqrstuv |Used with x\-tos\-server\-side\-encryption\-customer\-algorithm to specify the key used for SSE\-C encrypting the object. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |Header |String |No, but YES if SSE\-C is used. |0gYVWExOAz67jX5A6qY4+A== |Used with x\-tos\-server\-side\-encryption\-customer\-key to specify the MD5 value of the customer\-provided key. The value is derived by Base64\-encoding the 128\-bit MD5 of the key and is used for message integrity check to ensure error\-free transmission of the encryption key. |
|x\-tos\-website\-redirect\-location |Header |String |No |/anotherObjectName |For buckets with a Website configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata. |
|x\-tos\-storage\-class |Header |String |No |STANDARD |Specifies the storage type of the object. If this parameter is unset, the object inherits the default storage type of its containing bucket. For detailed information, please refer to [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type). |
|x\-tos\-tagging |Header |String |No |Key1=Value1&Key2=Value2 |Specifies the tags of the object, in the format of `{Key}={Value}`. Separate multiple tags with `&`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The tag keys and values need to be URL\-encoded.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If a tag key is not followed by <code>=</code> when you set the value, TOS treats the value as an empty string.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For more restrictions on object tags, see <a href="https://docs.byteplus.com/docs/tos/docs-managing-file-labels">Object tags</a>.</div><br> |
|x\-tos\-forbid\-overwrite |Header |String |No |false |Is it allowed to overwrite objects with the same name? The values are as follows:<br><br><br>* Not specified or specified as false: Indicates allowing the overwriting of objects with the same name.<br><br>* When set to true: It indicates that overwriting objects with the same name is prohibited.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">When the target bucket is in a versioning state of enabled or suspended, the x\-tos\-forbid\-overwrite parameter setting is invalid, allowing the overwriting of objects with the same name.</div><br> |
|x\-tos\-object\-expires |Header |String |No |3 |Set the expiration time for the object, after which TOS will automatically delete the object. The expiration time is calculated from the object's Last\-Modified time, in days.<br><br>After setting the object's expiration time, TOS will start executing the deletion task at midnight on the day the expiration time is reached. For example, if the object's Last\-Modified time is 2024\-09\-26 12:00 and the expiration time is set to 3 days, the object will expire at 2024\-09\-30 00:00.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The expiration time of an object takes priority over the deletion rule based on its lifecycle. For example, if an object has an expiration time set to 5 days and a lifecycle rule specifies the object should be deleted after 3 days, the object will be deleted based on the expiration time, which means it will be deleted after 5 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TOS supports setting or modifying the expiration time of an object by adding an expiration time to the object or by querying the expiration time using the or command.</div><br> |
|x\-tos\-object\-lock\-mode |Header |String |No |COMPLIANCE |The mode of the retention policy can only be set to `COMPLIANCE`, which indicates compliance mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To configure a retention policy for an object, you must first enable the retention policy feature. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Putbucketobjectlockconfiguration">PutBucketObjectLockConfiguration</a>.</div><br> |
|x\-tos\-object\-lock\-retain\-until\-date |Header |String |No |2025\-01\-01T00:00:00Z |The lock expiration date of the object; during this period, the object cannot be deleted or overwritten. Follow the ISO 8601 time format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>x-tos-object-lock-retain-until-date</code> must be used together with the <code>x-tos-object-lock-mode</code> parameter.</div><br> |


<span id="6d66d3c5"></span>
## **Request body elements**

No elements are used.

<span id="71f552c7"></span>
## **Response headers**

For common response headers, see [Common parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-server\-side\-encryption |String |When SSE\-TOS encryption or SSE\-KMS is used, this header is returned, indicating the server\-side encryption method for the object.Valid values:<br><br><br>* `AES256`: Use the encryption method of SSE\-TOS.<br><br>* `kms`:Use the encryption method of SSE\-KMS. |
|x\-tos\-server\-side\-encryption\-kms\-key\-id |String |When SSE\-KMS encryption is used for the object, this header is returned, indicating the KMS master key ID used for SSE\-KMS encryption. |
|x\-tos\-server\-side\-encryption\-customer\-algorithm |String |Algorithm used for encrypting the object, which is returned if the object is SSE\-C encrypted. |
|x\-tos\-server\-side\-encryption\-customer\-key\-MD5 |String |MD5 value of the encryption key, which is returned if the object is SSE\-C encrypted. |


<span id="7a0cd1f0"></span>
## **Response body elements**


|**Name** |**Type** |**Description** |
|---|---|---|
|Bucket |String |Bucket name. |
|Key |String |Object name. |
|UploadId |String |Initialized task ID. |
|EncodingType |String |Encoding of Key in the response. If the request specifies an encoding\-type, the Key property in the response will be encoded accordingly. |


<span id="1ed3f6e0"></span>
## **Sample request**

```JSON
POST /objectName?uploads HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 00:07:49 GMT
Authorization: authorization string
```


<span id="b785a8ab"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 4fac130c7d550034-a444ed0
x-tos-request-id: 4fac130c7d550034-a444ed0
Date: Fri, 30 Jul 2021 00:07:49 GMT
server: TosServer
Content-Length: 210

{
    "Bucket": "bucketName",
    "Key": "objectName",
    "UploadId": "f93f6fc9da94371f321e1008"
}
```
