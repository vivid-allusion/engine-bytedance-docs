---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-overview_6"
---

When you create an Identity and Access Management (IAM) user, you need to grant permissions to the user by selecting a specific authorization policy. This topic describes how to create an IAM policy.

<span id="c93aa1ca"></span>
## Applicable scenarios

Use an IAM policy if you need to:


* Grant IAM users permissions on multiple cloud resources.

* Set the same permission for multiple buckets.

* Grant different IAM users different permissions.

* Configure service\-level permissions, for example, creating buckets or listing all buckets under an account.


<span id="e31e1e52"></span>
## Preset IAM policies

IAM presets the following default policies for TOS.


|**Policy name** |**Description** |**Supported TOS actions** |
|---|---|---|
|AdministratorAccess |Permission to manage services and resources for an account |Allows the specified user to perform all operations supported by TOS on the current bucket and all its objects. |
|TOSFullAccess |Full read and write permission on TOS |Allows the specified user to perform all operations supported by TOS on all the buckets and objects of the account. |
|TOSReadOnlyAccess |Read\-only permission on TOS |Allows the specified user to perform the following operations on the current bucket and all its objects:<br><br><br>* **Get**\*: All GET operations.<br><br>* **List**\*: All LIST operations.<br><br>* **HeadBucket**: Checks whether the bucket exists. |


<span id="be435332"></span>
## Supported actions

<span id="4d23bb9e"></span>
### General actions


|**Action** |**Description** |
|---|---|
|\* |The wildcard, which indicates all operations that can be performed on the resource. |
|Get\* |Indicates all GET operations that can be performed on the resource. |
|Put\* |Indicates all PUT operations that can be performed on the resource. |
|List\* |Indicates all LIST operations that can be performed on the resource. |


<span id="1347e5fa"></span>
### Bucket actions


|**Category** |**Action** |**Description** |
|---|---|---|
|Bucket operations |CreateBucket |Creates a bucket. |
||ListBuckets |Lists all buckets. |
||ListBucket |Lists objects in a bucket and obtains bucket metadata. |
||HeadBucket |Checks whether a bucket exists. |
||DeleteBucket |Deletes a bucket. |
|Bucket location |GetBucketLocation |Obtains the location information about a bucket. |
|Bucket policy |GetBucketPolicy |Obtains a bucket policy. |
||PutBucketPolicy |Sets a bucket policy. This permission allows users to change bucket polices and obtain other permissions. |
||DeleteBucketPolicy |Deletes a bucket policy. |
|Bucket versioning |GetBucketVersioning |Obtains multiversion information about a bucket. |
||PutBucketVersioning |Sets the mutiversion status of a bucket. |
||ListBucketVersions |Lists multiversion objects in a bucket. |
|Bucket ACL |GetBucketACL |Obtains bucket ACL information. |
||PutBucketACL |Sets the bucket ACL. |
|Lifecycle rule |GetLifecycleConfiguration |Obtains a bucket lifecycle rule. |
||PutLifecycleConfiguration |Sets or deletes a bucket lifecycle rule. |
|CORS rule |GetBucketCORS |Obtains the cross\-origin resource sharing (CORS) rule of a bucket. |
||PutBucketCORS |Sets or deletes the CORS rule of a bucket. |
|Others |ListBucketMultipartUploads |Lists part upload tasks. |


<span id="caee9696"></span>
### Object actions


|**Category** |**Action** |**Description** |
|---|---|---|
|Object operations |GetObject |Obtains the content and metadata of an object. |
||PutObject |Performs PUT upload, part upload, part upload initialization, or part merging. |
||DeleteObject |Deletes an object. |
|Object ACL |GetObjectAcl |Obtains the object ACL information. |
||PutObjectAcl |Sets the object ACL. |
|Object version |GetObjectVersion |Obtains the content and metadata of an object of a specified version. |
||DeleteObjectVersion |Deletes an object of a specified version. |
|Others |AbortMultipartUpload |Cancels a multi\-part upload task. |
||ListMultipartUploadParts |Lists uploaded parts. |


<span id="ed5cdc7f"></span>
## Customizing an IAM policy

If the default IAM policies do not meet your needs, you can customize a policy by referring to the following topics:


* [Configuring IAM policies](https://docs.byteplus.com/tos/docs/configuring-an-iam-policy?version=1.0.0)

* [IAM policy examples](https://docs.byteplus.com/en/docs/tos/docs--common-iam-policies)
