---
title: "API Operations Supported by Single-Region Access Point"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/API-operations-supported-by-single-region-access-point"
---

When accessing TOS via a single\-region access point domain name, only some operations on TOS are supported. This document presents the list of API operations supported by single\-region access points.

<span id="374843e6"></span>
## Bucket Operations


|**Classification** |**Operation** |**Description** |
|---|---|---|
|Basic Operations |[ListObjects](https://docs.byteplus.com/docs/tos/reference-listobjects) |List the objects in the bucket. |
||[ListObjectVersions](https://docs.byteplus.com/docs/tos/reference-listobjectversions) |List multi\-version objects in the bucket. |
||[HeadBucket](https://docs.byteplus.com/docs/tos/reference-headbucket) |Determine whether the bucket exists and whether you have permission to access the bucket. |
|Bucket ACL |[GetBucketACL](https://docs.byteplus.com/docs/tos/reference-getbucketacl) |Obtain the access control permissions of the specified bucket. |
|Bucket Strategy |[GetBucketPolicy](https://docs.byteplus.com/docs/tos/reference-getbucketpolicy) |Get the bucket policy of the specified bucket. |
|Cross\-Origin Resource Sharing |[GetBucketCORS](https://docs.byteplus.com/docs/tos/reference-getbucketcors) |Retrieve the current Cross\-Origin Resource Sharing (CORS) configuration rules for the specified storage bucket. |


<span id="7bdb1cb0"></span>
## Object Operations


|**Classification** |**Operation** |**Description** |
|---|---|---|
|Basic Operations |[GetObject](https://docs.byteplus.com/docs/tos/reference--getobject) |Download the specified object. |
||[PutObject](https://docs.byteplus.com/docs/tos/reference-putobject) |Add objects to the bucket. |
||[HeadObject](https://docs.byteplus.com/docs/tos/reference-headobject) |Retrieve the metadata of the object. |
||[DeleteObject](https://docs.byteplus.com/docs/tos/reference-deleteobject) |Delete the specified object. |
||[RestoreObject](https://docs.byteplus.com/docs/tos/reference-restoreobject) |Restore object. |
||[AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject) |Append\-write the object. |
||[CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject) |Copy object. |
||[SetObjectMeta](https://docs.byteplus.com/docs/tos/reference-setobjectmeta) |Update object metadata. |
||[SetObjectExpires](https://docs.byteplus.com/docs/tos/SetObjectExpires) |Add an expiration time to an object, or modify the expiration time of an object. |
||[RenameObject](https://docs.byteplus.com/docs/tos/Renameobject) |Rename object. |
|Object ACL |[PutObjectACL](https://docs.byteplus.com/docs/tos/reference-putobjectacl) |Set the access control permissions (ACL) for the object. |
||[GetObjectACL](https://docs.byteplus.com/docs/tos/reference-getobjectacl) |Obtain the access control permissions (ACL) of the specified object. |
|Object Tag |[PutObjectTagging](https://docs.byteplus.com/docs/tos/reference-putobjecttagging-) |Set and update the tag information of the object. |
||[GetObjectTagging](https://docs.byteplus.com/docs/tos/reference-getobjecttagging) |Retrieve the label information of the object. |
||[DeleteObjectTagging](https://docs.byteplus.com/docs/tos/reference-deleteobjecttagging) |Delete the tag information of the object. |
|Crawling Target |[FetchObject](https://docs.byteplus.com/docs/tos/Fetchobject) |Fetch resources from the specified URL and store them in the storage bucket. |
|Symbolic link |[PutSymlink](https://docs.byteplus.com/docs/tos/Putsymlink) |Create a symbolic link. |
||[GetSymlink](https://docs.byteplus.com/docs/tos/Getsymlink) |Obtain symbolic link object information. |
|Object WORM |[PutObjectRetention](https://docs.byteplus.com/docs/tos/Putobjectretention) |Create or modify the retention policy for an object. |
||[GetObjectRetention](https://docs.byteplus.com/docs/tos/Getobjectretention) |Retrieve the retention policy information of the object. |
|Multipart Upload |[CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload) |Initialize multipart upload task. |
||[UploadPart](https://docs.byteplus.com/docs/tos/reference-uploadpart) |Upload chunked data. |
||[CompleteMultipartUpload](https://docs.byteplus.com/docs/tos/reference-completemultipartupload) |Merge the already uploaded chunks. |
||[AbortMultipartUpload](https://docs.byteplus.com/docs/tos/reference-abortmultipartupload) |Cancel multipart upload task. |
||[UploadPartCopy](https://docs.byteplus.com/docs/tos/reference-uploadpartcopy) |Copy part or all of an uploaded object to create a part. |
||[ListMultipartUploads](https://docs.byteplus.com/docs/tos/reference-listmultipartuploads) |List ongoing multipart upload tasks. |
