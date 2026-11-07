---
title: "Database inspection management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Database_inspection_management"
---

The Database Workshop (DBW) provides a database inspection feature that can periodically and automatically perform health checks and risk assessments on database instances, helping you understand the operational status of your database instances. This topic explains how to enable database inspection and view database inspection reports.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A NDB for MySQL instance and account has been created, and the instance status is running. For detailed operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts#.5Yib5bu66LSm5Y-3).

* If the target instance has security control enabled, you need to apply for read\-only or read\-write operation permissions for the target instance for the current account. For more information, refer to  [Enabling instance security controls (NDB for MySQL)](https://bytedance.larkoffice.com/6956/1262771), and [Applying for operation permissions (NDB for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

During the use of the database inspection feature, do not modify the instance's configurations, as this may prevent the database inspection feature from properly checking and evaluating the instance.

<span id="b47xpQ8N"></span>
## Inspection scoring rules


* The weight distribution for database inspection is as shown in the table below.

   
   |**Weight value** |**Proportion explanation** |
   |---|---|
   |High |15% |
   |Medium |10% |
   |Low |5% |
   |Ignore |0 |
   

* The scoring rules for database inspection are as shown in the table below.

   
   |**Deduction item** |**Rule** |**Calculation method** |
   |---|---|---|
   |CPU usage rate |Deduct points based on the average CPU usage rate.<br><br> |* No points are deducted when the average CPU usage is < 70%.<br><br>* When the average CPU usage is \>= 70%, the deduction calculation method is as follows.<br><br>   1. Use the formula `score = min ((utilization rate-70)*40/100, 10)` to calculate the deduction score.<br><br>   2. Use weighted values to calculate the final deduction score with the formula: `final deduction = score / 10 * CPU utilization weight ratio / sum of all weight ratios * 90`. |
   |Memory usage rate |Points are deducted based on the average memory usage. |* No points are deducted when the average memory usage is less than 70%.<br><br>* When the average memory usage is \>= 70%. The deduction calculation method is as follows.<br><br>   1. Use the formula `score = min ((usage rate-70)*40/100, 10)` to calculate the deduction score.<br><br>   2. Use weighted values to calculate the final deduction score with the formula: `final deduction = score / 10 * memory usage weight ratio / sum of all weight ratios * 90`. |
   |Connection usage rate |Deductions are based on the average connection usage rate. |* No deduction when the average connection usage rate is < 70%.<br><br>* When the average connection usage rate \>= 70%, the deduction is calculated as follows.<br><br>   1. Use the formula `score = min ((usage rate-70)*40/100, 10)` to calculate the deduction score.<br><br>   2. Use weighted values to calculate the final deduction score with the formula: `Final deduction = score / 10 * connection usage rate weight ratio / sum of all weight ratios * 90`. |
   |Slow logs |Deductions are based on the number of slow logs every 24 hours. |* No points are deducted when the number of slow logs equals 0.<br><br>* When the number of slow logs is greater than 0, the deduction is calculated as follows.<br><br>   1. Calculate the deduction score based on the number of slow logs.<br><br>      * When 0 < number of slow logs < 50, deduct 1 point, i.e., s`core = 1`.<br><br>      * When the number of slow logs \>= 50, the deduction formula is `score = int(min(quantity/50, 10))`.<br><br>   2. The final deduction score is calculated using a weighted value, with the formula: Final deduction = `score / 10 * slow log weight ratio / sum of all weight ratios * 90`. |
   |Disk usage |Deduct points based on the estimated remaining disk usage days. |* Calculate deductions based on available days<br><br>   * No deduction if available days \>= 15.<br><br>   * When available days < 15, the deduction is calculated as follows.<br><br>      1. Use the formula `score = int(15 - days/3)` to calculate the deduction score.<br><br>      2. Use weighted values to calculate the final deduction score with the formula: `Final deduction = score / 10 * disk usage weight ratio / sum of all weight ratios * 90`.<br><br>* Calculate deductions based on usage rate<br><br>   * No deduction if average disk usage rate < 70%.<br><br>   * When average disk usage rate \>= 70%, the deduction is calculated as follows.<br><br>      1. Use the formula `score = min ((usage rate-70)*40/100, 10)` to calculate the deduction score.<br><br>      2. Use weighted values to calculate the final deduction score with the formula: `Final deduction = score / 10 * disk usage weight ratio / sum of all weight ratios * 90`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When calculating the final score for disk usage rate, deduct points based on the higher score between the two deduction methods.</div><br> |
   

* Taking CPU usage as an example, the calculation process for the inspection score is explained.

   1. In the inspection weight settings, the weight for CPU usage is set to **high** (15%), while the weights for the other 4 deduction items are set to **medium** (10%).

   2. Assuming the current instance has a CPU usage of 80%, the deduction score for CPU usage is calculated as follows.

      score = min ((80 \- 70) \* 40 /100, 10) = 4

   3. The final deduction score is calculated using weighted values, as shown in the formula below.

      Final Deduction = 4 / 10 \* 15% / (15% + 10% + 10% + 10% + 10%) \* 90 = 9.7

   4. The final inspection score for the instance is calculated as: `Inspection Score = 100 - (Sum of all deduction scores)`.


<span id=".5byA5ZCv5pWw5o2u5bqT5beh5qOA"></span>
## Set inspection weight

DBW defaults the weight of each deduction item for all instance nodes to medium, while also supporting the modification of each deduction item's weight based on business requirements.


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select a region.

3. Set the database inspection weight as follows:

   * Set Inspection Weight for a Single Instance

      1. In the left navigation bar, click **Instance list**.

      2. On the **Instance list** page, click **Inspection weight settings** under the **Actions** column of the target instance.

      3. In the **Inspection weight settings** window, you can set the weight for each deduction item for each node. For the definition of weight levels, refer to [Scoring rules](https://docs.byteplus.com/en/docs/DBW/Database_inspection_management#b47xpQ8N).

         
         |**Deduction items** |**Default value** |**Description** |
         |---|---|---|
         |Slow SQL |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |CPU usage |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |Memory usage |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |Disk usage |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |Connection usage rate |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         

      4. Click **OK**.

   * Batch set inspection weights for instances of the same type

      5. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

      6. On the top menu bar, select the database type **RDS for MySQL**.

      7. On the **Database inspection records** page, click **Inspection records**.

      8. On the **Inspection records** tab, click **Scoring weight settings**.

      9. In the **Scoring weight settings** pop\-up, batch set the weight for each deduction item for the current type of database instance.

         
         |**Setting item** |**Default value** |**Target value** |
         |---|---|---|
         |Slow SQL |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |CPU usage |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |Memory usage |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |Disk usage |Middle |Select High, Medium, Low, or Ignore from the dropdown. |
         |Connection usage rate |Medium |Select High, Medium, Low, or Ignore from the dropdown. |
         |Coverage policy |Only cover instances consistent with the default values. |* Only cover instances consistent with default values: The inspection weight set here only applies to instances with default inspection weights and does not affect instances with custom inspection weights.<br><br>* Cover all instances: The inspection weight set here applies to all instances of the current database type. |
         

      10. Click **OK**.


<span id=".5byA5ZCv5pWw5o2u5bqT5beh5qOA"></span>
## Enable database inspection

Enable database inspection. The specific steps are as follows:


* Enable automatic inspection

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The default automatic inspection period is from <code>00:00:00 to 23:59:59</code> of the previous day, and it will be executed once daily.   </div>
   

   * Enable Automatic Inspection for a Single Instance

      1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

      2. On the left navigation bar, click **Instance list**.

      3. On the top menu bar, select the project and region.

      4. In the top\-left corner of the **Instance list** page, select the database type as **veDB** **for** **MySQL.** 

      5. On the **Instance list** page, click the pencil icon in the **Automatic inspection** column of the target instance.

      6. In the **Auto inspection settings** dialog box, enable auto inspection and set the time period for inspection to start.

      7. Click **OK**.

   * Enable auto inspection for multiple instances in bulk

      1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

      2. On the left navigation bar, click **Instance list**.

      3. On the top menu bar, select the project and region.

      4. In the top\-left corner of the **Instance list** page, select the database type as **veDB** **for MySQL.** 

      5. On the **Instance list** page, check the instances that need auto inspection enabled, and click **Automatic inspection settings**.

      6. In the **Automatic inspection settings** dialog box, enable automatic inspection and set the time period for the inspection to start.

      7. Click **OK**.

* Enable Manual Inspection

   1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

   2. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

   3. On the top menu bar, select the project and region.

   4. In the top\-left corner of the **Database inspection records** page, select the database type as **NDB** **for MySQL.** 

   5. On the **Inspection summary** or **Inspection records** tab, click **Initiate manual inspection**.

      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9e807efd4687ce0df3415236f229fd4a.png) </span>

   6. In the **Manual inspection** dialog box, select the instances to be manually inspected in the **Select instances for inspection** section, and set the time period for the database instance inspection.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">The inspection time cannot be later than the current time, and the interval between the inspection start time and end time must be between 1 to 24 hours.      </div>
      

   7. Click **OK**.


<span id=".5p-l55yL5beh5qOA5oql5ZGK"></span>
## View Inspection Records


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

3. On the top menu bar, select the region.

4. In the top\-left corner of the **Database inspection records** page, select the database type as **NDB** **for MySQL.** 

5. On the **Database inspection records** page, view the following information.



|Operation |Description |
|---|---|
|View inspection summary information |Click **Inspection summary**, and on the **Inspection summary** tab, you can view the **Total number of inspections for the day**, **Instances with a score of 100**, **Instances with a Score of 99\-80**, **Instances with a score of 79\-60**, and **Instances with a score below 60** for the specified date **.**  |
|View inspection record information |Click **Inspection records** to view all automatic and manual inspection records under the **Inspection records** tab **.**  You can use the search function to filter the inspection records you want to find. |
|View inspection basic information |On the **Inspection summary** or **Inspection record** tabs, you can view all automatic and manual inspection records, including inspection execution time, task status, inspection type, inspection period, instance ID/name, health score, CPU usage, memory usage, disk usage, connection usage, QPS, TPS, and slow SQL count.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Health Score: The system deducts points based on scoring rules. For more details, refer to <a href="https://docs.byteplus.com/en/docs/DBW/Database_inspection_management#b47xpQ8N">Scoring rules</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">CPU Usage: Represents the average ratio of CPU used time to total time during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Memory Usage: Represents the average ratio of used memory to total memory during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Disk Usage: Represents the average ratio of occupied disk space to total disk space during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Connection utilization rate: Represents the average ratio of used connections to available connections during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">QPS: Represents the average QPS during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">TPS: Represents the average number of query requests processed per second during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Slow SQL count: Represents the average number of slow SQLs during the inspection period.</div><br> |
|View inspection report |Refer to [View inspection report](https://docs.byteplus.com/en/docs/DBW/Database_inspection_management#EKQ3lxWy). |


<span id="EKQ3lxWy"></span>
## View the inspection report


1. Log on to the [DBW Console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

4. On the top menu bar, select the database type as **RDS for MySQL**.

5. On the **Inspection summary** or **Inspection records** tab, select the target record and click **View report** in the Actions column. On the **Inspection report details** control panel, you can view the inspection results of the instance or node. Also, in the top right corner of the inspection report details control panel, click **Download report** to download the inspection report in PDF format for local viewing.

   
   |**Parameter** |**Description** ||
   |---|---|---|
   |**Instance score summary** |Summarizes the scores of instances and each node within the instances. ||
   |**Select instance/Node** |DBW supports viewing inspection reports from the instance or node level.<br><br><br>* Click **Instance** to view the resource usage of each node within the instance.<br><br>* Click **Node** and select the node to view from the dropdown to see the resource usage of a specific node within the instance. ||
   |**Basic information** |In the **Basic information** section, you can view the basic information of the current instance, including **Instance ID**, **Instance specification**, and **Database version**. ||
   |**Health score** |Health score for the current node. ||
   |**Deduction details** |Deduction details for the current node. ||
   |**Resource usage**<br><br> |**TOP 10 CPU usage (%)**  |CPU usage rate indicates the CPU resources consumed by the database server while processing requests. You can effectively manage and reduce CPU usage by monitoring and optimizing, improving the overall performance and response speed of the database. |
   ||**TOP 10 memory usage (%)**  |Memory usage indicates the extent to which the database's memory is utilized during the specified time period. Through effective monitoring and optimization strategies, you can ensure the stability and good performance of the database system in high\-concurrency environments. Adjusting the buffer pool, optimizing queries and table structures, properly configuring query caching, and increasing hardware resources are all effective methods for optimizing memory usage. Continuous monitoring of memory usage and optimization adjustments based on actual conditions are key to ensuring the stable and efficient operation of the database system. |
   ||**TOP 10 average disk usage (%)**  |The average disk usage represents the average ratio of occupied disk space to total disk space during the inspection period.<br><br>You can effectively manage and reduce the average disk usage rate through monitoring, optimization, and scaling, improving the overall performance and response speed of the database. |
   ||**TOP 10 slow SQL count** |Slow SQL refers to SQL queries that exceed the expected or set execution time threshold, used to evaluate the health and overall efficiency of the database. By continuously monitoring and analyzing slow queries, you can identify and resolve potential performance bottlenecks, ensuring the system can respond quickly even under high load, providing a superior user experience. |
   ||**TOP 10 current open connections** |The current number of open connections represents the number of database connections in use on each node. You can effectively manage the number of connections by optimizing application connection management with connection pools, adjusting database configuration parameters appropriately, continuously monitoring system health and load distribution strategies, ensuring database performance and stability in high\-concurrency environments. This not only improves the system's response speed to meet business needs but also prevents service interruptions caused by resource bottlenecks. |
   ||**Connection usage rate** |Connection usage rate indicates the proportion of connections currently used by the database relative to the configured maximum number of connections. You can effectively control the connection usage rate through strategies such as proper connection management, application optimization, database configuration adjustments, monitoring, and load balancing, ensuring the database maintains performance and stability under high concurrency. Monitoring the connection usage rate helps identify potential resource bottlenecks in time, prevent performance issues caused by resource exhaustion, and provides a reference for system scaling. |
   ||**TOP 10 QPS**<br><br> |QPS represents the number of queries executed per second. By implementing reasonable monitoring and optimization strategies, you can enhance the database's query processing capabilities, ensuring the system maintains performance and stability under high concurrency. Optimizing queries and indexes, increasing caching, implementing read\-write separation, upgrading hardware, and using connection pools can all effectively improve QPS and enhance the overall performance of the database. Continuously monitoring performance metrics such as QPS helps in timely identification and resolution of potential performance bottlenecks, ensuring smooth business operations. |
   ||**TOP 10 TPS** |TPS represents the number of transactions processed per second. Through reasonable monitoring and optimization strategies, you can enhance the transaction processing capability of the database, ensuring system performance and stability under high concurrency. Measures such as optimizing transaction management, adjusting cache parameters, implementing read\-write separation, optimizing hardware, and using connection pools can effectively improve TPS and enhance the overall performance of the database. Continuous monitoring of performance metrics like TPS helps to promptly identify and resolve potential performance bottlenecks, ensuring smooth business operations. |
   |**TOP 10 slow SQL** |In the **TOP 10 slow SQL** list area, you can view information for each SQL template, including the **Database, Executing user, Execution count, Total execution time, Average execution time (s), Maximum execution time (s), Average lock wait time (s)** , and **Average rows scanned**.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default"><strong>Total execution time</strong>: Represents the time taken to execute the statement.</div><br><br><br>* <div data-tips="true" data-tips-type="default">All SQL commands matching the template are aggregated within each SQL template.</div><br> ||
   |**TOP SQL (Based on aggregated sessions)**  |In the **TOP SQL (based on aggregated sessions)**  list area, you can view information for each TOP SQL, including **SQL template**, **execution count**, **Average execution duration (s)** , **Maximum execution duration (s)** , and **Total execution duration (s)** . ||
   |**TOP SQL (based on full SQL insights)**  |**In the TOP SQL (Based on full SQL insights)**  list area, you can view information for each TOP SQL, including **Average SQL execution time**, **SQL execution time**, **SQL template**, **SQL type**, **Database name**, **Table name**, **Total SQL execution time**, **Execution count**, **Average CPU time**, **Average InnoDB lock wait time**, **Average MDL lock wait time**, **Average latch wait time**, **Average transaction commit time**, **Average SQL throttle wait time**, **Average socket send data time**, **Average thread scheduling wait time**, **Average thread wait time**, **Average affected rows**, **Average scanned rows**, **Average returned rows**, **Average sent bytes**, **Average logical page reads**, **Average** **IO** **read bytes**, **Average IO read pages**, **Average disk temporary table count**.<br><br>Click the **Favorite** icon in the operation column to save the SQL information. ||
   |**TOP Tables (Based on Space Analysis)**  |**In the TOP table (based on space analysis)**  list area, you can view information for each TOP table, including **Table name**, **Database name**, **Storage engine**, **Table space**, **Table space ratio**, **Data space**, **Index space**, **Fragmentation rate**, **table row count**, **average row count**, and **auto\-increment** **ID** **Value**. ||
   |**TOP 10 auto\-increment column usage** |**In the TOP 10 auto\-increment column usage** list area, you can view information for each TOP auto\-increment column, including **Column name**, **Table name**, **Database name**, **Data type**, **Data type maximum value**, **Current value of auto\-increment column**, and **Auto\-increment column ratio**. ||
