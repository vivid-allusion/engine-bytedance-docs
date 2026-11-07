---
title: "Configure Retention Policy (WORM)"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/Configure-retention-policy"
---

In industries such as healthcare and finance, strict compliance requirements stipulate that certain documents must not be deleted or overwritten within specified time periods to ensure data integrity and auditability. To meet such requirements, TOS provides a retention policy feature that ensures objects cannot be deleted or overwritten by anyone within a specified period, thereby enabling Write Once Read Many (WORM) data storage behavior. This document presents the application scenarios, key considerations, operational steps for configuring retention policies, and other related content.

<span id="f8232201"></span>
## Function Introduction

To use the retention policy feature, you must first enable object lock on the storage bucket. Once enabled, you can configure either the bucket retention period or the object retention period. Details are as follows:


* Bucket Retention Period: TOS supports configuring a retention period for storage buckets. Once the bucket retention period is set, any newly uploaded object that does not have an individual object retention period specified will, by default, inherit the bucket retention period and automatically enter a locked state. Before the retention period expires, no one will be able to delete or overwrite the object. Objects uploaded before the bucket retention period is set will not automatically inherit that retention period.

* Object Retention Period: TOS supports setting the retention period for objects individually. You can specify the retention period for objects that have already been uploaded or for newly uploaded objects. Object retention time takes precedence over bucket retention time. If both are set, the object's retention time will be used.


If only the object lock feature is enabled without setting either the bucket retention period or the object retention period, objects will not enter the locked state and cannot obtain protection against deletion or overwriting.

<span id="4a57eb71"></span>
## Application Scenarios

The retention policy feature supports WORM (Write Once Read Many) functionality, enabling customers to retain electronic records in a non\-erasable and non\-deletable format to meet regulatory requirements in specific industries. It is suitable for scenarios that require compliance, tamper resistance, and deletion prevention.


* Machine learning: Model data obtained through prolonged training is a valuable asset. If the data source or model data is overwritten or accidentally deleted during training, the training task will be interrupted, resulting in GPU resource waste. Retention policies can protect this data from being arbitrarily overwritten or deleted.

* Intelligent Driving: In intelligent driving systems, retention strategies can be employed to protect critical data—including sensor data, model training sets, and log files—ensuring the integrity and immutability of such information to meet increasingly stringent compliance and regulatory requirements. Once written, the data cannot be deleted or overwritten, thereby enhancing the overall security and trustworthiness of the system.

* Compliance scenarios such as those in finance and healthcare: Institutions such as those in finance, insurance, healthcare, etc., must comply with strict laws and regulations, and rigorously manage and protect sensitive information, including image data and customer information. The retention policy feature ensures that data cannot be overwritten or deleted during the specified retention period, thereby meeting compliance audit requirements.


<span id="452d4bf8"></span>
## Precautions

**Retention Period**


* Once the object lock feature is enabled, it cannot be disabled; however, you may deactivate the retention period.

* The bucket retention period can be extended or shortened, whereas the object retention period can only be extended and cannot be shortened.

* Object retention period cannot be canceled and will only automatically expire when the retention period ends. Therefore, once a retention period is set for an object, no one—including the object owner—can delete or overwrite the object before the retention period expires.

* In cases of account cancellation or overdue account arrears, data will be deleted even if the retention period has not expired.

* After an Appendable type object is locked, append write operations cannot be performed on the object during the retention period; once the retention period expires, you may resume append write operations on the object as normal.

* After the bucket retention period is set, shards are not subject to the bucket retention period rules, and you can still delete shards within the bucket.


**Bucket Replication**


* The object lock status of the source bucket and the destination bucket must be consistent; otherwise, same\-region replication and cross\-region replication rules cannot be configured.

* There are restrictions on the order in which bucket replication rules and retention policies can be enabled. If you need to create a retention policy and a replication rule in a specified storage bucket, you must create the retention policy before creating the replication rule. If replication rules have already been created for your bucket, creating retention policies is not supported.


**Lifecycle Rule**

