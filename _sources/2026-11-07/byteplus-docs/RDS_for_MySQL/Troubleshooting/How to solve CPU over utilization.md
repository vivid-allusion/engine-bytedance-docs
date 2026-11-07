---
title: "How to solve CPU over utilization"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/how_to_solve_cpu_over_utilization"
---

When using RDS for MySQL, if the CPU usage rate of an instance is too high or close to 100%, it may lead to slow data read and write processing, increased connection latency, and even errors during deletion operations, seriously affecting the normal operation of the business. This article provides the location and solutions for several common causes.

<span id="problem-confirmation"></span>
## Problem confirmation

Check the monitoring item of CPU usage rate to confirm the current CPU usage rate of the instance.


1. On the **Instances** page, click the instance name of the target instance to enter the **Instances** page.

2. At the top of the page, click the **Monitoring** tab.

3. Under the **resource monitoring** category, view **CPU Usage**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the CPU usage rate of each node of the instance according to the node dimension.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_a1794c875795be9278c86f812c23182e.png) </span>


<span id="quick-stop-loss"></span>
## Quick stop loss

If the CPU usage rate is already very close to 100%, you can quickly restore instance performance through the following two methods.


* Restart the instance.

* Switch the main node of the instance.


<span id="restart-the-instance"></span>
### Restart the instance

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The time\-consuming of restarting an instance depends on the load status of the instance. It will cause 1\-2 flashes of the business. Please operate with caution. It is recommended that you add a reconnection mechanism to the application, which can greatly reduce the impact of database connection flashes on the business.</div>



1. On the **Instances** page, click  **... \> Restart instance** in the **Actions** column of the target instance.

2. In the pop\-up dialog box, select **Restart scope** as **All nodes** and **Restart time** as **Restart immediately**, and then click **OK**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the CPU usage rate of each node of the instance according to the node dimension. If the node with high CPU usage rate is the main node, the <strong>Restart scope</strong> should be <strong>All nodes</strong>. If the node with high CPU usage rate is a certain read\-only node, the <strong>Restart scope</strong> should be <strong>Specified read\-only node</strong>, and select the corresponding read\-only node in the <strong>read\-only node</strong> drop\-down list.   </div>
   

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_f1b42c361b89fce665fb347a5963989c.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more detailed information, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance">Restarting an instance</a>.   </div>
   

<span id="switch-the-main-node-of-the-instance"></span>
### Switch the main node of the instance

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">During the switching of the main node, the database will have 1\-2 flashes. Please operate with caution. At the same time, it is recommended that you add a reconnection mechanism to the application program.</div>



1. On the **Instances** page, click the instance name of the target instance to enter the **Instances** tab.

2. Click the **Connectivity** tab. In the **Instance topology** area, point the mouse pointer to the **Secondary node**, click **Switch to primary node** in the pop\-up window, and click **OK** in the pop\-up dialog box to complete the switching of the primary and secondary nodes.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_fa6421ce15bab4a8345870e6f7d66873.png) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For more detailed information, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_primary_nodes">Switching primary nodes</a>.   </div>
   

<span id="cause-location-and-solution"></span>
## Cause location and solution

<span id="abnormal-sql-load"></span>
### Abnormal SQL load

<span id="qps-reason"></span>
#### QPS reason


* **Cause analysis**

   TP system SQL execution is generally relatively fast. The CPU of the MySQL instance will not increase without reason when there is no load. Most of the increase in CPU usage rate is due to abnormal SQL load, which leads to excessive consumption of resources. Therefore, it is necessary to first confirm whether the traffic has changed and whether new SQL has been launched. The specific way is to view the monitoring item of **queries_ps** of the instance in the database workbench.

   Operation path: **Login** [Database Workbench](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Performance monitoring** \> **queries_ps**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_2dc6142ef8029cae20b840d6abf08467.png) </span>

