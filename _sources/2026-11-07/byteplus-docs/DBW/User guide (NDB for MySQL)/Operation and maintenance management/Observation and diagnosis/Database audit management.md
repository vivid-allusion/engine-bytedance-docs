---
title: "Database audit management"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/Database_audit_management"
---

This topic describes how to manage audit logs on the Database Workshop (DBW) console, including enabling, querying, and disabling audit logs.

## Background

DBW provides V1 and V2 versions of the database audit feature. The following table shows information about two versions.

**V2 (Recommended)**

* **Fee**: DBW will provide you with a free 1\-day usage period for the V2 version of data audit. For billing information on the database audit, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/DBW/billing-items-and-price).

* **Audit log storage method**: Audit data is stored by DBW.

* **Function**: Supports more metrics than the V1 version, and the operation is simpler. At the same time, more new functions have been added. For details, refer to [Querying audit logs](https://docs.byteplus.com/en/docs/DBW/Database_audit_management#.5p-l6K-i5a6h6K6h5pel5b-X).

* **Delete an instance**: When a database instance is deleted, the audit function of the instance is forcibly disabled, and the audit logs of the database instance are also deleted.

* **Download audit logs**:

   * A maximum of 1 million data entries can be exported at a time.

   * Audit log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted. The obtained download link is valid for 5 minutes. Download the audit logs in time after obtaining the link.

**V1**

* **Fee**: The fees for V1 are as follows:

   * Collection fee: Log collection is free during the promotion period. After the promotion period, fees will be charged based on the amount of logs collected. For details, refer to [Billing rules](https://docs.byteplus.com/en/docs/DBW/billing-description) for DBW.

   * Storage fee: Each instance has 5 GiB of free storage space during the promotion period, and corresponding fees will be charged for exceeding this amount. For details, refer to [Billing rules](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode) for Log Service.

* **Function**: Supports basic audit metrics and exporting audit logs.

* **Audit log storage method**: Audit data is stored by Log Service. When audit is enabled, a **Log topic** is created by default in the **Log project** available in Log Service to store the audit logs of this instance. The naming format of the audit logs is `rds-sql-audit-****`. If no **Log project** is available, a **Log project** is created first. Do not delete the **Log project** and **Log topic** involved in the audit function in Log Service. Otherwise, the function is unavailable.

* **Delete instance**: When a database instance is deleted, the audit function of the instance is forcibly disabled. After you disable this function, the maximum retention period of audit logs will be based on the Audit log retention period you set. Log service will continue to be charged during this period, and you can also delete the logs in the Log Service in advance.

* **SQL storage duration**: During the promotion period, you can view audit logs within the past 30 days for free. If the V1 version of the database audit has other requirements, you can modify it in the **Log topic**. For detailed steps, refer to [Modifying log topic configurations](https://docs.byteplus.com/en/docs/tls/Managing_topics).

* **Download audit logs**:

   * A maximum of 1 million data entries can be exported at a time.

   * Audit log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted. The obtained download link is valid for 5 minutes. Download the audit logs in time after obtaining the link.

## Prerequisite

**Enable V2 prerequisites**

* A NDB for MySQL instance has been created, and the instance status is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For details, refer to [ ](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[ ](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)and [Apply for operation permissions for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).

**Enable V1 prerequisites**

> **tip**

> You can enable V1 audit logs in Hong Kong, China. If you need to enable them in other regions, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.

* Torch Log Service (TLS) is enabled. For detailed steps, refer to [Torch Log Service](https://www.byteplus.com/en/product/tls).

* DBW is authorized to access Log Service.

* A veDB for MySQL instance has been created, and the instance status is Running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Creating_an_instance_1).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For details, refer to [Enable security control for NDB for MySQL instances](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)[ ](https://docs.byteplus.com/en/docs/DBW/Enabling_security_control)and [Apply for operation permissions for NDB for MySQL](https://docs.byteplus.com/en/docs/DBW/Creating_an_operation_permission_ticket).

## Precautions

**V2 Precautions**

* Operations such as deleting databases or users performed in the database engine console are not recorded in DBW SQL Audit; only operations performed through the DBW console are recorded.

* Supports recording audit logs under SSL connections.

* Since the V2 version of database audit information includes all the SQL details recorded in the full SQL insight, when the V2 version of database audit is enabled, the SQL details of the full SQL insight are enabled by default. Conversely, when the V2 version of database audit is disabled, the details of the full SQL insight are also disabled synchronously.

* When the SQL record of the database audit exceeds 8K, the V2 of the kernel truncates the SQL information. After truncation, the table name and SQL fingerprint cannot be parsed normally.

* Database audit counts all DQL, DML, and DDL operation records, which are obtained by the database kernel analysis. Therefore, data may be inaccurate.

* Audit logs do not parse actual parameter values, and a small number of records may be lost when the SQL query volume is large. Therefore, there may be inaccuracies in the way incremental data is collected.

* Although database audit has verified the data integrity of the open\-source standard MySQL Driver, if a third\-party tool is used or the Driver is modified, some statements may be incomplete due to network protocol compatibility issues.

* The system downloads database audit files compressed in the .gz (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

   * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

   * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.

* Storage resources

   * Storage location: DBW provides storage for audit data, so it does not occupy the storage capacity of the database instance itself.

   * Hierarchical storage policy

      Audit logs beyond the standard retention period are automatically moved to infrequent access storage:

      * Infrequent access storage is much cheaper than standard storage. It is designed for long\-term archiving and historical logs that are rarely accessed.

      * While there may be minor Retrieval fees when accessing the data, the total cost remains far lower than maintaining it in standard storage over the long term.

      * Ensures data accessibility while effectively lowering long\-term storage expenses.

* After database audit is enabled, to view SQL statements that miss indexes through audit logs, you must enable both the `log_queries_not_using_indexes` parameter and the `slow_query_log` parameter of the instance, and set both parameters to `ON`.

**V1 Precautions**

* Operations such as deleting databases or users performed in the database engine console are not recorded in DBW SQL Audit; only operations performed through the DBW console are recorded.

* Audit logs do not record the `Prepare` and `Close` operations in the pre\-processing protocol.

* Database audit collects all DQL, DML, and DDL operation records. These operation records are obtained by the system through network protocol analysis. Therefore, inaccurate data may occur.

* Audit logs do not parse actual parameter values, and a small number of records may be lost when the SQL query volume is large. Therefore, there may be inaccuracies in the way incremental data is collected.

* Although database audit has verified the data integrity of the open\-source standard MySQL Driver, if a third\-party tool is used or the Driver is modified, some statements may be incomplete due to network protocol compatibility issues.

* Recording audit logs under SSL connections is not supported.

* Due to the specific design of the database audit mechanism, database audit only counts the source IP of newly established connections after the function is enabled. To enable existing sessions to have a complete source IP audit, it is recommended that you terminate existing connection sessions and trigger automatic reconnection. This ensures that the source IP of all sessions can be accurately recorded and audited, thereby improving database security and traceability.

* The system downloads database audit files compressed in the .gz (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

   * Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

   * To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.

## Billing

For billing information on the database audit, refer to [Billing items and prices](https://docs.byteplus.com/en/docs/DBW/billing-items-and-price).

## Enable audit logs

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to cloud database NDB MySQL edition.

5. In the upper\-left corner of the **Observation and diagnosis** page, click the drop\-down icon to select the target instance.

   > **tip**

   > You can also switch to the target instance by searching for the instance ID.

6. On the target instance page, click **Database audit**.

7. On the **Database audit** page, enable database audit of different versions as needed.

   **V2**

1. On the **Select audit version** configuration wizard, select **Audit V2 version**.

   2. Click **Next step**.

   3. On the **Configure function settings** wizard page, configure the following information:

      |**Parameter** |**Description** |
      |---|---|
      |**Features to be enabled** |Check the box to enable the full SQL insight feature as needed. If the full SQL insight feature is checked, the full SQL insight feature of the instance will be enabled synchronously. If the full SQL insight feature is not selected, only the SQL details function of the full SQL insight is enabled by default. Because the SQL details of the full SQL insight are database audit\-related information. |
      |**Standard storage duration** |Select the retention period for Audit V2 version logs as needed. Currently supported options are **1 day** (default), **7 days**, **30 days**, **180 days**, **1 year**, or **3 years**. A custom retention period is also supported, with a maximum of 1095 days.<br><br>> **tip**<br><br><br>> The storage space for SQL data is provided by DBW and does not occupy the storage space of the database instance.<br> |
      |**Infrequent\-access storage** |Enable infrequent\-access storage for instances on demand to optimize storage costs. The low\-frequency storage duration feature allows infrequently accessed but undeletable data to be stored securely at a lower cost, achieving a balance between cost and performance.<br><br><br>* Disabled: If disabled, DBW will clear SQL audit logs that exceed the standard storage duration. It is recommended to download and save SQL audit logs locally for future queries.<br><br>* Enabled: If enabled, DBW will transfer SQL audit logs exceeding the standard storage duration to low\-frequency storage. Data in low\-frequency storage will have reduced retrieval efficiency. |
      |**Infrequent\-access retention period** |Set the infrequent\-access retention period as needed. Currently, you can select **30 days** (default), **60 days**, **90 days**, **180 days**, **1 year**, or **3 years**. You can also customize the infrequent\-access retention period, up to 3648 days. |
      |**SQL storage duration** |The default storage duration for SQL data is the standard storage duration plus the infrequent\-access storage duration. The maximum storage period supported by the system is 3650 days. This upper limit is fixed and cannot be modified. |
      |**Storage SQL type** |Select **`SELECT`**, **`INSERT`**, **`UPDATE`**, **`DELETE`**, **`ALTER`**, **`CREATE`**, **`DROP`**, **`RENAME`**, **`TRUNCATE`**, and **`OTHER`** (all other SQL types) as needed. |
      |**Tag** |Tags are used to mark resources to facilitate searching and resource aggregation. You can add tags to the SQL insight and auditing feature of an instance in the following two ways:<br><br><br>* Manual addition: Click the pen icon, and in the **Edit tag** dialog box, set the tag key and tag value. Configuration must follow the rules below:<br><br>   * Naming restrictions: Tag keys cannot start with `volc:` (case\-insensitive, such as `Volc:`, `VOLC:`, etc. are not allowed).<br><br>   * Character support: Supports uppercase and lowercase letters, numbers, spaces, and specific English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, `@`).<br><br>   * Length limit: Must be between 1 and 128 characters.<br><br>   * Encoding format: Supports Unicode in UTF\-8 encoding.<br><br>* Copy instance tag: Copies the current instance tags directly to the SQL audit fee tags. If the instance tags change later, the SQL audit fee tags are not automatically synchronized. You need to manually copy them again.<br><br><br>Click **Copy instance** tag. In the **Copy Instance Tag** dialog, click **Copy instance tag** to copy the instance tags to the SQL audit tags. If a tag key from the instance conflicts with an existing SQL audit fee tag, the conflicting item is skipped during copying, and only the remaining tags are copied.<br><br>> **tip**<br><br><br><br>* > Each time, you can bind up to 20 tags, and each instance can bind up to 50 tags. To centrally manage tags, refer to Tag management.<br><br><br>* > The tag keys of the same resource can not be repeated, and one tag key can only have one value.<br> |
      |**Agreement** |Read and check **I have read and agree to Database Workshop (DBW) terms of service**. |

   4. Click **Enable database auditing & SQL insights**.

   **V1**

> **tip**

   > You can enable V1 audit logs in Hong Kong, China. If you need to enable them in other regions, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.

   1. On the **Select audit version** configuration wizard, select **Audit V1 version**.

   2. Click **Next step**.

   3. On the **Configuration function** configuration wizard, click **Click to enable** to activate the log service.

      > **tip**

      > Before enabling the audit log feature, you need to activate the log service TLS. You can skip this step if the authorization has been granted.

   4. Optional. Authorize DBW to access the log service.

      > **tip**

      > Before enabling the audit log feature, you must authorize DBW to access BytePlus Log Service (TLS). You can skip this step if the authorization has been granted.

      4. On the **Database audit** tab, click **Click authorize**.

      5. In the **Are you sure to authorization?**  dialog box, click **OK** to authorize DBW to access Log Service.

      > **tip**

      > Logs can be successfully written to Log Service only after successful authorization.

   5. On the **Configuration function** configuration wizard, read the precautions carefully and configure the following information:

      1. **Audit log retention period**: Currently, retention for **1 day**, **7 days**, **30 days** (default), **180 days**, **1 year**, or **3 years** is supported. If you have other duration requirements, after enabling this function, you can click **View log topic** on the **Database audit** tab to modify the log storage duration.

      2. **Set tag**: Tags are used to mark resources for easy searching and resource aggregation. Click the edit icon after the tag to set the tag key and tag value to add a tag for the instance. The configuration rules for tag keys and tag values are as follows:

         * Setting a key that starts with any form of `volc:` is not supported, such as `Volc:` and `VOLC:`.

         * It can contain language characters, number, spaces, and English symbols, including `_`, `.`, `:`, `/`, `=`, `+`, `-` and `@`.

         * The length must be between 1 and 128 characters.

         * Use the Unicode format encoded with UTF\-8.

            > **tip**

            * > Each time, you can bind up to 20 tags, and each instance can bind up to 50 tags.

            * > The tag keys of the same resource can not be repeated, and one tag key can only have one value.

      3. **Data retention policy**: Optional. Select whether to delete the corresponding Log Service topic and clear the historical data when deleting the instance.

      4. **Agreement**: Read and check **I have read and agree to the Database Workshop (DBW) Terms of Service**.

   6. Click **Enable audit**.

## Query audit logs

When you query database audit information, you can only set any query start time within the SQL storage duration of the database instance and view up to 24 hours of data. To query SQL records in a larger time range, it is recommended that you export them before querying. The export function asynchronously exports logs and is suitable for queries within a large time range.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to cloud database NDB MySQL edition.

5. In the upper\-left corner of the **Observation and diagnosis** page, click the drop\-down icon to select the target instance.

   > **tip**

   * > You can also switch to the target instance by searching for the instance ID.

   * > When you access the **Database audit** tab through **Observation and diagnosis** on the left navigation bar, information about the first instance in the instance list is displayed by default.

6. On the target instance page, click **Database audit**.

7. On the **Database audit** tab, view the audit logs of the target version.

   If you have enabled both V1 and V2 versions of database audit, you can filter the audit logs of the target version as needed in the upper\-right corner of the page.

   **Audit V2**

You can filter by date, **Database name**, **Table name**, and node. You can also click **Advanced filtering** for more granular filtering. Some parameters are shown as follows.

   * **Date**: Set the time to query the audit logs as required. You can set any query start time within the SQL storage duration of the database instance, and view up to 24 hours of data. If you want to query SQL records in a larger time range, we recommend that you export the records and then query them. The export function asynchronously exports logs and is suitable for queries within a large time range.

   * **Execution time**: The response time (RT) of the public service area network. Set the execution duration as needed, in milliseconds (ms).

   **Audit V1**

You can filter by date, **Database name**, or **Table name**, or click **Advanced filtering** for more granular filtering. Specific parameter details are as follows.

   * **Date**: During the promotion period, you can view the audit logs of the past 30 days for free. After the promotion period, you can only view the audit logs of the past 1 day for free. If you have other needs, you can click **View log topic** in the upper right corner of the tab to modify the log retention time.

   * **Log level**: Select the log level as needed from the drop\-down list, supporting multiple selections. The currently supported log levels are `normal`, `warning`, and `incident`.

   * **Execution time**: The response time (RT) of the public service area network. Set the execution duration as needed, in milliseconds (ms).

   * **Log type**: Select the target log type from the drop\-down list, supporting multiple selections. The supported log types are as follows:

      * `normal`: Includes logging in to and out of the database, creating a database, creating a table, modifying a table, creating a view, modifying a view, creating an index, creating a stored procedure, modifying a stored procedure, creating a function, modifying a function, creating a trigger, modifying a trigger, creating an event, modifying an event, executing a stored procedure, executing a function, querying a table, querying a table (system table), inserting data, deleting data, and other operations.

      * `warning`: Includes modifying a database, deleting a view, modifying an index, deleting a stored procedure, deleting a function, deleting a trigger, deleting an event, performing a full table query, updating table information, and performing a large\-scale table query.

      * `incident`: Includes deleting a database, deleting an index, deleting a table, updating system table information, inserting data (system table), deleting data (system table), performing a full table deletion, performing a large\-scale table deletion, performing a full table update, performing a large\-scale table update, and truncating a table.

   > **tip**

   > A `warning` level is also assigned when a large number of rows are affected for some reason, and the affected data exceeds 500 rows and 10% of the table data.

8. Click **Query**. After successful filtering, you can view the target log information on the **Audit log list** pane, as follows:

   * The audit log details for V2 and V1 are as follows:

      * **Common metrics for V2 and V1**: Username, database name, table name, SQL statement, SQL type, rows affected, log level, client IP, and log type.

      * **Exclusive metrics for V2**: Execution time, SQL time (ms), execution result, node name, session ID, CPUTime, RowLockWaitTime, MDLWaitTime, LatchWaitTime, TRXCommitTime, CCLWaitTime, SocketSendTime, ThreadScheduleTime, ThreadWaitTime, rows scanned, rows returned, bytes sent, logical page reads, number of pages read by IO, IO read pages, and number of disk temporary tables.

      * **Exclusive metrics for V1**: Generation time and execution time.

   * You can also perform the following operations:

      * To view the specific executed statements in the logs: Click the copy icon in the **SQL statement** column of the target log to view the specific executed statement.

      * Download logs: Click the download icon to download the audit log information you need to export.

      * View SQL optimization suggestions: Click **SQL optimization** in the Actions column of the target log to view optimization suggestions. SQL optimization suggestions include the executed SQL statement, **Execution plan**, and **Optimization suggestions**, including **Index optimization** and **SQL rewrite**.

      > **tip**

      > If the **Automatic index creation** function has been enabled in AutoOps, DBW will automatically create an index for the current slow SQL based on the SQL optimization suggestions. For more information, refer to [Automatic index creation management](https://docs.byteplus.com/en/docs/DBW/Automatic_index_creation_management).

## Download audit logs

> **tip**

> The system downloads database audit files compressed in the .gz (Gzip) format. For macOS users, please extract the downloaded file using the steps below:

* > Decompress using the built\-in gzip or gunzip command\-line tools:Open the Terminal and run the gzip or gunzip commands provided by the system to extract the files. The command format is `gzip -d your_filename.gz` or `gunzip your_filename.gz`.

* > To decompress the file using the tar tool: Download and install the tar tool to decompress the file. The command format is `tar -xz --force-local -f file_name.gz`.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to cloud database NDB MySQL edition.

5. In the upper\-left corner of the **Observation and diagnosis** page, click the drop\-down icon to select the target instance.

   > **tip**

   > You can also switch to the target instance by searching for the instance ID.

6. On the target instance page, click **Database audit**.

7. In the upper\-right corner of the page, switch the database version to **Audit V1 version** or **Audit V2 version**.

   If you have enabled both V1 and V2 versions of database audit, you can filter the audit logs of the target version as needed in the upper\-right corner of the page.

8. On the **Audit log** tab, click the download icon and select a download type.

   **Export current page**

1. Click **Export current Page**.

   2. In the **Export data** dialog box, select the fields for which you want to download audit logs as needed.

   3. Click **OK**.

   **Export all logs**

1. Export logs

      1. Click **Export all logs**.

      2. In the **Export audit log** dialog box, configure the relevant parameter information, as shown in the following table.

               |**Parameter** |**Description** |
               |---|---|
               |**File format** |Select the format for downloaded logs. Currently, CSV and JSON formats are supported. |
               |**Export range** |Select a log range to export as needed. The system supports Custom, Past 2 hours, Past 12 hours, and Past 24 hours. |
               |**Custom time period** |Select the time range for log export. This parameter can be set only when you select Custom for the export range. |

      3. Click **OK**.

   1. Download logs

      1. On the **Database audit** tab, click the download icon, and then select **Export history**.

      2. In the **Export history** dialog box, select the target task whose **Status** is **Generated**, and click **Download file** in the **Actions** column.

## Disable V1 database audit logs

> **tip**

* > After you disable this function, the maximum retention period of audit logs will be based on the **Audit log retention period** you set. Audit logs will continue to be charged during this period, and you can also delete the logs in the Log service in advance.

* > After you disable this function, the free quota of the Log service will be invalid.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to cloud database NDB MySQL edition.

5. On the target instance page, click **Database audit**.

6. On the **Database audit** tab, switch the database version to **Audit V1 version**.

   1. On the **Audit log** tab, click **Disable database audit**.

   2. In the **Confirm deletion** dialog box, confirm **Delete log topic?** .

      If you do not delete the audit logs, they will be retained based on the audit log retention period you set. You will be charged for audit logs during this period. If you delete the audit logs, the historical data will be cleared, the log service storage space will be released, and you will not be continuously charged for the Log service.

   3. Click **OK**.

## Set audit logs

> **tip**

* > After you disable this function, the maximum retention period of audit logs will be based on the **Audit log retention period** you set. Audit logs will continue to be charged during this period, and you can also delete the logs in the Log service in advance.

* > After you disable this function, the free quota of the Log service will be invalid.

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management** \> **Observation and diagnosis**.

4. On the top menu bar in the upper\-right corner of the **Observation and diagnosis** page, switch the database type.

   Switch the database type to cloud database NDB MySQL edition.

5. On the target instance page, click **Database audit**.

6. On the **Database audit** tab, select the audit version to disable, and click **Service settings**.

7. In the **Service settings** dialog box, configure the following parameters:

   **V2**

|**Parameter** |**Description** |
   |---|---|
   |**Disable SQL insight and auditing** |When you disable SQL insights and auditing, you simultaneously disable database audit and full SQL insights.<br><br>> **tip**<br><br><br>> After you disable SQL insights and auditing, all stored data will be cleared. If necessary, download all data locally before it is cleared, otherwise it may result in data loss.<br> |
   |**Full SQL insight** |SQL insights and auditing includes two features: database audit and full SQL insight. In SQL insights and auditing, you can enable or disable the Full SQL insight feature as needed.<br><br><br>* Click **Enable** to enable the Full SQL insight feature.<br><br>* Click **Close** to disable the full SQL insight feature. Currently, only full SQL insight can be disabled separately. The database audit feature can not be disabled individually. When disabling full SQL insight, all stored data will be cleared. We recommend downloading the data locally before disabling it to avoid potential data loss.<br><br><br>> **tip**<br><br><br><br>* > After SQL insight is disabled, new data will not be collected and stored. Existing stored data will not be cleared immediately. DBW still cleans up SQL insight data according to the standard storage duration previously set.<br><br><br>* > Enabling or disabling full SQL insight will change the cost. For more information, see [Billing items and prices](https://docs.byteplus.com/en/docs/DBW/vedb-billing-items-and-price?lang=en).<br> |
   |**Standard storage duration** |Select the retention period for Audit V2 version logs as needed. Currently supported options are **1 day** (default), **7 days**, **30 days**, **180 days**, **1 year**, or **3 years**. A custom retention period is also supported, with a maximum of 1095 days.<br><br>> **tip**<br><br><br>> The storage space for SQL data is provided by DBW and does not occupy the storage space of the database instance.<br> |
   |**Infrequent\-access storage** |Enable infrequent\-access storage for instances on demand to optimize storage costs. The low\-frequency storage duration feature allows infrequently accessed but undeletable data to be stored securely at a lower cost, achieving a balance between cost and performance.<br><br><br>* Disabled: If disabled, DBW will clear SQL audit logs that exceed the standard storage duration. It is recommended to download and save SQL audit logs locally for future queries.<br><br>* Enabled: If enabled, DBW will transfer SQL audit logs exceeding the standard storage duration to low\-frequency storage. Data in low\-frequency storage will have reduced retrieval efficiency. |
   |**Infrequent\-access retention period** |Set the infrequent\-access retention period as needed. Currently, you can select **30 days** (default), **60 days**, **90 days**, **180 days**, **1 year**, or **3 years**. You can also customize the infrequent\-access retention period, up to 3648 days. |
   |**SQL storage duration** |The default storage duration for SQL data is the standard storage duration plus the infrequent\-access storage duration. The maximum storage period supported by the system is 3650 days. This upper limit is fixed and cannot be modified. |
   |**Storage SQL type** |Select **`SELECT`**, **`INSERT`**, **`UPDATE`**, **`DELETE`**, **`ALTER`**, **`CREATE`**, **`DROP`**, **`RENAME`**, **`TRUNCATE`**, and **`OTHER`** (all other SQL types) as needed. |
   |**Tag** |Tags are used to mark resources to facilitate searching and resource aggregation. You can add tags to the SQL insight and auditing feature of an instance in the following two ways:<br><br><br>* Manual addition: Click the pen icon, and in the **Edit tag** dialog box, set the tag key and tag value. Configuration must follow the rules below:<br><br>   * Naming restrictions: Tag keys cannot start with `volc:` (case\-insensitive, such as `Volc:`, `VOLC:`, etc. are not allowed).<br><br>   * Character support: Supports uppercase and lowercase letters, numbers, spaces, and specific English symbols (`_`, `.`, `:`, `/`, `=`, `+`, `-`, `@`).<br><br>   * Length limit: Must be between 1 and 128 characters.<br><br>   * Encoding format: Supports Unicode in UTF\-8 encoding.<br><br>* Copy instance tag: Copies the current instance tags directly to the SQL audit fee tags. If the instance tags change later, the SQL audit fee tags are not automatically synchronized. You need to manually copy them again.<br><br><br>Click **Copy instance** tag. In the **Copy Instance Tag** dialog, click **Copy instance tag** to copy the instance tags to the SQL audit tags. If a tag key from the instance conflicts with an existing SQL audit fee tag, the conflicting item is skipped during copying, and only the remaining tags are copied.<br><br>> **tip**<br><br><br><br>* > Each time, you can bind up to 20 tags, and each instance can bind up to 50 tags. To centrally manage tags, refer to Tag management.<br><br><br>* > The tag keys of the same resource can not be repeated, and one tag key can only have one value.<br> |

   **V1**

* Audit log retention period: Set the retention period of audit logs as required. You can select **1 day**, **7 days**, **30 days**, **180 days**, **1 year**, or **3 years**.

   * Set tag: Tags are used to mark resources for easy searching and resource aggregation. Click the edit icon after the tag to set the tag key and tag value to add a tag for the instance. The configuration rules for tag keys and tag values are as follows:

      * Setting a key that starts with any form of `volc:` is not supported, such as `Volc:` and `VOLC:`.

      * It can contain language characters, number, spaces, and English symbols, including `_`, `.`, `:`, `/`, `=`, `+`, `-` and `@`.

      * The length must be between 1 and 128 characters.

      * Use the Unicode format encoded with UTF\-8.

      > **tip**

      * > Each time, you can bind up to 20 tags, and each instance can bind up to 50 tags.

      * > The tag keys of the same resource can not be repeated, and one tag key can only have one value.

8. Click **OK**.
