---
title: "Same-account cross-region replication"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Cross-regional-replication-within-the-same-account"
---

TOS supports same\-account cross\-region replication, which allows you to automatically copy objects from one bucket to another in different regions under the same account. This topic explains how to configure a rule for same\-account cross\-region replication.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

Before configuring a same\-account cross\-region replication rule for the first time, you must grant TOS permissions to read all objects from the source bucket and to write objects to the destination bucket. If your bucket uses server\-side encryption with KMS keys (SSE\-KMS), you must also authorize TOS to access KMS. Otherwise, the rule cannot be executed.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>



* <div data-tips="true" data-tips-type="warning">To authorize TOS to access KMS, navigate to the <strong>CRR</strong> page and click <strong>Click to Authorize</strong> under the KMS and read/write authorization section. Then, confirm by clicking <strong>OK</strong> in the box that appears. After authorization, TOS automatically creates the ServiceRoleforReplicationAccessTOS role, granting it permissions to access KMS and read and write objects in the source and destination buckets.</div>


* <div data-tips="true" data-tips-type="warning">To create the ServiceRoleforReplicationAccessTOS role, your account must have the iam:ListAttachedRolePolicies, iam:CreateRole, and iam:AttachRolePolicy permissions. If the <strong>CRR</strong> page shows <strong>No permission</strong>, you must first grant your account the iam:ListAttachedRolePolicies, iam:CreateRole, and iam:AttachRolePolicy permissions. Then, proceed with read/write and KMS authorizations. For instructions, see <a href="https://docs.byteplus.com/docs/tos/docs-configuring-an-iam-policy">Configuring IAM policies</a>.</div>



<span id=".5Yib5bu66Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Creating a rule for same\-account cross\-region replication


