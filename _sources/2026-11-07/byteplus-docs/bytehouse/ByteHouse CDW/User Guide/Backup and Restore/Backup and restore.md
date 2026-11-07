---
title: "Backup and restore"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/full-backup-restore"
---

To protect your data from accidental deletion or modification and prepare for disaster recovery, you can use ByteHouse's data backup feature. This guide walks you through configuring backup policies, including full and incremental options, restoring data from a specific backup set, and managing your backups directly in the ByteHouse Console to ensure data security and control costs.

<span id="770d1e26"></span>
# Caution


|Items |Caution |
|---|---|
|Supported tables |* Currently, only table backups are supported. Data objects such as views, materialized views, and Kafka tables are not supported for backup.<br><br>* Currently, only backups within the same region are supported; cross\-region backups are not supported. |
|Cost |* Cost of computing: Both data backup and restore operations use virtual warehouse resources and incur computing costs.<br><br>* Storage fees: After data backup, storage resources will be occupied, resulting in storage fees. Billing starts once the backup policy takes effect. |


<span id="471e14eb"></span>
# Data backup

<span id="571e47aa"></span>
## Enable data backup

Log in to the ByteHouse Cloud Data Warehouse Console, click the top **Tenant management**, and then click the **Data Backup** tab. When accessing for the first time, a welcome prompt will appear. Click the **OK** button on the prompt page to enable the data backup feature. The following image shows the welcome prompt for first\-time access.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/aaf9c32afb5342c1a56fef3a9e36a90f~tplv-goo7wpa0wc-image.image) </span>

<span id="a6e64913"></span>
## Create backup policy


1. On the \*\*Data backup \*\*page, click the \*\*Backup policy \*\*tab and then the \*\*Create backup policy \*\*button.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/893a2dc2c27143f69e360b16014bd83e~tplv-goo7wpa0wc-image.image) </span>

2. In the dialog box, configure the backup policy.

   1. Fill in the basic information, including the backup policy name and select the virtual warehouse to use.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2105da9d8c540069c515f4b4a6c2765~tplv-goo7wpa0wc-image.image) </span>

      * The policy name must meet the following conditions: it can contain numbers, letters, and underscores; it cannot start with a number; it can be up to 64 characters long; and it must not duplicate an existing task name.

      * The virtual warehouse is used to execute data backup and restore. If you do not specify one, the system will use the default virtual warehouse. If the virtual warehouse you select has enabled the "auto resume/suspend" feature, then when a backup task is triggered, a virtual warehouse in the suspend state will automatically resume.

   2. Select the backup object, which can be a database or an entire table.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82d7c4cb5f294de3a385c2956f4425c3~tplv-goo7wpa0wc-image.image) </span>

   3. Confirm the backup plan.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/770dbf160d4b43f497bbd03d82b4ba6d~tplv-goo7wpa0wc-image.image) </span>

      
      |Parameters |Configuration description |
      |---|---|
      |Backup method |Supports setting to full backup or full + incremental backup.<br><br><br>* **Full** **backup**: Full data backup of the cluster.<br><br>* **Full** + **incremental backup**: When this policy runs for the first time, it performs a full backup. Subsequent backups under this policy are incremental. Incremental backups are performed based on a full backup or the previous incremental backup under the same policy. |
      |Backup set retention period |Set the retention duration for the backup set. Backup sets can be retained for up to 90 days. |
      |Execution time zone |Set the time zone referenced for backup execution. This time zone is used to determine the actual execution time of the backup task. |
      |Execution cycle |This parameter is required for full backup. It can be set as one\-time or repeatable.<br><br><br>* **One\-time**: Backup is executed only once at the specified time.<br><br>* **Repeatable**: Backup tasks are executed on schedule according to the repeat cycle you set. |
      |Execution time |This parameter is required for one\-time full backup. This parameter is used to set the execution time for the one\-time full backup task. |
      |Repeat cycle |This parameter is required for **repeatable** **full backup** and **full** + **incremental backup**. This parameter specifies the time for periodic execution of backup tasks. You can select the repeat cycle from the drop\-down list as needed. |
      |Full backup |This parameter is required for **full** + **incremental backup**. It is used to set the execution time for full backup. After configuration is complete, you can preview whether the configured cycle meets your requirements in the preview area. |
      |Incremental backup |When **full** + **incremental backup** and **weekly incremental backup** are selected, you must set which day of the week to execute the incremental backup.<br><br>If **increment by day** is selected for your incremental backup, the execution time for incremental backup each day will be consistent with the time set for full backup, and no configuration is required.<br><br>After configuration is complete, you can preview whether the configured cycle meets your requirements in the preview area. |
      

3. Click **Create**.

4. Successfully created tasks will appear in the backup policy list. The system automatically runs the backup task at the scheduled time.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/197e1e3069a34539ac55860cf7d26ee3~tplv-goo7wpa0wc-image.image) </span>

5. You can click the **Backups** tab to view completed backup sets.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2bd294c2511f415abaa269ae00f1741a~tplv-goo7wpa0wc-image.image) </span>


<span id="301714df"></span>
## View the status of the backup set

After the backup task is automatically completed, you can view the status of the backup in the backup set. If the backup is not successful, you can click the corresponding backup set task name to view Task Details, including the data range and reason for backup failure.

<span id="9c3057c7"></span>
## View backup set storage usage


* After the backup task starts executing, you can view the storage space currently occupied by all databases, tables, and backup sets at \*\*Tenant management \*\*\> \*\*Basic information \*\*\> **Storage information**, and estimate the storage costs generated by all backup sets.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a5de9aae4ab43238656973aec1f3ca1~tplv-goo7wpa0wc-image.image) </span>

* You can also view the storage size occupied by a specific backup data in **Tenant management** \> **Data backup** \> **Backups**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0baf7c63ec484d639d2cf11e02551769~tplv-goo7wpa0wc-image.image) </span>


<span id="083fe5a6"></span>
# Restore data

After executing the backup task, you can restore data from the backup set.

**Steps**:


1. Go to the **Tenant management** \> **Data backup** page, click the **Backups** tab, and click the **restore** button to the right of the data you want to restore.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f911c29ab560474784850279884caf08~tplv-goo7wpa0wc-image.image) </span>

2. Select the virtual warehouse to execute the restore task, and select the database and table information to restore.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1fe8b03aadc24b9092682f4f8893dd31~tplv-goo7wpa0wc-image.image) </span>

3. Click **Apply**, and the system will start restoring the data.

4. After a restore operation succeeds, you can view its details in the **Restoration records** tab.


<span id="7cd72972"></span>
# Delete backup set

You can view all executed backup sets in the **Backups** tab. To save storage costs, you can delete unneeded backup sets by clicking the **Delete** button next to them.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Deleting the backup set is irreversible. Proceed with caution.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb3fddf022ae46269167abe60b0e7b02~tplv-goo7wpa0wc-image.image) </span>
