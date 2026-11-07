---
title: "Database inspection management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Redis_database_inspectioin_management"
---

DBW provides a database inspection feature that performs regular automated health checks and risk assessments on database instances, helping you understand their operational status. This topic describes how to enable database inspection for Cache for Redis and view database inspection reports.

<span id="QMJCLxEL"></span>
## Prerequisites


* An instance has been created and is in the Running state. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, see [Enable security control for Cache for Redis instances](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-redis?lang=en) and [Apply for operation permissions for Cache for Redis](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket-for-redis?lang=en).


<span id="7We8ha6E"></span>
## Precautions


* When you use the database inspection feature, do not change the configurations of the instance. Otherwise, the database inspection feature can not be used to inspect and evaluate the instance.

* In the inspection record list, DBW retains the inspection records and reports for the past 30 days, and the expired reports will be automatically deleted Download the inspection report in time.


<span id="MBRknFDP"></span>
## Inspection scoring rules

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Formula for calculating the final inspection score of an instance: Inspection score = 100 \- (Sum of deductions for each deduction item).</div>


* <div data-tips="true" data-tips-type="default">When calculating the final score of a Cache for Redis instance, the higher deduction score in the node is deducted.</div>



The scoring rules of database inspection are shown in the following table


|**Deduction items** |**Rule** |**Calculation method** |
|---|---|---|
|CPU usage |Deduct points based on average CPU usage. |* No points are deducted when the average CPU usage is less than 70%.<br><br>* When the average CPU usage is greater than or equal to 70%, use the formula score = min((usage \-70)\*40/100, 10) to calculate the deduction score. |
|Memory usage |Deduct points based on the average memory usage. |* No points are deducted when the average memory usage is < 70%.<br><br>* When the average memory usage is greater than or equal to 70%, use the formula score = min((usage \-70)\*40/100, 10) to calculate the deduction score. |
|Connection usage |Deduct points based on the average connection usage. |* No points are deducted when the average connections are less than 70%.<br><br>* When the average connection usage is greater than or equal to 70%, use the formula score = min((usage \-70)\*40/100, 10) to calculate the deduction score. |


&nbsp;

<span id="GgJHSIH4"></span>
## Enable database inspection


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. To enable database inspection, perform the following steps:

   * Enable automatic inspection

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The automatic inspection period defaults to 00:00:00 to 23:59:59 of the previous day, and an inspection is automatically performed once a day.      </div>
      

            * Enable automatic inspection for a single instance

         1. On the left navigation bar, click **Instance list**.

         2. On the **Instance list** page, click the pen icon in the **Automatic inspection** column of the target instance.

         3. In the **Automatic inspection settings** dialog box, enable automatic inspection and set the period during which the inspection starts to be performed.

         4. Click **OK**.

      * Batch enable instance automatic inspection

         1. On the left navigation bar, click **Instance list**.

         2. On the **Instance list** page, check the instances for which you want to enable automatic inspection, and click **Automatic inspection settings**.

         3. In the **Automatic inspection settings** dialog box, enable automatic inspection and set the period during which the inspection starts to be performed.

         4. Click **OK**.

   * Enable manual inspection

      1. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

      2. On the **Inspection report** or **Inspection records** tab, click **Initiate manual inspection**.

      3. In the **Manual inspection** dialog box, locate the **Select instance to be inspected:**  area, check the instances you want to inspect manually, and set the time period for the database instances to be inspected.

         <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="default" data-wrapper-indent="3">The inspection time can not be later than the current time, and the interval between the inspection start time and the inspection end time ranges from 1 to 24 hours.         </div>
         

      4. Click **OK**.


<span id="ccAPDTMQ"></span>
## View inspection records

The inspection report supports filtering and viewing by instance name, instance ID, and time range.


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

4. On the top menu bar, select the database type **Cache for Redis**.

