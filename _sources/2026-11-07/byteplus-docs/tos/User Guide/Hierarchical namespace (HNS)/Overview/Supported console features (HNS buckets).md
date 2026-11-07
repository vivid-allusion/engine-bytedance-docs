---
title: "Supported console features (HNS buckets)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Console-function-list-hierarchical-buckets"
---

This article describes the status of functional support for hierarchical namespaces when accessed via the TOS Console.

<span id="e2a0011e"></span>
## Background Information

This document only describes the features supported by the TOS Console. For details on features supported by other access methods, please refer to the following documents:


* [API List (Tiered Buckets)](https://docs.byteplus.com/docs/tos/API-list-hierarchical-bucket)

* [SDK Overview (Layered Bucket)](https://docs.byteplus.com/docs/tos/Sdk-overview-hierarchical-bucket)

* [Tool Overview (Layered Bucket)](https://docs.byteplus.com/docs/tos/Tool-overview-hierarchical-bucket)


<span id="67bc13b0"></span>
## Precautions

The following is an explanation of the symbols used in the table:


* ✅: Indicates support for this function.

* ✔️: Indicates partial support; for specific details, please refer to the remarks.

* ❌: Indicates that this feature is not supported.


<span id="6a8bf788"></span>
## Bucket Level


|Function |Description |Is it supported |Note |
|---|---|---|---|
|[Storage Type](https://docs.byteplus.com/en/docs/tos/docs-storage-type) |TOS offers multiple storage types, including Standard, Infrequent Access, Archive, Cold Archive, and Deep Cold Archive, comprehensively covering a wide range of data storage scenarios from hot to cold. |✅ |For the support status of the multi\-AZ redundancy feature for HNS buckets, please refer to the console display. |
|[Lifecycle Rule](https://docs.byteplus.com/en/docs/tos/Lifecycle-rules-overview) |Lifecycle management supports scheduled conversion of storage types and object deletion. It also supports deletion of cold data, such as archived and deep cold archive data. |✅ |* The directory only has the standard storage type and will not convert the storage type.<br><br>* Directories that meet the expiration criteria will only be deleted after all files and directories under the directory have been deleted (deletion of non\-empty directories is not supported). |
|[Set up static website](https://docs.byteplus.com/en/docs/tos/Set-up-a-static-website) |TOS supports hosting static websites. You can store all content of your static website in a TOS bucket. After configuring static website rules, you can access the website via the bucket domain name. |✅ | |
|[Back-to-origin rules](https://docs.byteplus.com/en/docs/tos/Overview9) |After configuring origin retrieval rules for the bucket, if the requested object does not exist in the bucket, TOS will retrieve the target file from the origin server specified in the rule. |✅ | |
|[Event Notification](https://docs.byteplus.com/en/docs/tos/Event-notification-overview) |TOS supports delivering certain event changes to Function Service, enabling you to monitor resource changes in TOS in real time. |✅ |The event notification feature of HNS buckets only supports the following events:<br><br><br>* tos:ObjectCreated:Put<br><br>* tos:ObjectCreated:Post<br><br>* tos:ObjectCreated:Copy<br><br>* tos:ObjectCreated:CompleteUpload<br><br>* tos:ObjectCreated:Modify<br><br>* tos:ObjectRemoved:Delete<br><br>* tos:ObjectRemoved:TrashMoved<br><br>* tos:LifecycleExpiration:Delete<br><br>* tos:LifecycleExpiration:TrashMoved<br><br>* tos:ObjectRestore:Post<br><br>* tos:ObjectRestore:Completed<br><br>* tos:LifecycleTransition<br><br>* tos:ObjectRename |
|[Bucket Label](https://docs.byteplus.com/en/docs/tos/Set-bucket-tag) |You can use the bucket tagging feature to identify resources and to label and classify buckets according to various dimensions—such as purpose, type, owner, and environment—making it easier to manage buckets with similar characteristics. |✅ | |
|[Bucket List](https://docs.byteplus.com/en/docs/tos/Bucket-inventory) |You can use the bucket inventory feature to regularly obtain information about all objects or objects with a specified prefix within a specified bucket. The inventory includes details such as object size, storage type, and last updated date. |✅ |* The HNS bucket inventory does not support exporting object replication status or encryption status.<br><br>* When a bucket inventory rule is created for the first time, the bucket inventory file will be generated within 48 hours. |
|[Batch Processing](https://docs.byteplus.com/en/docs/tos/Batch-processing1) |The batch processing feature supports batch execution of certain operations on objects within a bucket, such as batch data replication, batch replacement of object ACLs, and more. |❌ | |
|[RenameObject](https://docs.byteplus.com/en/docs/tos/Use-renameobject) |TOS supports renaming objects using the RenameObject function. |✅ |There are differences compared to ordinary buckets. For details, please refer to the [API List (Tiered Buckets)](https://docs.byteplus.com/docs/tos/API-list-hierarchical-bucket). |
|[Bucket Policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5) |For policies configured for individual storage buckets and resources within the bucket, you can grant other users permissions to the relevant resources through bucket policies. |✅ | |
|[IAM Policy](https://docs.byteplus.com/en/docs/tos/docs-overview_6) |IAM is a permissions management system provided by BytePlus for customers, designed to control access to cloud resources by different identities. You can grant IAM users permissions to relevant resources through IAM policies. |✅ | |
|[Bucket ACL](https://docs.byteplus.com/en/docs/tos/docs-configuring-a-bucket-acl) |ACL is account\-based read and write access control; the owner of a bucket or object has full control over the resource. You can grant the IAM primary account read and write permissions for the current bucket and read and write permissions for the bucket ACL. After authorization, the authorized user can access the bucket using their own AKSK credentials. |✅ | |
|[Object ACL](https://docs.byteplus.com/en/docs/tos/docs-configuring-an-object-acl) |ACL is an account\-based read/write access control mechanism, and the owner of a bucket or object has full control over the resource. You can set file read/write permissions (ACL) for individual objects in the TOS Console. |✅ | |
|[Cross-Domain Access Settings](https://docs.byteplus.com/en/docs/tos/docs-cross-origin-resource-sharing-settings) |After configuring cross\-origin rules, when TOS receives a cross\-origin request or an OPTIONS request, it reads the corresponding CORS rules for the bucket, performs the necessary permission checks, and returns the appropriate headers to ensure the security of cross\-origin data transmission. |✅ | |
|[Custom Domain Name](https://docs.byteplus.com/en/docs/tos/Set-up-a-custom-domain-name) |If you want to use your own domain name to access files stored in TOS, you can bind your own domain name to the bucket. After binding, files can be accessed via the corresponding domain name. |✅ | |
|[Cross-Region Replication](https://docs.byteplus.com/en/docs/tos/Cross-region-replication-overview) |Cross\-region replication enables automatic copying of files from one bucket to other buckets in different regions, supports filtering files for replication as needed, and allows monitoring of replication progress. |❌ | |
|[Intra-region replication](https://docs.byteplus.com/en/docs/tos/Same-region-replication-overview) |Intra\-region replication enables automatic copying of files from one bucket to other buckets within the same region. It also supports filtering files for replication as needed and viewing the replication progress. |❌ | |
|[Version Control](https://docs.byteplus.com/en/docs/tos/docs-overview) |The version control feature enables retention of historical versions of storage bucket data, preventing accidental deletion of data within the bucket. |❌ | |
|[Multi-AZ Redundancy](https://docs.byteplus.com/en/docs/tos/Multi-az-redundancy) |The multi\-AZ redundancy feature enables your data to be stored across multiple availability zones within the same region. If one availability zone experiences a failure, the other zones can continue to provide stable storage services. |✔️ |Only North China 2 (Beijing) supports the multi\-AZ redundancy feature for tiered buckets. |
|[Image Style](https://docs.byteplus.com/en/docs/tos/docs-creating-an-image-style) |An image style refers to a template that includes multiple image processing parameters, such as format conversion and progressive display. You can use image styles to process multiple images in a unified manner, thereby simplifying operations. |❌ | |
|[Original Image Protection](https://docs.byteplus.com/en/docs/tos/docs-original-image-protection) |The original image protection feature is a safeguard for images designed to prevent the original image from being misappropriated by anonymous users. |❌ | |
|[Usage Statistics](https://docs.byteplus.com/en/docs/tos/docs-usage-statistics) |TOS supports viewing multiple basic data metrics for storage buckets, including usage, traffic, and request counts. |❌ | |
|[Log Management](https://docs.byteplus.com/en/docs/tos/Log-analysis) |You can use the log service to retrieve and analyze access logs generated during your visits to TOS, and view log reports. |❌ | |
|[Upload Callback](https://docs.byteplus.com/en/docs/tos/Upload-callback) |When making a request, the client includes a callback parameter. After the upload is completed, the server sends a synchronous POST callback request to the third\-party application server specified in the callback parameter. Only after the third\-party application server confirms receipt and returns a result does the server return all results to the client. |❌ | |
|[Server-Side Encryption](https://docs.byteplus.com/en/docs/tos/Server-side-encryption-overview) |TOS supports file\-level encryption of your uploaded data upon receipt, and persistently stores the encrypted data. When you download a file, TOS automatically decrypts the data and returns it to you. |❌ | |
|[Security Settings](https://docs.byteplus.com/en/docs/tos/Security-configuration) |Security settings refer to the configuration of warning levels for dangerous operations. When set to a high level, data deletion requires manual entry of confirmation information, which can effectively reduce the possibility of your accidental operation. |❌ | |
|[Image Processing](https://docs.byteplus.com/en/docs/tos/docs-image-processing_1) |TOS supports processing stored image files. You can use the GetObject interface and include relevant image processing parameters in your request to perform operations such as image resizing, image cropping, and image watermarking. |❌ | |
|[Video Processing](https://docs.byteplus.com/en/docs/tos/docs-overview_7) |TOS supports processing stored video files. You can use the GetObject interface and include relevant video processing parameters in your request to perform video frame extraction and obtain video metadata. |❌ | |
|[TOS accelerator](https://docs.byteplus.com/en/docs/tos/Overview11) |TOS supports Availability Zone (AZ) level accelerator functionality, caching frequently accessed files in TOS on high\-performance NVMe SSD storage media, supporting fast response with millisecond\-level latency and high\-throughput data transfer capabilities to meet business performance requirements. |✅ | |


<span id="c15b345c"></span>
## Object Level


|**Function** |**Description** |**Is it supported** |**Notes** |
|---|---|---|---|
|[Upload File](https://docs.byteplus.com/en/docs/tos/docs-uploading-a-file) |Upload local files to the storage bucket via the TOS console. |✅ | |
|[Download File](https://docs.byteplus.com/en/docs/tos/docs-downloading-a-file) |Download objects that have been uploaded to the storage bucket to your local device via the TOS console. |✅ | |
|[View File Details](https://docs.byteplus.com/en/docs/tos/docs-viewing-file-details) |TOS supports viewing detailed file information, including file name, file size, URL, storage type, and more. |✅ | |
|[Share File](https://docs.byteplus.com/en/docs/tos/Sharing-files) |After you upload files to object storage, you can share files or folders with other users via a URL. |✅ | |
|[Search File](https://docs.byteplus.com/en/docs/tos/docs-searching-for-files) |You can search for files in the storage bucket as needed in the TOS console (using prefix matching). |✅ | |
|[Rename File](https://docs.byteplus.com/en/docs/tos/docs-renaming-files) |You can change the names of files in a bucket via the TOS console. |✅ | |
|[Copy File](https://docs.byteplus.com/en/docs/tos/docs-copying-files) |TOS supports copying files or folders in a bucket to another path. |✅ | |
|[Move File](https://docs.byteplus.com/en/docs/tos/docs-moving-files) |TOS supports moving files or folders within a storage bucket to another path. |✅ | |
|[Managing Document Labels](https://docs.byteplus.com/en/docs/tos/docs-managing-file-labels) |TOS supports assigning tags to objects and manages the lifecycle of specific objects based on their tags. |✅ | |
|[Manage File Metadata](https://docs.byteplus.com/en/docs/tos/docs-managing-file-metadata) |File metadata is a set of key\-value pairs that describe file attributes. You can customize the file metadata. |✅ | |
|[Modify file access permissions](https://docs.byteplus.com/en/docs/tos/docs-modifying-the-file-access-permission) |Uploaded files automatically inherit the access permissions of the bucket. You can modify the access permissions (ACL) of individual files on the **File List** page. |✅ | |
|[Modify File Storage Type](https://docs.byteplus.com/en/docs/tos/docs-changing-the-file-storage-type) |TOS supports multiple storage types, and you can modify the storage type of a file as needed. |❌ | |
|[Delete File](https://docs.byteplus.com/en/docs/tos/docs-deleting-a-file) |To conserve storage space and reduce costs, you may delete files when you no longer need to keep stored files. |✅ | |
|[Shard Management](https://docs.byteplus.com/en/docs/tos/docs-managing-parts) |When you use multipart upload for large files, if the parts are not merged, they will be stored in the part list. You can view and delete shards in the shard list. |✅ | |
|[Create Folder](https://docs.byteplus.com/en/docs/tos/docs-creating-a-folder) |TOS supports folder functionality, enabling you to categorize and manage your files. |✅ | |
|[Delete Folder](https://docs.byteplus.com/en/docs/tos/docs-deleting-a-folder) |TOS supports deleting folders that are no longer needed. After deletion, both the folder and all files within it will be removed. |✅ | |
|[Restore File](https://docs.byteplus.com/en/docs/tos/docs-restoring-files) |Files stored in archive storage, cold archive, and deep cold archive must be restored before they can be accessed. |✅ | |
|[Task Center](https://docs.byteplus.com/en/docs/tos/docs-task-center) |TOS enables users to view task status and manage tasks in the Task Center after submitting operations such as uploading files, copying files, moving files, deleting directories, restoring files, or deleting multipart tasks. |✅ | |
