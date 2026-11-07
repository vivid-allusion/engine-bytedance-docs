---
title: "Bucket ACLs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-bucket-acls"
---

You can set bucket ACLs and manage permissions for buckets and ACLs in the TOS console.

<span id="b12b7139"></span>
## **Prerequisites**


* Only the bucket creator or users with the write permission for the bucket ACL can configure the bucket ACL.

* An ACL can be configured for accounts but not sub accounts.


<span id="c7e370ad"></span>
## **Background**

You can grant an IAM account read and write permissions for the bucket and its ACL by creating account authorization. Then, the IAM account can access the bucket with its access key ID and secret key.

<span id="1dc35599"></span>
## **Creating account authorization**


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permission Management \> Bucket ACLs**. On the **Bucket ACLs** page, click **Create Account Authorization**.

4. In the pop\-up dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Account ID |The ID of the IAM account.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The account to be configured must not be a sub account.</div><br> |
   |Bucket Access Permission |* **Read Permission**: Select **Read Permission** will grant permissions to access bucket metadata, access object metadata, and download objects.<br><br>* **Include object enumeration/multi\-paragraph enumeration**: ** ** Select **Read Permission** and **Include object enumeration/multi\-paragraph enumeration** will grant permissions to access bucket metadata, access object metadata, download objects, list objects within a bucket, and list shard tasks.<br><br>* **Write Permission**: Select **Write Permission** will grant permissions to the upload object, overwrite existing objects in the bucket, and delete objects in the bucket.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
   |ACL Access Permission |* **Read Permission**: Obtains the bucket ACL.<br><br>* **Write Permission**: Modifies the bucket ACL;Deletes the bucket ACL.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">This operation is risky. Proceed with caution.</div><br> |
   

5. Click **Save**.

   After authorizing the account, you can view the created permissions in the list or click **Edit** or **Delete** in the **Operation** column of the target permission.


<span id="e3dd215d"></span>
## **Creating a public access permission**

You can grant permissions to all users by performing following operations. After that, they can access the bucket without authentication.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">A public access permission indicates that all users (including anonymous users) can access your bucket without authentication, which may cause security issues. Proceed with caution.</div>


* <div data-tips="true" data-tips-type="warning">A public access permission can be edited but not deleted after being created.</div>


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permission Management \> Bucket ACLs**.

4. In the **Public Access Permission** section of the **Bucket ACLs**, click **Edit** in the **Operation** column of **All Users**.

5. In the pop\-up dialog box, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Bucket Access Permission |* **Read Permission**: Select **Read Permission** will grant permissions to access bucket metadata, access object metadata, and download objects.<br><br>* **Include object enumeration/multi\-paragraph enumeration**: ** ** Select **Read Permission** and **Include object enumeration/multi\-paragraph enumeration** will grant permissions to access bucket metadata, access object metadata, download objects, list objects within a bucket, and list shard tasks.<br><br>* **Write Permission**: Select **Write Permission** will grant permissions to the upload object, overwrite existing objects in the bucket, and delete objects in the bucket. |
   |ACL Access Permission |* **Read Permission**: Obtains the bucket ACL.<br><br>* **Write Permission**: Modifies or deletes the bucket ACL. |
   

6. Click **Save**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After authorizing all users (including anonymous users), you can click <strong>Edit</strong> in the <strong>Operation</strong> column of the target permission.   </div>