5. On the **Database inspection** page, view the following information.

   
   |**Actions** |**Description** |
   |---|---|
   |View inspection report information |Click **Inspection report**. On the **Inspection report** tab, you can view the **Total number of inspections for the day**, **Instances with a score of 100**, **Instances with scores between 99 and 80**, **Instances with scores between 79 and 60**, and **Instances with scores below 60** for a specified date **.**  |
   |View inspection record information |Click **Inspection records**. On the **Inspection records** tab, you can view all automatic and manual inspection records **.**  You can use the search function to filter the inspection records you want to find. |
   |View basic inspection information |On the **Inspection report** or **Inspection records** tab, you can view all automatic and manual inspection records, including the inspection execution time, task status, inspection type, inspection period, instance ID/name, health score, CPU usage, memory usage, connection usage, and QPS.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">Health score: The system deducts points based on the scoring rules.</div><br><br><br>* <div data-tips="true" data-tips-type="default">CPU usage: Indicates the average ratio of CPU usage time to total time within the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Memory usage: Indicates the average ratio of used memory to total memory during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Connection usage: Indicates the average ratio of used connections to available connections during the inspection period.</div><br><br><br>* <div data-tips="true" data-tips-type="default">QPS: Indicates the average QPS during the inspection period.</div><br> |
   |View the inspection report |Refer to [Viewing inspection reports](https://docs.byteplus.com/en/docs/DBW/Redis_database_inspectioin_management#sapg51Vx).<br><br> |
   


<span id="sapg51Vx"></span>
## View the inspection report


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Database inspection**.

4. On the top menu bar, select the database type **Cache for Redis**.

5. On the **Inspection report** or **Inspection records** tab, select the target record and click **View report** in the Actions column. On the **Inspection report details** control panel, you can view the inspection results of the instance or node. In the upper\-right corner of the Inspection report details control panel, click **Download report** to download the inspection report to your computer in PDF format.

   
   |**Parameter** |**Description** ||
   |---|---|---|
   |**Instance score summary** |Aggregates the scores for instances and each node within the instances. ||
   |**Basic information** |On the **Basic information** pane, you can view the basic information of the current instance, including **Instance ID**, **Instance specification**, and **Database version**. ||
   |**Health score** |The health score of the current instance. ||
   |**Deduction details** |Deduction details of the current instance. ||
   |**Resource usage** |**CPU usage (%)**  |CPU usage indicates the CPU resources consumed by the database server when processing requests. You can effectively manage and reduce CPU usage by monitoring and optimizing, thereby improving the overall performance and response speed of the database. |
   ||**Memory usage (%)**  |The memory usage indicates the extent to which the database memory is used within a specified period. You can ensure the stability and good performance of the database system in a high\-concurrency environment through effective monitoring and optimization strategies. Adjusting the buffer pool, optimizing queries and table structures, reasonably configuring query caches, and increasing hardware resources are all effective means of optimizing memory usage. Continuously monitoring memory usage and making optimization adjustments based on the actual situation are key to ensuring the stable and efficient operation of the database system. |
   ||**Connection usage (%)**  |Connection usage indicates the percentage of the current database connections used relative to the maximum number of connections configured. You can effectively control connection usage and ensure the database maintains performance and stability in high\-concurrency environments through strategies such as reasonable connection management, application optimization, database configuration adjustments, monitoring, and load balancing. Monitoring the connection usage helps to identify potential resource bottlenecks in a timely manner, prevent performance problems caused by resource exhaustion, and provide a reference basis for system expansion. |
   ||**QPS** |QPS indicates the number of queries executed per second. You can improve the query processing capability of the database through reasonable monitoring and optimization strategies to ensure that the system maintains performance and stability in a high\-concurrency environment. Optimizing queries and indexes, increasing cache, implementing read\-write separation, upgrading hardware, and using connection pools can effectively improve QPS and enhance the overall performance of the database. Continuous monitoring of performance metrics such as QPS helps to identify and resolve potential performance bottlenecks in a timely manner, providing a guarantee for the smooth operation of the business. |
   ||**Network input bandwidth rate** |The network input bandwidth rate represents the rate at which the Cache for Redis database receives data from the network during a specified time period (the amount of data received per unit of time). This indicator reflects the network traffic of clients sending requests and data to the Cache for Redis instance. It is a key performance parameter for measuring network data flowing into the Cache for Redis instance, which directly affects data transmission efficiency and the instance's processing capability. |
   ||**Network output bandwidth rate** |Network output bandwidth rate represents the rate at which the Cache for Redis database sends data to the network within a specified time period (the amount of data sent per unit of time). This indicator reflects the network traffic of the Cache for Redis instance returning responses or transmitting data to the client side. It is a key performance parameter for measuring the network data flowing out of the Cache for Redis instance, which directly affects data transmission efficiency and instance processing capabilities. |
   |**Top 10 Keys (by memory usage)**  |On the **Top 10 Keys (by memory usage)**  list pane, you can view the information of each top Key, including **Key**, **Database type**, **Memory usage (Bytes)** , **Number of elements**, and **Database name**. ||
   |**Top 10 Keys (by number of elements)**  |On the **Top 10 Keys (by number of elements)**  list pane, you can view the information of each top Key, including **Key**, **Database type**, **Memory usage (Bytes)** , **Number of elements**, and **Database name**. ||
   |**Hot Key** |On the **Hot Key** list pane, you can view the information of each hot Key, including **Key**, **Database type**, **Number of visits**, and **Database name**. ||