* **Solution**

   Determine which SQL causes the increase in CPU load through the slow log analysis and full SQL insight functions of the database workbench, and limit the execution frequency of SQL through [Throttling SQL](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql) to prevent abnormal loads from saturating the CPU.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Full SQL insight and SQL throttling are currently in the invitation test function of the database workbench. If you need to use them, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to apply.   </div>
   

   1. Locate SQL

      * **Slow log analysis**

         The operation path for slow log analysis is: **Login** [Database Workbench](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Slow log analysis**. For more detailed information, please see [Slow log management](https://docs.byteplus.com/en/docs/DBW/slow-log-management-for-mysql).

         <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_6c4bcb85a030b878470e0db2bbad4976.png) </span>

         When performing slow log analysis, you can focus on the following information:

         * **Average lock waiting time** Determine whether slow SQL is more off\-CPU or on\-CPU. A long wait time indicates that SQL does not occupy the CPU for a long time. Conversely, it proves that there is more on\-CPU time.

         * **Average number of rows scanned** Generally positively correlated with CPU usage rate.

         * Focus on the `Rows_examined` field. If it is very high, it indicates that more resources are needed to scan rows and will occupy more CPU resources.

         ```sql
         # Time: 2022-12-14T15:01:34.892085Z
         # User@Host: root[root] @ localhost []  Id:     8
         # Query_time: 3.985637  Lock_time: 0.000138 Rows_sent: 165346 Rows_examined: 9900000 Thread_id: 8 Errno: 0 Killed: 0 Bytes_received: 0 Bytes_sent: 4848540 Read_first: 0 Read_last: 0 Read_key: 1 Read_next: 9900000 Read_prev: 0 Read_rnd: 0 Read_rnd_next: 0 Sort_merge_passes: 0 Sort_range_count: 0 Sort_rows: 0 Sort_scan_count: 0 Created_tmp_disk_tables: 0 Created_tmp_tables: 0 Start: 2022-12-14T15:01:30.906448Z End: 2022-12-14T15:01:34.892085Z Schema: slow Rows_affected: 0
         SET timestamp=1671030090;SELECT * FROM `student` WHERE id>100000 AND `name`='Yunxi';
         ```
         

   2. Process SQL

      After locating the SQL, it can be processed by SQL throttling or killing the session.

      * SQL Throttling

         After locating the problem SQL, you can limit the execution frequency of SQL through SQL throttling.

         Operation path:

         1. Create [Throttling SQL](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql) task.

         2. In the Create SQL Throttling Task window, enter the problem SQL, adjust the maximum concurrency number (when the maximum concurrency number is 0, this SQL will be completely blocked), click **Keyword Generation and Verification** to split keywords. Keywords will be separated by wavy lines (~).

            <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_efff8cecb7a4a37b01115c0c2c430920.png) </span>

         3. Click **OK** to submit the task.

            <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="4">tip            </div>
            

            <div data-tips="true" data-tips-type="tip" data-wrapper-indent="4">For more detailed information, please see <a href="https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql">Throttling SQL</a>.            </div>
            

      * KILL Session

         1. Log in to [Database Workbench](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Session**.

         2. In the **Real\-Time conversation** area, pay attention to the **Time** and **State** of the session. If the State of a certain session is updating, but the value of Time is already very large, then attention needs to be paid to processing.


<span id="many-scanned-rows"></span>
#### Many scanned rows


* **Cause analysis**

   The number of logical reads is generally positively correlated with CPU consumption. If the number of logical reads increases, it can basically be confirmed that the increase in CPU usage rate is related to SQL rather than a change in the database environment. You can confirm the correlation between the number of read rows and CPU usage rate by viewing the following monitoring items.

   * InnoDB Read Volume

   * Average number of times InnoDB reads pages from BufferPool per second (logical read).

   Operation path: **Login** [Database Workbench](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Performance monitoring**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_2f09194172aeaa4076ecc1434cd3088a.png) </span>

* **Solution**

   * Execute the `show processlist` command, or determine which SQL causes the increase in CPU load through the [Slow log analysis](https://docs.byteplus.com/en/docs/DBW/slow-log-management-for-mysql) of the database workbench, and solve it by killing SQL or [Throttling SQL](https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql). The way to kill SQL is as follows:

      1. View the running transactions to see if there are long\-running SQL.

         ```sql
         mysql> select * from information_schema.innodb_trx \G;
         *************************** 1. row ***************************
                         trx_id: 1335
                      trx_state: LOCK WAIT
                    trx_started: 2023-12-28 17:36:35
              trx_requested_lock_id: 1335:25:3:2
               trx_wait_started: 2023-12-28 17:45:31
                     trx_weight: 2
            trx_mysql_thread_id: 7432 # The same value as the ID in processlist
                      trx_query: update t1 set c2 = c2 + 200 where c1 = 1
            trx_operation_state: starting index read
              trx_tables_in_use: 1
              trx_tables_locked: 1
               trx_lock_structs: 2
          trx_lock_memory_bytes: 1160
                trx_rows_locked: 3
              trx_rows_modified: 0
         trx_concurrency_tickets: 0
            trx_isolation_level: REPEATABLE READ
              trx_unique_checks: 1
         trx_foreign_key_checks: 1
         trx_last_foreign_key_error: NULL
          trx_adaptive_hash_latched: 0
          trx_adaptive_hash_timeout: 0
               trx_is_read_only: 0
         trx_autocommit_non_locking: 0
         ```
         

      2. Execute the KILL command to prevent this SQL from continuing to consume CPU. The ID used is the ID in processlist.

         ```sql
         mysql> KILL 7432  -- from processlist
         ```
         

   * Optimize SQL to reduce logical reads. For SQL with too many scanned rows but difficult to optimize, you can add an index to improve filtering.


<span id="wrong-execution-plan"></span>
#### Wrong execution plan

There are two reasons for wrong execution plans. One is lagging statistical data, and the other is an optimizer problem.


* Lagging Statistical Data

   * **Cause analysis**

      MySQL will automatically update table statistics to help the optimizer choose a suitable access path. If the statistical information is inaccurate, the judgment of the optimizer may be affected. For example, if the actual number of rows is much larger than the number of rows in the statistical information, the optimizer may think that **full table scan efficiency** is higher, resulting in a wrong execution plan and scanning too many rows, leading to an increase in CPU usage rate. Execute the following command to view statistical information to determine whether statistical data is lagging.

      ```sql
      select * from innodb_table_stats where database_name='' and table_name='';
      ```
      

   * **Solution**

      Do not rely on MySQL's mechanism of regularly updating statistical information. Evaluate statistical data for large tables that are frequently modified. You can view the `last_update` field of `mysql.innodb_table_stats`. Pay special attention to statistical data that has not been changed for a long time and manually update statistical information by `analyze table` during off\-peak periods.

* Optimizer Problem

   * **Cause analysis**

      Using `order by limit` may cause the optimizer to misjudge and use full table scan.

   * **Solution**

      * View the optimizer parameter `select @@optimizer_switch\G`, try to turn off the problem optimizer parameter, such as `prefer_ordering_index`.

      * Use `FORCE INDEX` to specify an index.


<span id="abnormal-connection-thread-pool"></span>
### Abnormal connection thread pool


* **Cause analysis**


If the configured concurrency exceeds the reasonable value for the current configuration, it leads to a high number of active threads in MySQL. When concurrency increases, MySQL may experience "congestion" due to excessive active threads, resulting in an increase in CPU usage rate. You can confirm the correlation between the number of read rows and CPU usage rate by checking the monitoring item "Number of Running Threads".

Operation path: Log in [Database Workbench](https://console.byteplus.com/dbw) \> **Observation diagnosis** \> **Performance monitoring** \> **threads_running**.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cd68b594bd870e79ad3c94d4010a8a8d.png) </span>


* **Solution**

   * Control the concurrency at the server layer and pay attention to the value of `thread_pool_size` \* `thread_pool_oversubscribe`. The product of these two parameters is the maximum allowed number of active threads. As a rule of thumb, it should not exceed 2\-3 times the number of CPU cores.

   * Control the concurrency at the InnoDB layer by configuring `innodb_thread_concurrency`.

   * Upgrade the kernel version in a timely manner. If necessary, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support for an upgrade.


<span id="isolation-level"></span>
### Isolation level


* **Cause analysis**


The default isolation level of RDS for MySQL is Read\-Committed (RC), but users are allowed to set it to Repeatable\-Read (RR). At the RR level, there may be issues of increased CPU usage rate that do not occur at the RC isolation level.


* **Solution**

   * Confirm whether RR is the required isolation level. If not, it can be adjusted to RC.

   * If the long historical linked list causes an increase in the scan volume, you can configure auto kill to kill SQL with excessively long execution time.


<span id="upgrade-instance-specification"></span>
### Upgrade instance specification

After troubleshooting and resolving through the above methods, if the CPU usage rate continues to increase, it may be a normal situation caused by business pressure. At this time, you can consider upgrading the instance specification through regular resizing or temporary upgrading. Increasing the number of CPU cores can reduce instance pressure.

For information on how to perform regular resizing or temporary upgrading of an instance, please refer to the following documents:


* [Standard instance specification modification](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification)

* [Temporary instance specification upgrade](https://docs.byteplus.com/en/docs/RDS_for_MySQL/temporary_instance_specification_upgrade)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Temporary upgrading is currently an invitation test function of RDS for MySQL. If you need to use it, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> to apply.</div>
