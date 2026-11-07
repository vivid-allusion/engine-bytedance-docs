---
title: "Database audit"
product: "Database Workshop"
product_code: "DBW"
source: "https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-PG"
---

This topic describes how to manage audit logs on the Database Workshop (DBW) console, including enabling, querying, and disabling audit logs.

> **tip**

* > Currently, there are database audit (new) and Database audit (old) in DBW. The old database audit (V1) is served and charged by Log service TLS, and the new database audit (V2) is served and charged by DBW. For more fee information, see [PostgreSQL Billing items and prices](https://docs.byteplus.com/en/docs/DBW/postgresql-billing-items-and-price).

* > Compared with the old database audit, the new database audit has lower fees, richer indicators, and more convenient operations. Currently, only the old database audit is maintained, and it is no longer supported to enable the old database audit. It is recommended that you use the new database audit.

**Database audit (new)**

Database audit (new) is fully aligned with the SQL audit function in SQL insights and auditing. To avoid functional duplication, the database audit tab will be removed and only the SQL insights and auditing tab will be retained.

For more information about database audit (new), see [SQL insights and auditing](https://docs.byteplus.com/en/docs/DBW/SQL_insights_and_auditing).

**Database audit (old)**

## Prerequisite

* [Log service](https://www.byteplus.com/en/product/tls) is enabled.

* DBW is authorized to access Log Service. For detailed steps, refer to [Permission management](https://docs.byteplus.com/en/docs/DBW/managing-permissions-of-a-main-account#.5o6I5p2D5pWw5o2u5bqT5bel5L2c5Y-wLWRidy3orr_pl67ml6Xlv5fmnI3liqEtdGxz).

* An instance for RDS for PostgreSQL has been created, and the instance status is running. For detailed steps, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

* If the target instance has security control enabled, you need to apply for operation and maintenance read\-only or read/write permissions for the current account. For more information, refer to [Enabling instance security control (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/enabling-security-control), and [Applying for operation permissions (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DBW/Create_operation_permission_ticket).

## Precautions

|**Type** |**Precautions** |
|---|---|
|Enable audit logs |* Audit data will be stored by Log Service.<br><br>* When audit is enabled, a **Log topic** is created by default in the **Log project** available in Log Service to store the audit logs of this instance. If no **Log project** is available, a **Log project** is created first. Do not delete the **Log project** and **Log topic** involved in the audit function in Log Service. Otherwise, the function is unavailable.<br><br>* Billing rules<br><br>   * Collection fee: Log collection is free during the promotion period. After the promotion period, fees will be charged based on the amount of logs collected. For details, refer to [Billing rules](https://docs.byteplus.com/en/docs/DBW/billing-description) for DBW.<br><br>   * Storage fee: Each instance has 5 GiB of free storage space during the promotion period, and corresponding fees will be charged for exceeding this amount. For details, refer to [Billing rules](https://docs.byteplus.com/en/docs/tls/Billing_items_based_on_pay-by-feature_mode) for Log Service.<br><br>   * DBW does not support collecting audit logs while SSL connection is enabled for the database.<br><br>* When a database instance is deleted, the audit function of the instance is forcibly disabled. After you disable this function, the maximum retention period of audit logs will be based on the Audit log retention period you set. Log service will continue to be charged during this period, and you can also delete the logs in the Log Service in advance.<br><br>* Audit logs can not be collected while SSL is enabled for the instance. |
|Query audit logs |* During the promotion period, you can view audit logs within the past 30 days for free. If you have other requirements, you can modify them in the **Log topic**. For detailed steps, refer to [Modifying log topic configurations](https://docs.byteplus.com/en/docs/tls/Managing_topics). After the promotion period, there will be a limit on the query time.<br><br>* You can download the queried logs and export them in tables with the CSV format.<br><br>* Operations such as deleting databases or users performed in the database engine console are not recorded in the SQL Audit of DBW; only operations performed through the DBW console are recorded. |
|Download audit logs |* A maximum of 1 million data entries can be exported at a time.<br><br>* Audit log download tasks are retained for 1 day by default. Expired tasks will be automatically deleted. The obtained download link is valid for 5 minutes. Download the audit logs in time after obtaining the link. |
|Disable audit logs |* After you disable this function, the maximum retention period of audit logs will be determined by the **Audit log retention period** you set. Audit logs will continue to be charged during this period, and you can also delete the logs in Log Service in advance.<br><br>* After you disable this function, the free quota of the Log service will be invalid. |
|Others |When a database instance is deleted, the audit function of the instance is forcibly disabled. After you disable this function, the maximum retention period of audit logs will be based on the Audit log retention period you set. Log service will continue to be charged during this period, and you can also delete the logs in the Log Service in advance. |

## Enable audit logs

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management \> Observation and diagnosis**.

4. To switch to the target instance on the Operations observability page, perform the following:

   1. In the upper right corner of the page, click the drop\-down icon and switch the instance type to **RDS for PostgreSQL**.

   2. In the upper left corner of the Operations observability page, click the drop\-down icon and switch to the target instance.

5. On the target instance page, click **Database audit**.

6. Optional. On the **Database audit** tab, click **Click to enable** to activate the log service.

   > **tip**

   > Before enabling the audit log feature, you need to activate the log service TLS. You can skip this step if the authorization has been granted.

7. Optional. Authorize DBW to access the log service.

   > **tip**

   > Before enabling the audit log feature, you must authorize DBW to access BytePlus Log Service (TLS). You can skip this step if the authorization has been granted.

   1. On the **Database audit** tab, click **Click authorize**.

   2. In the **Are you sure to authorization?**  dialog box, click **OK** to authorize DBW to access Log Service.

      > **tip**

      > Logs can be successfully written to Log Service only after successful authorization.

8. In the **Enable audit** dialog box, read the precautions carefully and configure the following information:

   ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_73b75a530c0e7af6e138a6296a4e0236.png)

|**Parameter** |**Description** |
|---|---|
|**Audit log retention period** |Currently, retention for **1 day**, **7 days**, **30 days** (default), **180 days**, **1 year**, or **3 years** is supported. If you have other duration requirements, after enabling this function, you can click **View log topic** on the **Database audit** tab to modify the log storage duration. |
|**Tag** |Tags are used to mark resources to facilitate searching and resource aggregation. Click the edit icon after the tag to set the tag key and tag value to add a tag for the instance. The configuration rules for tag keys and tag values are as follows:<br><br><br>* Setting a key that starts with any form of `volc:` is not supported, such as `Volc:` and `VOLC:`.<br><br>* It can contain language characters, number, spaces, and English symbols, including `_`, `.`, `:`, `/`, `=`, `+`, `-` and `@`.<br><br>* The length must be between 1 and 128 characters.<br><br>* Use the Unicode format encoded with UTF\-8.<br><br><br>> **tip**<br><br><br><br>* > Each time, you can bind up to 20 tags, and each instance can bind up to 50 tags. To centrally manage tags, refer to [Tag management](https://docs.byteplus.com/en/docs/6649/189377).<br><br><br>* > The tag keys of the same resource can not be repeated, and one tag key can only have one value.<br> |
|**Data retention policy** |Optional. Select whether to delete the corresponding Log Service topic and clear the historical data when deleting the instance. |
|**Agreement** |Read and check **I have read and agree to Database Workshop (DBW) terms of service**. |

9. Click **Enable audit**.

## Query audit logs

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management \> Observation and diagnosis**.

4. To switch to the target instance on the Operations observability page, perform the following:

   1. In the upper right corner of the page, click the drop\-down icon and switch the instance type to **RDS for PostgreSQL**.

   2. In the upper left corner of the Operations observability page, click the drop\-down icon and switch to the target instance.

5. On the target instance page, click **Database audit**.

6. On the **Database audit** tab, filter target logs.

   You can filter by date, **Database name**, or **Table name**, or click **Advanced filtering** for finer\-grained filtering. The following table describes the details.

   |**Filter items** |**Description** |
   |---|---|
   |Date |During the promotion period, you can view the audit logs of the past 30 days for free. After the promotion period, you can only view the audit logs of the past 1 day for free. If you have other needs, you can click **View log topic** in the upper right corner of the tab to modify the log retention time. |
   |Database name |Select the target database from the drop\-down list as needed. Multiple selections are supported. |
   |Table name |Select the target table as needed from the drop\-down list. Multiple selections are supported. |
   |Username |Select the user as needed from the drop\-down list. Multiple selections are supported. |
   |Client IP |Select one or more client IPs from the drop\-down list as needed. |
   |Log level |Select the log level as needed from the drop\-down list, supporting multiple selections. The currently supported log levels are `normal`, `warning`, and `incident`. |
   |Execution time |Set the execution duration as needed, in milliseconds (ms). |
   |Rows affected |Set the execution rows as required. |
   |Log type |Select the target log type from the drop\-down list, supporting multiple selections. The supported log types are as follows:<br><br><br>* `normal`: Includes logging in to and out of the database, creating a database, creating a table, modifying a table, creating a view, modifying a view, creating an index, creating a stored procedure, modifying a stored procedure, creating a function, modifying a function, creating a trigger, modifying a trigger, creating an event, modifying an event, executing a stored procedure, executing a function, querying a table, querying a table (system table), inserting data, deleting data, and other operations.<br><br>* `warning`: Includes modifying a database, deleting a view, modifying an index, deleting a stored procedure, deleting a function, deleting a trigger, deleting an event, performing a full table query, updating table information, and performing a large\-scale table query.<br><br>* `incident`: Includes deleting a database, deleting an index, deleting a table, updating system table information, inserting data (system table), deleting data (system table), performing a full table deletion, performing a large\-scale table deletion, performing a full table update, performing a large\-scale table update, and truncating a table.<br><br><br>> **tip**<br><br><br>> A `warning` level is also assigned when a large number of rows are affected for some reason, and the affected data exceeds 500 rows and 10% of the table data.<br> |
   |SQL type |Select the SQL type you want to query from the drop\-down list. |

7. Click **Query**.

After successful filtering, you can view the target log information in the **Audit log list** area. You can also perform the following operations:

* To view the specific executed statements in the logs: Click the copy icon in the **SQL statement** column of the target log to view the specific executed statement.

* Download logs: Click the download icon. In the **Export current page** dialog box, select the log information to be exported as needed.

## Download audit logs

1. Export files.

   1. Log on to the [DBW console](https://console.byteplus.com/dbw).

   2. On the top menu bar, select the region.

   3. On the left navigation bar, select **Operation and maintenance management \> Observation and diagnosis**.

   4. To switch to the target instance on the Operations observability page, perform the following:

      1. In the upper right corner of the page, click the drop\-down icon and switch the instance type to **RDS for PostgreSQL**.

      2. In the upper left corner of the Operations observability page, click the drop\-down icon and switch to the target instance.

   5. On the target instance page, click **Database audit**.

   6. On the **Database audit** tab, filter the target logs as needed, and then click the download icon to select the log range to be exported, as shown below:

      ![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_699327a35382a00ac20665540407b232.png)

      * **Export current page**: In the **Export logs on current page** dialog box, select the log to be exported as needed, and then click **OK**. The system will generate a CSV table.

      * **Export all logs**: In the **Export audit logs** dialog box, configure the relevant parameter information, as shown in the following table. Then, click **OK**. The system will generate a file based on the file format you select.

         |**Parameter** |**Description** |
         |---|---|
         |**File format** |Select the format for downloaded logs. Currently, **CVS** and **JSON** formats are supported. |
         |**Export range** |Select a log range to export as needed. The system supports **Custom**, **Past 2 hours**, **Past 12 hours**, and **Past 24 hours**. |
         |**Custom time period** |Select the time range for log export.<br><br>> **tip**<br><br><br>> This parameter can be set when **Export range** is set to **Custom**.<br> |

2. Download files

   After exporting the file, select a method to download the logs based on the export type, as shown below:

   * **Export current page**: After the audit logs on the current page are exported, the system will generate a CSV table on your computer. You don't need to download it again.

   * **Export all logs**: For audit logs that are exported on demand, you need to download them before you can view the specific log information. The specific steps are as follows:

      1. On the **Audit log** tab, click the download icon, and then select **Export history**.

      2. In the **Export history** dialog box, select the target task whose **Status** is **Generated**, and click **Download file** in the **Actions** column.

## Set audit logs

1. Log on to the [DBW console](https://console.byteplus.com/dbw).

2. On the top menu bar, select the region.

3. On the left navigation bar, select **Operation and maintenance management \> Observation and diagnosis**.

4. To switch to the target instance on the Operations observability page, perform the following:

   1. In the upper right corner of the page, click the drop\-down icon and switch the instance type to **RDS for PostgreSQL**.

   2. In the upper left corner of the Operations observability page, click the drop\-down icon and switch to the target instance.

5. On the **Database audit** tab of the target instance, click **Service settings**.

6. In the **Service settings** dialog box, configure the following parameters.

   |**Parameter** |**Description** |
   |---|---|
   |Disable database auditing |1. Click **Close**.<br><br>2. Select **Delete log topic?**  as needed. If you do not delete the audit logs, they will be retained based on the audit log retention period you set. You will be charged for audit logs during this period. If you delete the audit logs, the historical data will be cleared, the log service storage space will be released, and you will not be continuously charged for the Log service. |
   |Set tag |Tags are used to mark resources to facilitate searching and resource aggregation. Click the edit icon after the tag to set the tag key and tag value to add a tag for the instance. The configuration rules for tag keys and tag values are as follows:<br><br><br>* Setting a key that starts with any form of `volc:` is not supported, such as `Volc:` and `VOLC:`.<br><br>* It can contain language characters, number, spaces, and English symbols, including `_`, `.`, `:`, `/`, `=`, `+`, `-` and `@`.<br><br>* The length must be between 1 and 128 characters.<br><br>* Use the Unicode format encoded with UTF\-8.<br><br><br>> **tip**<br><br><br><br>* > Each time, you can bind up to 20 tags, and each instance can bind up to 50 tags. To centrally manage tags, refer to [Tag management](https://docs.byteplus.com/en/docs/6649/189377).<br><br><br>* > The tag keys of the same resource can not be repeated, and one tag key can only have one value.<br> |

7. Click **Close**. Operations such as deleting databases or users performed in the database engine console are not recorded in the SQL Audit of DBW; only operations performed through the DBW console are recorded.
