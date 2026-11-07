---
title: "Modifying file permissions"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-modifying-the-file-access-permission"
---

A file uploaded to a bucket will inherit the access permission (ACL) from the bucket, and you can modify the file permission on the **Objects** page.

<span id="4bbbf26b"></span>
## Permissions

Files can have the following permissions:


* **Inherit bucket**: ** ** The object will inherit the bucket ACL, meaning the object's ACL policy will be consistent with the bucket's ACL policy. For the corresponding relationship between object ACL and bucket ACL, please refer to [Object ACL default policy](https://docs.byteplus.com/docs/tos/docs-overview_4#9b50293d).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also enable the default bucket ACL inheritance feature, which, when enabled, will ensure that the ACL policy of newly uploaded objects will be consistent with the bucket ACL policy. For specific instructions, please refer to the documentation <a href="https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl#c50eea03">Enabling objects to automatically apply bucket ACL</a>.   </div>
   

* **Private**: It is the default and recommended value, indicating that only the object owner and authorized accounts can read and write the file.

* **Public read**: Files whose permission is Public Read can be read by anyone, which incurs traffic fees and may cause property loss and data leakage.

* **Public read/write**: Files whose permission is Public Read and Write can be read and written by anyone, which incurs traffic fees and may cause property loss and data leakage.


<span id="9ededed3"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation pane, click **Buckets**. On the bucket list page, click the target bucket name.

3. On the **Objects** page, click  **··· \> Modify Access Permission** in the **Actions** column of the target file.

4. In the pop\-up dialog box, select the target permission and click **Save**.
