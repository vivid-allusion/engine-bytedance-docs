---
title: "PutBucketStorageClass"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-putbucketstorageclass"
---

<span id="ec00af42"></span>
## **Description**

This API is used to set the default storage type of a bucket. After the default storage type is set for the bucket, objects uploaded, copied, or initialized for multipart uploads without a specified storage type inherit this default storage type. By default, the storage type of a bucket is STANDARD (Standard Storage).

<span id="8f26fc63"></span>
## Note


* This API must be called by the bucket owner or user with the PutBucketStoragePolicy permission for the bucket. For detailed instructions on how to achieve access control using bucket policies, see [Bucket Authorization Policy Management](https://docs.byteplus.com/en/tos/docs/overview_5).

* For applicable scenarios of different storage types of TOS and their differences, see [Storage Type](https://docs.byteplus.com/en/tos/docs/storage-type).


<span id="f3897b22"></span>
## **Request syntax**

```JSON
PUT /?storageClass HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
X-Tos-Storage-Class: "STANDARD"
```


<span id="7d59da65"></span>
## **Request parameters and headers**

For common request headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).


|**Name** |**Location** |**Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|---|
|storageClass |Query |String |Yes |\- |Identifies a PutBucketStorageClass request. |
|x\-tos\-storage\-class |Header |String |Yes |STANDARD |The default storage type of the bucket. Valid values:<br><br><br>* `STANDARD`: Standard Storage.<br><br>* `IA`: Infrequent Access Storage.<br><br>* `ARCHIVE_FR`: Flashback Archive.<br><br>* `ARCHIVE`: Archive Storage.<br><br>* `COLD_ARCHIVE`: Cold Archive Storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Cold Archive Storage is supported only in China (Beijing), China (Shanghai), and China (Guangzhou).   </div><br>   <br><br>* `DEEP_COLD_ARCHIVE`: Deep Cold Archive Storage.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Deep Cold Archive Storage is only supported in China (Beijing), China (Shanghai), and China (Guangzhou), and all are in the invitation\-only testing phase. If you need to use this storage type, please contact your account manager.   </div><br>    |


<span id="4b232da2"></span>
## **Request body elements**

No elements are used.

<span id="7477fdb9"></span>
## **Response headers**

For common response headers, see [Common Parameters](https://docs.byteplus.com/en/tos/reference/common-parameters).

<span id="ca95375b"></span>
## **Response body elements**

No elements are used.

<span id="91db2dbd"></span>
## **Sample request**

```JSON
PUT /?storageClass HTTP/1.1
Host: bucketname.tos-ap-southeast-1.bytepluses.com
Date: Fri, 30 Jul 2021 08:05:36 +0000
Authorization: authorization string
X-Tos-Storage-Class: "STANDARD"
```


<span id="758829f3"></span>
## **Sample response**

```JSON
HTTP/1.1 200 OK
x-tos-id-2: f91b0c03a01300c1-a444ed0        
x-tos-request-id: f91b0c03a01300c1-a444ed0            
Date: Fri, 30 Jul 2021 06:45:39 GMT
Content-Length: 0
server: TosServer
```
