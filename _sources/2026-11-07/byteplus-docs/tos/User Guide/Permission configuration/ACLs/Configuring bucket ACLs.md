---
title: "Configuring bucket ACLs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-configuring-a-bucket-acl"
---

You can grant an Identity and Access Management (IAM) account read and write permissions on a bucket and its Access Control Lists (ACLs). Then, the IAM account can access the bucket with its Accesskey ID and AccessKey secret.

<span id="b89f83c8"></span>
## Prerequisites


* The account used to configure the bucket ACL must be the bucket creator, or have the write permission on the bucket ACL.

* The account to be configured must not be a sub account.


<span id="8a0a68e8"></span>
## Creating account authorization


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permissions \> Bucket ACLs**. On the **Bucket ACLs** page, click **Create Account Authorization**.

4. In the pop\-up dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Account ID |The ID of the IAM account.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The account to be configured must not be a sub account.</div><br> |
   |Bucket Access Permission |* **Read Permission**: Select **Read Permission** will grant permissions to access bucket metadata, access object metadata, and download objects.<br><br>* **Include object list/multi\-parts list**: ** ** Select **Read Permission** and **Include object list/multi\-parts list** will grant permissions to access bucket metadata, access object metadata, download objects, list objects within a bucket, and list multipart uploads.<br><br>* **Write Permission**: Select **Write Permission** will grant permissions to the upload object, overwrite existing objects in the bucket, and delete objects in the bucket.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
   |ACL Access Permission |* **Read Permission**: Obtains the bucket ACL.<br><br>* **Write Permission**: Modifies the bucket ACL; Deletes the bucket ACL.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
   

5. Click **Save**.

   After authorizing the account, you can view the created permissions in the list or click **Edit** or **Delete** in the **Actions** column of the target permission.


<span id="57a77d0b"></span>
## Creating a public access permission

You can grant permissions to all users by performing following operations. After that, they can access the bucket without authentication.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A public access permission indicates that all users (including anonymous users) can access your bucket without authentication, which may cause security issues. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">A public access permission can be edited but not deleted after being created.</div>


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permissions \> Bucket ACLs**.

4. In the **Public Access Permission** section of the **Bucket ACLs**, click **Edit** in the **Actions** column of **All Users**.

5. In the pop\-up dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Bucket Access Permission |The following bucket access permissions are available:<br><br><br>* **Read Permission**: Granting only **Read Permission** allows all users to retrieve bucket metadata.<br><br>* **Read Permission + Include object list/multi\-parts list**: Selecting both **Read Permission** and **Include object list/multi\-parts list** gives all users permission to retrieve bucket metadata, list objects, and list multipart uploads.<br><br>* **Write Permission**: Allows all users to upload objects, overwrite existing objects, and delete objects. |
   |ACL Access Permission |The following ACL permissions are available:<br><br><br>* **Read Permission**: Allows all users to read the bucket's ACL.<br><br>* **Write Permission**: Allows all users to modify or delete the bucket's ACL. |
   

6. Click **Save**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Once you have authorized all users, you can view the permissions that have been created in the list. To edit user permissions, you can click <strong>Edit</strong> in the <strong>Actions</strong> column of the permission you want to modify.   </div>
