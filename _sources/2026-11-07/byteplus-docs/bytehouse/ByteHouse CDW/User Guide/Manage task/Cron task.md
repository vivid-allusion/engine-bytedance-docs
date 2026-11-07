---
title: "Cron task"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/docs-cron-task"
---

ByteHouse Cloud Data Warehouse supports managing virtual warehouse scaling and running SQL queries through timed tasks. This tutorial introduces how to manage scheduled tasks.

<span id="61441ab0"></span>
# Function overview

ByteHouse timed tasks support two core capabilities to meet operations and query requirements:


1. **Virtual warehouse scheduled scaling**: Automatically adjust the elastic scaling of the virtual warehouse based on the execution time set in the task settings to match query traffic and workloads during different time periods.

2. **SQL query scheduled execution**: At the preset time, automatically execute the preconfigured SQL statements.


In particular, adjusting virtual warehouse specifications through timed task can provide the following value:


* **Save costs**: Use the timed task to manage virtual warehouse specifications and lower costs.

* **Improve maintenance and operation efficiency**: There is no need to maintain external tools or manually modify virtual warehouse configurations, which reduces manual operation costs.


<span id="e02fd994"></span>
# Manage tasks

<span id="cd001352"></span>
## Create cron tasks


1. Log in to the ByteHouse cloud data warehouse edition console, click the top **Task center**, click **Create new task** under the **Cron tasks** tab, and enter the new timed task page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee08411ce3bd425dbc43c757ab094d31~tplv-goo7wpa0wc-image.image) </span>

2. Configure task general information. Fill in the task name, select the task type, and fill in the task description as needed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6dbb3027d0524a4abd28c1a3ff1ede7e~tplv-goo7wpa0wc-image.image) </span>

   Task type can be set to virtual warehouse scaling or SQL query:

   * **Virtual warehouse** **scaling**: ByteHouse will automatically adjust the specifications of the virtual warehouse on schedule, based on the specifications set in the task settings and the execution plan.

   * **SQL query**: According to the SQL query specified in the task settings, ByteHouse will automatically execute this query on schedule.

3. Set the content of the execution task The parameters to be configured vary depending on the selected task type. You can view the instructions for configuring parameters for each task type.

   
   |Parameter |Configuration description |
   |---|---|
   |**Virtual warehouse scaling parameters** ||
   |Virtual warehouse |Select the virtual warehouse to be adjusted. |
   |Scaling action |Select the target virtual warehouse specification from the dropdown list. Currently, only pay\-as\-you\-go billing is supported, and after scaling up or down, ByteHouse will charge according to the new specifications.<br><br><br>* **Scale\-up**: The goal specification must be more than the current specification.<br><br>* **Scale\-down**: The goal specification must be less than the current specification. |
   |**SQL query parameters** ||
   |Virtual warehouse |Select computing resources for executing SQL queries. |
   |SQL dialect |Select the SQL dialect for subsequent statements. Supported dialects include ANSI SQL, ClickHouse SQL, and MySQL. |
   |SQL statement |Input the SQL statements to be executed in the code block, specify the data objects to be queried, and do not configure connection information. Supports setting multiple SQL statements. ByteHouse will generate multiple query IDs during execution, which you can view in the Task Details. For Activity details, see [View task details](https://docs.byteplus.com/docs/bytehouse/docs-cron-task#d1eb7112).<br><br>```SQL```<br>```SELECT * FROM demo_db.demo_table LIMIT 10;```<br>```SELECT * FROM demo_db2.demo_table2 LIMIT 10;```<br> |
   

4. Set the execution plan of the task

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e982bdbbd0be4e1d9eda77a08c7333c7~tplv-goo7wpa0wc-image.image) </span>

   The parameter descriptions are as follows:

   
   |Parameter |Configuration description |
   |---|---|
   |Start date |Select the start time of the task. |
   |End date |Select the task's end time; the task execution period must not exceed this time. |
   |Timezone |Select the time zone corresponding to the task execution time. |
   |Execution cycle |Select the valid period for the task. You can choose every day, every week, every month, or custom. The parameters that need to be configured in subsequent steps vary for different periods. For details, see the parameter description below.<br><br><br>* **Every day**: You need to configure **execution time**.<br><br>* **Weekly**: You need to configure **execution days** and **execution time**.<br><br>* **Monthly**: You need to configure **execution day** and **execution time**.<br><br>* **Custom**: You need to configure **Cron** **expression**. |
   |Execution days |This parameter must be configured when the execution cycle is set to weekly or monthly.<br><br><br>* **Weekly**: Select which day or days of the week to execute the task.<br><br>* **Monthly**: Select on which day or days of the month the task will run. This setting only supports days 1–28. To set other dates in the month, use a Cron expression. |
   |Execution time |Select the specific execution time for the task on the designated execution day. |
   |Cron expression |When the period is set to Custom, this parameter must be configured to specify the time and frequency for executing scheduled tasks.<br><br>When the date is set to 29, 30, or 31, if the current month does not have that date, ByteHouse will run the task on the last day of the current month. |
   |Recovery time |Optional: Once set, the task will be restored to its pre\-execution state at the specified time. |
   |Post\-creation status |Select the initial status after the task is created.<br><br><br>* **Active**: After the task is created, it remains in an active status and will execute the task at the next scheduled execution time.<br><br>* **Pause**: After a task is created, it remains inactive and will not run at the next execution time. To enable this task, you can use the following two methods:<br><br>   * **Run once**: On the **Task center** page, click **Start now** in the Operation column to immediately execute the task.<br><br>   * **Periodic execution**: Edit the task and set the task status to active. Please refer to [Edit a task](https://docs.byteplus.com/docs/bytehouse/docs-cron-task#5f0d1192). |
   

5. Click **Save** to finish creating a new timed task. You can view all timed tasks in **Task center**.

6. (Optional) After the task is created, you can click the **Start now** button in the Actions column to immediately execute the current task once.


<span id="d1eb7112"></span>
## View task details

On the **Task center** page, click the task name to enter the task details page. You can view the execution records of tasks, including task type, UUID, status, message, query ID, execution start time, duration, and other information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b4a8696653a45b2b23d7f9af31a60c8~tplv-goo7wpa0wc-image.image) </span>

If the task execution fails, you can click the details button in the Notification column to view the specific reason for the task's failure and assist with troubleshooting.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69f5318c9c344d64a27950eb7068ffec~tplv-goo7wpa0wc-image.image) </span>

<span id="5f0d1192"></span>
## Edit a task

On the \*\*Task center \*\*page, click the **Edit** button in the task operation column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bd83482e2c6148399a3ed7a171248c47~tplv-goo7wpa0wc-image.image) </span>

<span id="007b570c"></span>
## Delete a cron task

On the **Task center** page, click the **Delete** button in the Action column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6e47d0088ed744dd8fe5fac5fdb0634b~tplv-goo7wpa0wc-image.image) </span>

<span id="798d050c"></span>
# View virtual warehouse monitoring

After creating a task, you can view the monitoring metric data of the task on **Tenant management** \> **Cloud monitor** page.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/abb8bd0fd1494b40950cec2f9bbf9c4d~tplv-goo7wpa0wc-image.image) </span>

For details about the currently supported task monitoring metrics and operation guidelines for creating monitoring and alarms via BytePlus Cloud Monitor, please refer to [Monitoring and alarm](https://docs.byteplus.com/docs/bytehouse/monitoring-and-alarm).