When an object is in a locked state, lifecycle deletion rules will not take effect until its retention period expires, while archiving rules will continue to operate normally. Lifecycle deletion rules take effect only after the retention period expires.


|**Lifecycle Rule** |**Object Retention Time** |**Execution Result** |
|---|---|---|
|10\-Day Subsidence Targets |20 days |The object is moved to a lower storage tier on the 10th day after upload. |
|Delete object after 10 days |20 days |The object will not be deleted on the 10th day after upload, but will be deleted on the 21st day after upload. |
|30\-Day Subsidence Targets |20 days |The object is moved to cold storage on the 30th day after upload. |
|Delete Object After 30 Days |20 days |The object is deleted on the 30th day after upload. |


**Version Control**

TOS supports setting an independent retention period for each version of an object. When performing delete or overwrite operations on locked objects, the results will vary depending on the status of version control, as explained below:


|**Version Control Status** |**Delete Locked Object** |**Overwrite Locked Object (Upload Object with the Same Name)**  |
|---|---|---|
|Not Enabled |Deletion failed. |Upload failed. |
|Enable |Adding a deletion marker to locked objects is supported; permanently deleting locked objects is not supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Setting a retention period for deletion markers is not supported.</div><br> |A new version object is generated, and the previously locked object is converted into a historical version object. |
|Pause After Enabling |A null version object exists and is locked; deletion failed. |A null version object exists and is locked, resulting in upload failure. |


<span id="63a02fdc"></span>
## Set Retention Policy

<span id="f9d03723"></span>
### Set Bucket Retention Time


<Tabs>
<Tab zoneid="WMeju8Xy9m" title="Set the bucket retention period when creating a new bucket">
<TabTitle>Set the bucket retention period when creating a new bucket</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets.** 

3. On the **Buckets** page, click **Create bucket**.

4. On the **Create bucket** page, click **Advanced settings** and enable **Retention Policy**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For a detailed description of other parameters for creating a bucket, see <a href="https://docs.byteplus.com/docs/tos/docs-create-a-bucket">Create Bucket</a>.   </div>
   

5. After completing the settings, click **Create**.

6. In the left navigation bar, click **Security** ＞ **Retention policy**.

7. On the **Retention policy** page, click **Edit**, enable **Default retention period** and set the **Default retention time**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The retention policy only supports compliance mode, meaning that no user can delete or overwrite locked objects during the retention period.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default retention period can be configured by day or by year, with a value range of 1 to 36,500 days or 1 to 100 years.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default retention period is a relative time interval, calculated from the moment the object is uploaded, and the lock status ends after the specified duration. It should be noted that the retention period for sharded objects is calculated from the time the sharding task is created.   </div>
   

8. After completing the setup, click **Select**.

9. In the pop\-up dialog box, click **OK**.


</Tab>
<Tab zoneid="BSExmEiArs" title="Set bucket retention time for existing buckets">
<TabTitle>Set bucket retention time for existing buckets</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. In the left navigation bar, select **Security ＞ Retention policy**.

4. On the **Retention policy** page, enable **Object locking** and **Default retention period**, and set the **Default retention time**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The retention policy only supports compliance mode, which means that no user can delete or overwrite protected objects during the retention period.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default retention period supports configuration by day or by year, with a value range of 1 day to 36,500 days or 1 year to 100 years.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default retention time is a relative time period, calculated from the moment the object is uploaded, and the locked status ends after the specified duration. It should be noted that the retention period for sharded objects is calculated from the time the sharding task is created.   </div>
   

5. After completing the setup, click **Select**.

6. In the pop\-up dialog box, click **OK**.


</Tab>
</Tabs>


<span id="QI3SM7e7"></span>
### Set Object Retention Time


