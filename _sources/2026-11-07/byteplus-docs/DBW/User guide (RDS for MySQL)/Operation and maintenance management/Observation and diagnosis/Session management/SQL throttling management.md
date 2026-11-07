---
title: "SQL throttling management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/preview-sql-throttle-task-management-for-mysql"
---

The Database Workshop (DBW) provides SQL throttling functionality. You can use this feature to control the request volume and SQL concurrency of the database, ensuring service availability. This topic explains how to manage SQL throttling tasks on the DBW console, including enabling SQL throttling, creating or deleting SQL throttling tasks.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* An instance and account for RDS for MySQL have been created, and the instance status is running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_databases_and_accounts#.5Yib5bu66LSm5Y-3).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This feature is not supported when the instance status is creating, recovering, importing, error, deleted, terminated, waiting for payment, billing suspension in progress, billing restoring, billing reclaiming or reconstructing.   </div>
   

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql), and [Applying for operation permissions (RDS for MySQL)](https://docs.byteplus.com/en/docs/DBW/creating-an-operation-permission-ticket).


<span id="rxm48NuI"></span>
## Supported versions


* MySQL 5.7 version, and the kernel minor version is MySQL 5.7.32_20231015 and above.

* MySQL 8.0 version, and the kernel minor version is MySQL 8.0.32_20231015 and above.

* MySQL 8.4 version, and the kernel minor version is MySQL 8.4.7_20260415 and above.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You can view the kernel minor version of an instance by <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_instance_details?lang=en">Viewing instance information</a>. If the kernel minor version of your instance is not within the supported kernel minor version range, you can <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/upgrading_instance_kernel_minor_version?lang=en">Manually upgrade the instance kernel minor version</a>.</div>


<span id="rxm48NuI"></span>
## Throttling notifications

SQL throttling tasks support keyword\-based throttling, which controls the concurrency of specific SQL types by matching keywords in SQL statements. After creating an SQL throttling task for an RDS for MySQL instance, DBW will provide throttling notifications based on the version of RDS for MySQL when the task takes effect, as shown in the table below.


|Database version |Error code |Throttling notifications |
|---|---|---|
|MySQL 5.7 |3245 |`ccl refuse to execute query` |
|* MySQL 8.0<br><br>* MySQL 8.4 |4169 |`ccl refuse to execute query` |


<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* The maximum number of rate limiting tasks is 128, which includes both manually created SQL rate limiting tasks and automatic rate limiting tasks.

* Notes for manually creating SQL rate limiting tasks

   * SQL throttling is an emergency measure. It is recommended to promptly close the throttling task after completion.

   * After deleting an SQL throttling task, the selected throttling task will be immediately closed and deleted. Proceed with caution.

   * While using the SQL throttling feature, avoid modifying instance configurations, as such changes may disrupt normal SQL throttling management.

* For notes on automatic rate limiting, see [Automatic rate limiting management](https://docs.byteplus.com/en/docs/DBW/Auto-throttling_management?lang=en).


<span id="OnObPHRT"></span>
## Feature comparison


|**Dimension** |**SQL throttling** |**Automatically limit viewership of** |
|---|---|---|
|**Trigger method** |Manual configuration |System automatic detection + triggering |
|**Dependencies** |Identify the problematic SQL statement yourself |Dependent on real\-time session snapshots and transactions and locks |
|**Response speed** |Effective immediately after configuration |Respond in seconds to minutes after detecting an anomaly |
|**Applicable scenarios** |Known risky SQL (e.g., pre\-release protection) |Unknown burst traffic, avalanches, DoS attacks, etc. |


<span id=".5Yib5bu6LXNxbC3pmZDmtYHku7vliqE="></span>
## Create a rate limiting task


<Tabs>
<Tab zoneid="ATq73gDLqV" title="Create an SQL throttling task">
<TabTitle>Create an SQL throttling task</TabTitle>

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Session management ** tab, click **SQL throttling**.

   In the upper\-left corner of the **Session management** tab, switch to the target instance.

5. On the **SQL throttling** tab, click **Create task**.

6. In the **SQL throttling task** dialog box, set the following parameter information.

   
   |**Parameter** ||**Description** |
   |---|---|---|
   |**SQL type** ||Select the SQL types to be throttled from the dropdown list, which include **`SELECT`**, **`UPDATE`**, **`DELETE`**, **`INSERT`** and **`REPLACE`**. |
   |**Throttling end method** ||Choose the throttling end method as needed, supporting the following two methods:<br><br><br>* **Automatic**: The throttling task will run for the set duration after creation. Once the throttling time is reached, the system will automatically close the throttling task.<br><br>* **Manual**: The throttling task will continue to run after creation until you manually close it. |
   |**Throttling time** ||Set the effective duration of the throttling task as needed, with a range of [1, 99999] in minutes.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">When the <strong>Throttling end method </strong>is set to <strong>Automatic</strong>, the <strong>Throttling time</strong> can be configured.</div><br><br><br>* <div data-tips="true" data-tips-type="default">After the task reaches the throttling time, the throttling task will be automatically closed, and manual early closure is also supported.</div><br> |
   |**Maximum concurrency** ||Set the maximum concurrency for the SQL throttling task, indicating that SQL throttling will be triggered when the number of concurrently executed SQL statements reaches the maximum concurrency. If SQL throttling is set to **0**, it means all SQL executions of the selected SQL type will be restricted. Valid range is [0, 99999]. |
   |**Rate limiting object**<br><br> |**SQL keywords**<br><br> |The system supports generating throttling rules by extracting core features from SQL statements, including operation commands, table names, and column names. Simply enter the raw SQL, and the system will automatically break it down into a series of matching feature codes.<br><br><br>* Generation logic<br><br>   * Automatic deconstruction: The system ignores whitespace characters such as spaces and line breaks, splits the SQL statement into syntax units, and connects them using the ~ symbol.<br><br>   * Examples:<br><br>      * Input: `select a,b from t where a=2`<br><br>      * Generated rule: `select~a~b~from~t~where~a`<br><br>      * Meaning: This rule indicates that all fragments, such as `select`, `a`, `b`, and `from`, must be included in order.<br><br>* Matching mechanism<br><br>   * Strict ordered matching: The signature matching in this system is strictly order\-sensitive.<br><br>      * Match successful: The executed SQL is `select * from test where a > 1 and b > 1` (the order matches the rule).<br><br>      * Match failed: The executed SQL is `select * from test where b > 1 and a > 1` (although it contains the same fields, the order of appearance for `a` and `b` does not match the rule, so it will not be throttled).<br><br>* Character limit: The generated signature length cannot exceed 512 characters. If the text is too long, consider removing unnecessary fields (e.g., omit specific column names after `select`, and only keep `select~from~table`).<br><br>* Special characters: The generated rules must not contain commas (,), single quotes ('), or semicolons (;).<br><br>* No validation generated: If you do not click "Generate and validate," the system will treat the entire entered text as an exact string for matching. |
   ||**SQL template** |Abstract specific parameters in the SQL into placeholders (`?`) to generate a standardized template (e.g., `SELECT * FROM orders WHERE user_id = ?`).<br><br>Set the SQL statements to be rate\-limited as needed, then click **Generate SQL templates**. The system will automatically generate the SQL template.<br><br>For example, to rate\-limit the statement `SELECT * FROM users WHERE id = 1001;`, enter it in the input box and click Generate SQL templates. The system will automatically convert the SQL statement to `SELECT * FROM users WHERE id = ?` and apply it. This means all queries with `id=?` will be rate\-limited. Regardless of whether `?` is `1001`, `2002`, or any other value, they will all be rate\-limited.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is currently in invitation\-only testing. To use it, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact technical support.</div><br> |
   ||**SQL full text**<br><br> |Set the SQL statements to be throttled as needed. This means an exact match of the original text of the entire SQL statement (including case, spaces, parameter values, etc.), ensuring a precise match.<br><br>For example, if the SQL full text you enter is SELECT \* FROM orders WHERE user_id = '12345' AND status = 'pending';, the SQL throttling task will only restrict this statement, and the statement with user_id = '67890' will not be affected.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This feature is currently in invitation\-only testing. To use it, <a href="https://console.byteplus.com/workorder/create">Submit a ticket</a> to contact technical support.</div><br> |
   

7. Click **OK**.


</Tab>
<Tab zoneid="b90TjzUYui" title="Create Auto-throttling task">
<TabTitle>Create Auto-throttling task</TabTitle>

For detailed configuration of automatic throttling, see [Automatic throttling management](https://docs.byteplus.com/en/docs/DBW/Auto-throttling_management?lang=en).


</Tab>
</Tabs>


<span id=".5p-l55yLLXNxbC3pmZDmtYHku7vliqE="></span>
## View an SQL throttling task


1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Session management ** tab, click **SQL throttling**.

   1. In the upper\-left corner of the **Session management** tab, switch to the target instance.

   2. In the **SQL throttling** pane, you can view the **Task ID**, **Task status**, **SQL type**, **Rate limiting object**, **SQL keywords**, **Start time**, **Remaining time**, **End time**, **Number of rejections**, and **Maximum concurrency**.

      **Task status** includes **Running**, ** Completed**, ** Terminated**, ** Deletion failed** and ** Termination failed**.


<span id=".5Yig6ZmkLXNxbC3pmZDmtYHku7vliqE="></span>
## Delete an SQL throttling task

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After deletion, the selected throttling task will be immediately closed and deleted. Proceed with caution.</div>



1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Session management ** tab, click **SQL throttling**.

   In the upper\-left corner of the **Session management** tab, switch to the target instance.

5. In the **SQL throttling** pane, in the **Actions** column of the target SQL throttling task, select  **...**  \> **Delete**.

6. In **Are you sure you want to delete?**  dialog box, click **OK**.
