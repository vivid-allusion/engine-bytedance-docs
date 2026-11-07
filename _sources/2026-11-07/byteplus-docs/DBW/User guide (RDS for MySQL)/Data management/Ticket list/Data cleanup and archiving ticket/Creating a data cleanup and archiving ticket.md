---
title: "Creating a data cleanup and archiving ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/create-data-cleansing-and-archiving-ticket-for-mysql"
---

Data cleanup and archiving tickets are mainly used to delete historical data. This topic describes how to create a data cleanup and archiving ticket on the Database Workshop (DBW) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* An instance for RDS for MySQL has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Function overview: The Data cleanup and archiving ticket is primarily used to periodically and batch delete historical data to ensure database performance and space.

* Creation restrictions and permission requirements:

   * Instance control: Tickets can only be created for instances under security control. If the target instance cannot be found, contact an administrator to add it to the security control list. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql?_vtm_=a106466.b106468.0_0.0_0.0.1678_7610615829733918244&lang=en).

   * Permission verification: Archive tickets can only be submitted for database objects with SQL change permissions.

   * Index requirement: The selected target table must contain a non\-null unique index or primary key; otherwise, verification fails.

* Execution mechanism and considerations:

   * Time reference: The offset time is based on the task's actual running time (in UTC+8). For a single manual trigger, the archiving time processing is based on the current time when the execution is clicked.

   * Scheduling deviation: Due to system scheduling, the actual start time of a task may deviate by 1–2 minutes from the configured scheduled time.

   * Data volume suggestion: To avoid deletion failures or table locking risks, it is recommended to limit the data volume for a single deletion to within tens of millions of rows.

   * When a cleanup and archiving task is running on the target table, a new data cleanup and archiving ticket cannot be submitted. Wait until the current task completes.

