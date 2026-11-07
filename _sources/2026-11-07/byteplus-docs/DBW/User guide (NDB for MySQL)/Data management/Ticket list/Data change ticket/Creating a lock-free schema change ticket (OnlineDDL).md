---
title: "Creating a lock-free schema change ticket (OnlineDDL)"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-schema-change-ticket-OnlineDDL"
---

When creating a schema change ticket, the SQL command is executed using OnlineDDL by default. An OnlineDDL ticket helps you prevent DDL or query blocking caused by locked databases and tables. This topic describes how to create a lock\-free schema change ticket, that is, an OnlineDDL ticket, on the Database Workshop (DBW) console.

## Prerequisite

* An instance and account for veDB for MySQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1) and [Creating an account](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_and_deleting_accounts#.5Yib5bu66LSm5Y-3).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions).

## Precautions

* When creating a lock\-free schema change ticket, the selected table must have a primary key.

* Only instances with security controls enabled are supported for creating lock\-free schema change tickets for management.

* Only users added within DBW User management are allowed to create tickets.

* Supports executing multiple change operations in a single `ALTER TABLE` statement, but does not support directly using `CREATE INDEX` or `DROP INDEX` statements. Related index operations must be implemented via the `ALTER TABLE` syntax. For specific syntax information, see the [Reference documentation](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-schema-change-ticket-OnlineDDL?TagIDs=2&lang=en#VPLUNM1G).

* Before creating a lock\-free schema change ticket, ensure no locks are held on the database instance, as this may block the execution of the ticket.

* Do not manually execute other DDL operations during OnlineDDL execution, as this may result in overwriting the outcomes of manually executed DDL.

* In lock\-free schema change tickets, the recommended total string length for databases and tables is no more than 52 characters, and the string length for a single table is no more than 49 characters. Otherwise, SQL statements may fail to execute or cause database system runtime errors.

* Schema changes for HTAP tables via lock\-free schema change tickets are not supported. Additionally, converting regular tables to HTAP tables via lock\-free schema change tickets is also not supported.

* Lock\-free schema change table switching may trigger table locks, blocking business requests. Long transactions during switching will be terminated by default. Schedule table switching during off\-peak business hours to minimize impact.

* The system supports only one ticket in execution status at any given time.

* **Force ignore strategy**:

      * Ignorable check items: In pre\-checking, the following check items that result in Failed, Pending confirmation, or Alarm can be skipped using the Force ignore button:

         * SQL\-related checks: Syntax check, DryRun check, Database & Table check, Remaining space check, Primary key check, etc.

         * Other checks: Instance check, DTS task check, Explain check.

      * Non\-ignorable check items: The following check items are mandatory and must be passed before submitting a ticket. Force ignore is not supported:

         * Permission check: Ensure the submitter has the required permissions to execute the change.

         * DDL suggestion: Ensure the change statement is safe and compliant, and the current database environment can handle the change.

         * Security check: Ensure the SQL does not violate database security requirements and best practices.

      * **Execution limit**: After force ignore, the ticket does not support automatic or scheduled execution. It must be executed manually after approval.

      * **Mode restriction**: Unparseable SQL can only be executed in lock\-free mode and does not support Instant DDL.

      * **Data risk**: If the SQL involves adding a unique index, ensure the target column has no duplicate data. Otherwise, only one duplicate record will be retained after execution, and the rest will be discarded.

## Pre\-check

|**Check item** |**Check content** |**Inspection results are negligible** |**Remarks** |
|---|---|---|---|
|Syntax check |Ensure that the SQL statements you submit are syntactically correct, comply with database standards, and can be properly parsed and executed by the system. |Yes (Force ignore) |None |
|Online DDL DryRun check |Simulate and preview the entire lock\-free change process without touching any real data, ensuring the feasibility and security of the change plan. |Yes (Force ignore) |None |
|Online DDL Table Check |Check whether a primary key or unique index exists in the database table. |Yes (Force ignore) |None |
|Online DDL remaining space check<br><br> |Check whether the disk space of the database instance is sufficient to accommodate the temporary data generated during the change, to avoid change failures or even database instance crashes due to insufficient space. |Yes (Force ignore) |None |
|Online DDL add unique key check |Check whether there are identical values in the target column (or column combination). |Yes (Force ignore)<br><br> |* If duplicate data is detected during the pre\-check, you need to configure the task execution mode for the index. For details, see [What should I do if I receive the prompt "Your lock-free schema change task may have potential issues during execution, such as data loss due to duplicate data" during the pre-check of a lock-free schema change ticket?](https://docs.byteplus.com/en/docs/DBW/during-the-pre-check-of-a-lock-free-structure-change-ticket-if-you-encounter-the-prompt-your-lock-?lang=en).<br><br>* It is recommended to execute during off\-peak business hours to reduce potential impact on online services. |
|Security check |Check whether the SQL in the lock\-free schema change ticket violates security requirements and best practices in the database. |No |For details, refer to [Security rule](https://docs.byteplus.com/en/docs/DBW/Security_rules?lang=en). |
|Permission check |Ensure the ticket submitter has the required permissions to execute the change, preventing improper change risks. |No |For details, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/Granting_system_role_operation_permissions?lang=en). |
|Instance check |Check the running status of the instance and whether there are any OnlineDDL tickets already in progress. |Yes (Force ignore) |None |
|Explain check |Accurately analyze the actual execution mechanism of the DDL statement you submitted at the database layer in advance, then evaluate whether the statement can be executed and estimate the number of affected rows. |Yes (Force ignore) |None |
|DTS task check |Check whether there are associated data migration or synchronization tasks on the instance to ensure the safety and stability of data synchronization links during OnlineDDL changes. |Yes (Force ignore) |None |
|DDL suggestions |Ensure that the change statement you are currently submitting is safe and compliant, and that the current database environment can handle the change. |No |None |

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

5. On the dialog box that appears, select **Data changes** \> **Lock\-free schema change**.

6. On the control panel of **Create lock\-free schema change ticket**, configure the following parameter information.

   |**Parameter** ||**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   |**Database & table selection** |**Database type** |Select **NDB for MySQL**. |
   ||**Ticket type** |The **Lock\-free structural change** is selected by default and can not be switched. A structural change refers to executing multiple change operations in a single `ALTER TABLE` statement to modify the database structure, such as adding new tables or modifying table columns.<br><br>> **tip**<br><br><br>> SQL commands are preferentially executed using OnlineDDL by default.<br> |
   ||**Instance** |From the drop\-down list, select the instance for which you want to create a lock\-free schema change ticket. |
   ||**Database** |From the drop\-down list, select the database for which you want to create the ticket. |
   |**Change configuration** |**Execute command** |Set an SQL statement as needed. For more information on SQL statements supported in structural changes, refer to [References](https://docs.byteplus.com/en/docs/DBW/creating-a-lock-free-schema-change-ticket-OnlineDDL?TagIDs=2&lang=en#VPLUNM1G).<br><br>> **tip**<br><br><br>> Lock\-free structural change tickets can only contain one SQL statement.<br> |
   |**Policy configuration** |**Execution method**<br><br> |Select an execution method as required. Valid values:<br><br><br>* **Automatic execution after approval**: After the ticket is approved, the SQL statement is automatically executed.<br><br>* **Manually executed after approval**: After the ticket is approved, the creator must manually execute the SQL statement.<br><br>* **Scheduled execution after approval**: After the ticket is approved, the ticket is executed at a specified time. |
   ||**Execution start time** |Set the ticket execution start time as needed.<br><br>> **tip**<br><br><br>> When selecting **Scheduled execution after approval** as the **Execution method**, you can set the **Execution start time**.<br> |
   ||**Execution end time** |Enable and set the ticket execution end time as needed.<br><br>> **tip**<br><br><br>> When **Scheduled execution after approval** is selected as the **Execution method** and an **Execution start time** is set, the end time must be later than the start time.<br> |
   ||**DDL statements are executed with priority.**  |When enabled, the system will prioritize Online DDL for executing changes. During the final table switching phase, if long\-running transactions blocking the DDL are detected, the system will actively terminate them to ensure the successful completion of the DDL. |
   ||**Long transaction threshold** |Set the judgment time for long transactions. Transactions that run longer than this threshold are considered long transactions and will be actively terminated during the table switching phase. Value range: 1 to 10000 (unit: seconds). The default value is 3 seconds. This parameter can be configured when DDL priority execution is enabled. |
   ||**Switch table time window** |Select the table switching time as needed. You can choose **Execute now** or **Scheduled execution** to switch tables.<br><br>Lock\-free schema change operations may trigger table locks. It is recommended to schedule the table switching time during off\-peak business hours to avoid impacting business operations. |
   ||**Execution window type**<br><br> |The system supports controlling the execution timing of DDL changes through a time window to avoid impact during business peak hours.<br><br><br>* **Allowed time window**: Changes (table switching) are only allowed within the set time period. If the current time is outside the set range, the task will be automatically suspended and wait. Up to 5 time periods can be configured.<br><br>* **Blocked time window**: Changes (table switching) are prohibited within the set time period. Execution is allowed at all times except during the blocked period. This is suitable for scenarios where specific peak periods need to be avoided. Up to 5 time periods can be configured.<br><br><br>> **tip**<br><br><br>> Table structure switching operations usually involve brief table locking. Be sure to limit them to off\-peak business hours.<br> |
   ||**Full copy policy and size** |Configure the execution method and resource consumption of the data migration phase during Online DDL as needed. Valid values:<br><br><br>* **DBW dynamic tuning(Recommend)** : The system automatically adjusts the amount of data copied in each batch based on real\-time metrics such as current database load, table size, and disk I/O capacity. For example, it automatically increases the batch size during off\-peak hours and decreases it during peak hours. This intelligent throttling mechanism ensures both efficiency and safety.<br><br>* **Specify fixed size**: You can manually set the number of rows to be copied in each batch. This is suitable for scenarios that require strict control over resource consumption, such as when server performance bottlenecks are known or when it is necessary to strictly align with maintenance windows. |
   ||**Cleanup strategy for the original table after table switching** |Select the system's handling method for the original table after the specified table is successfully switched as needed. The options are as follows:<br><br><br>* **Directly delete invalid original table(Recommend)** : After the table switch is successful, the system will automatically delete the original table. The data in the original table will be unrecoverable. Proceed with caution. Ideal for scenarios where the new table data is verified to be correct and immediate storage space release is desired.<br><br>* **Keep the invalid original table in the source database (Manual cleanup)** : After the table switch is successful, the original table will be renamed and retained in the source database. You must manually delete it. Ideal for scenarios where you want to retain the original table as a backup for safety, and manually clean it up after a period of observation to ensure there are no issues. |
   ||**Primary\-standby delay threshold** |Set the alarm threshold for instance primary\-secondary replication delay (unit: seconds). During data copy, the system monitors the primary\-secondary delay in real time. If the delay exceeds the threshold, the system automatically suspends data copy for new tables to prevent high primary database load from affecting services. After the primary/secondary delay falls below the threshold, the system automatically resumes the copy task. The default value is 3 seconds.<br><br>> **tip**<br><br><br>> It is recommended to adjust the value based on the sensitivity of your business to the primary database performance. If your business is extremely sensitive to latency, you can lower the value appropriately.<br> |
   ||**Advanced configuration** |* **Timeout duration for table locking during switching**: Set the lock timeout for the table switching phase as needed. Unit: seconds (s). Value range: 1 to 10. Default value: 5.Timeout duration for table locking during switching:<br><br>* **Number of retries when switching table fails**: Set the number of retries on table switching failure as needed. Value range: 1 to 30. Default value: 3.Number of retries when switching table fails:<br><br>* **Full copy interval**: The wait time after each batch of full data copy is completed. The value range is 0 ms to 1000 ms (default: 0 ms).<br><br><br>> **tip**<br><br><br>> When the full copy interval is set to 0 ms, data is copied continuously, which provides the fastest copy speed but has the greatest impact on the source database load. Increasing the interval can effectively reduce the pressure on the source database, but it will correspondingly extend the overall copy duration.<br> |
   |**Preview**<br><br> |**Approval workflow** |Tickets use a fixed three\-level approval workflow: level one, level two, and level three. Approvers are configured when instance security control is enabled and cannot be directly modified after ticket submission. To adjust the approver, you can modify the instance's security control settings. For details, see [Enable security control](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control). |
   ||**Business background** |Fill in the business reason and usage scenario for creating the ticket as needed, so that approvers can quickly understand the ticket purpose, reduce communication costs, and use it for subsequent audits. |

6. Click **Next step: Pre\-check**.

7. On the **Ticket pre\-check** configuration wizard page, you can view pre\-check items including **syntax check**, **security rule check**, **permission check**, and **number of rows affected (system statistical value, the actual number of rows affected is still subject to SQL execution**).

   * **Check passed**: All preset check items meet the requirements, with no risks or non\-compliance issues.

   * **Pending confirmation**: Indicates that non\-blocking issues or potential risks are detected, but they do not affect the core execution logic of the ticket. The system suggests paying attention to them, but allows you to continue. You must manually confirm and ignore the prompts to proceed with submitting the ticket.

   * **Failed**: Blocking issues exist. Continuing execution may cause failures, data loss, or system anomalies. You can click **View details** in the **Results details** column of a check item to see the specific reasons for the failure, then fix the issues and create a new ticket.

   > **tip**

   * > Check items related to SQL (such as syntax, DryRun, Database & Table, remaining space, and unique keys), instances, DTS tasks, and Explain support forced ignore. Operation path: Click **Force ignore syntax check results**, and in the dialog box that appears, click **Confirm ignore**.

   * > If the Online DDL remaining space check fails, refer to [Handling the "PrecheckFailed_DiskSpaceInsufficient" error when creating a ticket](https://docs.byteplus.com/en/docs/DBW/PrecheckFailed_DiskSpaceInsufficient).

   * > If your account is the primary account, and both the syntax check and rows affected pre\-checks pass, but the security rule check or permission check fails, you can still click **Confirm** to create the ticket.

   * > If your account is a sub\-user, and the syntax check, rows affected pre\-check, and permission check all pass, with no high\-alert items failing in the security rule check, you can click **Confirm** to create the ticket directly.

8. Click **Submit ticket**.

## Next steps

[Managing data change tickets](https://docs.byteplus.com/en/docs/DBW/Managing_data_change_tickets?lang=en)

## **References**

The following table describes SQL statements supported in schema changes.

|**Category** |**DDL operations** |**Change method** |
|---|---|---|
|Index operations |Add a unique index |```sql```<br>```ALTER TABLE table_name ADDUNIQUEINDEX idx_name(col_list);```<br> |
||Add a secondary index |```sql```<br>```ALTER TABLE tbl_name ADD INDEX name (col_list);```<br> |
||Delete an index |```sql```<br>```ALTER TABLE tb_name DROP INDEX index_name;```<br> |
||Rename an index |```sql```<br>```ALTER TABLE tbl_name RENAME INDEX old_index_name TO new_index_name;```<br> |
||Add a FullText index |```sql```<br>```ALTER TABLE tbl_name ADD FULLTEXT INDEX name (col_list);```<br> |
||Add a SPATIAL index |```sql```<br>```ALTER TABLE tbl_name ADD SPATIAL INDEX name (col_list);```<br> |
||Modify the type of an index |```sql```<br>```ALTER TABLE tbl_name DROP INDEX i1, ADD INDEX i1(key_part,...) USING BTREE;```<br> |
|Column operations |Add a column |```sql```<br>```ALTER TABLE table_name ADD COLUMN col_name column_definition;```<br> |
||Delete a column |```sql```<br>```ALTER TABLE table_name DROP COLUMN col_name;```<br> |
||Reorder columns |```sql```<br>```ALTER TABLE tbl_name MODIFY COLUMN col_name column_definition FIRST;```<br> |
||Set the default value for a column |```sql```<br>```ALTER TABLE tbl_name ALTER COLUMN col SET DEFAULT literal;```<br> |
||Delete the default value of a column |```sql```<br>```ALTER TABLE tbl ALTER COLUMN col DROP DEFAULT;```<br> |
||Modify the data type of a column |```sql```<br>```ALTER TABLE tbl_name CHANGE col_name col_name new_data_type;```<br> |
||Extend VarChar type length \- increase |```sql```<br>```ALTER TABLE tbl_name CHANGE col_name col_name VARCHAR(255);```<br> |
||Extend VarChar type length \- decrease |```sql```<br>```ALTER TABLE tbl_name CHANGE col_name col_name VARCHAR(250);```<br> |
||Modify `auto-increment` value |```sql```<br>```ALTER TABLE table AUTO_INCREMENT=next_value;```<br> |
||Set a column to NULL |```sql```<br>```ALTER TABLE tbl_name MODIFY COLUMN column_name data_type NULL;```<br> |
||Set a column to NOT NULL |```sql```<br>```ALTER TABLE tbl_name MODIFY COLUMN column_name data_type NOT NULL;```<br> |
||Modify the definition of an ENUM or SET column |```sql```<br>```ALTER TABLE t1 MODIFY COLUMN c1 ENUM('a', 'b', 'c', 'd');```<br> |
|Foreign key operations |Add foreign key restrictions |```sql```<br>```ALTER TABLE tbl1 ADD CONSTRAINT fk_name FOREIGN KEY(col1)```<br>```REFERENCES tbl2(col2) referential_actions;```<br> |
||Delete foreign key restrictions |```sql```<br>```ALTER TABLE tbl DROP FOREIGN KEY fk_name;```<br> |
|Table operations |Modify a table character set |```sql```<br>```ALTER TABLE `test_db`.`user` CHARACTER SET = utf8mb4, COLLATE = utf8mb4_bin;```<br> |
||Modify ROW_FORMAT |```sql```<br>```ALTER TABLE tbl_name ROW_FORMAT = row_format;```<br><br><br>> **tip**<br><br><br>> Acceptable values for `row_format` include `REDUNDANT`, `COMPACT`, and `DYNAMIC`.<br> |
||Modify KEY_BLOCK_SIZE |```sql```<br>```ALTER TABLE tb_name KEY_BLOCK_SIZE=key_block_size;```<br> |
||Set a character set |```sql```<br>```ALTER TABLE tbl_name CHARACTER SET = charset_name;```<br> |
||`convert` a character set |```sql```<br>```ALTER TABLE tbl_name CONVERT TO CHARACTER SET charset_name;```<br> |
||FORCE rebuild a table |```sql```<br>```ALTER TABLE tbl_name FORCE;```<br> |
