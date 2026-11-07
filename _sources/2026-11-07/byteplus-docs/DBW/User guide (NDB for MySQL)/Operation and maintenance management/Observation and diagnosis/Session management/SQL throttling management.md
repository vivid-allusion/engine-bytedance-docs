---
title: "SQL throttling management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/SQL_throttling_management"
---

The Database Workshop (DBW) provides SQL throttling functionality. You can use this feature to control the request volume and SQL concurrency of the database, ensuring service availability. This topic describes how to manage SQL throttling tasks in the DBW console.

## **Prerequisite**

* An NDB for MySQL instance and an account have been created, and the Instance state is Running. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, see [ for MySQL instance security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[ for MySQL instance security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[ for MySQL instance security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control) and [ for MySQL instance related operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket) [ for MySQL instance related operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket)[ for MySQL instance related operation permissions](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).

## Throttling notifications

SQL throttling tasks support keyword\-based throttling, which controls the concurrency of specific SQL types by matching keywords in SQL statements. After creating an SQL throttling task for an NDB for MySQL instance, DBW will provide throttling notifications based on the MySQL database version when the task takes effect, as shown in the table below.

|Database version |Error code |Throttling notifications |
|---|---|---|
|MySQL 5.7 |13030 |`ccl refuse to execute query` |
|MySQL 8.0 |8032 |`ccl refuse to execute query` |

## **Precautions**

* SQL throttling is an emergency measure. It is recommended to promptly close the throttling task after completion.

* Refrain from changing any instance configurations while throttling is in effect. Otherwise, SQL throttling management for the instance will be disrupted.

* A maximum of 128 SQL throttling tasks can be created. Each rule supports a maximum of 128 keywords, and the total length of all keywords must not exceed 512 bytes.

* The limits for SQL keyword count and total length are adjustable up to 65,535 bytes; however, excessively large values are not advised.

   Excessively high thresholds can significantly increase memory and CPU consumption during throttling matching, thereby impacting the database's overall performance and stability. We recommend configuring reasonable rules based on your actual business needs. If you need to adjust the above thresholds, [submit ticket](https://console.byteplus.com/workorder/create). Our Technical Support team will evaluate your request based on your instance specifications and business scenarios.

* SQL keyword throttling relies on character\-by\-character matching, meaning the performance impact scales with the amount of character matching required. Longer SQL texts are more likely to share prefixes with rule keywords (even without a final match), which prolongs the character\-by\-character comparison process and increases the performance overhead.

* When an SQL statement's prefix closely resembles the throttling keyword, it can lead to an extra performance overhead of as much as 97%.

* The SQL keyword throttling feature relies on specific database kernel versions, with potential differences in capabilities between versions. For details on instance kernel versions, see [Kernel version release notes](https://docs.byteplus.com/en/docs/6357/1449532?lang=en).

* SQL statements within stored procedures are not subject to throttling rules.

* Deleting an SQL throttling task will immediately disable and remove it, so proceed with caution.

## Feature comparison

|**Dimension** |**SQL throttling** |**Automatically limit viewership of** |
|---|---|---|
|**Trigger method** |Manual configuration |System automatic detection + triggering |
|**Dependencies** |Identify the problematic SQL statement yourself |Dependent on real\-time session snapshots and transactions and locks |
|**Response speed** |Effective immediately after configuration |Respond in seconds to minutes after detecting an anomaly |
|**Applicable scenarios** |Known risky SQL (e.g., pre\-release protection) |Unknown burst traffic, avalanches, DoS attacks, etc. |

## Create a rate limiting task

**Create an SQL throttling task**

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Session management ** tab, click **SQL throttling**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. In the **SQL throttling** area, click **Create task**.

6. In the **SQL throttling task** dialog box, set the following parameter information.

   |**Parameter** ||**Description** |
   |---|---|---|
   |**SQL type** ||Select the SQL types to be throttled from the dropdown list, which include **`SELECT`**, **`UPDATE`**, **`DELETE`**, **`INSERT`** **and** **`REPLACE`**. |
   |**Throttling end method** ||Choose the throttling end method as needed, supporting the following two methods:<br><br><br>* **Automatic**: The throttling task will run for the set duration after creation. Once the throttling time is reached, the system will automatically close the throttling task.<br><br>* **Manual**: The throttling task will continue to run after creation until you manually close it. |
   |**Throttling time** ||Set the effective duration of the throttling task as needed, with a range of [1, 99999] in minutes.<br><br>> **tip**<br><br><br><br>* > When the **Throttling end method**is set to **Automatic**, the **Throttling time** can be configured.<br><br><br>* > After the task reaches the throttling time, the throttling task will be automatically closed, and manual early closure is also supported.<br> |
   |**Maximum concurrency** ||Set the maximum concurrency for the SQL throttling task, indicating that SQL throttling will be triggered when the number of concurrently executed SQL statements reaches the maximum concurrency. If SQL throttling is set to 0, it means all SQL executions of the selected SQL type will be restricted. The value range is 0 to 99999. |
   |**Rate limiting object**<br><br> |**SQL keywords**<br><br> |Enter the SQL statements to be rate\-limited as needed, then click Keyword generation and validation. The system will automatically split the keywords and generate rate limiting rules using ~ as separators. Examples are as follows:<br><br><br>* Example 1: Query with specified fields.<br><br><br>Enter SQL: `SELECT a, b, c FROM t WHERE a = ?` `AND b = 2 AND c = ?`<br><br>Generated rule: `select~a~b~c~from~t~where~a~and~b~2~and~c`<br><br>The executed SQL statement contains the keywords `select`, `a`, `b`, `c`, `from`, `t`, `where`, `a`, `and`, `b`, `2`, `and`, and `c` in order, this rate limiting rule is hit.<br><br><br>* Example 2: Query with wildcards.<br><br><br>Input SQL: `SELECT * FROM test WHERE name = das`<br><br>Generated rule: `select~from~test~where~name~das`<br><br>The executed SQL statement contains the six keywords `select`, `from`, `test`, `where`, `name`, and `das` in order, this rate limiting rule is hit.<br><br>> **tip**<br><br><br><br>* > Ordered matching: Keywords match the SQL statement in order. For example, the rule `select~from~test~where~a~b` matches `SELECT * FROM test WHERE a > 1 AND b > 1`, but does not match `SELECT * FROM test WHERE b > 1 AND a > 1` (different field order).<br><br><br>* > Whitespace characters ignored: Whitespace characters at the beginning and end of keywords are automatically ignored, including spaces, line breaks (`\\n`), carriage returns (`\\r`), tabs (`\\t`), and others.<br><br><br>* > No keyword generation and validation: If keyword generation and validation is not clicked, the system uses the entire input text as the rule for rate limiting control.<br><br><br>* > Disallowed characters: Keywords must not contain English commas (`,`), single quotes (`'`), or semicolons (`;`).<br><br><br>* > Length limit: The total length of keywords cannot exceed 65535 characters. It is recommended to reserve only necessary keywords to prevent oversized rules from affecting performance.<br> |
   ||**SQL template** |Abstract specific parameters in the SQL into placeholders (e.g., `?`) to generate a standardized template (e.g., `SELECT * FROM orders WHERE user_id = ?`).<br><br>Set the SQL statements to be throttled as needed, and then click **Generate SQL Template**. The system will automatically parse the statements and replace the parameters with ? as the separator.<br><br>For example, to rate\-limit the statement `SELECT * FROM users WHERE id = 1001;`, enter it in the input box and click **Generate SQL templates**. The system will automatically convert the SQL statement to `SELECT * FROM users WHERE id = ?` and apply it. This means all queries with `id=?` will be rate\-limited. Regardless of whether `?` is `1001`, `2002`, or any other value, they will all be rate\-limited. |

7. Click **OK**.

8.

**Create Auto-throttling task**

For detailed configuration of automatic throttling, see [Automatic throttling management](https://docs.byteplus.com/en/docs/DBW/auto-throttling-management-for-vedbmysql?lang=en).

## View an SQL throttling task

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Session management ** tab, click **SQL throttling**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

   In the **SQL throttling** pane, you can view the **Task ID**, **Task status**, **SQL type**, **Rate limiting object**, **SQL keywords**, **Start time**, **Remaining time**, **End time**, **Number of rejections**, and **Maximum concurrency**.

   **Task status** includes **Running**, ** Completed**, ** Terminated**, ** Deletion failed** and ** Termination failed**.

## Delete SQL throttling

> **tip**

> When deleting, the selected throttling task will be immediately closed and deleted. Proceed with caution.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

3. On the top menu bar, select the region.

4. On the **Session management ** tab, click **SQL throttling**.

   1. In the drop\-down list in the upper\-right corner of the page, select the **NDB for MySQL** database type.

   2. In the upper\-right corner of the page, locate the drop\-down list and select the target instance.

5. In the **SQL throttling** pane, in the **Actions** column of the target SQL throttling task, select  **...**  \> **Delete**.

6. In **Are you sure you want to delete?**  dialog box, click **OK**.