1. Log in to the [TOS console](https://console.byteplus.com/tos) .

2. In the left navigation pane, click **Buckets**.

3. In the top menu bar, select the project of the bucket you want to manage.

4. On the **Buckets** page, click the name of the bucket.

5. In the left navigation pane, select **Fault tolerance and disaster recovery \> CRR**.

6. On the **CRR** page, click **Create rule**. Set the following parameters in the box that appears:

   
   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |Source |Source bucket location |The region of the source bucket is displayed by default and cannot be changed. |
   ||Source bucket |The name of the source bucket is displayed by default and cannot be changed. |
   |Destination |Destination bucket owner type |Select **Select a bucket in this account**. |
   ||Region of the destination bucket |Select the region where the destination bucket is located. |
   ||Destination bucket |Select the name of the bucket where the replicas will be stored.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The versioning status of the source and destination buckets must be consistent—either both are enabled or both are disabled. If either is suspended, same\-account cross\-region replication is not supported.</div><br> |
   ||Destination storage type |Select the storage type for the replica:<br><br><br>* **Inherit target bucket**: The replica's storage type will match the destination bucket's default storage type.<br><br>* **Inherit source object**: The storage type of the replica will be consistent with that of the source object.<br><br>* **Custom**: Select a storage type for the replica manually.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Some storage types have a minimum billable object size. If the size of a replica does not meet the minimum size requirement for the selected storage type, storage costs will be calculated based on the minimum billable object size. For more information, see <a href="https://docs.byteplus.com/docs/tos/docs-storage-type">Storage type</a>.</div><br> |
   |Synchronization |Scope |Specify the scope of the data that will be replicated:<br><br><br>* **Entire bucket**: Copy all objects in the bucket to the destination bucket.<br><br>* **Specify prefix**: Copy all objects that match the specified prefix to the destination bucket. Select **Specify prefix** and enter the desired prefix(es). Only objects with the prefix(es) will then be replicated. The restrictions are as follows:<br><br>   * If this field is left empty, all objects in the bucket will be replicated.<br><br>   * Up to ten prefixes can be added.<br><br>   * Length must be between 1 and 1,024 characters.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Follow these guidelines when specifying a prefix:   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Prefixes can contain Chinese characters, letters, numbers, and common symbols.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Prefixes cannot start with a forward slash (/) or backslash (\). Consecutive forward slashes (/) are not allowed.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">".." cannot be used as a directory name.   </div><br>    |
   ||Tag |Enter the desired tag(s). Only objects containing the specified tag(s) will be replicated. Click **add row** to set the tag key and value. The restrictions are as follows:<br><br><br>* Up to ten tags can be added.<br><br>* The key length cannot exceed 128 characters.<br><br>* The value length cannot exceed 256 characters.<br><br>* Both the key and the value are case\-sensitive. Valid characters include uppercase and lowercase letters, numbers, spaces, and the special symbols `_ .: / = + -`.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Tags</strong> and <strong>prefixes</strong> have an "OR" relationship. If both are configured, objects matching either the tag rules or the prefix rules will be replicated.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Using tags and the historical objects synchronization feature simultaneously is not supported. If you want to use tags to filter objects, do not enable Sync historical object.</div><br> |
   ||Sync historical object |Select whether to synchronize objects that exist before the rule takes effect:<br><br><br>* **On**: Existing objects will be synchronized to the destination bucket.<br><br>* **Off**: Only objects uploaded after the rule takes effect will be synchronized. Existing objects will not be synchronized. |
   ||Synchronous delete tag |Select whether to synchronize deletion marks:<br><br><br>* **On**: Deletion marks will be synchronized to the destination bucket.<br><br>* **Off**: Only objects uploaded to the source bucket will be synchronized. Deletion marks will not be synchronized.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Deletion mark synchronization is only supported for buckets with versioning enabled.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This feature is currently in closed beta. Please contact your account manager for access.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Using tags and the deletion mark synchronization feature simultaneously is not supported. If you want to use tags to filter objects, do not enable Synchronous delete tag.</div><br> |
   ||Synchronize deleted objects |Select whether to synchronize the deletion of objects from the source bucket to the destination bucket:<br><br><br>* **On**: When an object is deleted from the source bucket, it will also be deleted from the destination bucket.<br><br>* **Off**: Only object uploads will be synchronized, not deletions.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Enabling this option will synchronize deletion operations from the source bucket to the destination bucket. For example, if you delete an object in the source bucket or if a lifecycle rule triggers a deletion, the corresponding object in the destination bucket will also be deleted. Proceed with caution.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When synchronous object deletion is enabled, TOS automatically ensures eventual consistency of data between the source and destination buckets. However, if you set up bidirectional replication rules between multiple buckets and then delete an object in a destination bucket during replication, TOS cannot guarantee the eventual consistency of data across those buckets.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This feature is currently in closed beta. Please contact your account manager for access.</div><br> |
   |Data transfer between the Chinese mainland and other locations<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The parameters, <strong>Compliance commitment</strong> and <strong>Accelerated program</strong>, only appear when you select to replicate objects between a region in the Chinese mainland and a region outside of the Chinese mainland.</div><br> |Compliance commitment |Transferring data between the Chinese mainland and other locations carries compliance and legal risks. To ensure compliant data transfer, you must read and agree to the **Data cross\-border compliance commitments**. |
   ||Accelerated program |**Transfer acceleration** is selected as the acceleration option by default. Before replicating objects between the Chinese mainland and other locations, you must first enable transfer acceleration on the source bucket. Once enabled, data will be transferred through the accelerated transfer path. This setting cannot be disabled after activation. For instructions, see [Enabling transfer acceleration](https://docs.byteplus.com/en/docs/tos/Transfer_acceleration#e67c338c).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After enabling transfer acceleration, it may take up to 30 minutes for the feature to take effect.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Transfer acceleration is billed separately. If you use transfer acceleration for replication, TOS will charge you for both the data transfer and the transfer acceleration. For billing details, see <a href="https://docs.byteplus.com/en/docs/tos/transfer-acceleration-fee">Transfer acceleration</a>.</div><br> |
   

&nbsp;

7. Once you have finished configuring, click **Create**.

   The rule adopts an asynchronous replication mechanism. Depending on the size of your objects, the process may take anywhere from a few minutes to several hours. You can check the replication state of existing objects and the last sync time on the **CRR** page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The last sync time refers to the completion time of the most recently replicated object. Since CRR tasks run concurrently, objects uploaded to TOS before the last sync time may not be replicated.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_317ee805dc65509ba37c34ef9832fe0f.png) </span>


<span id=".5YWz6Zet6Leo5Yy65Z-f5aSN5Yi26KeE5YiZ"></span>
## Disabling a rule for same\-account cross\-region replication

On the **CRR** page, toggle off the switch under the **Rule Status** column of the rule you want to disable.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3dd8244477a4b836051cd16b66021299.png) </span>

<span id=".5YW25LuW5pON5L2c"></span>
## Other operations


* **Edit a rule for same\-account cross\-region replication**: On the **CRR** page, click **Edit** in the **Actions** column of the rule you want to modify.

* **Delete a rule for same\-account cross\-region replication**: On the **CRR** page, click **Delete** in the **Actions** column of the rule you want to remove, and confirm the deletion by clicking **Delete** in the box that appears.
