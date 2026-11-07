---
title: "Batch processing"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Batch-processing1"
---

If you want to perform batch operations on objects in a bucket, you can use the batch processing feature of TOS. This article explains the prerequisites, features, and operational steps of batch processing.

<span id="e268dd21"></span>
## Prerequisites


* Before creating a batch task, you need to first create a bucket list to obtain information about all or specified objects in the bucket. To see the steps for creating a bucket list, please refer to [Bucket Inventory](https://docs.byteplus.com/docs/tos/Bucket-inventory).

* Before creating a batch task, you need to authorize TOS to read and write files in your bucket, which can be completed following the prompts in the console. If you have previously authorized, there is no need to re\-authorize.

* By default, the owner of an account has full permissions. IAM users have no permissions by default. If an IAM user needs to perform any of the following operations, the account owner must grant the user the appropriate permissions using an [IAM](https://docs.byteplus.com/en/docs/tos/docs-overview_6) or [Bucket policy](https://docs.byteplus.com/en/docs/tos/docs-overview_5).

   * Create batch processing tasks: `tos:CreateJob` 

   * Delete batch processing tasks: `tos:DeleteJob` 


<span id="e0397013"></span>
## Supported batch operations

After creating batch tasks, TOS will execute the set operations on the objects in the bucket list one by one. The currently supported batch operations and precautions are as follows.


|Task |Description |Remarks |
|---|---|---|
|**Batch data replication** |Objects in the bucket list are batch copied to other storage buckets in the same region. During the copying process, you can set the object ACL and metadata information. |* All objects to be processed must be in the same bucket.<br><br>* In a batch task, only one target bucket can be configured.<br><br>* Permissions required include reading the list, reading the source object, and writing to the target bucket.<br><br>* The object to be copied must not exceed 5GiB.<br><br>* If the target bucket has not enabled versioning, it will perform an overwrite operation when an object with the same name exists.<br><br>* If no version is specified in the list, the latest version is copied by default. |
|**Bulk replacement object ACL** |Batch update the object ACLs in the bucket list. |* All objects to be processed must be in the same bucket.<br><br>* You need the permissions to read the checklist, read the source object, and write to the target bucket.<br><br>* If it is an object with multiple versions, the latest version is operated on by default. |
|**Batch processing object tags** |Batch update tags of objects in the bucket list. ||
|**Batch recovery archive object** |Batch restore objects from the archive storage, cold archive storage, and deep cold archive storage. |* All objects to be processed should be in the same bucket.<br><br>* Batch restoration of archive storage objects requires permissions to read the inventory, read source objects, and write to the target bucket.<br><br>* If it is an object with multiple versions, the latest version is operated on by default.<br><br>* When batch restoring archive storage objects, if the target bucket contains copies of the restored objects, the expiry of those object copies will be updated.<br><br>* Batch restoration of archived storage objects only supports standard retrieval. Batch restoration of cold archive storage and deep cold archive storage objects supports both standard retrieval and batch retrieval.<br><br>* The batch restoration of archived objects function only applies to archive storage, cold archive storage, deep cold archive storage object. It will not perform any operations on objects of other storage types, which will be marked as failed. |


<span id="a4bf0272"></span>
## Notes


|Category |Description |
|---|---|
|Permissions |Before creating a batch job, ensure your account or subaccount has the appropriate IAM permissions. For example, if you have configured a task for batch data replication:<br><br><br>* You need to ensure your account has permission for `GetObject` on the source bucket and `PutObject` on the target bucket.<br><br>* In addition to operation permissions, you also need permission to read the object list and write batch processing reports.<br><br>* TOS has built\-in IAM roles that grant you the appropriate permissions. You can complete the corresponding authorization following the prompts on the console.<br><br>* If you want to grant different permissions for different accounts, please refer to [IAM policy management](https://docs.byteplus.com/en/docs/tos/docs-permission-configuration-guide). |
|Object list |The object list is used to store the objects you need to perform batch operations on. Currently, only the bucket inventory feature supports the creation of object listings. For detailed steps, please refer to [Bucket inventory](https://docs.byteplus.com/docs/tos/Bucket-inventory). |
|Object quantity |A single task can process up to 2 billion objects. |
|Priority |TOS supports prioritization of batch tasks by priority identifiers; the higher the numerical value, the higher the priority, but priority does not directly determine the order of task completion.<br><br>If you need to strictly ensure the order of task execution, you can manually control the sequence of tasks, starting the next task only after the previous one has finished. For detailed steps, please see [Other operations](https://docs.byteplus.com/docs/tos/Batch-processing1#6edb29a9). |
|Batch task report |TOS supports generating batch task reports, and you can configure the related information when setting task parameters. It is recommended to choose to generate reports, otherwise, task details will be inaccessible. |
|Task description (Optional) |* You can set a task description of up to 256 characters for the batch processing task you create, helping you track and monitor the task. TOS displays detailed information about task descriptions on the console, making it easy for you to arrange or filter relevant tasks.<br><br>* You can configure the same task description for similar tasks (e.g., weekly synchronized replication of log data) to manage similar tasks. |


<span id="d6ffbceb"></span>
## Procedure


1. Log in to the [TOS console](https://console.byteplus.com/tos/bucket).

2. In the left navigation bar, click **Batch processing**.On the **Batch processing** page, click **Create task**.

3. In the **Region and inventory configuration** wizard, set the following parameters.

   
   |**Parameter** |**Description** |
   |---|---|
   |Task area |Select the region for batch task execution from the dropdown list; it must match the region where the targeted storage bucket is located. |
   |Inventory format |Default is **TOS inventory format**, no setup required. |
   |Inventory bucket |Select the storage bucket where the manifest file is located from the dropdown list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If there are many buckets, you can directly enter the bucket name to search for the corresponding bucket.</div><br> |
   |Inventory file path |Click **Select inventory**, in the **Select file** dialog, choose the inventory files needed for batch processing, and then click **Select**.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The list must be in the format of <code>manifest.json</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If there is no manifest file in the bucket you selected, you can create a bucket manifest generation. For specific steps, see <a href="https://docs.byteplus.com/docs/tos/Bucket-inventory">Bucket inventory</a>.</div><br> |
   |Inventory ETag |The ETag is generated automatically based on the selected manifest file, no setup is needed. |
   

4. Click **Next: Operation configuration**. In the **Operation configuration** wizard, set the task parameters according to the type of task to be performed.

   * **Batch data replication**

      
      |Parameter |Description |
      |---|---|
      |Task type |Select **Batch data replication**. |
      |Region of the destination bucket |In the drop\-down list, select the region where the destination bucket is located.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">TOS only supports copying between the same Region; please select the same Region as the source.</div><br> |
      |Destination bucket |In the drop\-down list, select the destination bucket.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If there are many buckets in the dropdown list, you can enter the bucket name in the search box to directly search for the target bucket.</div><br> |
      |Prefix Operations |You can choose to **None**, **Add**, **Replace**, or **Delete** the prefix of the copied object.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you choose to perform a corresponding operation on the prefix, the prefix must not be empty or exceed 1024 bytes.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">If you wish to set a directory prefix, it should end with a slash <code>/</code>.</div><br> |
      |Storage type |Select the storage type of the object after copying, supports **Standard**, **Infrequent Access**, and **Flashback Archive**.<br><br>For detailed information about storage types, please refer to [Storage type](https://docs.byteplus.com/docs/tos/docs-storage-type). |
      |Server\-side Encryption |Choose whether to perform server\-side encryption on the copied object, currently supports **No encrypted** and **SSE_TOS**.<br><br>For more detailed information about encryption, please see [Server-side encryption overview](https://docs.byteplus.com/docs/tos/Server-side-encryption-overview). |
      |Access permissions |Select the access permissions for the copied object, supporting the following operations:<br><br><br>* **Copy all permissions**: The copied object will inherit the corresponding permissions from the source object.<br><br>* **Replace all permissions**: Set new permissions for the copied object.<br><br>* **Add new permissions**: Add new permissions on the basis of the original object permissions. |
      |Object metadata |Select the metadata of the object after copying; supported operations include:<br><br><br>* **Copy all metadata**<br><br>* **Replace all metadata**<br><br>* **Add new metadata**<br><br>* **None**<br><br><br>For detailed information about metadata, see [Managing file metadata](https://docs.byteplus.com/docs/tos/docs-managing-file-metadata). |
      |Object Tag |Select the label of the object to be copied, the supported operations are as follows:<br><br><br>* **Copy all tags**<br><br>* **Replace all tags**<br><br>* **Add new tags**<br><br>* **None**<br><br><br>For detailed information about Object Tagging, see [Managing file tags](https://docs.byteplus.com/docs/tos/docs-managing-file-labels). |
      

   * **Bulk replacement object ACL**

      
      |Parameters |Description |
      |---|---|
      |Task Type |Select **Bulk replacement object ACL**.<br><br>For detailed information about object ACLs, see [Configuring an Object ACL](https://docs.byteplus.com/docs/tos/docs-configuring-an-object-acl). |
      

   * **Batch Processing object tags**

      
      |Parameters |Description |
      |---|---|
      |Task Type |Select **Batch processing object tags**. |
      |Bulk operations |Select the label operations you need to process in bulk. Supported operations are as follows:<br><br><br>* **Replace all object tags**: Click to add a field and set the key\-value pairs that need to be replaced. You can add up to 10 tags.<br><br>* **Remove all object tags**: This operation will remove all tags from each object listed in the list. Before proceeding, you need to check the box stating **I understand that this action will remove all object tags on each object listed in the inventory**. |
      

   * **Batch recovery archive object**

      
      |**Parameters** |**Description** |
      |---|---|
      |Task Type |Select **Batch recovery archive object**. |
      |Validity of the copy |Set the validity period of the copy. The validity period must be a positive integer, ranging from 1 to 365, measured in days.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After recovering the file, a temporary copy file of standard storage type will be generated for your access and operation. The copy will be automatically deleted after the expiration period you set. Temporary storage fees will be incurred during the validity period of the copy. For more information, please refer to <a href="https://docs.byteplus.com/docs/tos/docs-temporary-storage-fee">Temporary storage</a>.</div><br> |
      |Recovery Mode |Set the recovery mode for the file. Different recovery modes vary in duration; the shorter the time, the higher the unit price. Description as follows:<br><br><br>* **Standard Retrieval**: Typical restoration of archived files is completed within 1 minute; cold archive files generally restore within 2 to 5 hours; deep cold archive files are typically restored within 12 hours.<br><br>* **Batch Retrieval**: Only cold archived and deep cold archived files support batch retrieval. Cold archived files are typically restored within 5~12 hours; deep cold archived files are typically restored within 48 hours.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Archived storage objects only support standard retrieval. If batch retrieval is selected, the operation to restore archived storage objects will fail.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Restoring archive storage files will incur data retrieval costs; restoring cold archived files or deep cold archived files will also incur data retrieval costs and request charges. For detailed instructions, please see <a href="https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee">Data retrievals</a> and <a href="https://docs.byteplus.com/docs/tos/docs-request-fee">Requests</a>.</div><br> |
      

5. Click **Next: other configuration**, and in the **Other configurations** wizard, set the following parameters.

   
   |Parameters |Description |
   |---|---|
   |Task description |Set the task description information, supporting up to 256 characters. |
   |Task priority |Set the task priority. The larger the number, the higher the priority, with values ranging from 1 to 1073741824.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Priority does not directly determine the order of task completion. If you need to strictly control the execution order, you must manually control the task sequence, starting the next task only after the previous one has finished. For detailed steps, please see <a href="https://docs.byteplus.com/docs/tos/Batch-processing1#6edb29a9">Other operations</a>.</div><br> |
   |Task report |Choose whether to generate a task report, supporting operations include:<br><br><br>* **Generate**: Select **Task report scope**, **Report delivery bucket**, and **Report delivery prefix** parameters.<br><br>* **Do not generate**: Do not generate a task report.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">If you choose not to generate a task report, you will not be able to view the task details, so please choose carefully.</div><br> |
   |IAM role |Generated by default, no selection needed. |
   

6. Click **Next: Confirm the configuration.** 

7. In the **Confirm configuration** wizard, after ensuring the parameters are correct, check **Check this box, the task will be started directly after it is created. Please make sure the above configuration information is correct**, then click **Create**.

   After the task is created, the page will automatically redirect to the batch processing task list, where you can perform operations such as viewing task details, cloning, or canceling tasks. For detailed information, please refer to other operations.


<span id="6edb29a9"></span>
## Other operations


* View task details: Click on the target task name in the task list. In the panel that pops up, view the task details.

* Clone a task: Click **Clone** corresponding to the **Actions** column of the target task in the task list, and you will enter the task creation wizard. You can set the task information according to your needs.

* Cancel a task: Click **Cancel** corresponding to the **Actions** column of the target task in the task list to cancel the task.

* Delete a task: After the task execution is completed, click **Delete** corresponding to the **Actions** column of the target task, and then click **Delete** in the pop\-up dialog box to delete the task.

* Start a task: Click **Start** corresponding to the **Actions** column of the target task in the task list to start the task.
