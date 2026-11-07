---
title: "Creating a clear table ticket"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Create_a_clear_table_ticket"
---

Data clear table tickets are mainly used to delete or remove tables with oversized data, and support secure data deletion, that is, to restore deleted data within a specified time. This article describes how to create a clear table ticket in Database Workshop (DBW).

## Background

For oversized tables, such as several TB or even dozens of TB of data tables, customers expect to be able to quickly remove tables without deleting data; or quickly delete table data while retaining or not retaining tables; and restore data in case of accidental deletion.

|**Customer requirements** ||**Requirements analysis** ||
|---|---|---|---|
|Do not delete data, quickly remove the table ||Similar to Rename table. |Currently, DBW provides Lock\-free structural change tickets and locked structural change tickets. Structural change tickets can be used to perform Rename, Truncate, and Drop operations, but this leads to the following two problems:<br><br><br>* If the Truncate and Drop operations are broken down into first performing Delete and then DDL, the execution efficiency is very low for extremely large tables, possibly taking several days, and a large amount of binlog will be generated during execution, which may even cause primary\-secondary delay.<br><br>* If the native Truncate and Drop operations are executed directly, it will also take a long time for extremely large tables. Severe DDL operations can generate large\-granularity locks, such as MDL locks, which can threaten the stable operation of the database. |
|Delete data |Reserved table |Similar to Truncate Table. ||
||Not reserved table |Similar to Drop table. ||

In view of the above requirement analysis, a new type of ticket, namely the checklist ticket, needs to be redesigned to meet customer needs. The clear table ticket can achieve the operation effects of Rename, Truncate, and Drop without affecting the stable operation of the database, while taking into account efficiency, and providing a safe deletion option.

## Clear table ticket execution logic

The DBW clear table ticket aims to achieve the operation effects of Rename, Truncate, and Drop without affecting the stable operation of the database, while taking into account efficiency, and can safely delete data. That is, in case of accidental deletion of data, the accidentally deleted data can be restored.

|**Function** |**Description** |**Execution logic** |
|---|---|---|
|**Modify table name** |Execute the rename table operation, which does not delete the data but only changes the name of the database table. |The ticket Creator enters the renamed table name, and DBW will rename the source table. This function does not clean up table Data. |
|**Clear the table** |Quickly delete data in the source table and retain the source table, similar to the TRUNCATE operation. |When performing Clear the table or Drop table operations, DBW creates a temporary table and temporarily stores the deleted data in it. The temporary table's name is `{Source TableName}_{last six digits of the Ticket ID}_{three-digit random String}_{rds_del}`.<br><br>When creating a checklist ticket, the ticket creator can **historical data retention policy** to set the retention period of the temporary table (0 to 72 hours). Deleted data can be restored within the temporary table retention period. |
|**Delete a table** |Quickly deletes the source table and the data within it, similar to the Drop table operation. ||

## Difference between clear table ticket and data cleanup and archiving ticket

Although both DBW's data cleaning ticket and data cleanup and archiving ticket involve deleting data, there are differences in purpose and application scenarios, as shown in the following table.

|**Difference type** |**Clear table ticket** |**Data cleanup and archiving ticket** |
|---|---|---|
|**Execution object** |Table (more efficient for extremely large tables than ordinary execution methods). |Data in the table. |
|**Purpose**<br><br> |* Quickly remove the table while retaining the data.<br><br>* Delete data, but you can keep the table or not. |Deletes data that meets the criteria in the table and retains the table. By cleaning table data, you can realize the reuse of table storage space, free up available disk space, and improve system performance. |
|**Application scenarios** |Applies to removing an entire table or deleting the data of an entire table as a unit. |Used to remove infrequently accessed or expired data from a table. |

## Pre\-check items