1. Enable object lock.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To set the retention period for a single object, you must first enable the object lock feature; otherwise, you cannot set the retention period for a single object.   </div>
   

   1. Log in to the [TOS console](https://console.byteplus.com/tos).

   2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

   3. In the left navigation bar, select **Security ＞ Retention policy**.

   4. On the **Retention policy** page, enable **Object locking**, and click **Select**.

   5. In the pop\-up dialog box, click **OK**.

2. Set the retention time for the object.

   
   <Tabs>
   <Tab zoneid="xyIsomO7yD" title="Set Retention Time When Uploading Objects">
   <TabTitle>Set Retention Time When Uploading Objects</TabTitle>
   
   You can set the `x-tos-object-lock-mode` and `x-tos-object-lock-retain-until-date` parameters via the following API to configure the retention period for an object. Details are as follows:
   
   
   * [PutObject](https://docs.byteplus.com/docs/tos/reference-putobject)
   
   * [PostObject](https://docs.byteplus.com/docs/tos/reference-postobject)
   
   * [CreateMultipartUpload](https://docs.byteplus.com/docs/tos/reference-createmultipartupload)
   
   * [CopyObject](https://docs.byteplus.com/docs/tos/reference-copyobject)
   
   * [AppendObject](https://docs.byteplus.com/docs/tos/reference-appendobject)
   
   
   </Tab>
   <Tab zoneid="zETQ8cZoWg" title="Set retention period for uploaded objects">
   <TabTitle>Set retention period for uploaded objects</TabTitle>
   
   1. Log in to the [TOS console](https://console.byteplus.com/tos).
   
   2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.
   
   3. On the **Objects** page, click  **...**   **＞ Set retention date ** under the **Actions** column for the target file. 
   
   4. In the pop\-up dialog box, set the end date for the object lock, and click **OK**.
   
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   
   * <div data-tips="true" data-tips-type="default">The retention date specifies the deadline by which an object cannot be deleted or overwritten, and it is defined as an absolute time. After the retention date is set, the object will exit the locked state at 23:59:59 on the retention date.</div>
   
   
   * <div data-tips="true" data-tips-type="default">You can also call PutObjectRetention to set the retention period for uploaded objects. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Putobjectretention">PutObjectRetention</a>.</div>
   
   
   5. Click **OK.** 
   
   
   </Tab>
   </Tabs>
   


<span id="c8c78e6c"></span>
## Extend Retention Period

The bucket retention period can be extended or shortened, but the object retention period can only be extended and cannot be shortened.


<Tabs>
<Tab zoneid="Ch57HPfj9g" title="Extend Bucket Retention Time">
<TabTitle>Extend Bucket Retention Time</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. In the left navigation bar, select **Security ＞ Retention policy**.

4. On the **Retention policy** page, click **Edit**, extend the default retention period, and then click **Select**.

5. In the pop\-up dialog box, click **OK**.


</Tab>
<Tab zoneid="WF9Fvw7J9T" title="Extend Object Retention Period">
<TabTitle>Extend Object Retention Period</TabTitle>

1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. On the **Objects** page, click  **...**   **＞ Set retention date ** under the **Actions** column for the target file. 

4. In the pop\-up dialog box, extend the protection period of the object. Click **OK**.

5. Click **OK**.


</Tab>
</Tabs>


<span id="IUoYRGvo"></span>
## View Object Retention Information


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. On the **Objects** page, click **Details** under the **Actions** column for the target file.

4. In the object details panel, view the object's **Retention mode** and **Retention expiration date**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Bucket inventory supports exporting the retention mode and retention expiration date of objects. You can use bucket inventory to obtain the retention mode and retention expiration date of objects in the bucket in bulk. For detailed information, see <a href="https://docs.byteplus.com/docs/tos/Bucket-inventory">Bucket Inventory</a>.   </div>
   

<span id="78d5366b"></span>
## Disable Bucket Retention Time

Only disabling the bucket retention period is supported; canceling the existing retention period for objects is not supported. After the bucket retention period is disabled, newly uploaded objects will no longer automatically enter the locked state, and the retention period for existing objects will remain unchanged.


1. Log in to the [TOS console](https://console.byteplus.com/tos).

2. In the left navigation bar, click **Buckets**. On the **Buckets** page, click the target bucket name.

3. In the left navigation bar, select **Security ＞ Retention policy**.

4. On the **Retention policy** page, click **Edit**, disable the **Default retention period**, and click **Select**.

5. In the pop\-up dialog box, click **OK**.
