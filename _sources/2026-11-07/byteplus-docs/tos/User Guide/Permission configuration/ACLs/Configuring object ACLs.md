---
title: "Configuring object ACLs"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-configuring-an-object-acl"
---

You can set Access Control Lists (ACLs) for individual objects in the Torch Object Storage (TOS) console.

<span id="0a936062"></span>
## Background

You can set an ACL when uploading an object and modify the ACL after upload. An object supports the following access permissions:


* **Inheritance bucket**：Objects will inherit the bucket ACL, meaning the ACL policy of the object will be consistent with the bucket ACL policy. For the corresponding relationship between object ACL and bucket ACL, please refer to [Object ACL default policy](https://docs.byteplus.com/docs/tos/docs-overview_4#9b50293d).

* **Private**: It is the default recommended value, indicating that only the object owner and authorized accounts can read and write the object.

* **Public Read**: All users (including anonymous users) can read the object, but only the object owner and authorized accounts can write the object.

* **Public Read and Write**: All users (including anonymous users) can read and write the object.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Files set with <strong>public\-read</strong> permission are exposed over the public network and can be read by anyone, which incurs traffic fees and may cause property loss and data leakage. We recommend that you set the permission to <strong>private</strong>.</div>


<span id="b9d401df"></span>
## Modify object ACL


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click  **··· \> Modify Access Permission** in the **Actions** column of the target object.

4. In the pop\-up dialog box, select the target permission and click **Save**.


<span id="c50eea03"></span>
## Enable upload object ACL default policy.

After enabling the default bucket ACL inheritance feature, the ACL policy of newly uploaded objects will default to be consistent with the bucket ACL policy. The ACL policy of objects uploaded before this feature was enabled will not change.


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. In the left navigation pane, select **Permissions \> Bucket ACLs**

4. At the bottom of the Bucket ACLs page, enable Upload **Object ACL Default Policy.** 

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can disable the default bucket ACL inheritance feature on the Bucket ACLs page. After disabling it, the default ACL policy for newly uploaded objects will be private.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can enable the default bucket ACL inheritance feature when creating a storage bucket. For specific operations, please refer to the <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Creating a bucket</a>.   </div>
