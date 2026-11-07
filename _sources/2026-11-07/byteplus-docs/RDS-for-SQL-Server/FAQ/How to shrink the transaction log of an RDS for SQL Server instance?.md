---
title: "How to shrink the transaction log of an RDS for SQL Server instance?"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/shrink_the_transaction_log"
---

This topic describes the steps to shrink a transaction log.

<span id="EXYXgRRF"></span>
## Description

**What is a transaction log?** 

A transaction log is a key component of a database management system that records all transaction operations to enable data recovery. By recording details of database operations, such as additions, deletions, and modifications, it supports rolling back uncommitted transactions or redoing committed transactions in case of a system failure to ensure database consistency.

**What is the underlying logic of shrinking a transaction log?** 

Shrinking a transaction log file releases unallocated space, which reduces the storage space it occupies. This action essentially deletes inactive virtual log files, which are virtual log files that do not contain any logical log content. During the shrink process, inactive virtual log files are removed from the end of the log file to reduce the log to the desired size.

<span id="mGZlKyxM"></span>
## **Applicable scenarios**

When transaction log files consume a large amount of disk space and cause disk alerts or insufficient space due to unexpected events, such as super large transactions or index rebuilds, you can temporarily use the shrink feature to mitigate the issue.

<span id="SBnMBEpC"></span>
## Prerequisites


* An instance has been created and you have [connected to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance). For more information, see Connect to an instance.

* The value of the `log_reuse_wait_desc` attribute for the target database is `NOTHING`. For more information, see [How to view the value of the log_reuse_wait_desc attribute for a database?](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/log_reuse_wait_desc_attribute_value)


<span id="Gf2web7y"></span>
## Precautions

SQL Server Management Studio (SSMS) can only be installed on the Windows operating system.

<span id="0cCWzTfM"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default"><a href="https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms?spm=a2c63.p38356.879954.7.15df54088yM5PK&view=sql-server-2017">SQL Server Management Studio (SSMS) </a> uses English as the default language. </div>



1. Start the SQL Server Management Studio client on an ECS instance or a local device and [Connect to an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/connect-instance).

2. You can shrink the transaction log in the following two ways:

   * **Method 1**: Shrink the transaction log by using the Graphical User Interface.

      1. In SSMS, right\-click the target database, select **Tasks** \> **Shrink** \> **Files**, and click **Files**.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e12f3876f071d4cd90478c9874763f64.png) </span>

      2. On the **Shrink File** page, configure the following settings:

         * In the **Database files and filegroups** section, click the **File type** drop\-down list and select **Log**.

         * In the **Shrink action** section, select **Release unused space**.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6b290d7423fe2f95cb14e2489d3b9219.png) </span>

      3. Click **OK** to shrink the transaction log.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f827d4840b7a84ef143fae83123a049d.png) </span>

   * **Method 2**: Shrink the transaction log by using a script.

      1. Click **New Query** to create a new query window.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2de3ebad8ebe1944971d34439446c5e6.png) </span>

      2. The following is an example of shrinking the transaction log of testDB:

         * `testDB` is the database name.

         * `testDB_log` is the corresponding transaction log name.

         When using the following SQL statements, replace the database and transaction log names with the names of your target database and transaction log. The SQL statement is as follows:

         ```SQL
         USE [testDB] 
         GO
         DBCC SHRINKFILE (N'testDB_log' , 0, TRUNCATEONLY)
         GO
         ```
         

      3. Click **Execute** to shrink the transaction log.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4c4b51a861d911ddb22a7d9a8ecd396e.png) </span>

3. To view the available free space after shrinking the transaction log, right\-click the target database, select **Tasks** \> **Shrink** \> **Files**, and click **Files**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ba3c37f4eb697e0ed873842e1a5c4603.png) </span>

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_adb01981e15ba087c7cbf599a018fa65.png) </span>
