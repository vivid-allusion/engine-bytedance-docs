---
title: "Creating a data backup manually"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/manually_creating_a_data_backup"
---

This topic describes how to create a data backup manually.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The instance has been created and is in the **Running** or **Stopped** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. At the top of the page, click the **Backups** tab.

6. On the **Data backup** tab, on the **Basic backup list** sub\-tab, click **Data backup**, and then click **Manual backup**.

7. In the pop\-up dialog box, set the backup information. After configuring the **Backup type**, **Backup method**, and **Backup object**, click **OK** to create the manual backup.

   
   |Configuration items |Description |
   |---|---|
   |Backup type |The supported backup types vary based on the instance's storage type:<br><br><br>* If the instance's storage type is local disk, you can select **physical backup** or **logical backup**.<br><br>* If the instance's storage type is cloud disk, you can select **snapshot backup**. |
   |Backup method |If you select **Physical backup** or **Snapshot backup** as the backup type, the backup method can only be **Full backup**.<br><br>If you select **Logical backup** as the backup type, the backup method can be **Full database backup** or **Database & table backup**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The database & table backup method of logical backup only backs up the data structures and contents of the specified databases and tables; it does not back up views, stored procedures, user\-defined functions, triggers, or other objects.</div><br> |
   |Backup object |If you select **Physical backup** or **Snapshot backup** as the backup type, the backup object can only be **the entire instance**.<br><br>If you select **Logical backup** as the backup type, you do not need to set the backup object. |
   |Databases and tables |If the backup method is Database & table backup, select the databases and tables to back up. Select the databases and tables to back up from the table.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Up to 5,000 databases are displayed for each expanded instance, and up to 5,000 tables are displayed for each expanded database.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Search libraries or tables via regular expressions or fuzzy matching. When searching for libraries and tables at the same time, the search results for the libraries and tables will be output based on "and logic".</div><br> |
   |Backup name |Set the backup name. Naming rules are as follows:<br><br><br>* Cannot start with a hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length must be between 1 and 128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The backup name is an optional configuration. If a backup name is not set, the backup ID is used as the backup name.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If cross\-region backup is enabled for the instance and a backup name is set during manual backup, the cross\-region backup triggered by the manual backup will also use the specified backup name. If no backup name is set during the manual backup, the cross\-region backup triggered by the manual backup will also use the backup ID as the backup name.</div><br> |
   


<span id=".5bi46KeB6Zeu6aKY"></span>
## FAQs

**Why can't I perform a backup?** 

If you are unable to perform a backup operation, check the following:


* Confirm that the MySQL instance is **Running**.

* Confirm that the instance to be backed up is a primary instance. Read\-only nodes cannot be backed up.

* Confirm that no DDL operations are ongoing during the backup period to avoid table locks that may cause a backup failure.

* Backups cannot be created for databases with more than 600,000 tables. Database sharding is recommended when there are too many tables.


If the problem persists, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

**What are the reasons for backup failure?** 

A backup can fail for the following reasons. You can check the specific failure reason in the Status column in the backup list.


* Backup execution failed

* Backup task canceled

* Failed to upload the backup file

* Failed to download the backup file

* Object storage configuration error

* Failed to connect to or query the database

* The backup task held the backup lock for too long

* A backup task is already executing

* When performing an incremental backup, no completed full backup is available


**Does the backup type support logical backup?** 

Support.

<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[CreateBackup](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createbackup1) |Call the CreateBackup API to create a backup. |
