---
title: "Database inspection management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql"
---

DBW provides a database inspection feature that performs regular automated health checks and risk assessments on database instances, helping you understand their operational status. This topic describes how to enable database inspection and view database inspection reports.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance has been created and is in the Running state. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If the target instance has turned on security control, then you need to apply for the operation read\-only or operation read\-write permission of the target instance for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you use the database inspection feature, do not change the configurations of the instance. Otherwise, the database inspection feature can not be used to check and evaluate the instance.

* In the inspection record list, DBW retains the inspection records and reports for the past 30 days, and the expired reports will be automatically deleted Download the inspection report in time.


<span id="KkGJjV0G"></span>
## Inspection scoring rules


* The weight proportion of the database inspection is shown in the following table

   
   |**Weight value** |**Proportion** |
   |---|---|
   |High |15% |
   |Medium |10% |
   |Low |5% |
   |Ignore |0 |
   

* The scoring rules of database inspection are shown in the following table

   
   |**Deduction items** |**Rule** |**Calculation method** |
   |---|---|---|
   |CPU usage |Deduct points based on average CPU usage. |* No points are deducted when the average CPU usage is less than 70%.<br><br>* When the average CPU usage is greater than or equal to 70%, the deduction calculation method is as follows:<br><br>   1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>   2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * CPU usage weight ratio / Sum of all weight ratios * 90`. |
   |Memory usage |Deduct points based on the average memory usage. |* No points are deducted when the average memory usage is < 70%.<br><br>* When the average memory usage is \>= 70%. The score deduction calculation method is as follows.<br><br>   1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>   2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Memory usage weight ratio / Sum of all weight ratios * 90`. |
   |Connection usage |Deduct points based on the average connection usage. |* No points are deducted when the average connections are less than 70%.<br><br>* When the average connection usage is greater than or equal to 70%, the deduction calculation method is as follows:<br><br>   1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>   2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Connection usage weight ratio / Sum of all weight ratios * 90`. |
   |Slow log |Deduct points based on the number of slow logs per 24 hours. |* When the number of slow logs is equal to 0, no points will be deducted.<br><br>* When the number of slow logs is greater than 0, the score deduction is calculated as follows.<br><br>   1. Deduct points based on the number of slow logs.<br><br>      * When 0 < number of slow logs < 50, deduct 1 point, that is, `score = 1`.<br><br>      * When the number of slow logs \>= 50, the score deduction formula is `score = int(min(number/50, 10))`.<br><br>   2. Use a weighted value to calculate the final score deduction. The formula is: Final score deduction = `score / 10 * Slow log weight ratio / Sum of all weight ratios * 90`. |
   |Disk usage |Deduct points based on the estimated number of days of remaining disk usage. |* Deduct points based on available days.<br><br>   * No points are deducted if available days \>= 15.<br><br>   * If available days < 15, the score deduction calculation method is as follows:<br><br>      1. Use the formula `score = int(15 - days/3 )` to calculate the deduction score.<br><br>      2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Disk usage weight ratio / Sum of all weight ratios * 90`.<br><br>* Calculate deductions based on usage<br><br>   * No points are deducted when the average disk usage is less than 70%.<br><br>   * When the average disk usage is greater than or equal to 70%, the deduction calculation method is as follows:<br><br>      1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>      2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Disk usage weight ratio / Sum of all weight ratios * 90`.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When calculating the final score of the statistical disk usage, deduct the higher score of the two deduction methods.</div><br> |
   

* The following uses CPU usage as an example to describe the calculation process of the inspection score.

   1. In the inspection weight settings, set the weight of CPU usage to **High** (15%), and the weight of the other four deduction items to **Medium** (10%).

   2. Assume that the CPU usage of the current instance is 80%. The calculation formula of the deduction score for CPU usage is as follows.

      score = min ((80 \- 70) \* 40 /100, 10) = 4

   3. Use weighted values to calculate the final deduction score using the following formula.

      Final deduction = 4 / 10 \* 15% / (15% + 10% + 10% + 10% + 10%) \* 90 = 9.7

   4. Formula for calculating the final inspection score of an instance: `Inspection score = 100 - (Sum of deductions for each deduction item)`.


<span id=".5byA5ZCv5pWw5o2u5bqT5beh5qOA"></span>
## Set inspection weight

By default, DBW sets the weight of each score deduction item of all instance nodes to Medium. It also supports modifying the weight of each score deduction item based on business requirements.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. The following shows how to set the database inspection weight:

   * Set an inspection weight for a single instance

      1. On the left navigation bar, click **Instance list**.

      2. On the **Instance list** page, click **Inspection weight settings** in the **Actions** column of the target instance

      3. In the **Inspection weight settings** window, you can set the weight of each deduction item for each node. See [Scoring rules](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql#KkGJjV0G) for weight level definitions.

         
         |**Deduction items** |**Default value** |**Description** |
         |---|---|---|
         |Slow SQL |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |CPU usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Memory usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Disk usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Connection usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         

      4. Click **OK**.

   * Set inspection weights in batches for instances of the same type

      1. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

      2. On the top menu bar, select the database type **RDS for MySQL**.

      3. On the **Database inspection records** page, click **Inspection records**.

      4. On the **Inspection records** tab, click **Weighted scoring configuration**.

      5. In the **Weighted scoring configuration** dialog box, set the weight of each deduction item in batches for the current type of database instance.

         
         |**Settings** |**Default value** |**Target value** |
         |---|---|---|
         |Slow SQL |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |CPU usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Memory usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Disk usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Connection usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
         |Coverage policy |Only cover instances consistent with the default value |* Only cover instances with the same default values: The inspection weight set here only applies to instances with the default inspection weight, and does not apply to instances with the custom inspection weight.<br><br>* Cover all instances: The inspection weight set here applies to all instances of the current type of database. |
         

      6. Click **OK**.


<span id=".5byA5ZCv5pWw5o2u5bqT5beh5qOA"></span>
## Enable database inspection


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. To enable database inspection, perform the following steps:

   * Enable automatic inspection

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The automatic inspection period defaults to 00:00:00 to 23:59:59 of the previous day, and an inspection is automatically performed once a day.      </div>
      

      * Enable automatic inspection for a single instance

         1. On the left navigation bar, click **Instance list**.

         2. On the **Instance list** page, click the pen icon in the **Automatic inspection** column of the target instance.

         3. In the **Automatic inspection settings** dialog box, enable automatic inspection and set the period during which the inspection starts to be performed.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bb49dd94104ea1772b61472ed0e8d4d3.png) </span>

         4. Click **OK**.

      * Batch enable instance automatic inspection

         1. On the left navigation bar, click **Instance list**.

         2. On the **Instance list** page, check the instances for which you want to enable automatic inspection, and click **Automatic inspection settings**.

         3. In the **Automatic inspection settings** dialog box, enable automatic inspection and set the period during which the inspection starts to be performed.

            <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c434f769ef01329477eb63e9d9ddbf71.png) </span>

         4. Click **OK**.

   * Enable manual inspection

      1. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

      2. On the **Inspection report** or **Inspection records** tab, click **Initiate manual inspection**.

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5744b2d343dec95bbe259b70714d4c09.png) </span>

      3. In the **Manual inspection** dialog box, locate the **Select instance to be inspected:**  area, check the instances you want to inspect manually, and set the time period for the database instances to be inspected.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">The inspection time can not be later than the current time, and the interval between the inspection start time and the inspection end time ranges from 1 to 24 hours.         </div>
         

      4. Click **OK**.


<span id=".5p-l55yL5beh5qOA5oql5ZGK"></span>
## View inspection records

The inspection report supports filtering and viewing by instance name, instance ID, and time range.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

4. On the top menu bar, select the database type **RDS for MySQL**.

5. On the **Database inspection records** page, view the following information.

   
   |Actions |Description |
   |---|---|
   |View inspection report information |Click **Inspection report**. On the **Inspection report** tab, you can view the **Total number of inspections for the day**, **Instances with a score of 100**, **Instances with scores between 99 and 80**, **Instances with scores between 79 and 60**, and **Instances with scores below 60** for a specified date **.**  |
   |View inspection record information |Click **Inspection records**. On the **Inspection records** tab, you can view all automatic and manual inspection records **.**  You can use the search function to filter the inspection records you want to find. |
   |View basic inspection information |On the **Inspection report** or **Inspection records** tab, you can view all automatic and manual inspection records, including the inspection execution time, task status, inspection type, inspection period, instance ID/name, health score, CPU usage, memory usage, disk usage, connection usage, QPS, TPS, and the Slow SQL number.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Health score: The system deducts points based on the scoring rules. For details, refer to <a href="https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql#KkGJjV0G">Scoring rules</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">CPU usage: Indicates the average ratio of CPU usage time to total time within the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Memory usage: Indicates the average ratio of used memory to total memory during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disk usage: Indicates the average ratio of occupied disk space to total disk space during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Connection usage: Indicates the average ratio of used connections to available connections during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">QPS: Indicates the average QPS during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TPS: Indicates the average number of query requests processed per second during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Slow SQL number: Indicates the average number of slow SQL queries during the inspection period.</div><br> |
   |View the inspection report |Refer to [Viewing inspection reports](https://docs.byteplus.com/en/docs/DBW/database-inspection-management-for-mysql#kN3L2i8A). |
   


<span id="kN3L2i8A"></span>
## View the inspection report


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

4. On the top menu bar, select the database type **RDS for MySQL**.

5. On the **Inspection report** or **Inspection records** tab, select the target record and click **View report** in the Actions column. On the **Inspection report details** control panel, you can view the inspection results of the instance or node. In the upper\-right corner of the Inspection report details control panel, click **Download report** to download the inspection report to your computer in PDF format.



|**Parameter** |**Description** ||
|---|---|---|
|**Instance score summary** |Aggregates the scores for instances and each node within the instances. ||
|**Select instance/node** |DBW allows you to view inspection reports from the perspective of instances or nodes.<br><br><br>* Click **Instance** to view the resource usage of each node within the instance.<br><br>* Click **Node** and select the node you want to view from the drop\-down list to view the resource usage of a node within the instance. ||
|**Basic information** |On the **Basic information** pane, you can view the basic information of the current instance, including **Instance ID**, **Instance specification**, and **Database version**. ||
|**Health score** |Health score of the current node. ||
|**Deduction details** |Deduction details of the current node. ||
|**Resource usage**<br><br> |**Top 10 CPU usage (%)**  |CPU usage indicates the CPU resources consumed by the database server when processing requests. You can effectively manage and reduce CPU usage by monitoring and optimizing, thereby improving the overall performance and response speed of the database. |
||**Top 10 memory usage (%)**  |The memory usage indicates the extent to which the database memory is used within a specified period. You can ensure the stability and good performance of the database system in a high\-concurrency environment through effective monitoring and optimization strategies. Adjusting the buffer pool, optimizing queries and table structures, reasonably configuring query caches, and increasing hardware resources are all effective means of optimizing memory usage. Continuously monitoring memory usage and making optimization adjustments based on the actual situation are key to ensuring the stable and efficient operation of the database system. |
||**TOP 10 average disk usage (%)**  |Average disk usage refers to the average ratio between the occupied disk space and the total disk space during the inspection period.<br><br>You can effectively manage and reduce the average disk usage through monitoring, optimization, and capacity expansion to improve the overall performance and response speed of the database. |
||**Top 10 slow SQLs** |Slow SQL refers to SQL queries whose execution time exceeds the expected or set threshold. It is used to evaluate the health and overall efficiency of the database. You can continuously monitor and analyze slow queries to identify and resolve potential performance bottlenecks, ensuring the system responds quickly and provides a high\-quality user experience even under high loads. |
||**TOP 10 open connections** |The current open connections indicate the number of database connections currently in use on each node. You can effectively manage the number of connections by using connection pools to optimize application connection management, reasonably adjusting database configuration parameters, continuously monitoring system operating conditions, and implementing load\-sharing strategies, ensuring that the database maintains performance and stability in high\-concurrency environments. This not only improves the response speed of the system to meet business needs but also prevents service interruptions due to resource bottlenecks. |
||**Connection usage** |Connection usage indicates the percentage of the current database connections used relative to the maximum number of connections configured. You can effectively control connection usage and ensure the database maintains performance and stability in high\-concurrency environments through strategies such as reasonable connection management, application optimization, database configuration adjustments, monitoring, and load balancing. Monitoring the connection usage rate helps to identify potential resource bottlenecks in a timely manner, prevent performance problems caused by resource exhaustion, and provide a reference basis for system expansion. |
||**TOP 10 QPS**<br><br> |QPS indicates the number of queries executed per second. You can improve the query processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing queries and indexes, increasing cache, implementing read\-write separation, upgrading hardware, and using connection pools can effectively improve QPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as QPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
||**TOP 10 TPS** |TPS represents the number of transactions processed per second. You can improve the transaction processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing transaction management, adjusting cache parameters, implementing read\-write separation, optimizing hardware, and using connection pools can effectively improve TPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as TPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
|**Top 10 slow SQL** |On the **TOP 10 slow SQL** pane, you can view the information of each SQL template, including the SQL template's **Database**, **Execution User**, **Execution time(s)** , **Total time**, **Average execution time(s)** , **Maximum execution time(s)** , **Average lock wait time(s)** , and **Average rows scanned**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Total time</strong>: Indicates the time to execute the statement.</div><br><br><br>* <div data-tips="true" data-tips-type="default">All SQL commands that meet the template are aggregated within each SQL template.</div><br> ||
|**TOP SQL (based on aggregation sessions)**  |On the **Top SQL (based on aggregation sessions)**  pane, you can view the information for each Top SQL, including **SQL template**, **Execution time(s)** , **Average execution time(s)** , **Maximum execution time(s)** , and **Total execution time(s)** . ||
|**Top SQL (based on full SQL insights)**  |On the **Top SQL (based on full SQL insights)**  pane, you can view the information of each Top SQL, including **Average SQL execution time**, **SQL time**, **SQL template**, **SQL type**, **Database name**, **Table name**, **Total SQL execution time**, **Execution time(s)** , **Average CPU time**, **Average innoDB lock wait time**, **Average MDL lock wait time**, **Average Latch wait time**, **Average transaction submit time**, **Average SQL throttling wait time**, **Average socket send time**, **Average thread scheduling wait time**, **Average thread wait time**, **Average rows affected**, **Average rows scanned**, **Average rows returned**, **Average bytes sent**, **Average logical page reads**, **AverageIOread bytes**, **Average number of pages read by IO**, **Average number of disk temporary tables**.<br><br>Click the **Favorite** icon in the Actions column to favorite SQL information. ||
|**Top tables (based on space analysis)**  |On the **Top tables (based on space analysis)**  pane, you can view the information of each TOP table, including **Table name**, **Database name**, **Storage engine**, **Tablespace**, **Tablespace ratio**, **Data space**, **Index space**, **Fragmentation ratio**, **Number of table rows**, **Average rows**, and **Auto\-increment** **ID value**. ||
|**TOP 10 auto\-increment column usage** |On the **TOP10 auto\-increment column usage** pane, you can view the information of each TOP auto\-increment column, including **Column name**, **Table name**, **Database name**, **Data type**, **Maximum value of data type**, **Current auto\-increment value**, and **Auto\-increment column ratio**. ||
