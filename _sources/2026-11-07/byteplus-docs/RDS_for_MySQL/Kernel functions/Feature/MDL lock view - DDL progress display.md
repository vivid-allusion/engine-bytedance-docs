---
title: "MDL lock view/DDL progress display"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/mdl_lock_view_ddl_progress_display"
---

DDL operations on large tables are often time\-consuming. It can be problematic when you are unable to track the progress and stages of the entire DDL process. Enabling the native MySQL `performance_schema` feature causes performance degradation and increased memory usage. To solve these problems, RDS for MySQL provides a lightweight `performance_schema` feature that offers MDL lock view and DDL progress display capabilities with low overhead.

<span id=".5pSv5oyB54mI5pys"></span>
## Supported version


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.44_20240815 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20230815 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version">Manually upgrading the instance kernel minor version</a>.</div>


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Usage


1. Modify the `loose_rds_performance_schema` parameter to `ON`.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more information about how to modify parameters, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters">Modifying parameters</a>. If this parameter is not available in the modifiable parameters for your instance, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to contact technical support to upgrade the instance.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When <code>performance_schema = on</code>, <code>loose_rds_performance_schema</code> is invalid.   </div>
   

2. Obtain the MDL lock view and DDL progress.

   1. Check the `performance_schema.metadata_locks` table to view the MDL lock usage of the current system.

   ```sql
   MySQL [****]> select * from performance_schema.processlist;
   +----+-----------------+---------------------+--------+---------+------+---------------------------------+----------------------------------------------------------+---------+-----------+---------------+------------------+
   | ID | USER            | HOST                | DB     | COMMAND | TIME | STATE                           | INFO                                                     | TIME_MS | ROWS_SENT | ROWS_EXAMINED | EXECUTION_ENGINE |
   +----+-----------------+---------------------+--------+---------+------+---------------------------------+----------------------------------------------------------+---------+-----------+---------------+------------------+
   |  5 | event_scheduler | localhost           | NULL   | Daemon  | 1925 | Waiting on empty queue          | NULL                                                     | 1925356 |         0 |             0 | PRIMARY          |
   | 13 | root            | 127.***.***.1:39294 | testDB | Query   |    0 | executing                       | select * from performance_schema.processlist             |       0 |         1 |             4 | PRIMARY          |
   | 15 | root            | 127.***.***.1:56616 | testDB | Query   |  208 | Waiting for table metadata lock | alter table T add column d varchar(10),algorithm=inplace |  208006 |         9 |            29 | PRIMARY          |
   +----+-----------------+-----------------+------+---------+------+---------------------------------+----------------------------------------------------------+---------+-----------+---------------+------------------+
   
   MySQL [****]> select OBJECT_SCHEMA, OBJECT_NAME, LOCK_TYPE, LOCK_STATUS, OWNER_THREAD_ID from performance_schema.metadata_locks;
   +--------------------+----------------+---------------------+-------------+-----------------+
   | OBJECT_SCHEMA      | OBJECT_NAME    | LOCK_TYPE           | LOCK_STATUS | OWNER_THREAD_ID |
   +--------------------+----------------+---------------------+-------------+-----------------+
   | NULL               | NULL           | INTENTION_EXCLUSIVE | GRANTED     |              84 |
   | NULL               | NULL           | INTENTION_EXCLUSIVE | GRANTED     |              84 |
   | testDB             | NULL           | INTENTION_EXCLUSIVE | GRANTED     |              84 |
   | testDB             | T              | SHARED_UPGRADABLE   | GRANTED     |              84 |
   | NULL               | NULL           | INTENTION_EXCLUSIVE | GRANTED     |              84 |
   | NULL               | testDB/T       | INTENTION_EXCLUSIVE | GRANTED     |              84 |
   | testDB             | #sql-1aafcb_f  | EXCLUSIVE           | GRANTED     |              84 |
   | testDB             | T              | EXCLUSIVE           | PENDING     |              84 |
   | performance_schema | processlist    | SHARED_READ         | GRANTED     |              80 |
   | performance_schema | metadata_locks | SHARED_READ         | GRANTED     |              80 |
   | testDB             | T              | SHARED_READ         | GRANTED     |              80 |
   +--------------------+----------------+---------------------+-------------+-----------------+
   11 rows in set (0.00 sec)
   ```
   

   2. Check the `performance_schema.events_stages_current` table to view the current DDL execution progress.

      * During DDL execution, you can check the `events_stages_current` table to obtain the execution state and progress of the DDL.

         ```sql
         MySQL [****]> SELECT THREAD_ID,EVENT_ID, EVENT_NAME, WORK_COMPLETED, WORK_ESTIMATED,(WORK_COMPLETED/WORK_ESTIMATED)*100 as PROGRESS FROM performance_schema.events_stages_current;
         +-----------+----------+------------------------------------------------------+----------------+----------------+----------+
         | THREAD_ID | EVENT_ID | EVENT_NAME                                           | WORK_COMPLETED | WORK_ESTIMATED | PROGRESS |
         +-----------+----------+------------------------------------------------------+----------------+----------------+----------+
         |        84 |        2 | stage/innodb/alter table (read PK and internal sort) |         115952 |         312538 |  37.1001 |
         +-----------+----------+------------------------------------------------------+----------------+----------------+----------+
         1 row in set (0.00 sec)
         ```
         

      * During DDL execution, you can use the `threads` and `processlist` tables to view the SQL for the current event.

         ```sql
         MySQL [****]> SELECT esc.THREAD_ID, esc.EVENT_NAME, esc.WORK_COMPLETED, esc.WORK_ESTIMATED, pl.INFO FROM performance_schema.events_stages_current esc LEFT JOIN performance_schema.threads th ON esc.thread_id = th.thread_id LEFT JOIN performance_schema.processlist pl ON th.PROCESSLIST_ID = pl.ID;
         +-----------+------------------------------------------------------+----------------+----------------+----------------------------------------------------------+
         | THREAD_ID | EVENT_NAME                                           | WORK_COMPLETED | WORK_ESTIMATED | INFO                                                     |
         +-----------+------------------------------------------------------+----------------+----------------+----------------------------------------------------------+
         |        84 | stage/innodb/alter table (read PK and internal sort) |         150660 |         312538 | alter table T add column d varchar(10),algorithm=inplace |
         +-----------+------------------------------------------------------+----------------+----------------+----------------------------------------------------------+
         1 row in set (0.11 sec)
         ```
         


