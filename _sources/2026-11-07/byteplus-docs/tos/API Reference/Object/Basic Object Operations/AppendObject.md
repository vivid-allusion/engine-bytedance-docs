---
title: "AppendObject"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-appendobject"
---

<span id="a2be0542"></span>
## **Description**

This API is used to append data to an object. Objects created by using this API are of type "Appendable", while objects uploaded through the PutObject API or in parts are of type "Normal".

<span id="16aaeb9b"></span>
## **Instructions**

AppendObject has the following restrictions:


* The minimum data size for each append is 128 KB, and the maximum size of the resulting object is 5 GB.

* Performing a PutObject operation on an object created through AppendObject will result in the object being overwritten, and the object type changing from "Appendable" to "Normal". Conversely, objects uploaded through PutObject cannot be appended with additional data.

* Objects created through AppendObject cannot be copied.

* If an object is in Infrequent Access Storage or Flashback Archive, data cannot be appended using AppendObject.

* AppendObject cannot be used for versioning\-enabled or \-suspended buckets.

* AppendObject does not support server\-side encryption.

* Appendable objects do not have an ETag, resulting in its absence in the response to GET and HEAD requests for such objects.

* Avoid concurrent append operations on the same appendable object, as this can lead to execution failure.


<span id="7a325edc"></span>
## **Request syntax**

```JSON
POST /objectName?append&offset=Offset HTTP/1.1
Host: buketname.tos-ap-southeast-1.bytepluses.com
Date: GMT Date
Authorization: authorization string

<append data>
```


<span id="51b3e13c"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|append |Query |String |Yes |\- |Identifies an AppendObject request. |
|offset |Query |Integer |Yes |0 |Specifies where to start appending. Upon a successful append, the response will contain the x\-tos\-next\-append\-offset header, which indicates the offset for the next append. |
|Content\-Length |Header |Integer |Yes |100 |Length of the message body. |
|Content\-Type |Header |String |No |text/plain |Object content type,which is valid only when offset is 0. |
|x\-tos\-acl |Header |String |No |private |Object ACL setting. Valid values:<br><br><br>* `private`: private permission.<br><br>* `public-read`: publicly readable.<br><br>* `public-read-write`: publicly readable and writable.<br><br>* `authenticated-read`: Authenticated users have read access.<br><br>* `bucket-owner-read`: The bucket owner has read access.<br><br>* `bucket-owner-full-control`: The bucket owner has full control.<br><br>* `bucket-owner-entrusted`: controlled by the bucket policy, with the bucket owner having full control.<br><br>* `default`：Inherit bucket ACL, that is, the ACL policy of the object remains consistent with the bucket ACL policy. |
|x\-tos\-grant\-full\-control |Header |String |No |id=123,id=456 |Grants the grantees READ, READ_ACP, and WRITE_ACP permissions on the object at object creation. Syntax: id=account1,id=account2. |
|x\-tos\-grant\-read |Header |String |No |id=123,id=456 |Allows the grantees to read the object and its metadata. Syntax: id=account1,id=account2. |
|x\-tos\-grant\-read\-acp |Header |String |No |id=123,id=456 |Allows the grantees to read the object ACL. Syntax: id=account1,id=account2. |
|x\-tos\-grant\-write\-acp |Header |String |No |id=123,id=456 |Allows the grantees to modify the object ACL. Syntax: id=account1,id=account2. |
|x\-tos\-meta\-\* |Header |String |No |x\-tos\-meta\-key: value |When creating an object, you can specify custom metadata through HTTP request headers prefixed with "x\-tos\-meta\-" to tailor object management. Your custom metadata will appear in the response headers when others retrieve this object or query the object metadata. |
|x\-tos\-website\-redirect\-location |Header |String |No |/anotherObjectName |For buckets with a Website configuration, requests to this object are redirected to another object in the bucket or an external URL. TOS will extract the value and save it in the object metadata. |
|x\-tos\-storage\-class<br><br>x\-tos\-traffic\-limit |Header<br><br>Header |String<br><br>String |No<br><br>No |STANDARD<br><br>819200 |Specifies the storage type of the object. If this parameter is unset, the object inherits the default storage type of its containing bucket. For detailed information, please refer to [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type).<br><br>TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-traffic\-limit |Query |String |No |819200 |TOS supports per\-link rate limiting of file uploads and downloads, ensuring ample bandwidth for other applications. Valid values:<br><br><br>* A value between 819200 and 838860800, in bit/s.<br><br>* This parameter can be specified in either the header or the query. |
|x\-tos\-object\-expires |Header |String |No |3 |Set the expiration time for the object, after which TOS will automatically delete the object. The expiration time is calculated from the object's Last\-Modified time, in days.<br><br>After setting the object's expiration time, TOS will start executing the deletion task at midnight on the day the expiration time is reached. For example, if the object's Last\-Modified time is 2024\-09\-26 12:00 and the expiration time is set to 3 days, the object will expire at 2024\-09\-30 00:00.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Only the first append write operation supports setting x\-tos\-object\-expires. Subsequent append write operations setting x\-tos\-object\-expires will be ignored.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The expiration time of an object takes priority over the deletion rule based on its lifecycle. For example, if an object has an expiration time set to 5 days and a lifecycle rule specifies the object should be deleted after 3 days, the object will be deleted based on the expiration time, which means it will be deleted after 5 days.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TOS supports querying the expiration time of objects via <a href="https://docs.byteplus.com/docs/tos/reference--getobject">GetObject</a> or <a href="https://docs.byteplus.com/docs/tos/reference-headobject">HeadObject</a>.</div><br> |
|x\-tos\-object\-lock\-mode |Header |String |No |COMPLIANCE |The mode of the retention policy can only be `COMPLIANCE`, which indicates compliance mode.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">To set a retention policy for an object, you must first enable the retention policy feature. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Putbucketobjectlockconfiguration">PutBucketObjectLockConfiguration</a>.</div><br> |
|x\-tos\-object\-lock\-retain\-until\-date |Header |String |No |2025\-01\-01T00:00:00Z |The lock expiration date of the object is the date during which the object cannot be deleted or overwritten. Follow the ISO 8601 time format.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>x-tos-object-lock-retain-until-date</code> parameter must be used together with the <code>x-tos-object-lock-mode</code> parameter.</div><br> |


<span id="5b423863"></span>
## **Request body elements**

The request uses no body elements. The message body is the appended data.

<span id="9ddeddd8"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/docs/tos/reference-common-parameters).


|**Name** |**Type** |**Description** |
|---|---|---|
|x\-tos\-next\-append\-offset |Integer |Offset for the next append. |
|x\-tos\-hash\-crc64ecma |Integer |CRC\-64 value of the object,which is calculated according to the ECMA\-182 standard.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the object was created before TOS supported CRC\-64 verification, this header will not appear in the response.</div><br> |


<span id="2b538069"></span>
## **Response body elements**

No elements are used.

<span id="142fb357"></span>
## **Sample request**

```JSON
POST /objectName?append&offset=0 HTTP/1.1
Host: buketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 GMT
Authorization: authorization string
```


<span id="5ef32cb0"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: 5726ce090a2d002d-a444ed0
x-tos-request-id: 5726ce090a2d002d-a444ed0
Date: Fri, 30 Jul 2021 08:05:36 GMT
server: TosServer
Content-Length: 0
x-tos-next-append-offset: 4379329
x-tos-hash-crc64ecma: 6186290338114851376
```
