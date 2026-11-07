---
title: "Configure data verification"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/configuring_data_validation"
---

This topic describes how to configure a data verification job in the Database Transmission Service Console to help you verify and check the different data between the source end and the destination without service interruption. This can help you identify data or schema inconsistencies in time.

## Background

The data verification task supports three methods for checking data discrepancies between the source and target ends: full data verification, full row verification, and schema verification. The specific differences between the three verification methods are shown in the following table:

|**Verification method** |**Full verification** |||**Schema verification** |**Increment verification** |
|---|---|---|---|---|---|
||**Content verification** |**Row verification** |**Primary key verification** |||
|**Description** |This verification method can compare all or part of the data content between two databases or data entities. The full data verification process can ensure data consistency, and the accuracy and integrity of the data are guaranteed. |The validation method can simply compare whether the total number of rows in the source database and the target database is the same. The verification method is fast and effective, and can quickly detect problems such as data loss or duplicate addition. |This verification method can verify whether the primary keys are consistent between the source and target. |This verification method can check the consistency of the data schema, such as whether the columns, data type, primary key, and index of the table are the same. This verification method ensures schema consistency between the source and target databases. |This verification method can verify whether all increment data at the source and target are consistent after the incremental task is enabled. |
|**Limits** |* If the table to be validated has no primary key and no unique index, DTS will not perform data validation.<br><br>* For MySQL\-to\-MYSQL single\-table data verification, DTS supports identifying up to 100,000 rows of differing data. If the number of differing rows exceeds 100,000, DTS will not perform data validation.<br><br>* For other types of databases, data validation for a single table supports identifying at most 100 rows of differing data; if the number of differing rows exceeds 100, DTS will not perform data validation.<br><br>* The default single table verification limit for PostgreSQL data verification task is 100 rows. If you need to verify more than 100 rows of data, [submit tickets](https://console.byteplus.com/workorder/create).<br><br>* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* If the table to be validated has no primary key and no unique index, DTS will not perform data validation.<br><br>* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* A maximum of 100 rows of different data can be verified in a single table. If this limit is exceeded, Database Transmission Service (DTS) will not perform data verification.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* Do not perform DDL operations on the source during the validation process, as this may result in inconsistent validation task results. |* A maximum of 10,000 different data entries can be verified.<br><br>* Data validation is not supported if ETL rules are configured in the data synchronization task.<br><br>* GTID is enabled for both the source and target database instances.<br><br>* Verification of tables without a primary key is not supported. |
|**Supported database types** |* MySQL<br><br>* veDB MySQL<br><br>* PostgreSQL<br><br>* MongoDB<br><br>* RDS for SQL Server<br><br>* Redis |* MySQL<br><br>* veDB MySQL<br><br>* MongoDB<br><br>* RDS for SQL Server<br><br>* PostgreSQL |* MongoDB |* MySQL<br><br>* veDB MySQL |* MySQL<br><br>* veDB MySQL<br><br>* MongoDB |

## Prerequisites

* A full migration task has been created, and its task status is in progress. For more information, refer to [Migration solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_migration_solutions).

* A full synchronization task has been created, and its task status is in progress. Refer to [Overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions) for detailed operations.

## Precautions

* Data verification objects can only be selected from the migration/synchronization objects, meaning only DTS migration/synchronization objects support data verification.

* If synchronization objects are deleted, data verification will not be deleted automatically. At this point, modifying the validation object no longer supports verification for that object.

* After modifying the target instance of a migration or synchronization task, existing data verification tasks may no longer be reusable. If a data verification task reports an error, create a new data verification task.

* The verification task starts verifying data only when the task completes full migration or full initialization.

* During full data verification, if the data undergoes frequent changes, it may lead to inconsistent task results. A second data verification task can be initiated.

* Before performing the verification task, you need to evaluate the source database and target database performance. It is recommended that you perform data verification during off\-peak hours (for example, the CPU load of the source database and target database is below 30%). Because DTS will occupy certain read resources of the source database and target database during data verification, which may cause the database load to increase. In the case of poor database performance, low specifications, or large business volume, it may increase the pressure on the database, or even cause the database service to be unavailable.

* For MySQL\-to\-MySQL single\-table data verification, DTS supports identifying up to 100,000 rows of differing data. If the number of differing rows exceeds 100,000, DTS will not perform data validation. Console page does not display Diff data; to view it, download the data locally. For detailed steps, refer to [Download verification result](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation?lang=en#.5LiL6L295pWw5o2u5qCh6aqM57uT5p6c). This feature is available on an allowlist basis. To use it, [Submit tickets](https://console.byteplus.com/workorder/create).

* The single table data verification feature from MySQL to MySQL displays up to 2,000 rows of difference data by default; the overall verification limit per table is 100,000 rows. Beyond this threshold, verification will be skipped automatically (no Diff results generated). The console page shows only partial diff data. To view the complete verification result, download the local file. For detailed steps, refer to [Download verification result](https://docs.byteplus.com/en/docs/DTS/viewing_data_validation?lang=en#.5LiL6L295pWw5o2u5qCh6aqM57uT5p6c). This feature is available on an allowlist basis. To use it, [Submit tickets](https://console.byteplus.com/workorder/create).

* In MongoDB data validation, the source database serves as the reference. The validation only checks whether the selected synchronized or migrated data from the source exists and is consistent in the target database; it cannot detect extra data present in the target database that is not in the source.

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration** or **Data synchronization**.

4. On the **Migration task list** or **Data synchronization list** page, select a path to configure data verification in the following ways:

   **Path 1: Configure a data verification task on the task list page**

1. In the upper\-right corner of the target migration or synchronization task, select **More operations** \> **Create data verification task**.

   2. In the **Create verification task** dialog box, configure the relevant parameters.

   **Path 2: Configure a data verification task on the data verification tab of the target task**

1. Click the target task name.

   2. On the target task page, click **Data verification**.

   3. On the **Data verification** tab, click **Create data verification**.

   4. In the **Create verification task** dialog box, configure the relevant parameters.

         |**Name** |**Description** |
         |---|---|
         |**Task name** |Custom task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task name by default according to the naming rule, starting with `dts-`.<br> |
         |**Validation type** |Select the verification method as required. Currently, **Full validation**, **Schema verification**, and **Increment validation** are supported. For more information on the verification method, refer to [Background](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation#.6IOM5pmv5L-h5oGv). |
         |**Verification method** |When the **Validation type** is **Full validation**, you can set the verification method. Currently, you can select **Sample content validation**, **Row verification**, and **Primary key validation**. |
         |**Sampling percentage** |Set the data sampling percentage to be verified as needed. The default value is 100, and the value range is [1,100]. It helps to improve efficiency, save resources, quickly identify problems, and improve the user experience when verifying large amounts of data.<br><br>> **tip**<br><br><br><br>* > This parameter can be configured only when **Validation type** is **Full validation** and **Verification method** is **Sample content validation**.<br><br><br>* > This feature is only applicable to MySQL data transmission tasks.<br> |
         |**Verification mode** |Select a verification mode from the drop\-down list as needed. Currently, **Compare key and value**, **Compare key only**, and **Compare the length of value only** are supported.<br><br>> **tip**<br><br><br>> Only Redis data transmission tasks support configuring this parameter.<br> |
         |**Validation object** |Select the object to be verified. You can perform the following operations in the **Selected object** area:<br><br><br>* Rename databases: Click the pencil icon next to the target databases to rename them. If you select entire databases in the **Validation object** area, you can only modify the database name in the **Selected object** area, and can not expand the database.<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object ** area supports fuzzy search to batch delete unwanted databases and tables.<br><br><br>> **tip**<br><br><br><br>* > Data verification objects can only be selected from the migration/synchronization objects, meaning only DTS migration/synchronization objects support data verification.<br><br><br>* > If new synchronization objects are added, data verification will not automatically add verification for the new objects by default. You can add validation objects manually if needed; if synchronization objects are deleted, data verification will not automatically delete them by default.<br> |
         |**Batch Count**<br><br> |Set the number of keys to process per batch as needed. The value range is 1 to 10,000, and the default value is 300.<br><br>> **tip**<br><br><br>> Only Redis data transmission tasks support configuring this parameter.<br> |
         |**Billing type** |Currently, only **Pay\-as\-you\-go** is supported and can not be modified. |
         |**Error retry time** |If a data verification task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86,400, in seconds (s). The default value is 600 seconds. |
         |**Full read rate**<br><br> |If the read rate is too high, it may affect the performance of the source database. You can appropriately adjust the migration rate based on the read and write pressure of the source and target databases.<br><br><br>* **Rows read per second**: Enable and set rows read per second as needed to prevent excessive read rate from affecting the performance of the source database. You can adjust the number based on the read and write pressure of the source and target databases. The default value is 100,000, and the value range is 1 to 100,000.<br><br>* **Verification task concurrency**: Set the concurrency of the data verification task as needed. This concurrency can improve the performance and efficiency of the data verification task, ensuring it completes quickly and stably. The default value is 8, and the valid range is 1 to 64.<br><br><br>> **tip**<br><br><br><br>* > Only tasks with instance types of MySQL, MongoDB, and PostgreSQL support setting the full read rate.<br><br><br>* > The full read rate can only be adjusted when the data verification has progressed to full validation.<br> |

5. Click **Pre\-check**.

6. On the create verification task page, perform the following actions based on the pre\-check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the verification task. You can also click **Ignore all** to ignore all alert messages with one click.

   > **tip**

   * > Selecting **Ignore** the alert and starting the verification task may result in verification failure.

   * > For more information about pre\-check, refer to [Pre\-check (Data verification)](https://docs.byteplus.com/en/docs/DTS/beta-pre-check-items-data-verification).

7. Click **Confirm order**.

## Subsequent operations

### Modify a data verification task

After a data verification task is created, you can configure the data verification task.

> **tip**

> The data verification tasks in the following states support configuration.

* > Increment validation task: The execution status of the verification task is **To be started** or **In progress**.

* > Other verification task types: The execution status of the verification task is**To be started**.

1. Log on to the [DTS console](https://console.byteplus.com/dts/).

2. On the top menu bar, select the project and region.

3. In the left\-side navigation pane, click **Data verification**.

4. On the **Data verification list ** page, click **Configure** in the **Actions** column for the target data verification task.

5. On the **Modify verification task** page, configure **Task name** and **Validation object**.

   |**Name** |**Description** |
   |---|---|
   |**Task name** |Custom task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task name by default according to the naming rule, starting with `dts-`.<br> |
   |**Sampling percentage**<br><br> |Set the data sampling percentage to be verified as needed. The default value is 100, and the value range is [1,100]. It helps to improve efficiency, save resources, quickly identify problems, and improve the user experience when verifying large amounts of data.<br><br>> **tip**<br><br><br><br>* > This parameter can be configured only when **Validation type** is **Full validation** and **Verification method** is **Sample content validation**.<br><br><br>* > This feature is only applicable to MySQL and Redis data transmission tasks.<br> |
   |**Verification mode** |Select a verification mode from the drop\-down list as needed. Currently, **Compare key and value**, **Compare key only**, and **Compare the length of value only** are supported. |
   |**Validation object** |Select the object to be verified. You can perform the following operations in the **Selected object** area:<br><br><br>* Rename databases: Click the pencil icon next to the target databases to rename them. If you select entire databases in the **Validation object** area, you can only modify the database name in the **Selected object** area, and can not expand the database.<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object ** area supports fuzzy search to batch delete unwanted databases and tables.<br><br><br>> **tip**<br><br><br><br>* > Data verification objects can only be selected from the migration/synchronization objects, meaning only DTS migration/synchronization objects support data verification.<br><br><br>* > If new synchronization objects are added, data verification does not automatically increase verification for the new objects by default; manual addition of verification objects is required if needed. If synchronization objects are deleted, data verification does not automatically delete them; when modifying verification objects, verification for those objects is no longer supported.<br> |
   |**Batch Count**<br><br> |Set the number of keys to process per batch as needed. The value range is 1 to 10,000, and the default value is 300.<br><br>> **tip**<br><br><br>> Only Redis data transmission tasks support configuring this parameter.<br> |
   |**Full read rate**<br><br> |If the read rate is too high, it may affect the performance of the source database. You can appropriately adjust the migration rate based on the read and write pressure of the source and target databases.<br><br><br>* **Rows read per second**: Enable and set rows read per second as needed to prevent excessive read rate from affecting the performance of the source database. You can adjust the number based on the read and write pressure of the source and target databases. The default value is 100,000, and the value range is 1 to 100,000.<br><br>* **Verification task concurrency**: Set the concurrency of the data verification task as needed. This concurrency can improve the performance and efficiency of the data verification task, ensuring it completes quickly and stably. The default value is 8, and the valid range is 1 to 64.<br><br><br>> **tip**<br><br><br><br>* > Only tasks with instance types of MySQL, MongoDB, and PostgreSQL support setting the full read rate.<br><br><br>* > The full read rate can only be adjusted when the data verification has progressed to full validation.<br> |

6. Click **Pre\-check**.

7. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the verification task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

8. On the create verification task page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the verification task. You can also click **Ignore all** to ignore all alert messages with one click.

   > **tip**

   * > Selecting **Ignore** the alert and starting the verification task may result in verification failure.

   * > For more information about pre\-check, refer to [Pre\-check (Data verification)](https://docs.byteplus.com/en/docs/DTS/beta-pre-check-items-data-verification).

9. Click **Confirm order**.
