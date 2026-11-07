---
title: "One-click diagnosis management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/one-click-diagnostics-management-for-mysql"
---

Database Workshop (DBW) provides a one\-click diagnosis feature that allows you to intuitively view the overall performance of your database and quickly confirm whether there are any anomalies in the instance. This topic describes how to manage one\-click diagnosis.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL has been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* When you use the one\-click diagnosis feature, do not change the configurations of the instance. Otherwise, you will not be able to view the database performance using the one\-click diagnosis feature.

* The deduction rules are as follows.

   * The weight ratio of inspection is shown in the table below.

      
      |**Weight value** |**Proportion** |
      |---|---|
      |High |15% |
      |Medium |10% |
      |Low |5% |
      |Ignore |0 |
      

   * The scoring rules for database inspection are shown in the table below.

      
      |**Deduction items** |**Rule** |**Calculation method** |
      |---|---|---|
      |CPU usage |Deduct points based on average CPU usage. |* No points are deducted when the average CPU usage is less than 70%.<br><br>* When the average CPU usage is greater than or equal to 70%, the deduction calculation method is as follows:<br><br>   1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>   2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * CPU usage weight ratio / Sum of all weight ratios * 90`. |
      |Memory usage |Deduct points based on the average memory usage. |* No points are deducted when the average memory usage is < 70%.<br><br>* When the average memory usage is \>= 70%. The score deduction calculation method is as follows.<br><br>   1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>   2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Memory usage weight ratio / Sum of all weight ratios * 90`. |
      |Connection usage |Deduct points based on the average connection usage. |* No points are deducted when the average connections are less than 70%.<br><br>* When the average connection usage is greater than or equal to 70%, the deduction calculation method is as follows:<br><br>   1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>   2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Connection usage weight ratio / Sum of all weight ratios * 90`. |
      |Slow log |Deduct points based on the number of slow logs per 24 hours. |* When the number of slow logs is equal to 0, no points will be deducted.<br><br>* When the number of slow logs is greater than 0, the score deduction is calculated as follows.<br><br>   1. Deduct points based on the number of slow logs.<br><br>      * When 0 < number of slow logs < 50, deduct 1 point, that is, `score = 1`.<br><br>      * When the number of slow logs \>= 50, the score deduction formula is `score = int(min(number/50, 10))`.<br><br>   2. Use a weighted value to calculate the final score deduction. The formula is: `Final score deduction = score / 10 * Slow log weight ratio / Sum of all weight ratios * 90`. |
      |Disk usage |Deduct points based on the estimated number of days of remaining disk usage. |* Deduct points based on available days.<br><br>   * No points are deducted if available days \>= 15.<br><br>   * If available days < 15, the score deduction calculation method is as follows:<br><br>      1. Use the formula `score = int(15 - days/3 )` to calculate the deduction score.<br><br>      2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Disk usage weight ratio / Sum of all weight ratios * 90`.<br><br>* Calculate deductions based on usage<br><br>   * No points are deducted when the average disk usage is less than 70%.<br><br>   * When the average disk usage is greater than or equal to 70%, the deduction calculation method is as follows:<br><br>      1. Use the formula `score = min ((usage - 70) * 40 / 100, 10)` to calculate the deduction score.<br><br>      2. The final deduction score is calculated using weighted values. The formula is: `Final deduction = score / 10 * Disk usage weight ratio / Sum of all weight ratios * 90`.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When calculating the final score of the statistical disk usage, deduct the higher score of the two deduction methods.</div><br> |
      

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The following uses CPU usage as an example to describe the calculation process of the inspection score.      </div>
      

      1. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">In the inspection weight settings, set the weight of CPU usage to <strong>High</strong> (15%), and the weight of the other four deduction items to <strong>Medium</strong> (10%).      </div>
      

      2. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Assume that the CPU usage of the current instance is 80%. The calculation formula of the deduction score for CPU usage is as follows.      </div>
      

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>score = min ((80 - 70) * 40 /100, 10) = 4</code>   </div>
   

      3. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Use weighted values to calculate the final deduction score using the following formula.      </div>
      

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="2"><code>Final deduction = 4 / 10 * 15% / (15% + 10% + 10% + 10% + 10%) * 90 = 9.7</code>   </div>
   

      4. <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Formula for calculating the final inspection score of an instance: Inspection score = 100 \- (Sum of deductions for each deduction item)      </div>
      

   * The risk levels for diagnostic results are as follows.

      
      |**Diagnostic item** |**Risk\-free** |**Low risk** |**Medium risk** |**High risk** |
      |---|---|---|---|---|
      |**CPU usage** |cpuUsage < 70% |70% <= cpuUsage < 80% |80% <= cpuUsage < 90% |90% <= cpuUsage |
      |**Memory usage** |memUsage < 70% |70% <= memUsage < 80% |80% <= memUsage < 90% |90% <= memUsage |
      |**Connection usage** |connectionUsage < 70% |70% <= connectionUsage < 80% |80% <= connectionUsage < 90% |90% <= connectionUsage |
      |**Slow log** |slowlogs = 0 |0 <= slowlogs < 100 |100 <= slowlogs < 300 |300 <= slowlogs |
      |**Disk usage** |* 15 <= days<br><br>* diskUsage < 70% |* 12 <= days < 15<br><br>* 70% <= diskUsage < 80% |* 7 <= days < 12<br><br>* 80% <= diskUsage < 90% |* 0 <= days < 7<br><br>* 90% <= diskUsage |
      


