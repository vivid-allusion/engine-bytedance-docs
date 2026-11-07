---
title: "Viewing object details"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-viewing-file-details"
---

You can view object details in the TOS console, including filename, size, URL, and storage type.

<span id="RGylKPkC"></span>
## Notes

By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform this operation, the account owner must grant the user the `tos:ListBucket` permission using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

<span id=".5pON5L2c5q2l6aqk"></span>
## Steps


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. On the **Objects** page, click **Details** in the **Actions** column of the object you want to check. The object's details will then appear in a panel, with the parameters listed below.

   
   |**Parameter** |**Note** |
   |---|---|
   |Filename |Name of the object. |
   |URL |Link to download the object, which is valid for an hour.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If your bucket policy conflicts with object access control, for example, the object access control is set to <strong>public read</strong> but the bucket policy denies access, the bucket policy takes precedence. In this case, you may not be able to access your object through the object URL. You can click <strong>Generate and Copy Pre\-signed Link </strong>after the URL to access the object using the pre\-signed link.</div><br> |
   |Custom domain URL |Select a custom domain and click **Generate and Copy Pre\-signed Link** to create a pre\-signed link for the object using the custom domain.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The pre\-signed link for the custom domain is valid for 1 hour by default. During this time, anyone can download the object through the pre\-signed link.</div><br> |
   |Size |Size of the object. |
   |Version ID |The current object version ID can be viewed on the **Objects** page after enabling the **Show versions** toggle.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If versioning is disabled for the bucket where the object is stored, the ID is <strong>null</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For detailed steps on enabling versioning, see <a href="https://docs.byteplus.com/docs/tos/docs-overview">Versioning</a>.</div><br> |
   |Storage type |Storage type of the object. For more information about storage type, see [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type). |
   |Access Control |Access permission of the object. For detailed information about object access permissions, see [Configuring object ACLs](https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl). |
   |Server\-Side encryption |The server\-side encryption information of the object.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can only set the server\-side encryption method when uploading objects. You cannot change the encryption settings of uploaded objects. For detailed information about server\-side encryption, see <a href="https://docs.byteplus.com/docs/tos/Server-side-encryption-overview">Server\-side encryption</a>.</div><br> |
   |Encryption algorithm |The encryption algorithm used for server\-side encryption. |
   |Tag |Tags of the object. |
   |Replication state |The status of the object's cross\-region or same\-region replication includes the following:<br><br><br>* If the object is the source object of cross\-region or same\-region replication, it includes the statuses **Pending replication**, **Replication failed**, ** Replication completed**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The feature that allows you to view the replication status of cross\-region or same\-region source objects is currently in beta. Contact your account manager if you need to use this feature.   </div><br>   <br><br>* If the object is the target object of cross\-region or same\-region replication, it will show **Replicated object**.<br><br>* If the object is neither a source nor a target for cross\-region or same\-region replication, it will be displayed  **\-** . |
   |ETag |The ETag of the object. |
   |Retention mode |The retention mode of the retention policy. Currently, only compliance mode is supported, which means that no user can delete or overwrite the protected object during the retention period. |
   |Retention expiration date |The time until which the object cannot be deleted or overwritten under the retention policy.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">After enabling object locking on your bucket, you can set a retention period for the entire bucket or a specific object. For more information, see <a href="https://www.volcengine.com/docs/6349/1764510">Configuring retention policies</a>.</div><br> |
   


<span id=".55u45YWz5pON5L2c"></span>
## Related operations


* Change the number of objects displayed

   When the number of objects exceeds 100, you can switch the number of objects displayed per page from **100 per page** to **200 per page** at the bottom right of the **Objects** page.

* Copy object path

   On the **Objects** page, click **Copy Path** to the right of **All Files** in the upper\-left corner to copy the current path of the object.
