---
title: "Same-account same-region replication"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Same-region-replication-within-the-same-account"
---

TOS supports same\-account same\-region replication, which allows you to automatically copy objects across buckets within the same region and account. This topic explains how to configure a rule for this type of replication.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before configuring a same\-account same\-region replication rule for the first time, you must grant TOS permissions to read all objects from the source bucket and to write objects to the destination bucket. If your bucket uses server\-side encryption with KMS keys (SSE\-KMS), you must also authorize TOS to access KMS. Otherwise, the rule cannot be executed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To authorize TOS to access KMS, navigate to the <strong>SRR</strong> page and click <strong>Click to Authorize</strong> under the KMS and read/write authorization section. Then, confirm by clicking <strong>OK</strong> in the box that appears. After authorization, TOS automatically creates the ServiceRoleforReplicationAccessTOS role, granting it permissions to access KMS and read and write objects in the source and destination buckets.</div>


* <div data-tips="true" data-tips-type="warning">To create the ServiceRoleforReplicationAccessTOS role, your account must have the iam:ListAttachedRolePolicies, iam:CreateRole, and iam:AttachRolePolicy permissions. If the <strong>SRR</strong> page shows <strong>No permission</strong>, you must first grant your account the iam:ListAttachedRolePolicies, iam:CreateRole, and iam:AttachRolePolicy permissions. Then, proceed with read/write and KMS authorizations. For instructions, see <a href="https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy">Configuring IAM policies</a>.</div>



<span id=".5Yib5bu65ZCM5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Creating a rule for same\-account same\-region replication


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **Fault tolerance and disaster recovery \> SRR**.

6. On the **SRR** page, click **Create rule**. Set the following parameters in the box that appears:

   
   |**Parameter** |**Description** |
   |---|---|
   |Source bucket location |The region of the source bucket is displayed by default and cannot be changed. |
   |Source bucket |The name of the source bucket is displayed by default and cannot be changed. |
   |Destination bucket owner type |Select **Select a bucket in this account**. |
   |Region of the destination bucket |The region of the destination bucket is displayed by default and cannot be changed. |
   |Destination bucket |Select the name of the bucket where the replicas will be stored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The versioning status of the source and destination buckets must be consistent—either both are enabled or both are disabled. If either is suspended, same\-account same\-region replication is not supported.</div><br> |
   |Destination storage type |Select the storage type for the replica:<br><br><br>* **Inherit target bucket**: The replica's storage type will match the destination bucket's default storage type.<br><br>* **Inherit source object**: The storage type of the replica will be consistent with that of the source object.<br><br>* **Custom**: Select a storage type for the replica manually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Some storage types have a minimum billable object size. If the size of a replica does not meet the minimum size requirement for the selected storage type, storage costs will be calculated based on the minimum billable object size. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-storage-type">Storage type</a>.</div><br> |
   |Scope |Specify the scope of the data that will be replicated:<br><br><br>* **Entire bucket**: Copy all objects in the bucket to the destination bucket.<br><br>* **Specify prefix**: Copy all objects that match the specified prefix to the destination bucket. Select **Specify prefix** and enter the desired prefix(es). Only objects with the prefix(es) will then be replicated. The restrictions are as follows:<br><br>   * If this field is left empty, all objects in the bucket will be replicated.<br><br>   * Up to ten prefixes can be added.<br><br>   * Length must be between 1 and 1,024 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Follow these guidelines when specifying a prefix:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Paths can contain Chinese characters, letters, numbers, and common symbols.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">".." cannot be used as a directory name.</div><br> |
   |Tag |Enter the desired tag(s). Only objects containing the specified tag(s) will be replicated. Click **add row** to set the tag key and value. The restrictions are as follows:<br><br><br>* Up to ten tags can be added.<br><br>* The key length cannot exceed 128 characters.<br><br>* The value length cannot exceed 256 characters.<br><br>* Both the key and the value are case\-sensitive. Valid characters include uppercase and lowercase letters, numbers, spaces, and the special symbols `_ .: / = + -`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Tags</strong> and <strong>prefixes</strong> have an "OR" relationship. If both are configured, objects matching either the tag rules or the prefix rules will be replicated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Using tags and the historical objects synchronization feature simultaneously is not supported. If you want to use tags to filter objects, do not enable Sync historical object.</div><br> |
   |Sync historical object |Select whether to synchronize objects that exist in the source bucket before the rule takes effect:<br><br><br>* **On**: Existing objects will be synchronized to the destination bucket.<br><br>* **Off**: Only objects uploaded after the rule takes effect will be synchronized. Existing objects will not be synchronized. |
   |Synchronous delete tag |Select whether to synchronize deletion marks:<br><br><br>* **On**: Deletion marks will be synchronized to the destination bucket.<br><br>* **Off**: Only objects uploaded to the source bucket will be synchronized. Deletion marks will not be synchronized.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Deletion mark synchronization is only supported for buckets with versioning enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This feature is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Using tags and the deletion mark synchronization feature simultaneously is not supported. If you want to use tags to filter objects, do not enable Synchronous delete tag.</div><br> |
   |Synchronize deleted objects |Select whether to synchronize the deletion of objects from the source bucket to the destination bucket:<br><br><br>* **On**: When an object is deleted from the source bucket, it will also be deleted from the destination bucket.<br><br>* **Off**: Only object uploads will be synchronized, not deletions.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Enabling this option will synchronize deletion operations from the source bucket to the destination bucket. For example, if you delete an object in the source bucket or if a lifecycle rule triggers a deletion, the corresponding object in the destination bucket will also be deleted. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When synchronous object deletion is enabled, TOS automatically ensures eventual consistency of data between the source and destination buckets. However, if you set up bidirectional replication rules between multiple buckets and then delete an object in a destination bucket during replication, TOS cannot guarantee the eventual consistency of data across those buckets.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This feature is currently in closed beta. Please contact your account manager for access.</div><br> |
   

5. Once you have finished configuring, click **Create**.

   Depending on the size of your objects, the replication process may take anywhere from a few minutes to several hours. You can check the replication state of existing objects and the last sync time on the SRR page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The last sync time refers to the completion time of the most recently replicated object. Since SRR tasks run concurrently, objects uploaded to TOS before the last sync time may not be replicated.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e675d86c3c4ea458fe9bab0a344875e7.png) </span>


<span id=".5YWz6Zet5ZCM5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Disabling a rule for same\-account same\-region replication

On the **SRR** page, toggle off the switch under the **Rule Status** column of the rule you want to disable.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9a1d5db32a2cf1a1bc1d5ddad41e97c1.png) </span>

<span id=".5YW25LuW5pON5L2c"></span>
## Other operations


* **Edit a rule for same\-account same\-region replication**: On the **SRR** page, click **Edit** in the **Actions** column of the rule you want to modify.

* **Delete a rule for same\-account same\-region replication**: On the **SRR** page, click **Delete** in the **Actions** column of the rule you want to remove, and confirm the deletion by clicking **Delete** in the box that appears.