<span id=".5p-l55yL5LiA6ZSu6K-K5pat"></span>
## Set the score weight

By default, DBW sets the weight of each score deduction item of all instance nodes to Medium. It also supports modifying the weight of each score deduction item based on business requirements.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the project and region.

4. On the **Observation and diagnosis** page, click **One\-click diagnosis**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. Set the score weight, as shown in the following operations.

   * When the diagnostic target is the instance, click **Weighted scoring configuration** in the diagnostic overview.

   * When the diagnostic target is a single node, click **Weighted scoring configuration** in the diagnostic score.

6. In the **Inspection weight settings** window, you can set the weight of each deduction item for each node. See scoring rules for weight level definitions.

   
   |**Deduction items** |**Default value** |**Description** |
   |---|---|---|
   |Slow SQL |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
   |CPU usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
   |Memory usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
   |Disk usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
   |Connection usage |Medium |Select High, Medium, Low, or Ignore from the drop\-down box. |
   

7. Click **OK**.


<span id=".5p-l55yL5LiA6ZSu6K-K5pat"></span>
## View one\-click diagnosis

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One\-click diagnosis helps you comprehensively diagnose the running problems of RDS for MySQL instances from dimensions such as slow logs and real\-time sessions. At the same time, it will give you suggestions for solutions to help you quickly troubleshoot database failures.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the project and region.

