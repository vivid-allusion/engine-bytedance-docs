---
title: "Querying a slow log through operation observability"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/querying-slow-logs-through-operational-observation"
---

This topic describes how to query slow logs (i.e., logs of slow SQL queries) that are generated in the past 24 hours for the target instance in Database Workshop (DBW). RDS for MySQL is used as an example.

<span id="prerequisites"></span>
## Prerequisites


* A BytePlus account has been registered and completed verification. For the detailed method, refer to [Sign up and verify BytePlus account](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account).

* As per the regulations in the Chinese mainland, you must have completed real name registration before you can activate and use cloud services on regions in the Chinese mainland through BytePlus. For more details, refer to [Real name registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-real-name-registration).”

* An RDS for MySQL instance is created, and a database account is created. For more information, refer to [Creating RDS for MySQL instances](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The account you create must be granted the required permissions, such as querying and modifying the specified database.   </div>
   

<span id="procedure"></span>
## **Procedure**


1. Log on to the [DBW console](https://console.byteplus.com/dbw/region:dbw+cn-beijing/overview).

2. On the left navigation bar, click **Operation and maintenance management** \> **Observation diagnosis**.

3. On the **Observation diagnosis** page, click **Slow log analysis**.

4. On the upper\-left corner of the **Slow log analysis** tab, switch to the target region and the target instance.

5. On the **Slow log analysis** tab of the target instance, select **Past 24 hours** from the **Time** drop\-down list. You can view the detailed information as required.

   * View slow log trends: On the left pane of the **Slow log analysis** tab, you can view the slow log trends in the past 24 hours. In addition, you can click a time point to view the **slow** **SQL** **number** and **CPU usage** of the time point.

   * View slow log statistics: On the right pane of the **Slow log analysis** tab, you can view **slow** **SQL** **TOP point of the day** within a time range, that is, top points within the [NowTime\-24h, NowTime] time range, and view **Slow SQL 7\-day top point** within a time range, that is, top points within the [Now Time\-7\*24h, NowTime] time range.

   * View slow log details: On the **in slow** **SQL** **list** pane, you can view all slow logs for a certain time range, filter slow logs, and view details of slow logs.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">On the <strong>slow</strong> <strong>SQL</strong> <strong>list</strong> pane, you can view slow SQL log details in two ways:      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">On the <strong>Slow Log trend</strong> pane, click a specified time point.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">On the right pane of the <strong>Slow log analysis</strong> tab, click a target time in <strong>Slow</strong> <strong>SQL</strong> <strong>TOP point of the day</strong> or <strong>Slow SQL 7\-day top point</strong>.      </div>
      

      * View all slow SQL logs of a specified time range. Detailed information includes **SQL template**, **Database**, **Executive user**, **IP source**, **Average execution time(s)** , **Average number of rows returned**, **Maximum lock wait time(s)** , **First appearance time**, and **Last appearance time**.

      * To filter slow SQL logs, click **Advanced filtering**, and then filter slow logs by **Aggregation method**, **Database**, **User**, **IP**, **Keywords**, or **Time consuming interval** as required.

      * To view the details of slow SQL logs, click the target SQL template and then go to the **SQL details** panel to view the details displayed on the **Execution details**, **Execution statistics**, and **SQL analysis** tabs. The following table describes the tabs.

         
         |**Tab** |**Description** |
         |---|---|
         |**Execution details** |On the **Execution details** tab, you can view **Start Time**, **SQL text**, **Database**, **Executive user**, **IP source**, **Execution time(s)** , **Lock wait time(s)** , **Number of rows scanned**, and **Number of rows returned** of each SQL statement.<br><br>In addition, you can click the Copy icon to copy SQL text. On the **Advanced filtering** pane, you can skip setting **Executive user** or **IP source**, and then click the Filter icon on the right of **Executive user** or **IP source** to filter the results by user or IP address. |
         |**Execution statistics** |On the **Execution statistics** tab, you can view the information about all the SQL text that meets the filter criteria in the SQL template.<br><br><br>* **Total time spent**: the percentage of the total query time of the current SQL template in the total query time of all SQL log lists in the past 24 hours.<br><br>* **Total lock waiting time ratio**: the percentage of the total lock latency of the current SQL template in the total lock latency of all SQL log lists in the past 24 hours.<br><br>* **Proportion of total scanned lines**: the percentage of the total scanned rows of the current SQL template in the total scanned rows of all SQL log lists in the past 24 hours.<br><br>* **Percentage of total rows returned**: the percentage of the total returned rows of the current SQL template in the total returned rows of all SQL log lists in the past 24 hours.<br><br>* **SQL** **Number of executions:**  the development trends of slow SQL logs within the filter time range.<br><br>* **Run profiling**: the execution status of SQL statements in each stage. This information helps you analyze and locate problems. |
         |**SQL** **analysis** |On the **SQL** **analysis** tab, you can view the following information:<br><br><br>* **SQL** **text**: the information about all SQL text in the SQL template. You can click the Copy icon to copy the SQL text.<br><br>* **Execution plan**: the execution plan. Valid values: **select_type information interpretation**, **Type information interpretation**, and **Extra information interpretation**.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you execute <code>SELECT</code>, <code>DELETE</code>, <code>INSERT</code>, <code>REPLACE</code>, or <code>UPDATE</code> statements without <code>sleep</code> or <code>benchmark</code>, this tab can display <strong>Execution plan</strong>.   </div><br>   <br><br>* **Optimization suggestions**: suggestions on optimizing SQL statements. You can refer to the suggestions to optimize your SQL statements. |
         


<span id="relevant-api"></span>
## Relevant API


|**API** |**Description** |
|---|---|
|[DescribeSlowLogs](https://docs.byteplus.com/en/docs/DBW/describeslowlogs) |Call the DescribeSlowLogs to query the slow log information. |
