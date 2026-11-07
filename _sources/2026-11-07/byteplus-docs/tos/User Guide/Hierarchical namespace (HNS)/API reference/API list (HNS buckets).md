---
title: "API list (HNS buckets)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/API-list-hierarchical-bucket"
---

This article primarily introduces the status of API support for hierarchical namespaces. HNS buckets and FNS buckets share most APIs. You may refer to this document to understand the API differences between HNS buckets and FNS buckets. If this API is only supported for use in HNS buckets, this will be specified separately in this documentation.

<span id="25107581"></span>
## Background Information

This document provides only the list of APIs supported by HNS buckets. For detailed information on features supported by other access methods, please refer to the following documents:


* [Console feature list (HNS buckets)](https://docs.byteplus.com/docs/tos/Console-function-list-hierarchical-buckets)

* [SDK overview (HNS buckets)](https://docs.byteplus.com/docs/tos/Sdk-overview-hierarchical-bucket)

* [Tool overview (HNS buckets)](https://docs.byteplus.com/docs/tos/Tool-overview-hierarchical-bucket)


<span id="d63bb5f4"></span>
## Precautions

The following provides an explanation of the identifiers used in the table:


* ✅: Indicates support for this function.

* ✔️: Indicates partial support; please refer to the remarks for specific details.

* ❌: Indicates that this function is not supported.


<span id="e7973e23"></span>
## Bucket


|**Classification** |**API** |**Function** |Is HNS bucket supported? |Explanation of differences |
|---|---|---|---|---|
|Basic Operations |[CreateBucket](https://docs.byteplus.com/en/docs/tos/reference-createbucket) |Create bucket. |✅ |* The header field `x-tos-az-redundancy` only supports `single-az` (single AZ redundancy).<br><br>* Please add the header field `x-tos-bucket-type`, which indicates the bucket type. Parameter type: string. This is an optional parameter. The value description is as follows:<br><br>   * `fns`: FNS bucket.<br><br>   * `hns`: HNS bucket.<br><br>      If this message header is not included, an fns bucket will be created by default. |
||[DeleteBucket](https://docs.byteplus.com/en/docs/tos/reference-deletebucket) |Delete bucket. |✅ | |
||[HeadBucket](https://docs.byteplus.com/en/docs/tos/reference-headbucket) |Check whether bucket metadata exists. |✅ |* HNS bucket: The response message header carries the header field `x-tos-bucket-type`, with the value `hns`.<br><br>* FNS bucket: The response message header does not include the header field `x-tos-bucket-type`. |
||[ListBuckets](https://docs.byteplus.com/en/docs/tos/reference-listbuckets) |List all buckets. |✅ |* Please add the header field `x-tos-bucket-type` to clarify the content of the retrieved list using this message header. Parameter type: String. This is an optional parameter. The possible values are described as follows:<br><br>   * `hns`: Retrieve the list of all HNS buckets.<br><br>   * `fns`: Retrieve the list of all FNS buckets.<br><br>      If this header is not included, the list of all buckets will be retrieved.<br><br>* In the response message, a new `BucketType` has been added to indicate the bucket type. The parameter type is String. The possible values are as follows:<br><br>   * fns: FNS bucket.<br><br>   * hns: HNS bucket. |
||[PutBucketStorageClass](https://docs.byteplus.com/en/docs/tos/reference-putbucketstorageclass) |Set the default storage type for the bucket. |✅ | |
||[GetBucketLocation](https://docs.byteplus.com/en/docs/tos/reference-getbucketlocation) |Query the region information of the current bucket. |✅ | |
||[GetBucketInfo](https://docs.byteplus.com/en/docs/tos/Getbucketinfo) |Query the configuration information of the storage bucket. |✅ | |
|Lifecycle Rule |[PutBucketLifecycle](https://docs.byteplus.com/en/docs/tos/reference-putbucketlifecycle) |Set lifecycle rules. |✅ |Because HNS buckets do not support multiple versions, only the expiration attribute for deleting the latest version of an object can be specified. |
||[GetBucketLifecycle](https://docs.byteplus.com/en/docs/tos/reference-getbucketlifecycle) |Query lifecycle rules. |✅ | |
||[DeleteBucketLifecycle](https://docs.byteplus.com/en/docs/tos/reference-deletebucketlifecycle) |Delete lifecycle rules. |✅ | |
|Access Tracking |[PutBucketAccessMonitor](https://docs.byteplus.com/en/docs/tos/PutBucketAccessMonitor) |Set up access tracking for the bucket. |✅ | |
||[GetBucketAccessMonitor](https://docs.byteplus.com/en/docs/tos/GetBucketAccessMonitor) |Obtain the configuration information for access tracking. |✅ | |
|Bucket ACL |[PutBucketACL](https://docs.byteplus.com/en/docs/tos/reference-putbucketacl) |Set the access control permissions for the bucket. |✅ | |
||[GetBucketACL](https://docs.byteplus.com/en/docs/tos/reference-getbucketacl) |Obtain the access control permissions for the specified bucket. |✅ | |
|Cross\-Domain Access Rule |[PutBucketCORS](https://docs.byteplus.com/en/docs/tos/reference-putbucketcors) |Configure cross\-origin access rules. |✅ | |
||[GetBucketCORS](https://docs.byteplus.com/en/docs/tos/reference-getbucketcors) |Query cross\-origin access rules. |✅ | |
||[DeleteBucketCORS](https://docs.byteplus.com/en/docs/tos/reference-deletebucketcors) |Delete the cross\-origin access rules. |✅ | |
|Bucket List |[PutBucketInventory](https://docs.byteplus.com/en/docs/tos/PutBucketInventory) |Create a bucket inventory. |✅ | |
||[GetBucketInventory](https://docs.byteplus.com/en/docs/tos/GetBucketInventory) |View the list of buckets. |✅ | |
||[ListBucketInventory](https://docs.byteplus.com/en/docs/tos/ListBucketInventory) |Batch retrieve the inventories of all buckets. |✅ | |
||[DeleteBucketInventory](https://docs.byteplus.com/en/docs/tos/DeleteBucketInventory) |Delete the specified bucket inventory. |✅ | |
|Bucket Policy |[PutBucketPolicy](https://docs.byteplus.com/en/docs/tos/reference-putbucketpolicy) |Set bucket policy. |✅ | |
||[GetBucketPolicy](https://docs.byteplus.com/en/docs/tos/reference-getbucketpolicy) |Query bucket policy. |✅ | |
||[DeleteBucketPolicy](https://docs.byteplus.com/en/docs/tos/reference-deletebucketpolicy) |Delete bucket policy. |✅ | |
|Origin Retrieval Rule |[PutBucketMirrorBack](https://docs.byteplus.com/en/docs/tos/Putbucketmirrorback) |Set origin rules. |✅ | |
||[GetBucketMirrorBack](https://docs.byteplus.com/en/docs/tos/Getbucketmirrorback) |Query Origin Rules |✅ | |
||[DeleteBucketMirrorBack](https://docs.byteplus.com/en/docs/tos/Deletebucketmirrorback) |Delete the origin rule. |✅ | |
|Bucket Replication |[PutBucketReplication](https://docs.byteplus.com/en/docs/tos/Putbucketreplication) |Set cross\-region replication rules and same\-region replication rules. |✅ | |
||[GetBucketReplication](https://docs.byteplus.com/en/docs/tos/Getbucketreplication) |Query cross\-region replication rules and same\-region replication rules. |✅ | |
||[DeleteBucketReplication](https://docs.byteplus.com/en/docs/tos/Deletebucketreplication) |Delete cross\-region replication rules and same\-region replication rules. |✅ | |
|Version Control |[PutBucketVersioning](https://docs.byteplus.com/en/docs/tos/Putbucketversioning) |Set up version control. |❌ | |
||[GetBucketVersioning](https://docs.byteplus.com/en/docs/tos/Getbucketversioning) |Retrieve version control status. |❌ | |
|Static Website Hosting |[PutBucketWebsite](https://docs.byteplus.com/en/docs/tos/Putbucketwebsite) |Configure static website hosting rules. |✅ | |
||[GetBucketWebsite](https://docs.byteplus.com/en/docs/tos/Getbucketwebsite) |Query static website hosting rules. |✅ | |
||[DeleteBucketWebsite](https://docs.byteplus.com/en/docs/tos/Deletebucketwebsite) |Delete static website hosting rules. |✅ | |
|Event Notification |[PutBucketNotificationV2](https://docs.byteplus.com/en/docs/tos/PutBucketNotificationV2) |Set event notification rules. |❌ | |
||[GetBucketNotificationV2](https://docs.byteplus.com/en/docs/tos/GetBucketNotificationV2) |Query event notification rules. |❌ | |
|Custom Domain Name |[PutBucketCustomDomain](https://docs.byteplus.com/en/docs/tos/Putbucketcustomdomain) |Set a custom domain name. |✅ | |
||[GetBucketCustomDomain](https://docs.byteplus.com/en/docs/tos/Getbucketcustomdomain) |Query custom domain name. |✅ | |
||[DeleteBucketCustomDomain](https://docs.byteplus.com/en/docs/tos/Deletebucketcustomdomain) |Delete custom domain name. |✅ | |
|Server\-Side Encryption |[PutBucketEncryption](https://docs.byteplus.com/en/docs/tos/Putbucketencryption) |Set server\-side encryption. |❌ | |
||[GetBucketEncryption](https://docs.byteplus.com/en/docs/tos/Getbucketencryption) |Retrieve the server\-side encryption configuration. |❌ | |
||[DeleteBucketEncryption](https://docs.byteplus.com/en/docs/tos/Deletebucketencryption) |Delete server\-side encryption configuration. |❌ | |
|Bucket Label |[PutBucketTagging](https://docs.byteplus.com/en/docs/tos/Putbuckettagging) |Set bucket labels. |✅ | |
||[GetBucketTagging](https://docs.byteplus.com/en/docs/tos/Getbuckettagging) |Obtain the tag information of the specified bucket. |✅ | |
||[DeleteBucketTagging](https://docs.byteplus.com/en/docs/tos/Deletebuckettagging) |Delete the tag information of the specified bucket. |✅ | |
|Rename |[PutBucketRename](https://docs.byteplus.com/en/docs/tos/Putbucketrename) |Enable the RenameObject feature. |❌ |HNS buckets support the Rename feature by default; there is no need to enable it. |
||[GetBucketRename](https://docs.byteplus.com/en/docs/tos/Getbucketrename) |Check whether the RenameObject feature is enabled. |❌ |HNS buckets support the Rename function by default; no query is required. |
||[DeleteBucketRename](https://docs.byteplus.com/en/docs/tos/Deletebucketrename) |Disable the RenameObject feature. |❌ |The HNS bucket supports the Rename feature by default and does not need to be disabled. |
|Recycle Bin |[PutBucketTrash](https://docs.byteplus.com/en/docs/tos/PutBucketTrash) |Enable the Recycle Bin feature. |✅ |Only hierarchical namespaces support the recycle bin feature. For details, see [Recycle Bin](https://docs.byteplus.com/docs/tos/Recycle-bin). |
||[GetBucketTrash](https://docs.byteplus.com/en/docs/tos/GetBucketTrash) |Obtain detailed information about the Recycle Bin. |✅ |Only HNS namespaces support the recycle bin feature. For details, see [Recycle Bin](https://docs.byteplus.com/docs/tos/Recycle-bin). |
|Data Processing |[Pm3u8](https://docs.byteplus.com/en/docs/tos/Pm3u8) |Obtain download authorization for private m3u8. |❌ | |
|Requester Pays |[PutBucketRequestPayment](https://docs.byteplus.com/en/docs/tos/PutBucketRequestPayment) |Set the payment mode for the bucket. |✅ | |
||[GetBucketRequestPayment](https://docs.byteplus.com/en/docs/tos/GetBucketRequestPayment) |View the payment mode of the bucket. |✅ | |
|TLS Version |[PutBucketHttpsConfig](https://docs.byteplus.com/en/docs/tos/Putbuckethttpsconfig) |Enable or disable the TLS version setting feature. |✅ | |
||[GetBucketHttpsConfig](https://docs.byteplus.com/en/docs/tos/Getbuckethttpsconfig) |View TLS Version. |✅ | |


<span id="e794ab5c"></span>
## Object


|**Classification** |**API** |**Function** |Is HNS bucket supported? |Explanation of differences |
|---|---|---|---|---|
|Basic Operations |[CopyObject](https://docs.byteplus.com/en/docs/tos/reference-copyobject) |Copy object. |✅ |* Does not support including the header field `x-tos-server-side-encryption-*`.<br><br>* The header field `x-tos-storage-class` is supported; however, directories only support the `STANDARD` (standard storage) storage type.<br><br>* Soft copy is not supported; only hard copy is supported.<br><br>* When both the source and destination are HNS buckets, only file\-to\-file and directory\-to\-directory copying are supported; files and directories cannot be copied to each other.<br><br>* Copying a directory only copies the directory object itself and does not recursively copy subfiles or subdirectories.<br><br>* When the source is an FNS bucket and the destination is an HNS bucket, copying non\-empty source objects whose keys are in directory format as objects with directory\-format keys is not supported. |
||[DeleteObject](https://docs.byteplus.com/en/docs/tos/reference-deleteobject) |Delete object. |✅ |Deleting a non\-empty directory is not supported. |
||[DeleteMultiObjects](https://docs.byteplus.com/en/docs/tos/reference-deletemultiobjects) |Batch Delete Objects. |✅ |Only file deletion is supported; directory deletion is not supported. If a batch deletion request contains both files and directories, the files will be deleted successfully, while the directories will fail to be deleted. |
||[GetObject](https://docs.byteplus.com/en/docs/tos/reference--getobject) |Get object. |✅ |* When the object is a directory, the response includes the header field `x-tos-directory` with a value of `true`.<br><br>* After a file is uploaded, the Etag field in the response header of a GetObject request is the MD5 value of the file. After the file is modified and written, the Etag field in the response header of a GetObject request is the crc64 value of the file.<br><br>* When the request target is a directory, the response header does not include the Etag.<br><br>* The requested key begins with the specified value.`/`At the end, if the object is not actually a directory, return 409.<br><br>* If a file exists with the same name as an intermediate\-level directory in the requested key, a 409 response is returned. |
||[HeadObject](https://docs.byteplus.com/en/docs/tos/reference-headobject) |Check whether the object exists. |✅ |* When the object is a directory, the response header includes the header field `x-tos-directory` with a value of `true`.<br><br>* After a file is uploaded, the Etag field in the response header of the HeadObject request contains the MD5 value of the file. When the file is modified and written, the Etag field in the response header contains the crc64 value of the file.<br><br>* When the request target is a directory, the response header does not include the Etag.<br><br>* If the requested key ends with `/` and the object is not actually a directory, return 409.<br><br>* If a file exists with the same name as an intermediate\-level directory in the requested key, return 409. |
||[AppendObject](https://docs.byteplus.com/en/docs/tos/reference-appendobject) |Append a write object. |✔️ |HNS buckets support using ModifyObject to append objects. For more details, see [ModifyObject](https://docs.byteplus.com/docs/tos/Modifyobject). |
||[ModifyObject](https://docs.byteplus.com/en/docs/tos/Modifyobject) |Modify the write object.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Only HNS buckets support this interface.</div><br> |✅ |* Currently, only the append operation is supported, which requires a valid `offset`. The response header includes `x-next-modify-offset`, which should be used as the `offset` for the next modification write.<br><br>* Modification, write, and upload operations are not supported for non\-existent objects.<br><br>* A modify write operation requires specifying `Content-Length`, and `Content-Length` must be greater than 0; that is, a modify write operation must include data.<br><br>* After a file is modified and written, the Etag field in the response headers of HeadObject and GetObject is set to the file's crc64 value.<br><br>* The response header includes an Etag, which is the MD5 hash of the data uploaded in this session.<br><br>* The response header includes the CRC64 value, which corresponds to the CRC64 of the object after this modification and write operation. |
||[ListObjects](https://docs.byteplus.com/en/docs/tos/reference-listobjects) |List objects in the bucket. |✅ |The Query must include `delimiter`, and its value must be`/`. |
||[ListObjectsV2](https://docs.byteplus.com/en/docs/tos/reference-listobjectsv2) |List Bucket Objects (V2) |✅ |The Query must include `delimiter`, and its value must be`/`. |
||[ListObjectVersions](https://docs.byteplus.com/en/docs/tos/reference-listobjectversions) |List the version information of all objects in the bucket. |❌ | |
||[PutObject](https://docs.byteplus.com/en/docs/tos/reference-putobject) |Upload Objects |✅ |* The server considers that the client intends to operate on a directory when the requested key ends with `/`. Otherwise, the server operates on the actual object.<br><br>* Files and directories do not support overwriting each other.<br><br>* Directory overwrite is not supported. When uploading a directory that already exists, a 200 response is returned, but the directory will not be overwritten.<br><br>* If you upload an object with a directory\-formatted key, meaning one that ends in `/` , the object type is a directory. Otherwise, the object type is a file.<br><br>* If an intermediate directory does not exist, it will be created automatically.<br><br>* Data cannot be included when uploading a directory.<br><br>* Chunk mode upload is not supported.<br><br>* The header field `x-tos-storage-class` is supported; however, directories only support the `STANDARD` (standard storage) storage type. |
||[PostObject](https://docs.byteplus.com/en/docs/tos/reference-postobject) |Use a form to upload an object. |✅ |* The server considers that the client intends to operate on a directory when the requested key ends with `/`. Otherwise, the server operates on the actual object.<br><br>* Files and directories cannot overwrite each other.<br><br>* Directory overwrite is not supported. When uploading a directory that already exists, a 200 response is returned, but the directory will not be overwritten.<br><br>* If you post an object with a directory\-formatted key, meaning one that ends in `/`, the object type is a directory. Otherwise, the object type is a file.<br><br>* If an intermediate directory does not exist, it will be created automatically.<br><br>* Data cannot be included when uploading a directory.<br><br>* Supports chunk mode upload.<br><br>* Supports the header field `x-tos-storage-class`, but directories only support the `STANDARD` (standard storage) storage type. |
||[SetObjectMeta](https://docs.byteplus.com/en/docs/tos/reference-setobjectmeta) |Update the metadata of objects already uploaded to the bucket. |✅ | |
||[SetObjectExpires](https://docs.byteplus.com/en/docs/tos/SetObjectExpires) |Add an expiration time to an object, or modify the expiration time of an object. |✅ | |
||[RestoreObject](https://docs.byteplus.com/en/docs/tos/reference-restoreobject) |Restore archived, cold archived, and deep cold archived objects. |✅ | |
||[RenameObject](https://docs.byteplus.com/en/docs/tos/Renameobject) |Rename Object. |✅ |Renaming a directory to an existing directory is not supported. |
|Access Control |[PutObjectACL](https://docs.byteplus.com/en/docs/tos/reference-putobjectacl) |Set the access control permissions for the object. |✅ | |
||[GetObjectACL](https://docs.byteplus.com/en/docs/tos/reference-getobjectacl) |Obtain the access control permissions for the specified object. |✅ | |
|Object Label |[PutObjectTagging](https://docs.byteplus.com/en/docs/tos/reference-putobjecttagging-) |Set object label. |✅ | |
||[GetObjectTagging](https://docs.byteplus.com/en/docs/tos/reference-getobjecttagging) |View object label information. |✅ | |
||[DeleteObjectTagging](https://docs.byteplus.com/en/docs/tos/reference-deleteobjecttagging) |Delete object tag. |✅ | |
|Crawling Object |[FetchObject](https://docs.byteplus.com/en/docs/tos/Fetchobject) |Fetch resources from the specified URL and store them in the designated storage bucket. |✅ | |
||[PutFetchTask](https://docs.byteplus.com/en/docs/tos/Putfetchtask) |Create an asynchronous task to fetch resources from a specified URL and store them in the designated storage bucket. |❌ | |
||[GetFetchTask](https://docs.byteplus.com/en/docs/tos/Getfetchtask) |Query detailed information about the asynchronous task. |❌ | |
|Symbolic Link |[PutSymlink](https://docs.byteplus.com/en/docs/tos/Putsymlink) |Create a symbolic link. |✅ | |
||[GetSymlink](https://docs.byteplus.com/en/docs/tos/Getsymlink) |Retrieve symbolic link object information. |✅ | |


<span id="c2aa0d42"></span>
## Multipart upload


|**API** |**Function** |Is HNS bucket supported? |Explanation of differences |
|---|---|---|---|
|[CreateMultipartUpload](https://docs.byteplus.com/en/docs/tos/reference-createmultipartupload) |Initialize multipart upload task. |✅ |* The requested key does not support beginning with`/`Conclusion;<br><br>* If an intermediate directory does not exist, it will be created automatically.<br><br>* Directory overwrite is not supported; if the last segment of the uploaded object's path is an existing directory, a 409 error is returned.<br><br>* The header field `x-tos-storage-class` is supported; however, directories only support the `STANDARD` (Standard Storage) storage type. |
|[UploadPart](https://docs.byteplus.com/en/docs/tos/reference-uploadpart) |Upload shard data. |✅ |* Chunk mode upload is not supported. |
|[CompleteMultipartUpload](https://docs.byteplus.com/en/docs/tos/reference-completemultipartupload) |Merge and upload all fragment data of the entire object. |✅ | |
|[AbortMultipartUpload](https://docs.byteplus.com/en/docs/tos/reference-abortmultipartupload) |Cancel multipart upload task. |✅ | |
|[UploadPartCopy](https://docs.byteplus.com/en/docs/tos/reference-uploadpartcopy) |Upload the object using multipart replication. |✅ |* The header field `x-tos-server-side-encryption-*` is not supported.<br><br>* Soft copy is not supported; only hard copy is supported.<br><br>* When both the source and destination are HNS buckets, only file\-to\-file and directory\-to\-directory copying are supported; files and directories cannot be copied to each other.<br><br>* Copying a directory only copies the directory object itself and does not recursively copy subfiles or subdirectories.<br><br>* When the source is an FNS bucket and the destination is an HNS bucket, copying non\-empty directory\-style keys is not supported. |
|[ListMultipartUploads](https://docs.byteplus.com/en/docs/tos/reference-listmultipartuploads) |List multipart upload tasks. |✅ | |
|[ListParts](https://docs.byteplus.com/en/docs/tos/reference-listparts) |List the already uploaded fragments. |✅ | |