4. On the **Observation and diagnosis** page, click **One\-click diagnosis**.

   1. In the upper\-right corner of the page, locate the drop\-down list and select the target database type \- **RDS for MySQL**.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. On the **One\-click diagnosis** tab, you can view the diagnosis information of the instance or a single node.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the diagnosis information within the last 15 minutes is displayed. You can also view the diagnostic result within a specified period of time (last 30 days) as needed. The time span can not exceed 15 minutes.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">By default, the instance is diagnosed. You can also select a single node for diagnosis in the diagnostic target drop\-down list.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the status in the index analysis turns red, it indicates that there are risks in the instance. It is recommended that you troubleshoot your database instance and take corresponding measures to ensure that the system can run stably and efficiently.   </div>
   

   * Select a single node and the corresponding node ID in the diagnostic target to view the diagnosis information of a single node within the last 15 minutes.

      
      |**Parameter** |**Description** ||
      |---|---|---|
      |**Diagnostic overview** |On the **Diagnostic overview** tab, you can view the instance's **Diagnostic result** and **Diagnostic score**, as follows: ||
      ||**Diagnosis result** |In the **Diagnosis result** pane, you can view the **Diagnostic items** in the current instance, including **Slow** **SQL**, **CPU usage**, **Memory usage**, **Diagnosis result** of **Disk usage** and **Connection usage**, and **Start time**. You can also click **View details** in the **Actions** column of each diagnostic item to view its specific information. The specific information is as follows:<br><br><br>* **Slow** **SQL**: In the **Diagnostic result details: Slow SQL** dialog box, you can view the **Indicator description**, **TOP** **10** **slow SQL list** and **Performance monitoring**. The details are as follows.<br><br>   * **Indicator description**: This area displays the number of slow SQL queries in the current instance.<br><br>   * **TOP 10** **slow** **SQL list**: Displays the top 10 slow SQL queries in this area. Click **View all** to jump to the **Slow log analysis** tab to view more slow logs. For more information, refer to [Slow log management](https://docs.byteplus.com/en/docs/DBW/slow-log-management-for-mysql).<br><br>   * **Performance monitoring**: This area displays the **slow** **SQL count** and **CPU usage** for the current instance.<br><br>* **CPU usage**: In the **Diagnostic result details: CPU usage** dialog box, you can view the **Indicator description** and **Performance monitoring** of CPU usage. The details are as follows.<br><br>   * **Indicator description**: This area displays the CPU usage for the current instance.<br><br>   * **Performance monitoring**: This area displays **CPU usage**, **QPS**, and **TPS** for the current instance.<br><br>* **Memory usage**: In the **Diagnostic result details: memory usage** dialog box, you can view the **Indicator description** and **Performance monitoring** of memory usage. The details are as follows.<br><br>   * **Indicator description**: This area displays memory usage for the current instance.<br><br>   * **Performance monitoring**: This area displays **Memory usage** and **innodbBufferPool usage** for the current instance.<br><br>* **Disk usage**: In the **Diagnostic result details: Disk usage** dialog box, you can view the **Indicator description** and **TOP** **10 tablespace** and **Performance monitoring** of disk usage. The details are as follows:<br><br>   * **Indicator description**: This area displays the disk usage for the current instance.<br><br>   * **TOP 10** **tablespace**: This area displays the top 10 tablespaces of the current instance. Click **View all** to view the space usage of the current instance. For details, refer to [Spatial analysis management](https://docs.byteplus.com/en/docs/DBW/spatial-analysis-management-for-mysql).<br><br>   * **Performance monitoring**: This area displays the **Disk usage** and **Binlog size** for the current instance.<br><br>* **Connection usage**: In the **Diagnostic result details: connection usage** dialog box, you can view the **Indicator description** and **Session information**. The details are as follows.<br><br>   * **Indicator description**: This area displays the connection usage for the current instance.<br><br>   * **Session Information**: This area displays the **Connection usage** and **Connections** for the current instance. You can click **View active sessions** to view more sessions and real\-time sessions. For more information, refer to [Session management](https://docs.byteplus.com/en/docs/DBW/session-information-management-for-mysql).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Hover the mouse over each diagnostic item to view its risk definition. For risk rules, refer to <a href="https://docs.byteplus.com/en/docs/DBW/one-click-diagnostics-management-for-mysql#.5rOo5oSP5LqL6aG5">Precautions</a>.</div><br> |
      ||**Diagnostic score** |In the **Diagnostic score** pane, you can view the current instance's diagnostic score, including the number of **Health status**, **High risk**, and **Risk\-free** items. You can also click **View details**, and then view the specific deduction items within the current instance in the **Deduction details** dialog box. |
      |**Metrics analysis** |On the **Metrics analysis** tab, you can view the average, maximum, minimum, day\-over\-day, and hour\-over\-hour values for each metric.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Day\-over\-day value: The ratio compared to the same time period 24 hours ago.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Hour\-over\-hour value: The ratio compared to the same time period of the previous hour.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If the status in the index analysis turns red, it indicates that there are risks in the instance. It is recommended that you troubleshoot your database instance and take corresponding measures to ensure that the system can run stably and efficiently.</div><br> ||
      ||**CPU usage (primary node)**  |Indicates the CPU resources consumed by the database server when processing requests.<br><br>You can effectively manage and reduce CPU usage by monitoring and optimizing, thereby improving the overall performance and response speed of the database. |
      ||**QPS** |Indicates the number of queries executed per second.<br><br>You can improve the query processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing queries and indexes, increasing cache, implementing read\-write separation, upgrading hardware, and using connection pools can effectively improve QPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as QPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
      ||**TPS** |Indicates the number of transactions processed per second.<br><br>You can improve the transaction processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing transaction management, adjusting cache parameters, implementing read\-write separation, optimizing hardware, and using connection pools can effectively improve TPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as TPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
      ||**InnodbBufferPool** **Hit ratio (Primary node)**  |Indicates the percentage of data queries found in the InnoDB buffer pool in the primary node. A high hit rate means that most queries can retrieve data directly from memory, thereby improving database performance. |
      ||**Memory usage (primary node)**  |Indicates the extent to which the database's memory is used within a specified period of time.<br><br>You can ensure the stability and good performance of the database system in a high\-concurrency environment through effective monitoring and optimization strategies. Adjusting the buffer pool, optimizing queries and table structures, reasonably configuring query caches, and increasing hardware resources are all effective means of optimizing memory usage. Continuously monitoring memory usage and making optimization adjustments based on the actual situation are key to ensuring the stable and efficient operation of the database system. |
      ||**Number of open connections (primary node)**  |Indicates the number of database connections currently in use on the primary node.<br><br>You can effectively manage the number of connections by using connection pools to optimize application connection management, reasonably adjusting database configuration parameters, continuously monitoring system operating conditions, and implementing load\-sharing strategies, ensuring that the database maintains performance and stability in high\-concurrency environments. This not only improves the response speed of the system to meet business needs but also prevents service interruptions due to resource bottlenecks. |
      ||**Slow queries (primary node)**  |Indicates queries whose execution time exceeds the expected or set threshold and is used to evaluate the database's health and overall efficiency.<br><br>You can continuously monitor and analyze slow queries to identify and resolve potential performance bottlenecks, ensuring the system responds quickly and provides a high\-quality user experience even under high loads. |
      ||**Active sessions (primary node)**  |Indicates the number of client connections that are currently active on the primary node.<br><br>You can effectively manage the number of active sessions by using connection pools, optimizing queries and transactions, adjusting database configurations, monitoring, and load balancing strategies to ensure that the database maintains performance and stability in high\-concurrency environments. Proper active session management can improve system responsiveness and provide a stable user experience, while also preventing service interruptions and performance degradation due to resource bottlenecks. |
      ||**Connection usage (primary node)**  |Indicates the percentage of the current database connections used relative to the maximum number of connections configured.<br><br>You can effectively control connection usage and ensure the database maintains performance and stability in high\-concurrency environments through strategies such as reasonable connection management, application optimization, database configuration adjustments, monitoring, and load balancing. Monitoring the connection usage helps to identify potential resource bottlenecks in a timely manner, prevent performance problems caused by resource exhaustion, and provide a reference basis for system expansion. |
      |**TOP list** |On the **TOP list** pane, you can view TOP SQL details based on **TOP slow SQL**, **TOP SQL (based on aggregation sessions)** , **TOP SQL (based on full SQL insights)** , **TOP tables (based on space analysis)** , and **TOP 10 auto\-increment column usage** statistics in this instance. You can also click **View all** to view more SQL information. ||
      

   * Select the instance in the diagnostic target to view the diagnosis information of the instance within the last 15 minutes.

      
      |**Parameter** |**Description** ||
      |---|---|---|
      |**Diagnostic overview** |On the **Diagnostic overview** tab, you can view the score of the instance and each node. ||
      |**Metrics analysis** |On the **Metrics analysis** tab, you can view the average, maximum, and minimum values for each metric.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If the status in the index analysis turns red, it indicates that there are risks in the instance. It is recommended that you troubleshoot your database instance and take corresponding measures to ensure that the system can run stably and efficiently.</div><br> ||
      ||**Top 10 CPU usage** |Indicates the CPU resources consumed by the database server when processing requests. You can effectively manage and reduce CPU usage by monitoring and optimizing, thereby improving the overall performance and response speed of the database. |
      ||**Top 10 QPS** |Indicates the number of queries executed per second. You can improve the query processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing queries and indexes, increasing cache, implementing read\-write separation, upgrading hardware, and using connection pools can effectively improve QPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as QPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
      ||**Top 10 TPS** |Indicates the number of transactions processed per second. You can improve the transaction processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing transaction management, adjusting cache parameters, implementing read\-write separation, optimizing hardware, and using connection pools can effectively improve TPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as TPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
      ||**Top 10 InnodbBufferPool** **Hit rate** |Indicates the percentage of data queries found in the InnoDB buffer pool in the primary node. A high hit rate means that most queries can retrieve data directly from memory, thereby improving database performance. |
      ||**Top 10 memory usage** |Indicates the extent to which the database's memory is used within a specified period of time. You can ensure the stability and good performance of the database system in a high\-concurrency environment through effective monitoring and optimization strategies. Adjusting the buffer pool, optimizing queries and table structures, reasonably configuring query caches, and increasing hardware resources are all effective means of optimizing memory usage. Continuously monitoring memory usage and making optimization adjustments based on the actual situation are key to ensuring the stable and efficient operation of the database system. |
      ||**Top 10 open connections** |Indicates the number of database connections currently in use on the primary node. You can effectively manage the number of connections by using connection pools to optimize application connection management, reasonably adjusting database configuration parameters, continuously monitoring system operating conditions, and implementing load\-sharing strategies, ensuring that the database maintains performance and stability in high\-concurrency environments. This not only improves the response speed of the system to meet business needs but also prevents service interruptions due to resource bottlenecks. |
      ||**Top 10 slow queries** |Indicates queries whose execution time exceeds the expected or set threshold and is used to evaluate the database's health and overall efficiency. You can continuously monitor and analyze slow queries to identify and resolve potential performance bottlenecks, ensuring the system responds quickly and provides a high\-quality user experience even under high loads. |
      ||**Top 10 active sessions** |Indicates the number of client connections that are currently active on the primary node. You can effectively manage the number of active sessions by using connection pools, optimizing queries and transactions, adjusting database configurations, monitoring, and load balancing strategies to ensure that the database maintains performance and stability in high\-concurrency environments. Proper active session management can improve system responsiveness and provide a stable user experience, while also preventing service interruptions and performance degradation due to resource bottlenecks. |
      ||**Top 10 Connection usage** |Indicates the percentage of the current database connections used relative to the maximum number of connections configured. You can effectively control connection usage and ensure the database maintains performance and stability in high\-concurrency environments through strategies such as reasonable connection management, application optimization, database configuration adjustments, monitoring, and load balancing. Monitoring the connection usage helps to identify potential resource bottlenecks in a timely manner, prevent performance problems caused by resource exhaustion, and provide a reference basis for system expansion. |
      |**TOP list** |On the **TOP list** pane, you can view TOP SQL details based on **TOP slow SQL**, **TOP SQL (based on aggregation sessions)** , **TOP SQL (based on full SQL insights)** , **TOP tables (based on space analysis)** , and **TOP 10 auto\-increment column usage** statistics in this instance. You can also click **View all** to view more SQL information. ||
