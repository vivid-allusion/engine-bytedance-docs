---
title: "Synchronizing to Elasticsearch connected over public network"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Elasticsearch_connected_over_public_network"
---

This topic describes how to create a task for synchronizing MySQL connected over public network to Elasticsearch connected over public network on the Database Transmission Service (DTS) console.

## Prerequisites

* You have set up MySQL and Elasticsearch in a public network environment and created a database account.

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* The network connectivity and service availability of the source and destination have been confirmed.

* Optional. Check each synchronization object in the source and target databases according to the instructions in the pre\-check items. For more details, refer to [Pre-check items (MySQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql) and [Pre-check items (Elasticsearch)](https://docs.byteplus.com/en/docs/DTS/pre-check-items-elasticsearch).

## Precautions

* When the source database is a self\-managed RDS for MySQL, pay attention to the following information:

   * During synchronization, if the source database switches to the primary, the synchronization task will fail.

   * During synchronization, if the source database is restarted, the synchronization task will be temporarily interrupted and automatically attempt to recover. If the task does not recover for a long time, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

      > **tip**

      > If the synchronization object is the entire database, you can create a heartbeat table that is updated or written with data every second.

* During the database and table structure initialization, DTS synchronizes foreign keys from the source database to the target database.

* During full initialization and incremental synchronization, DTS temporarily disables constraint checks and foreign key cascade operations at the Session level. When the task runs, if the source database has cascade update or delete operations, data inconsistency may occur.

* During data synchronization, if duplicate primary keys or unique keys are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination. When a conflict overwrite occurs, if there is a table with the same name in the target database, it may cause data inconsistency issues or task failures as detailed below. It is recommended to use table name mapping or delete or rename the table with the same name in the target database to avoid data inconsistency and reduce business risks.

   * When the table structure is consistent, data from full synchronization overwrites records in the target table with the same primary key or unique key values as in the source database.

   * When the table structure is inconsistent, initialization of data may fail, and only partial column data can be synchronized or synchronization may fail.

* On the source end, if a database is not included in the synchronization objects, DDL operations can not be performed on databases that are included in the synchronization objects, or the synchronization task will fail.

* Do not perform frequent DDL operations on the same table, as repeated DDL operations may cause DTS metadata update failures and risk transmission interruptions. Method 1: In the console, DDL operations are spaced at least 1 to 3 seconds apart.

## Limits

### Application limits

|**Type** |**Description** |
|---|---|
|Source database limits |* Database version: MySQL 5.6, 5.7, and 8.0 instances are supported.<br><br>* When the source database instance version is 5.6 or higher, `gtid_mode` and `enforce_gtid_consistency` must both be set to `ON`.<br><br>   > **tip**<br>   <br><br>   > When the MySQL version is earlier than 8.0 and the parameter `gtid_mode` is disabled, foreign key cascading deletion may fail during data synchronization, resulting in data differences.<br>   <br><br>* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal synchronization performance.<br><br>* Supports the `InnoDB` database storage engine. `MariaDB` database engine is not supported currently.<br><br>* Tables to be synchronized must have a primary key or a unique non\-null constraint, and their fields must be unique. Otherwise, data inconsistency may occur.<br><br>* Binlog log parameter requirements:<br><br>   * The Binlog feature must be enabled, and the parameter `binlog_format` set to` row`, `binlog_row_image` set to `full`. Otherwise, pre\-check will report an error, and data synchronization tasks can not start successfully.<br><br>   * Binlogs must be retained for at least 24 hours, and a retention period of more than seven days is recommended. Otherwise, the DTS task may fail because it can not obtain the logs, potentially leading to data loss.<br><br>* It is recommended that the number of tables in a single task should not exceed 20,000, and the number of databases should not exceed 1,000. When a large number of databases and tables need to be synchronized, it is recommended to split them into multiple tasks.<br><br>* the source database does not support configuring multi\-node proxy addresses. during the incremental data synchronization phase, DTS needs to establish a stable long connection with a specific database instance. The load balancing or routing mechanism of multi\-node proxy may cause connection drift or log parsing failure. It is recommended to configure a single node connection address directly or use a database gateway (DG) for access. |
|Target database limits |Current support for the following instance versions:<br><br><br>* Elasticsearch instances: versions 6.7.1, 6.8.23, and 7.10.2.<br><br>* Opensearch instances: versions 2.9.0 and 3.3.0. |
|Other limits |* Prior to executing data synchronization, assess the performance of both source and target databases. It is also advised to perform synchronization during off\-peak business hours. Otherwise, during full data initiation, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* If the source database is RDS for MySQL 8.0, when configuring synchronization tasks, you must manually grant the relevant data synchronization permissions directly to the following accounts:<br><br>   * The accounts for the source database are granted relevant permissions through the Role.<br><br>   * The accounts that need to perform User synchronization are granted relevant permissions through the Role.<br><br>* Synchronization tasks only support synchronizing tables. |

### Operation limits

Currently, only synchronous DML statements are supported to be synced to Elasticsearch.

## Supported synchronization architectures

* One\-to\-one unidirectional synchronization

* One\-to\-many unidirectional synchronization

* Many\-to\-one unidirectional synchronization

For information on the types and usage of synchronization topology supported by DTS, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).

## Supported SQL operations

|**Operation type** |**SQL statement** |
|---|---|
|**DML** |INSERT, UPDATE, DELETE |

## Minimum database permission policy

|**Database** |**Schema initialization** |**Full initialization** |**Incremental synchronization** |
|---|---|---|---|
|Source database |`SELECT` permission |`SELECT` permission |`REPLICATION SLAVE`, `REPLICATION CLIENT`, and `SELECT` permissions. |
|Elasticsearch normal user |* Index: read, write, edit, and delete permissions<br><br>* Document: add, delete, modify, and query permissions |||

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, click **Create task**.

5. On the **Create synchronization task** page, locate the **Configure source and target database** wizard, and configure the following parameters information.

|**Type** |**Name** |**Description** |
|---|---|---|
|**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task name by default according to the naming rule, starting with `dts-`.<br> |
||**Link specification** |Select the link specifications for the synchronization task as needed **Compact**, **Medium**, and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br> |
||**Synchronization topology** |Select a synchronization topology based on your business needs. Only **Unidirectional synchronization** is currently supported.<br><br>> **tip**<br><br><br>> For more information about the synchronization topology, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).<br> |
|**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **MySQL**. |
||**Access method** |Select**MySQL connected over public network**.<br><br>> **tip**<br><br><br>> When synchronizing a MySQL connected over public network instance, add access permissions for the DTS IP range in the source's allowlist or security group policy in advance. Click **View DTS CIDR blocks** to view and copy the CIDR block.<br> |
||**region** |Select the region where the target instance is located. |
||**Host address** |Enter the host address of the target database's self\-managed instance. |
||**Port** |Enter the port number of the target self\-hosted instance. |
||**Database account** |Enter the database account of the target instance. |
||**Database password** |Enter the password corresponding to the database account of the target instance. |
||**Connection method** |Select an **Unencrypted connection** or **SSL\-secured connection** as needed to establish a more secure and reliable synchronization link.<br><br>> **tip**<br><br><br><br>* > When selecting **SSL secure connection**, you need to enable the SSL encryption feature of the **MySQL connected over public network** instance in advance.<br><br><br>* > Enabling SSL encryption on **MySQL** instances over public network may cause failure for a running synchronization **task** using an unencrypted connection.<br> |
||**SSL encryption certificate** |Click **Upload SSL encryption certificate** to upload the CA certificate. When the **Connection method** is set to **SSL\-secured connection**, this configuration is supported. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify your IP address. |
|**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **Elasticsearch**. |
||**Access method** |Select **Elasticsearch connected over public network**. |
||**Address** |Enter the host address of the target database's self\-managed instance. |
||**Database account** |Enter the database account of the target instance. |
||**Database password** |Enter the password corresponding to the database account of the target instance. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>> **tip**<br><br><br>> If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection.<br> |
|**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project.  <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |
||**Subscription duration** |Select the duration of the subscription as needed.<br><br>> **tip**<br><br><br>> When selecting **Subscription** in **Billing method**, you can set the purchase time and also check **Automatic renewal**. The system automatically renews before task expiration.<br> |