|**Check item** |**Check content** |**Inspection results are negligible** |**Remarks** |
|---|---|---|---|
|Rows affected |Check the rows of data actually affected during the table clearance process. |No |System statistics value. The actual affected rows are subject to SQL execution. |
|Syntax check |Check whether the SQL statements executed during the table clearing process comply with the syntax rules defined by MySQL. |No |None |
|Permission check |Check whether the account that creates the table clearance has the relevant permissions of the DBW role. |No |For details, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql). |
|Security rule check |Check whether the table clearance process violates the data and resource regulations in the database system. |No |For details, refer to [Security rule](https://docs.byteplus.com/en/docs/DBW/Security_rules-?lang=en). |
|Instance state check |Check whether the instance state of the table to be cleared is running. |No |None |
|Parameter check |Check whether the value of instance parameter `loose_innodb_data_file_logic_drop` is set to `ON` to enable asynchronous dropping of large tables.<br><br> |Yes |For detailed steps to enable this feature, refer to [Dropping a large table asynchronously](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deleting_a_table_asynchronously?lang=en).<br><br>> **tip**<br><br><br>> Ignoring alerts may impact instance performance and cause IO fluctuations. It is recommended to modify parameters before creating a ticket.<br> |

## Prerequisite

* An instance for RDS for MySQL has been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* The instance has enabled security control. For detailed steps, refer to [Enabling security control](https://docs.byteplus.com/en/docs/DBW/enabling-security-management-for-mysql).

* The user is added as a DBW role. For detailed steps, refer to [Adding a user](https://docs.byteplus.com/en/docs/DBW/Personal_user_management).

* Permissions related to adding users as DBW roles have been granted. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/user-management-for-mysql).

## Precautions

* Only database objects with SQL change permissions can create clear table tickets.

* When DBW executes the empty table or drop table operation of the clear table ticket, a temporary table will be created. The name of the temporary table is `{Source table name}_{last six digits of the Ticket ID}_{three random strings}_{rds_del}`.

* The temporary table stores the deleted data, and you can set the retention period of the temporary table (0 to 72 hours). The data in the temporary table can be restored during the temporary table retention period.

* During the temporary table retention period, the database storage space is not released. Therefore, monitor your database's space usage promptly to prevent high space utilization from affecting the stable operation of your business.

* DBW has no restrictions on the source table size and execution time in the clear table ticket.

* The offset time is calculated starting with the task execution time (in UTC + 8).

* There may be a 1~2 minute variance between actual execution time and the configured schedule.

* When viewing pre\-check results, ignoring alerts may impact instance performance and cause IO fluctuations. It is recommended to modify parameters before creating a ticket.

## Procedure

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the target region.

3. On the left navigation bar, select **Data management** \> **Ticket list**.

4. On the **Ticket list** page, click **Create ticket**.

   **Modify table name**

In the pop\-up dialog, select **Clear table tickets** \> **Modify table name**.

   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   |**Database & table selection** |**Database type** |Select **RDS for MySQL**. |
   ||**Instance** |Select the target instance from the drop\-down list.<br><br>> **tip**<br><br><br>> If the target instance is not in the drop\-down list, confirm whether security control is enabled for the target instance and whether the current account has management permissions for the target instance.<br> |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**Source table** |Select the target data table from the drop\-down list. |
   |**Cleanup configuration** |**Operation type** |By default, it is **Modify table name** and cannot be modified, indicating a Rename table operation that does not delete data but only changes the database table name. |
   ||**Rename to** |Enter the renamed table name. The naming rules for database table are as follows:<br><br><br>* able name is unique within the database.<br><br>* The length must be between 1 and 64 characters, and can not be empty.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* It consists of lowercase letters, numbers, underscores (_), or hyphens (\-). |
   |**Policy configuration** |**Execution method** |If the archive type is set to **Do not repeat**, the following information must be configured:<br><br><br>* **Automantic execution after approval**: After the current ticket approval is approved, the current ticket task is automatically executed.<br><br>* **Manually executed after approval**: After the current ticket approval is approved, you need to manually execute the current ticket task.<br><br>* **Scheduled execution after approval**: After the current ticket approval is approved, the current ticket task is executed at the specified time. The task start time must be configured. |
   ||**Execution start time** |If you select **Scheduled execution after approval** for the execution method, you need to configure the task start time, which is the time to execute the ticket. Click the time icon and select the task execution time as required. |
   ||**Approval workflow** |The approval process currently includes first level approval, second level approval, and third level approval, and the approvers of each node are the DBA, Owner, and Admin set when instance security control is enabled. |
   |**Statement preview** |**SQL statement** |DBW automatically generates SQL statements to be executed based on the above configuration information, such as **database**, **source table**, and **operation type**. If the generated SQL statement is incorrect, modify the configuration above until the statement is validated. |
   ||**Business background** |Fill in the business reason and usage scenario for the ticket as needed so approvers can quickly understand its purpose, reduce communication costs, and support future audits. |

   **Clear the table**

In the pop\-up dialog, select **Clear table tickets** \> **Clear the table**.

   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   |**Database & table selection** |**Database type** |Select **RDS for MySQL**. |
   ||**Instance** |Select the target instance from the drop\-down list.<br><br>If the target instance is not in the drop\-down list, confirm whether security control is enabled for the target instance and whether the current account has management permissions for the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**Source table** |Select the target data tables from the drop\-down list. Multiple tables can be selected at the same time. |
   |**Cleanup configuration** |**Operation type** |Default is **Clear the table** and cannot be modified. It means quickly deleting data from the source table while keeping the source table, similar to a TRUNCATE operation.<br><br><br>* When DBW performs the clear table operation, it creates a temporary table to temporarily store the deleted data. The temporary table's name is {Source TableName}_{last six digits of the Ticket ID}_{three\-digit random String}_{rds_del}.<br><br>* You can set the retention period (0–72 hours) for the temporary table via the **Historical data retention policy**. Deleted data can be restored within the temporary table retention period. |
   ||**Historical data retention policy** |When performing table emptying or table deletion operations, you can choose a data deletion policy as needed, which can be either immediate deletion or retention of deleted data for a period of time.<br><br><br>* **Delete immediately when the ticket is executed**: When the clear table operation is executed, the temporary table storing the cleared data is also deleted. If you select this option, you cannot recover accidentally deleted data.<br><br>* **Delayed deletion after work order execution**: When the clear table operation is executed, the temporary table storing the deleted data is retained for a period of time. The retention period for temporary tables is 0 to 72 hours, with a default of 24 hours. You can restore mistakenly deleted data during the temporary table retention period. After the temporary table retention period expires, DBW will automatically delete the temporary table, and the data cannot be recovered after deletion. |
   |**Policy configuration** |**Execution method** |If the archive type is set to **Do not repeat**, the following information must be configured:<br><br><br>* **Automantic execution after approval**: After the current ticket approval is approved, the current ticket task is automatically executed.<br><br>* **Manually executed after approval**: After the current ticket approval is approved, you need to manually execute the current ticket task.<br><br>* **Scheduled execution after approval**: After the current ticket approval is approved, the current ticket task is executed at the specified time. The task start time must be configured. |
   ||**Execution start time** |If you select **Scheduled execution after approval** for the execution method, you need to configure the task start time, which is the time to execute the ticket. Click the time icon and select the task execution time as required. |
   ||**Approval workflow** |The approval process currently includes first level approval, second level approval, and third level approval, and the approvers of each node are the DBA, Owner, and Admin set when instance security control is enabled. |
   |**Statement preview** |**SQL statement** |DBW automatically generates SQL statements to be executed based on the above configuration information, such as **database**, **source table**, and **operation type**. If the generated SQL statement is incorrect, modify the configuration above until the statement is validated. |
   ||**Business background** |Fill in the business reason and usage scenario for the ticket as needed so approvers can quickly understand its purpose, reduce communication costs, and support future audits. |

   **Delete a table**

In the pop\-up dialog, select **Clear table tickets** \> **Delete table**.

   |**Category** |**Parameter** |**Description** |
   |---|---|---|
   |**Basic information** |**Creator** |Defaults to the currently logged\-in account and can not be modified. |
   |**Database & table selection** |**Database type** |Select **RDS for MySQL**. |
   ||**Instance** |Select the target instance from the drop\-down list.<br><br>If the target instance is not in the drop\-down list, confirm whether security control is enabled for the target instance and whether the current account has management permissions for the target instance. |
   ||**Database** |From the drop\-down list, select the target database. |
   ||**Source table** |Select the target data table from the drop\-down list. To clear or drop tables, you can select multiple tables simultaneously. |
   |**Cleanup configuration** |**Operation type** |Default is **Drop table** and cannot be modified, which means quickly deleting the source table and the data within it, similar to the Drop table operation.<br><br><br>* When performing Drop table operations, DBW creates a temporary table and temporarily stores the deleted data in it. The temporary table's name is {Source TableName}_{last six digits of the Ticket ID}_{three\-digit random String}_{rds_del}.<br><br>* You can set the retention period (0–72 hours) for the temporary table via the **Historical data retention policy**. Deleted data can be restored within the temporary table retention period. |
   ||**Historical data retention policy** |When performing table emptying or table deletion operations, you can choose a data deletion policy as needed, which can be either immediate deletion or retention of deleted data for a period of time.<br><br><br>* **Delete immediately when the ticket is executed**: When performing the drop table operation, also delete the temporary table that stores the cleared data. If you select this option, you cannot recover accidentally deleted data.<br><br>* **Delayed deletion after work order execution**: When performing the drop table operation, retain the temporary table containing the deleted data for a period of time. The retention period for temporary tables is 0 to 72 hours. You can restore mistakenly deleted data during the temporary table retention period. After the temporary table retention period expires, DBW will automatically delete the temporary table, and the data cannot be recovered after deletion. |
   |**Policy configuration** |**Execution method** |If the archive type is set to **Do not repeat**, the following information must be configured:<br><br><br>* **Automantic execution after approval**: After the current ticket approval is approved, the current ticket task is automatically executed.<br><br>* **Manually executed after approval**: After the current ticket approval is approved, you need to manually execute the current ticket task.<br><br>* **Scheduled execution after approval**: After the current ticket approval is approved, the current ticket task is executed at the specified time. The task start time must be configured. |
   ||**Execution start time** |If you select **Scheduled execution after approval** for the execution method, you need to configure the task start time, which is the time to execute the ticket. Click the time icon and select the task execution time as required. |
   ||**Approval workflow** |The approval process currently includes first level approval, second level approval, and third level approval, and the approvers of each node are the DBA, Owner, and Admin set when instance security control is enabled. |
   |**Statement preview** |**SQL statement** |DBW automatically generates SQL statements to be executed based on the above configuration information, such as **database**, **source table**, and **operation type**. If the generated SQL statement is incorrect, modify the configuration above until the statement is validated. |
   ||**Business background** |Fill in the business reason and usage scenario for the ticket as needed so approvers can quickly understand its purpose, reduce communication costs, and support future audits. |

   For example, if the ticket creator wants to empty the data of the table `employee1112` in the database `dbw1` at 02:00 AM on 2025\-10\-16, and wants to keep this table, and wants the deleted data to be retained for 48 hours. The following figure shows the checklist ticket created according to this requirement. In the SQL preview of this example, `employees1112_{ticket_id}_cdj_rds_del` is a temporary table.

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_84139ea1d8303ebbd775c5750efea7f9.png)

5. Click **Next step: Pre\-check**.

6. On the **Create a clear table ticket** **Ticket pre\-check** configuration wizard page, you can perform the following operations based on the inspection results:

   * Click **View details** in the **Results details** column of the check item to view detailed alarms or failures. Modify the relevant information based on the error message and resubmit the ticket. For details about the pre\-check, refer to Pre\-check items.

   * Click **Ignore** in the **Inspection results are negligible** column to dismiss this alarm and proceed with ticket creation.

      > **tip**

      > Ignoring alerts may impact instance performance and cause IO fluctuations. It is recommended to modify parameters before creating a ticket.

7. Click **Submit ticket**.

## Next steps

[Manage clear table tickets](https://docs.byteplus.com/en/docs/DBW/Manage_clear_table_tickets?lang=en)
