---
title: "Overview"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-overview_4"
---

An access control list (ACL) is a list of authorized objects and permissions provided by Torch Object Storage (TOS).

<span id="584bffe2"></span>
## ACL permissions

An ACL is an account\-based read/write access control, where the bucket or object owner has full control.

ACLs are less refined than bucket or Identity and Access Management (IAM) policies. Therefore, we recommend that you use the bucket or IAM policies for access control.

<span id="87c78d68"></span>
## Authorized user

In an ACL, authorized users are divided into specified users and predefined groups.


* Specified user: IAM users. To grant different IAM users different permissions, use bucket policies.

* Predefined groups are as follows.



|**Group** |**Description** |
|---|---|
|AuthenticatedUsers |All signed (authenticated) users. |
|AllUsers |All users (authenticated or anonymous). |


<span id="84670661"></span>
## ACL permissions

TOS supports the following ACL permissions.


|**Permission** |**Bucket ACL** |**Object ACL** |
|---|---|---|
|READ |Allows an authorized user to list objects and part tasks in a bucket. |Allows the grantee to read the object data and its metadata. |
|READ_NON_LIST |Allow authorized users to access bucket metadata, retrieve object metadata, and download objects. |Allows the grantee to read the object data and its metadata. |
|WRITE |Allows the authorized user to create, overwrite, and delete any object in a bucket, initialize part tasks, upload parts, merge parts, and cancel part tasks. |N/A |
|READ_ACP |Allows the authorized user to read the bucket ACL. |Allows the authorized user to read the object ACL. |
|WRITE_ACP |Allows the authorized user to set ACLs for applicable buckets. |Allows the authorized user to set ACLs for applicable objects. |
|FULL_CONTROL |Grants the authorized user READ, WRITE, READ_ACP, and WRITE_ACP permissions on a bucket. |Grants the authorized user READ, READ_ACP, and WRITE_ACP permissions on a object. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If objects in a bucket are set to public\-read, the bucket are exposed over the public network, and its objects can be read by anyone, which incurs traffic fees and may cause property loss and data leakage. We recommend that you set the permission to private.</div>


<span id="446711aa"></span>
## Using header fields to set ACLs

You can select the following predefined permissions with the `x-tos-acl` header field.


|**Predefined Permission** |**Description** |
|---|---|
|private |The bucket or object owner has full control, and other users have no permissions.<br><br>The default policy is private. |
|public\-read |* Bucket\-level authorization: All users have READ permission on the bucket.<br><br>* Object\-level authorization: All users have READ permission on the object. |
|public\-read\-write |* Bucket\-level authorization: All users have READ and WRITE permissions on the bucket.<br><br>* Object\-level authorization: All users have READ permission on the object. |
|authenticated\-read |* Bucket\-level authorization: All authenticated users have READ permission on the bucket.<br><br>* Object\-level authorization: All authenticated users have READ permission on the object. |
|bucket\-owner\-read |Object\-level authorization: The bucket or object owner has READ permission on the object. |
|bucket\-owner\-full\-control |Object\-level authorization: The bucket or object owner has full control over the object. |
|bucket\-owner\-entrusted |Object\-level authorization: If the object owner is not the bucket owner, the bucket owner has full control over the object and can allow or deny other accounts or users to access the object through a bucket policy. |
|default |Granting permission on an object will inherit the bucket's ACL permissions, meaning the object's ACL policy will be consistent with the bucket's ACL policy. |


You can grant the specified user corresponding permissions through the following header fields.


|**Header Field** |**Description** |
|---|---|
|x\-tos\-grant\-read |The authorized user has READ permission. |
|x\-tos\-grant\-write |The authorized user has WRITE permission. |
|x\-tos\-grant\-read\-non\-list |The x\-tos\-grant\-read\-non\-list header must be used in conjunction with x\-tos\-grant\-read\-acp, as using it alone is meaningless.<br><br>This header is used to revoke permission for listing objects within a bucket and shard tasks. When used in conjunction with x\-tos\-grant\-read\-acp, it indicates that the grantee has READ_NON_LIST permission. |
|x\-tos\-grant\-read\-acp |The authorized user has READ_ACP permission. |
|x\-tos\-grant\-write\-acp |The authorized user has WRITE_ACP permission. |
|x\-tos\-grant\-full\-control |The authorized user has FULL_CONTROL permission. |


<span id="9b50293d"></span>
## Object ACL default policy

TOS supports setting the access control policy for objects as **Object ACL default policy**, meaning that the ACL policy for objects remains consistent with the bucket ACL policy. The following describes the permissions of objects inheriting READ, WRITE, and other ACLs from the bucket.


|Permission |Bucket ACL |Object ACL default policy |
|---|---|---|
|READ |Allow the authorized user to access bucket metadata, object metadata, download objects, list objects within a bucket, and view shard tasks. |Allow the authorized party to read object data and its metadata. |
|READ_NON_LIST |Allow authorized users to access bucket metadata and objects within the bucket. |Allow the authorized party to read object data and its metadata. |
|WRITE |Allow the authorized user to create, overwrite, and delete any object in the bucket, initialize shard tasks, upload shards, merge shards, and cancel shard tasks. |Due to the lack of write interface for objects, even after inheriting the WRITE ACL of the bucket, the authorized user still does not have permission for the object, only the bucket or object owner has full control permission. |
|READ_ACP |Allow the authorized user to read the ACL of the bucket. |Allow the authorized user to read the ACL of the object. |
|WRITE_ACP |Allow the authorized user to modify or delete the ACL of the storage bucket. |Allow the authorized party to modify the ACL of the object. |
|FULL_CONTROL |Allow the grantee to have READ, WRITE, READ_ACP, and WRITE_ACP permissions on the bucket. |Allow the grantee to have READ, READ_ACP, and WRITE_ACP permissions on the object. |
