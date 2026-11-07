---
title: "API Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/reference-api-overview"
---

This topic describes TOS APIs and their features.

<span id="d83cf380"></span>
## **Bucket**


|**Category** |**API** |**Feature** |
|---|---|---|
|Basic operation |[CreateBucket](https://docs.byteplus.com/docs/tos/reference-createbucket) |Creates a bucket. |
||[DeleteBucket](https://docs.byteplus.com/docs/tos/reference-deletebucket) |Deletes a bucket. |
||[HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket) |Queries whether the bucket metadata exists. |
||[ListBuckets](https://docs.byteplus.com/docs/tos/reference-listbuckets) |Lists all buckets. |
||[GetBucketLocation](https://docs.byteplus.com/docs/tos/reference-getbucketlocation) |Gets the region information of the bucket. |
||[GetBucketInfo](https://docs.byteplus.com/docs/tos/Getbucketinfo) |Query the configuration information of the storage bucket. |
|Bucket ACL |[PutBucketACL](https://docs.byteplus.com/docs/tos/reference-putbucketacl) |Sets a bucket ACL. |
||[GetBucketACL](https://docs.byteplus.com/docs/tos/reference-getbucketacl) |Gets the ACL of a specified bucket. |
|Lifecycle rules |[PutBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-putbucketlifecycle) |Sets lifecycle rules. |
||[GetBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-getbucketlifecycle) |Gets lifecycle rules. |
||[DeleteBucketLifecycle](https://docs.byteplus.com/docs/tos/reference-deletebucketlifecycle) |Deletes lifecycle rules. |
|Access monitor |[PutBucketAccessMonitor](https://docs.byteplus.com/docs/tos/PutBucketAccessMonitor) |Sets access monitor |
||[GetBucketAccessMonitor](https://docs.byteplus.com/docs/tos/GetBucketAccessMonitor) |Gets access monitor |
|CORS rule |[PutBucketCORS](https://docs.byteplus.com/docs/tos/reference-putbucketcors) |Sets a CORS rule. |
||[GetBucketCORS](https://docs.byteplus.com/docs/tos/reference-getbucketcors) |Gets a CORS rule. |
||[DeleteBucketCORS](https://docs.byteplus.com/docs/tos/reference-deletebucketcors) |Deletes a CORS rule. |
|Bucket inventory |[PutBucketInventory](https://docs.byteplus.com/docs/tos/PutBucketInventory) |Create a bucket inventory. |
||[GetBucketInventory](https://docs.byteplus.com/docs/tos/GetBucketInventory) |View a bucket inventory. |
||[ListBucketInventory](https://docs.byteplus.com/docs/tos/ListBucketInventory) |Batch retrieve all bucket inventorys. |
||[DeleteBucketInventory](https://docs.byteplus.com/docs/tos/DeleteBucketInventory) |Delete specified bucket inventory. |
|Bucket policy |[PutBucketPolicy](https://docs.byteplus.com/docs/tos/reference-putbucketpolicy) |Sets a bucket policy. |
||[GetBucketPolicy](https://docs.byteplus.com/docs/tos/reference-getbucketpolicy) |Gets a bucket policy. |
||[DeleteBucketPolicy](https://docs.byteplus.com/docs/tos/reference-deletebucketpolicy) |Deletes a bucket policy. |
|Default storage type |[PutBucketStorageClass](https://docs.byteplus.com/docs/tos/reference-putbucketstorageclass) |Sets the default storage type for a bucket. |
|Bucket replication |[PutBucketReplication](https://docs.byteplus.com/docs/tos/Putbucketreplication) |Sets a same\-region replication rule or a cross region replication rule |
||[GetBucketReplication](https://docs.byteplus.com/docs/tos/Getbucketreplication) |Gets a same\-region replication rule or a cross region replication rule |
||[DeleteBucketReplication](https://docs.byteplus.com/docs/tos/Deletebucketreplication) |Deletes a same\-region replication rule or a cross region replication rule |
|Static website |[PutBucketWebsite](https://docs.byteplus.com/docs/tos/Putbucketwebsite) |Set the Bucket to a static website. |
||[GetBucketWebsite](https://docs.byteplus.com/docs/tos/Getbucketwebsite) |Get the website configuration. |
||[DeleteBucketWebsite](https://docs.byteplus.com/docs/tos/Deletebucketwebsite) |Delete the website configuration. |
|Versioning |[PutBucketVersioning](https://docs.byteplus.com/docs/tos/Putbucketversioning) |Set version control features for the bucket. |
||[GetBucketVersioning](https://docs.byteplus.com/docs/tos/Getbucketversioning) |Check the version control status of a bucket. |
|Custom domain name |[PutBucketCustomDomain](https://docs.byteplus.com/docs/tos/Putbucketcustomdomain) |Bind a custom domain to a bucket. |
||[GetBucketCustomDomain](https://docs.byteplus.com/docs/tos/Getbucketcustomdomain) |Get the custom domain name configuration. |
||[DeleteBucketCustomDomain](https://docs.byteplus.com/docs/tos/Deletebucketcustomdomain) |Delete the custom domain name configuration. |
|Server\-side Encryption |[PutBucketEncryption](https://docs.byteplus.com/docs/tos/Putbucketencryption) |Set server\-side encryption for buckets. |
||[GetBucketEncryption](https://docs.byteplus.com/docs/tos/Getbucketencryption) |Get the server\-side encryption configuration for the specified bucket |
||[DeleteBucketEncryption](https://docs.byteplus.com/docs/tos/Deletebucketencryption) |Delete the server\-side encryption configuration of the bucket |
|Bucket tag |[PutBucketTagging](https://docs.byteplus.com/docs/tos/Putbuckettagging) |Set bucket tags. |
||[GetBucketTagging](https://docs.byteplus.com/docs/tos/Getbuckettagging) |Obtain the tagging information. |
||[DeleteBucketTagging](https://docs.byteplus.com/docs/tos/Deletebuckettagging) |Delete the tag information. |
|Rename |[PutBucketRename](https://docs.byteplus.com/docs/tos/Putbucketrename) |Enable the RenameObject feature. |
||[GetBucketRename](https://docs.byteplus.com/docs/tos/Getbucketrename) |Query whether the RenameObject function of the storage bucket is enabled. |
||[DeleteBucketRename](https://docs.byteplus.com/docs/tos/Deletebucketrename) |Disable the RenameObject feature. |
|Data processing |[Pm3u8](https://docs.byteplus.com/docs/tos/Pm3u8) |Obtain download authorization for private m3u8 files. |
|Event notification |[PutBucketNotificationV2](https://docs.byteplus.com/docs/tos/PutBucketNotificationV2) |Configure event notification rules. |
||[GetBucketNotificationV2](https://docs.byteplus.com/docs/tos/GetBucketNotificationV2) |Query event notification rules. |


#{.custom\-md\-table}#

&nbsp;

<span id="6d09d867"></span>
## **Object**


|**Category** |**API** |**Feature** |
|---|---|---|
|Basic operation |[CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |Copies an object. |
||[DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject) |Deletes an object. |
||[DeleteMultiObjects](https://docs.byteplus.com/docs/tos/reference-deletemultiobjects) |Batch deletes objects. |
||[GetObject](https://docs.byteplus.com/docs/tos/reference--getobject) |Gets an object. |
||[HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject) |Queries whether an object exists. |
||[AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject) |Appends data to an object. |
||[ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects) |Lists objects in a bucket. |
||[ListObjectsV2](https://docs.byteplus.com/docs/tos/reference-listobjectsv2) |Lists objects in a bucket. |
||[ListObjectVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions) |Lists the version information of all objects in a bucket. |
||[PutObject](https://docs.byteplus.com/docs/tos/reference-putobject) |Uploads an object. |
||[PostObject](https://docs.byteplus.com/docs/tos/reference-postobject) |Uploads an object using a form. |
||[SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta) |Updates the metadata of an object uploaded to a bucket. |
||[RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject) |Restores an object from Archive Storage or Cold Archive. |
||[RenameObject](https://docs.byteplus.com/docs/tos/Renameobject) |Rename objects. |
|Object ACL |[PutObjectACL](https://docs.byteplus.com/docs/tos/reference-putobjectacl) |Sets an object ACL. |
||[GetObjectACL](https://docs.byteplus.com/docs/tos/reference-getobjectacl) |Gets the ACL of a specified object. |
|Object tag |[PutObjectTagging](https://docs.byteplus.com/docs/tos/reference-putobjecttagging-) |Sets object tags. |
||[GetObjectTagging](https://docs.byteplus.com/docs/tos/reference-getobjecttagging) |Gets object tags. |
||[DeleteObjectTagging](https://docs.byteplus.com/docs/tos/reference-deleteobjecttagging) |Deletes object tags. |
|Capture object |[FetchObject](https://docs.byteplus.com/docs/tos/Fetchobject) |Fetch resources from the specified URL and store the resource in the specified bucket. |
||[PutFetchTask](https://docs.byteplus.com/docs/tos/Putfetchtask) |Create an asynchronous task to fetch resources from a specified URL and store the resource in a specified bucket. |
||[GetFetchTask](https://docs.byteplus.com/docs/tos/Getfetchtask) |Query detailed information about asynchronous tasks. |
|Symbolic link |[PutSymlink](https://docs.byteplus.com/docs/tos/Putsymlink) |Create a symbolic link for an existing target file. |
||[GetSymlink](https://docs.byteplus.com/docs/tos/Getsymlink) |Obtain symlink object information. |


#{.custom\-md\-table}#

&nbsp;

<span id="97f8da88"></span>
## **Multipart upload**


|**API** |**Feature** |
|---|---|
|[CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload) |Initializes a multipart upload task. |
|[UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart) |Uploads part data. |
|[CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload) |Merges the uploaded parts into a complete object. |
|[AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload) |Cancels a multipart upload task. |
|[UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy) |Uploads a part by copying data from an existing object as data source. |
|[ListMultipartUploads](https://docs.byteplus.com/docs/tos/reference-listmultipartuploads) |Lists multipart upload tasks. |
|[ListParts](https://docs.byteplus.com/docs/tos/reference-listparts) |Lists uploaded parts. |