* For detailed working principles and complete specifications of data cleanup and archiving, refer to [Introduction to data cleanup and archiving](https://docs.byteplus.com/en/docs/DBW/overview).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. In the dialog box that appears, select **Data cleanup and archiving** \> **Data cleanup and archiving**.

6. In the **Create an archive cleanup ticket** control panel, set the parameters described in the following table.

   
   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   ||**Ticket title** |Optional. Custom ticket title. The ticket title can not exceed 200 characters. |
   ||**Ticket remarks** |Optional. Customize your ticket remarks. We recommend including business\-specific details, as comprehensive remarks facilitate easier future maintenance. Ticket remarks can not exceed 200 characters. |
   |**Database & table selection** |**Database type** |Select **RDS for MySQL**. |
   ||**Instance** |From the drop\-down list, select the instance requiring data cleanup and archiving with security control enabled. |
   ||**Database** |From the drop\-down list, select the database requiring data cleanup and archiving. |
   ||**Archive table** |From the drop\-down list, select the table requiring data cleanup and archiving. |
   |**Cleanup configuration** |**Filter condition** |Optional. If you only need to clean up data that meets specific criteria, you can also enter filter conditions for the table data in the filter input box.<br><br>For example, if the target cleanup and archiving table in a database has an `id` field, and you need to clean up data where the id value is less than 10, configure the filter condition as `id < 10`. |
   ||**Variables configuration** |This variable can be used when configuring archiving filter conditions. A maximum of 10 variables can be added, and multiple variables will be combined into the WHERE clause using AND logic.<br><br>For example, if a table contains two time fields, `CreateTime` and `ModifyTime`, with a field format of `yyyy-mm-dd`, and you need to delete data that was added more than 10 days ago and modified more than 5 days ago, you must add two variables with the following configuration:<br><br><br>* Variable 2: The variable name is `CreateTime`, the time format is `yyyy-mm-dd`, and the time operation is set to minus 10 days. If the current date is 2024\-12\-03, the generated WHERE clause will be `CreateTime` `< '2024-11-24'`. If the current date is 2024\-12\-04, the generated WHERE clause will be `CreateTime` `< '2024-11-25'`.<br><br>* Variable 2: The variable name is `ModifyTime`, the time format is `yyyy-mm-dd`, and the time operation is \-, 5, Day(s). If the current date is 2024\-12\-03, the generated WHERE clause is `ModifyTime < '2024-11-24'`. If the current date is 2024\-12\-04, the generated WHERE clause is `ModifyTime < '2024-11-30'`.<br><br><br>For more information on configuring time variables, refer to [Configuring Variables](https://docs.byteplus.com/en/docs/DBW/variables).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The configured variable name must exist in the target archive table, and the time format must correspond to the field format used in the target archive table.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Time offset <code>-</code>indicates backward offset,<code>+</code> indicates forward offset,<code>+</code>,<code>-</code> both represent less\-than time comparison.</div><br> |
   ||**Data backup** |Check the **Backup deleted data** option, indicating that the data to be deleted will be backed up.<br><br>Uncheck the **Backup deleted data** option, indicating that the data will be deleted directly without creating a backup. |
   ||**Backup type** |Check the **Backup deleted data** option. You must also configure the following backup type.<br><br><br>* **Back up to built\-in TOS**: Retains the deleted data in the built\-in TOS for 30 days.<br><br>   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div><br>   <br><br>   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Data backed up to the built\-in TOS will be retained for 30 days and automatically deleted upon expiration. The download address for the built\-in TOS can be obtained by viewing logs in the ticket details page. If needed, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> promptly to download the data.   </div><br>   <br><br>* **Backup to original database**: Currently not supported. |
   |<div style="text-align: center"><br><strong>Policy configuration</strong></div><br> |**Archive type**<br><br> |* **Duplicate archive**: Currently supports periodic cleanup and archiving of data on a **daily**, **weekly**, **monthly**, or **Cron expression** basis. For more information, refer to [Schedule configuration](https://docs.byteplus.com/en/docs/DBW/create-data-cleansing-and-archiving-ticket-for-mysql#.5ZGo5pyf6YWN572u).<br><br>* **Do not repeat**: If **Do not repeat** is selected, the data cleanup and archiving process will be executed as a one\-time task upon ticket approval, following the configured **Execution method**. |
   ||**Execution time** |* **No limit on task runtime**: Allows the task to run naturally until completion.<br><br>* **Specify execution time**: Sets a time limit (in hours) after which the task will automatically terminate. If the task execution time exceeds the configured duration, it will be stopped automatically. Specifying an execution time prevents long\-running tasks from impacting normal business operations during peak hours. |
   ||**Execution method** |If the archive type is set to **Do not repeat**, the following information must be configured:<br><br><br>* **Automatic execution after approval**: The cleanup and archiving task for the current ticket will be executed automatically once the ticket is approved.<br><br>* **Scheduled execution after approval**: The cleanup and archiving task for the current ticket will be executed at a specified time after the ticket is approved. The task start time must be configured. |
   ||**Execution start time** |If the archive type is set to **Do not repeat** and the execution method is configured as **Scheduled execution after approval**, a task start time is required.<br><br>Click the time icon to select the scheduled execution time for the task. |
   ||**Batch execution** |When the data volume is large, batch execution of cleanup and archiving data is supported, as well as whether to enable the primary\-replica lag check.<br><br><br>* **Set the execution rows per batch as needed**, **and the sleep time between batches**. The default is to execute 1000 rows per batch, with a sleep time of 0.5 seconds per batch.<br><br>* **Enable primary\-replica lag check** When the primary\-replica lag check is enabled, it is necessary to set the threshold in seconds for interrupting task execution when the primary\-replica lag exceeds it. Primary\-replica lag check is disabled by default.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">The cleanup and archiving task is executed in batches by default according to the ascending order of the primary key until the task is complete.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Disabling the primary\-replica lag check may result in excessive latency, affecting failover operations.</div><br> |
   ||**Approval workflow** |The approval workflow currently includes Level 1, Level 2, and Level 3 approvals, consistent with the data change approval workflow. These correspond to the Owner, DBA, and Admin roles configured when instance security control is enabled. |
   |**Statement preview** |**SQL statement** |Based on the configured information, such as **Database**, **Archive table**, **Filter condition**, and **Variables configuration**, DBW automatically generates the SQL statement to be executed. If the generated SQL statement is incorrect, modify the configuration above until the statement is validated. |
   

7. Click **Next step: Pre\-check**.

8. On the **Ticket pre\-check** configuration wizard, you can view the results of pre\-check items, including **Rows affected (system statistics; the actual number of rows affected is subject to SQL execution)** , **Syntax check**, **Permission check**, and **Instance state check**.

   * **Check passed**: All preset check items meet the requirements, with no risks or non\-compliance issues.

   * **Pending confirmation**: Indicates that non\-blocking issues or potential risks are detected, but they do not affect the core execution logic of the ticket. The system suggests paying attention to them, but allows you to continue. You must manually confirm and ignore the prompts to proceed with submitting the ticket.

   * **Failed**: Blocking issues exist. Continuing execution may cause failures, data loss, or system anomalies. You can click **View details** in the **Results details** column of a check item to see the specific reasons for the failure, then fix the issues and create a new ticket.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If pre\-check fails, you can click <strong>View details</strong> in the <strong>Result details</strong> column of the check item to review the specific reasons for the failure. After making corrections, recreate the ticket.</div>



9. Click **Submit ticket**.

   The SQL statement generated based on the parameter examples in this topic is as follows:

   * When the current time is `2024-12-03`, the generated statement is shown below:

   ```sql
   delete from `test_db`.`common_types_table`   where (id < 10) AND  `createtime` < '2024-11-24'  AND  `modifytime` < '2024-11-29'    
   ```
   

   * When the current time is `2024-12-04`, the generated statement is shown below:

   ```sql
   delete from `test_db`.`common_types_table`   where (id < 10) AND  `createtime` < '2024-11-25'  AND  `modifytime` < '2024-11-30'    
   ```
   


<span id=".5ZGo5pyf6YWN572u"></span>
## Cycle Configuration


|**Parameter** |||**Description** |
|---|---|---|---|
|**Interval Period** |**Daily** |**Start Archiving Time** |Set the specific time for daily task execution on a daily cycle. |
||**Weekly** |**Specified Time** |Set the task execution days on a weekly basis, with multiple selections supported. |
|||**Archive Start Time** |Set the specific time for each task execution.<br><br>For example, if the specified days are Monday, Wednesday, and Friday, and the specific time is set to 02:30, the task will execute at 2:30 AM every Monday, Wednesday, and Friday. |
||**Monthly** |**Scheduled Time** |On a monthly basis, select the specific dates for task execution as needed, with support for multiple selections.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Since the number of days in a month varies, it supports selecting the last day of the month for task execution.</div><br> |
|||**Archive Start Time** |Set the specific time for each task execution.<br><br>For example, if the scheduled time is set on the 1st, 15th, and last day of each month, with the specific time set at 05:00, the task will be executed on the 1st, 15th, and last day of each month. |
||**Cron Expression** |**Cron Expression** |Supports configuring task execution cycles via Cron expressions, such as `0 0 1 * * ?`, which means executing the cleanup archive task once at 1 AM every day. |


&nbsp;