<span id=".5ZCO57ut5q2l6aqk"></span>
## Subsequent steps

Compared to the native MySQL `performance_schema`, the `performance_schema` feature provided by RDS for MySQL is a lightweight implementation that reduces instance resource consumption. However, this feature can still put significant pressure on instances with low specifications. Therefore, after you enable this feature, you must continuously monitor the memory usage rate of the instance.


* RDS for MySQL provides a `Memory usage rate` monitoring item. You can configure an alert policy for this item and set an alert threshold for your instance's memory usage rate. When the memory usage rate exceeds the threshold, you will receive a timely alert message. For more information about creating alert policies, refer to [Creating alert policies](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_alert_policies).

* RDS for MySQL provides the modifiable parameter `performance_schema_max_thread_instances`. This parameter sets the maximum number of observed threads, which is the maximum number of rows in the `performance_schema.threads` table, to control the memory consumption of the `performance_schema` feature. The default value of this parameter is `1024`, and you can adjust it based on your instance specification and business requirements. For more information about modifying parameters, see [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This parameter must be used with <code>loose_rds_performance_schema</code> and takes effect only when <code>loose_rds_performance_schema</code> is set to <code>ON</code>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the <code>performance_schema_max_thread_instances</code> parameter value is 1024, high concurrency may cause the loss of MDL lock records in the <code>performance_schema.metadata_locks</code> table. In this case, consider modifying the value of <code>performance_schema_max_thread_instances</code> to <code>-1</code>. This removes the limit on memory consumption for the <code>performance_schema</code> feature.   </div>
   

* You can also evaluate your business requirements to determine whether to continue using this feature. If you no longer need this feature, modify the `loose_rds_performance_schema` parameter to `OFF` to disable it.
