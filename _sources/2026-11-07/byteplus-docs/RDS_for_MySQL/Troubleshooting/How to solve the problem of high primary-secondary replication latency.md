---
title: "How to solve the problem of high primary-secondary replication latency"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/How_to_solve_the_problem_of_high_primary-secondary_replication_latency"
---

When using RDS for MySQL, high write traffic or table structure issues in an instance may cause increased data latency between the primary and read\-only nodes. When primary\-secondary latency increases, read requests routed to read\-only nodes may fail to access newly written data or may retrieve outdated data. For secondary nodes[[1]](https://www.volcengine.com/docs/6313/1411541#%E9%99%84%E5%BD%95) that use binlog replication, this may lead to failed switching between primary and secondary nodes and impact high\-availability.

<span id="问题确认"></span>
## Confirm the problem

View the monitoring items for **replication latency** to confirm if the instance has high primary\-secondary latency.


1. On the Instances page, click the instance name of the target instance to enter the Instances page.

2. Click the Monitoring and alarm tab at the top of the page.

3. Under the **Deployment Monitoring** category, view **Replication Latency**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">View the replication latency for each node of the instance.   </div>
   

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3f73c3ce636ec924be1c41ddadfb97ed.png) </span>


<span id="快速止损"></span>
## Quick stop\-loss

Pause writes if there is a known large write load. Resume writes after adjusting the write traffic. If you cannot determine the cause, continue to read this article for methods to locate and resolve the issue.

<span id="原因定位及解决"></span>
## Cause analysis

<span id="负载原因"></span>
### Load reason


* **Cause analysis**

   The MySQL slave node uses parallel replication playback, which typically prevents significant latency. If the database executes resource\-intensive loads, such as DDL for large table reconstruction, large transactions, or heavy write loads, slave node playback is delayed, which impacts the primary\-slave latency.

   * Request\-level analysis: In the **Deployment monitoring** category, view the monitoring items under **Engine monitoring** \> **Access** to check for a high volume of write requests (updates, inserts, deletes, or overwrites).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c23272392e442d984b124db9ba56a7ff.png) </span>

   * Row\-level analysis

      Under the **Deployment monitoring** category, go to **Engine monitoring** \> **Innodb** to check for a high number of row modifications. Focus on **Innodb rows inserted**, **Innodb rows deleted**, and **Innodb rows updated**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_df1177d3bcda3a654e757aaf9d291cb4.png) </span>



&nbsp;

