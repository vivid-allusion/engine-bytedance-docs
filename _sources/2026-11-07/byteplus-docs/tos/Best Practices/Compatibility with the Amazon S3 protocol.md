---
title: "Compatibility with the Amazon S3 protocol"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-compatibility-with-amazon-s3"
---

Torch Object Storage (TOS) is compatible with Amazon S3 (S3). Therefore, after you migrate data from other S3\-compatible storage services to TOS and switch the access destination, applications previously access those services can continue to access TOS. This topic describes how to switch the access destination and provides TOS\-compatible S3 APIs.

<span id="0a56091e"></span>
## Restrictions

As TOS is S3\-compatible, you can use S3 SDKs or other S3\-compatible tools to create buckets, upload objects, and perform other operations.

For more information about restrictions on bandwidth, QPS, and more, see [TOS Restrictions](https://docs.byteplus.com/en/tos/docs/restrictions?version=1.0.0).

<span id="37375473"></span>
## Switching the access destination for applications

Before you switch the access destination from an S3\-compatible storage service to TOS, you must migrate any existing data to TOS.

<span id="821c91b9"></span>
### Step 1: Migrating data to TOS

You can use Rclone to migrate data from an S3\-compatible storage service to TOS.

<span id="fa435bc5"></span>
### Step 2: Accessing TOS through S3

After data migration to TOS, you can access TOS through S3 SDKs or other S3\-compatible tools, such as AWS CLI, S3 Browser, and Postman. However, pay attention to the following items:


* **Endpoints**

   TOS provides S3\-dedicated [Endpoints](https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0) that are required if you access through S3.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">While AWS and other cloud services use the same endpoint for both intranet and extranet, TOS provides different endpoints for the two networks. For example, <code>tos-ap-southeast-1.ibytepluses.com</code> and <code>tos-ap-southeast-1.bytepluses.com</code> are used to access TOS Asia Pacific (Johor) over the intranet and extranet respectively.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">For more information, see <a href="https://docs.byteplus.com/en/tos/docs/region-and-endpoint?version=1.0.0">Endpoints</a>.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">TOS supports S3 Signature Version 4, but does not support Version 2.   </div>
   

* **Endpoint regions**

   While AWS and other cloud services use a global endpoint (s3.amazonaws.com) to access buckets in any region, TOS uses regional endpoints. Therefore, a bucket in TOS must be accessed with a specific regional endpoint.

* **Access keys**

   TOS signature and authentication are based on IAM access keys (consisting of an access key ID and access key secret). If you use S3\-compatible SDKs or tools to access TOS, you must configure the access key ID and access key secret obtained in IAM.

* **Request methods**

   TOS supports requests in [virtual host](https://docs.aws.amazon.com/AmazonS3/latest/userguide/VirtualHosting.html?spm=a2c4g.11186623.0.0.6b9d64012JMDoP) style (VirtualHostStyle) but not in path style (PathStyle). Therefore, when you access TOS through S3\-compatible SDKs or tools, make sure that the request method is set to VirtualHostStyle. For example, if you use an S3 Java SDK, you must make sure that PathStyle is disabled during client initialization: `AmazonS3Builder.withPathStyleAccessEnabled (false)`.

* **ACL permissions**

   TOS defines ACL permissions in the same way as S3 but supports fewer ACL features than S3. The following table describes the differences.

   
   |**Feature** |**S3** |**TOS** |
   |---|---|---|
   |Carries ACL enumeration in the request header (using the `x-amz-acl` header field). |Seven enumeration values are supported:<br><br><br>* private<br><br>* public\-read<br><br>* public\-read\-write<br><br>* authenticated\-read<br><br>* aws\-exec\-read<br><br>* bucket\-owner\-read<br><br>* bucket\-owner\-full\-control |Six enumeration values are supported, which are semantically the same as those in S3:<br><br><br>* private<br><br>* public\-read<br><br>* public\-read\-write<br><br>* authenticated\-read<br><br>* bucket\-owner\-read<br><br>* bucket\-owner\-full\-control |
   |Carries ACL configuration in the message body. |Three enumeration values are supported for Type:<br><br><br>* CanonicalUser<br><br>* AmazonCustomerByEmail<br><br>* Group<br><br>* If Type is Group, three enumeration values are supported for URI:<br><br>   * AllUsers:`http://acs.amazonaws.com/groups/global/AllUsers`<br><br>   * AuthenticatedUsers:`http://acs.amazonaws.com/groups/global/AuthenticatedUsers`<br><br>   * LogDelivery:`http://acs.amazonaws.com/groups/s3/LogDelivery` |Two enumeration values are supported for Type, which are semantically the same as those in S3:<br><br><br>* CanonicalUser<br><br>* Group<br><br>* If Type is Group, two enumeration values are supported for URI, which are semantically the same as those in S3:<br><br>   * AllUsers:`http://acs.amazonaws.com/groups/global/AllUsers`<br><br>   * AuthenticatedUsers:`http://acs.amazonaws.com/groups/global/AuthenticatedUsers` |
   

* **Storage types**

   TOS supports Standard Storage, Infrequent Access Storage, Intelligent Tiered Storage, Flashback Archive, Archive Storage, and Cold Archive. These align with part of the storage types available in S3.

   
   |**S3** |**TOS** |
   |---|---|
   |Nine enumeration values are supported:<br><br><br>* **STANDARD**<br><br>* REDUCED_REDUNDANCY<br><br>* **STANDARD_IA**<br><br>* ONEZONE_IA<br><br>* **INTELLIGENT_TIERING**<br><br>* **GLACIER_IR**<br><br>* **GLACIER**<br><br>* **DEEP_ARCHIVE**<br><br>* OUTPOSTS |Six enumeration values are supported:<br><br><br>* STANDARD: Standard Storage<br><br>* IA: Infrequent Access Storage<br><br>* INTELLIGENT_TIERING: Intelligent Tiered Storage<br><br>* ARCHIVE_FR: Flashback Archive<br><br>* ARCHIVE: Archive Storage |
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you use S3 SDKs, specify the storage type based on the enumeration values defined in S3; if you use TOS SDKs, specify it based on those defined in TOS.   </div>
   

* **APIs**

   TOS is fully compatible with common S3 APIs, such as CreateBucket, ListBuckets, PutObject, GetObject, and ListObjects. For more information, see the following table.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">However, certain S3 features are not available in TOS. As a result, some S3 parameters may be invalid in TOS requests.   </div>
   

<span id="6974dbb9"></span>
## Appendix: TOS\-compatible S3 APIs


|**API type** |**S3 API** |**Compatible with TOS** |
|---|---|---|
|Bucket APIs |CreateBucket |Yes |
||HeadBucket |Yes |
||DeleteBucket |Yes |
||ListBuckets |Yes |
|Object APIs |CopyObject |It has the same request parameters and results as S3 APIs. It supports intraregional but not interregional object replication. |
||DeleteObject |Yes |
||DeleteObjects |Yes. It is referred to as DeleteMultiObjects in TOS documentation. |
||GetObject |Yes |
||GetObjectAcl |Yes. It is referred to as GetObjectACL in TOS documentation. |
||HeadObject |Yes |
||ListObjects |Yes |
||ListObjectVersions |Yes |
||PutObject |Yes |
||PostObject |Yes |
||PutObjectAcl |Yes. It is referred to as PutObjectACL in TOS documentation. |
|Part APIs |CreateMultipartUpload |Yes |
||UploadPart |Yes |
||CompleteMultipartUpload |It has the same request parameters and results as S3 APIs. You can merge uploaded parts with specified IDs only. |
||AbortMultipartUpload |Yes |
||UploadPartCopy |Yes |
||ListMultipartUploads |Yes |
||ListParts |Yes |