5. Click **Next: configure synchronization object**.

6. On the **Configure synchronization object** wizard page, configure the related parameter information as shown in the table below.

   > **tip**

   * > If you do not need to start the synchronization task immediately, click **Save** in the lower\-right corner of the page after configuring the synchronization object.

   * > After saving, you will be redirected to the **Synchronization task list** page. The task status will be **To be started**, and you can configure the synchronization task at a suitable time. For configuration methods, refer to [Configuring a synchronization task](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

   |**Name** ||**Description** |
   |---|---|---|
   |**Synchronization type** ||Select the synchronization type as needed. Currently, **Schema initialization**, **Full initialization**, and ** Incremental synchronization** are supported.<br><br>> **tip**<br><br><br><br>* > **Incremental synchronization** is selected by default.<br><br><br>* > When you select **Schema initialization** or **Full initialization**, after the pre\-check is completed, DTS will initialize the data of the objects to be synchronized from the source instance in the target instance, which serves as the basis for subsequent incremental data synchronization.<br> |
   |**Index concatenation rule** ||Select index concatenation rules as needed, supporting **Table name** and **Database name + Table name** options:<br><br><br>* **Table name**: When you select **Table name**, the index name created in the target Elasticsearch instance is the same as the table name.<br><br>* **Database name + table name**: When you select **Database name + table name**, the index name created in the target Elasticsearch instance is the database name + table name.<br><br><br>> **tip**<br><br><br>> After a synchronization task is successfully created, modifying the index concatenation rule will reset the names of the synchronization objects. Proceed with caution.<br> |
   |**Primary key conflict handling** ||Select the method to handle when the target database already has rows with the same primary key value. Currently, only ** Overwrite on conflict** is supported, which means using source database data to overwrite target database data, allowing the synchronization task to start normally. |
   |**Synchronization starting point** ||Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify GTID**: Enter the specified GTID in the input box, formatted as `source_id:transaction_id`.<br><br>* **Set GTID**_**EXECUTED**: Enter the specified GTID_EXECUTED in the input box, formatted as `source_id:transaction_id`. If multiple exist, separate them with commas (,). For how to obtain the instance's GTID_EXECUTED, refer to [How to obtain the GTID_EXECUTED of the instance](https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance).<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**.<br><br><br>> **tip**<br><br><br><br>* > When **Synchronization type** selects **Full initialization**, this step is not supported.<br><br><br>* > When **Synchronization type** selects both **Full initiation** and **Incremental synchronization**, the **Starting timestamp** defaults to the current time point and can not be modified.<br><br><br>* > GTID and GTID_EXECUTED must be legal values from the source end. Otherwise, pre\-check reports an error.<br><br><br>* > When selecting **Specify timestamp**, the time you set must be later than the earliest Binlog time on the source end. If there is no corresponding time Binlog, the closest Binlog starting point will be selected.<br> |
   |**Sync type selection** ||Select the operation types to synchronize. Currently, only **DML** statements are supported, which include `DELETE`, `Insert`, and `Update`. All DML operations are selected by default and can be adjusted as needed. |
   |**Whether to enable foreign key check?**  ||Select whether to enable foreign key check as needed. When enabled, the tool supports synchronizing cascading updates and deletes of foreign keys from the source, ensuring data integrity and consistency throughout the synchronization. |
   |**Synchronization object** ||Select the tables to synchronize. Meanwhile, you can perform the following actions in the **Selected object** area:<br><br><br>* Rename databases or tables: Click the pencil icon next to the target database or table to rename them, supporting query of target objects via **Normal search** and **Global search** methods. If the entire database is selected in the **Synchronization object ** area, only the database name can be modified in the **Selected object ** area, and the database cannot be expanded. Click **Batch mapping** to modify database or table names in bulk. For more information, refer to [Database and table batch mapping](https://docs.byteplus.com/en/docs/DTS/Database_and_table_mapping).<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets.<br><br>* Filter data in tables: Check **Filter data** enables filtering of data within the table.<br><br><br>> **tip**<br><br><br>> Regular expression search for target objects is supported in the **Synchronization object** or **Selected object** areas.<br> |
   |**Filter condition** ||Optional. Filtering data during a full data scan improves synchronization performance. Click the pen icon in the **Filter condition** column for the target database, table, or view, set the filter condition, then click **Verification statement** to validate the condition.<br><br>> **tip**<br><br><br><br>* > This feature is currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.<br><br><br>* > This field can be configured only if **Filter data** is selected for the **Synchronization object**'s database, table, or view.<br><br><br>* > Filter condition currently supported `=`, `!=`, <code><</code>, `>`, <code><=</code>, `>=`, `in`, `is null`, `and`, `or`.<br> |
   |**Database and table field configuration** ||Configure related information of the database and table fields. You can route documents to shards of the Elasticsearch instance as custom routing:<br><br><br>* **Type name**: You can customize the Type name. Click **Batch set Type name** to batch set Type names. Naming rules are as follows:<br><br>   * It can not contain English commas (, ) or symbols (#).<br><br>   * It can not start with an English period (.). It can not start with an underscore (_) except for (_doc).<br><br>   * The length must be within 255 characters, and the name must not contain blank characters at the beginning or end.<br><br>   > **tip**<br>   <br><br>   * > Currently, only ES instances of version 7.x and earlier support custom Type names. ES instances of version 8.x and later, as well as OpenSearch versions, do not support custom Type names.<br>   <br><br>   * > If the target index already exists, the Type name must be consistent with the custom name you set. Otherwise, schema migration fails.<br>   <br><br>* **Whether _routing**: Specify whether to enable custom routing mode. It also supports setting the _routing of multiple database names to yes or no.<br><br>   * **Yes**: You can custom route documents to shards in Elasticsearch.<br><br>   * **No**: Documents can only route to shards in Elasticsearch via `_id`.<br><br>*  **_routing column**: Customize indexing a document into an Elasticsearch shard. The default is `_id`.<br><br>*  **_id value**: Customize the document `_id` value. When selecting multiple fields to form `_id`, connect with underscores (_). |
   |**Advanced configuration** |**Enable ETL configuration** |Choose whether to enable the ETL function. For more information about ETL, refer to [Introduction to ETL](https://docs.byteplus.com/en/docs/DTS/brief_introduction_to_etl).<br><br><br>* **Yes**: indicates enabling ETL functions.<br><br>   * After enabling ETL rules, click **Quick configuration field mapping/filtering rules**, configure synchronization objects in the **Quick configuration field mapping/filtering rules** dialog box, and click **OK** to quickly generate ETL statements.<br><br>   * After enabling the ETL function, you can configure data processing ETL rules by referring to the [DSL syntax](https://docs.byteplus.com/en/docs/DTS/dsl_syntax). Enter the data processing ETL rules, i.e., the DSL script, in the **Enter ETL statements or use ETL assistant to generate statements...** text box, and click **Validate syntax** to verify whether the data processing statements are correct.<br><br>   * You can also use the ETL assistant to generate ETL statements in natural language. In the upper\-right corner of the ETL statement text box, click **ETL assistant** to input ETL requirements, and press Enter. After generating the ETL, copy the generated ETL statements into the ETL text box. The ETL assistant offers a variety of ETL statement generation capabilities. For more information, refer to [ETL assistant capabilities](https://docs.byteplus.com/en/docs/DTS/configuring_etl_in_dts_synchronization_task?lang=en#.5pSv5oyB55qE5pWw5o2u5bqT).<br><br>   * Click **Debug** to test the effects of the ETL rules you created. For details on debugging, refer to [Verifying ETL rules via ETL Playground tool](https://docs.byteplus.com/en/docs/DTS/debugging-ETL-rules-with-ETL-Playground-tool).<br><br>* **No**: indicates not enabling ETL functions. |
   ||**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |

8. Click **Data validation configuration**.

9. On the **Create synchronization task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   |**Parameter** |**Description** |
   |---|---|
   |**Data verification**<br><br> |Select whether to configure the data verification function directly when creating a synchronization task (built\-in).<br><br><br>* **Enable**: Configure data verification tasks directly when creating a data synchronization task.<br><br>* **Disable**: Do not configure data verification tasks when creating a data synchronization task. |
   |**Validation type**<br><br> |DTS automatically generates validation types based on the database type and synchronization type, and does not support modification. For more information on validation types, refer to [Background](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation#.6IOM5pmv5L-h5oGv). |
   |**Validation object** |Select the object to be verified. You can perform the following operations in the **Selected object** area:<br><br><br>* **Consistent with the synchronization task**: The object to be verified matches the object to be migrated, meaning all migration objects are verified.<br><br>* **Custom**: Select the object to be verified as needed. |
   |**Startup settings** |Configure the timing of data verification in the synchronization task.<br><br><br>* **Automatic start**: The data verification task starts automatically along with the progress of the synchronization task. Automatic start occurs when full synchronization (if any) is complete and the delay of incremental synchronization is 0.<br><br>* **Manually start**: The data verification task does not start automatically with the synchronization task progress. You must manually start the data verification at the appropriate time. It is recommended to manually start data verification only after full synchronization (if any) is complete and the delay of incremental synchronization is 0. Otherwise, verification results may be inaccurate. |
   |**Billing type** |Currently, only **Pay\-as\-you\-go** is supported and can not be modified. |

10. Click **Pre\-check**.

11. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the synchronization task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

12. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the synchronization task. You can also click **Ignore all** to ignore all alert messages with one click.

      > **tip**

         * > If you choose to **Ignore** the alert and start the migration task, it may cause data inconsistencies and business risks.

         * > For details about the pre\-check, refer to [Pre\-check items (RDS for MySQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql) and [Pre\-check items (Elasticsearch)](https://docs.byteplus.com/en/docs/DTS/pre-check-items-elasticsearch).

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. Select the configuration method according to the billing method of the task creation:

   * Pay\-as\-you\-go

      On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm order information** configuration wizard page, confirm the billing information of the task.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

      > **tip**

      > Once the **Payment is completed** on the configuration wizard page, a **Successful payment** message means your task has been created.

After successfully creating the data synchronization task, you can return to the DTS console to view the data synchronization task information on the data synchronization task list.

## Related APIs

|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