* **Solution**

   Use the full SQL insight feature in Database Workshop to identify SQL statements with a high number of writes, and use [SQL throttling](https://www.volcengine.com/docs/DBW/preview-sql-throttle-task-management-for-mysql) to limit their execution frequency and prevent increases in primary\-replica latency.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Full SQL insight and SQL throttling are currently in the invitation test function of the database workbench.   </div>
   

   * Locate the SQL

      1. SQL insight The path for SQL insight is: **Log on** to [Database Workshop](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Full SQL insight \> Write analysis**. For more information, refer to [Full SQL insight](https://www.volcengine.com/docs/DBW/full-SQL-explorer).

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_921f6ca8e1a43eb92ccfb17075a7a8a1.png) </span>

      2. **DML statements**: Focus on **Average elapsed time** and **DML**. **Average scanned rows** and **DML** **Average affected rows**.

      3. **DDL statements**: rebuilding large tables with DDL also causes primary\-slave latency. Focus on **DDL**. **Average scanned rows** and **DDL** **Average affected rows**.

   * Process SQL

      After locating the SQL, it can be processed by SQL throttling or killing the session.

      2. SQL throttling

      After locating the problem SQL, you can limit the execution frequency of SQL through SQL throttling. Path:

      1. **Log on** [Database Workshop](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Session management** \> **SQL throttling** \> **Enable SQL throttling** \> **Create a task**.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_387b2f7455e71492278cd0eaa5b6037a.png) </span>

      2. In the Create SQL throttling task window, enter the problematic SQL and adjust the maximum concurrency. A maximum concurrency of 0 completely blocks the SQL. Click **Generate and verify keywords** to split the keywords. The keywords are separated by tildes (~).

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b85aa4fd3769c779eead66f14c348d78.png) </span>

      3. Click **OK** to submit the task.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">For more information, refer to <a href="https://www.volcengine.com/docs/DBW/preview-sql-throttle-task-management-for-mysql">SQL throttling management</a>.         </div>
         

      4. KILL session path:

         * **Log on** [Database Workshop](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Session management**.

         * In the **Real\-time sessions** area, monitor the **Time** and **State** of the session. If the State of a certain session is updating, but the value of Time is already very large, it may be a large write transaction, and attention needs to be paid to processing.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8df3cd1dc2b838e7c7b2d8d357044c0e.png) </span>


<span id="表结构原因"></span>
### Table structure reason


* **Cause analysis**

   Using a **primary key index** in MySQL tables is recommended. If a table lacks a primary or unique key, the slave node spends more time finding data to modify during playback, which increases primary\-slave latency. Tables without a primary key experience a significant increase in latency during large\-volume delete and update operations.

   * View the table structure for the write load

      ```sql
      SHOW CREATE TABLE example_table;
      ```
      

   * Analyze the table structure. If it lacks a PRIMARY KEY or UNIQUE KEY, the system may use an index with poor filtering during playback, sometimes even requiring a full table scan. For large tables, excessive retrieval time leads to increased latency.

   * Example of a table without a primary key:

      ```sql
      CREATE TABLE `example_table` (
        `column1` int(11) DEFAULT NULL,
        `column2` varchar(255) DEFAULT NULL,
        `column3` date DEFAULT NULL
      ) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4;
      ```
      

* **Solution**

   * If a unique column exists, modify the table structure to set it as a unique key:

      * Method 1: CREATE INDEX

         ```sql
         CREATE UNIQUE INDEX unique_col1 ON example_table (column1);
         ```
         

      * Method 2: ALTER TABLE

         ```sql
         ALTER TABLE example_table ADD UNIQUE (column1);
         ```
         

   * Add an auto\-incrementing primary key: For a table without a primary key, its data order is determined by the row_id of the storage engine. The row_ids on the primary and slave nodes may be different, leading to different data orders. When adding an auto\-incrementing primary key to such a table, the values are initialized based on the data order. This causes the same data to have different primary key values, and queries using the same primary key value will return different data on the primary and secondary nodes.

      When adding an auto\-incrementing column to a table with existing data, firstly, create a new table with the same structure. Then, add the auto\-incrementing column to the new table and import the data from the original table. (To avoid data inconsistencies between the original and new tables, do not perform write operations on the original table during data import.)

      Follow the steps below to resolve data inconsistency in queries between the primary and secondary nodes.

      * On the primary node, create a new table `t1_new` that is identical to the original table without a primary key (`t1`), and add an auto\-incrementing primary key to the new table.

         ```sql
         CREATE TABLE t1_new LIKE t1;
         ALTER TABLE t1_new ADD id INT AUTO_INCREMENT PRIMARY KEY;
         ```
         

      * Insert all data from the original table into the new table `t1_new`.

         ```sql
         INSERT INTO t1_new(column1, column2) 
             SELECT column1, column2 
             FROM t1 
             ORDER BY column1, column2;
         ```
         

      * Delete the original table `t1`, and rename the new table to the name of the original table.

         ```sql
         DROP TABLE t1;
         RENAME TABLE t1_new TO t1;
         ```
         


<span id="提升实例规格"></span>
### Upgrade instance specification

If the primary\-slave latency remains high after troubleshooting with the methods above, the slave node may be unable to keep up due to business pressure. In this case, consider upgrading the instance specification through a regular modification of specification or a temporary upgrade. Increasing the number of CPU cores can improve the processing capacity of the slave node and reduce primary\-slave latency.

For information about how to perform a regular modification of specification or a temporary upgrade for an instance, refer to the following documents:


* [Regular modification of specification](https://www.volcengine.com/docs/RDS_for_MySQL/standard_instance_specification_modification)

* [Temporary upgrade](https://www.volcengine.com/docs/RDS_for_MySQL/temporary_instance_specification_upgrade)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Temporary upgrade is currently an invitation\-only feature for RDS for MySQL. To use it, <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000178">submit a ticket</a> to apply.</div>


<span id="附录"></span>
## Appendix

**Glossary**

RDS for MySQL has two types of nodes that are replicated through binlogs:


* Read\-only node: handles user read traffic.

* Secondary node: a hot standby responsible for high\-availability that does not handle read traffic.


Common configurations: one primary and one secondary node; one primary, one secondary, and multiple read\-only nodes.
