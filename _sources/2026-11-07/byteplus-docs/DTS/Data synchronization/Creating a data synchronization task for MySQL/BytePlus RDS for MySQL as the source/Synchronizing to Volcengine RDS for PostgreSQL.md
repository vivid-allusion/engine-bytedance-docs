---
title: "Synchronizing to Volcengine RDS for PostgreSQL"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcengine_RDS_for_PostgreSQL"
---

This topic introduces how to create a MySQL connected over express network task synchronizing to Volcengine RDS for PostgreSQL in the Database Transmission Service (DTS) console.

## Prerequisites

* Set the source information as needed, as detailed below:

   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers?_vtm_=a106466.b106468.0_0.0_0.0.4652_7694130500017817107&lang=en).

   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network.   For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start?_vtm_=a106466.b106468.0_0.0_0.0.4652_7694130500017817107&lang=en#.6YWN572u5LiT57q_6L-e5o6l).

* An instance, a database, and an account for RDS for PostgreSQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance?_vtm_=a106466.b106468.0_0.0_0.0.4606_7694130500017817107&lang=en) and [Creating a database and an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts?_vtm_=a106466.b106468.0_0.0_0.0.4606_7694130500017817107&lang=en).

* When your instance connects via the express network, the subnet of the express network must communicate with the source or target database. To allow DTS to access instances in the express network normally, add the subnet CIDR block to the source or target database allowlist or security group rules. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server?_vtm_=a106466.b106468.0_0.0_0.0.4650_7694130500017817107&lang=en).

* Confirm the network connectivity and service availability of the source and target databases before creating a data synchronization task.

* Check each synchronization object on the source end and target end according to the instructions in the pre\-check items. for more details, refer to [pre-check items (MySQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql?lang=en) and [pre-check items (PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql?lang=en).

## Precautions

* **DDL restrictions**: confirm the ddl belongs to supported sql operations before execution; if an unsupported ddl enters the incremental link, the task will be Failed and the position will not surpass this event. For DDL operation statements supported by DTS during data synchronization, refer to [supported synchronized SQL operations](https://docs.byteplus.com/en/docs/DTS/Synchronize-to-volcano-engine-postgresql-for-express?TagIDs=2&lang=en#jKu2ArB0).

* **Synchronization objects and direction**:

   * Currently only supports creating unidirectional synchronization tasks.

   * Selectable synchronization objects: Supports selecting synchronization scope by MySQL database, table, and column.

   * Schema initialization objects: After choosing schema initialization, DTS synchronizes table structure objects within the supported range, such as primary keys, unique keys, ordinary indexes, CHECK constraints, foreign keys, and comments.

* **Data consistency and write recommendations**: tables without primary or unique keys support synchronization but do not guarantee exactly once (i.e., the same change may be applied multiple times or updates may be inaccurate); for businesses requiring high deduplication and precise updates, it is recommended to add primary or unique keys to the table.

* **Performance and resource evaluation**: For LONGTEXT, LONGBLOB, large transactions, or high write volume scenarios, evaluate synchronization time, network bandwidth, and destination disk usage first.

* **Name mapping**: Supports mapping source MySQL databases to destination PostgreSQL schema, as well as table name and column name mapping. If the source table's primary key or unique key columns are involved in column name mapping, the mapped target columns must still form a complete non\-null primary or unique key group.

* **high\-privilege account**: The target PostgreSQL database must be created before creating the synchronization task. When the target account has permission to create Schema, DTS can automatically create the mapped Schema in the connected target Database; if the account lacks this permission, manually create the target Schema before starting the synchronization task. DTS does not automatically create PostgreSQL Databases.

* When DTS replays the `CREATE TABLE` statement, it verifies the structure of the existing target table. Ensure that the target table's fields and data types meet the synchronization requirements. For source tables with primary or unique keys, the target table must have primary or unique keys formed by the same set of mapped columns, and all key columns must be non\-null; otherwise, DTS will reject incremental writes and the task will report an error.

## Limits

|**Type** |**Description** |
|---|---|
|Source database limits |* Database version: MySQL 5.7 and 8.0 instances are supported.<br><br>* Bandwidth requirement: The server hosting the source database must have sufficient outbound bandwidth; otherwise, synchronization speed will be affected.<br><br>* Instance ID: `server_id` must be greater than `0`.<br><br>* GTID requirement: When the source database version is `≥ 5.6`, both `gtid_mode` and `enforce_gtid_consistency` must be `ON`, or the task will fail to start.<br><br>* Binlog requirements:<br><br>   * Binlog must be enabled with `binlog_format` set to `row` and `binlog_row_image` set to `full`.<br><br>   * Retention time must cover full initialization, incremental synchronization catch\-up, and failure recovery time; otherwise, the task may fail or data may be lost. |
|Target database limits |* Database version: supports PostgreSQL versions 11 to 17.<br><br>* state and encoding: must be writable, UTF\-8 encoding is recommended.<br><br>* account privileges: to synchronize table, column, or index comments, the destination account must own the corresponding objects.<br><br>* resource reservation: reserve enough connections and disk space for full initialization and incremental catch\-up. |
|DDL usage restrictions |* Table structure initialization: schema initialization synchronizes supported foreign keys whose referenced objects are within the task scope; foreign keys that do not meet this condition must be handled according to compatibility rules. Target objects should be referred to as schema/table, not target database.<br><br>* Full/incremental process: the synchronization process does not disable foreign keys, triggers, or cascade behavior on the destination PostgreSQL by default. Existing constraints on the destination may cause write failures or alter execution results.<br><br>* creating/renaming tables:<br><br>   * For `CREATE TABLE` operations, when creating a synchronization task, select the entire database to which the new table belongs; otherwise, the new table will not be automatically added to the synchronization task.<br><br>   * for `rename table` operations, currently only single\-table renaming is supported. Both the original and renamed tables must fall within the synchronization objects of the task and must map to the same schema on the destination.<br><br>   * If `RENAME TABLE` involves objects like secondary indexes that cannot be safely converted, DTS will reject the operation.<br><br>* Unsupported online schema change tools: gh\-ost, pt\-online\-schema\-change, and their shadow tables, switch tables, and cleanup tables are not supported. If related DDL or DML operations enter the synchronization link, the destination will not execute the operation, the synchronization progress will not proceed, and the task will report an error at that operation. Do not use such online table alteration tools in the source database during task execution. |

## Supported synchronization architectures

* Unidirectional synchronization one\-to\-one: implemented by a single task.

* Unidirectional synchronization one\-to\-many: implemented by multiple independent tasks combined.

* Unidirectional synchronization many\-to\-one: implemented by multiple independent tasks combined.

* unidirectional synchronization cascading: implemented by chaining multiple independent tasks.

For information on the types and usage of synchronization topology supported by DTS, refer to Data synchronization topology.

## Supported SQL operations

|**Operation type** |**SQL statement** |
|---|---|
|**DML** |INSERT, UPDATE, DELETE |
|**DDL** |* **Create table:**  CREATE TABLE, where the default value supports literals and CURRENT_TIMESTAMP.<br><br>* **Modify column:** <br><br>   * ALTER TABLE ... ADD COLUMN<br><br>   * ALTER TABLE ... DROP COLUMN<br><br>   * ALTER TABLE ... MODIFY COLUMN<br><br>   * ALTER TABLE ... CHANGE COLUMN<br><br>   * ALTER TABLE ... ALTER COLUMN ... SET/DROP DEFAULT<br><br>* **Index:**  CREATE INDEX, DROP INDEX, ALTER TABLE ... ADD/DROP/RENAME INDEX<br><br>* **Key constraint:** <br><br>   * ALTER TABLE ... ADD/DROP PRIMARY KEY<br><br>   * ALTER TABLE ... ADD/DROP FOREIGN KEY<br><br>* **comment:**  supports table comments, column comments, and index comments.<br><br>* **drop and rename table:**  drop table, single\-table rename table.<br><br>* **other supported items:**  engine, row_format, lock, algorithm.<br><br><br>only the above ddl forms and compatible sub\-syntax are supported, which does not imply support for the full usage of create, alter, drop, rename statements. |

## Database account minimum permission policy

|**Database** |**Schema initialization** |**Full initialization** |**Incremental synchronization** |
|---|---|---|---|
|Source database |SELECT permission |SELECT permission |REPLICATION SLAVE, REPLICATION CLIENT, and SELECT permissions. |
|Target database |The target Schema must have permissions to create tables, modify tables, write data, and read metadata. To synchronize table, column, or index comments, ownership of the corresponding object is also required. |||

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Data synchronization list** page, click **Create task**.

5. On the **Create synchronization task** page, locate the **Configure source and target database** wizard, and configure the following parameters information.

|**Name** ||**Description** |
|---|---|---|
|**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task name by default according to the naming rule, starting with `dts-`.<br> |
||**Link specification** |Select the link specifications for the synchronization task as needed **Compact**, **Medium**, and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications?_vtm_=a106466.b106468.0_0.0_0.0.4567_7694130500017817107&lang=en).<br> |
||**Synchronization topology** |Select a synchronization topology based on your business needs. Only **Unidirectional synchronization** is currently supported.<br><br>> **tip**<br><br><br>> For more information about the synchronization topology, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology?_vtm_=a106466.b106468.0_0.0_0.0.4567_7694130500017817107&lang=en).<br> |
|**Source database configuration**<br><br> |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source?_vtm_=a106466.b106468.0_0.0_0.0.4567_7694130500017817107&lang=en).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **MySQL**. |
||**Access method** |Select **MySQL connected over express network**. |
||**region** |Select the region of the virtual private cloud. |
||**Host address** |Enter the host address of the MySQL instance connected over express network.<br><br>> **tip**<br><br><br>> Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br> |
||**Port** |Enter the port of the MySQL instance connected over express network. |
||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When synchronizing a MySQL connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
||**Database account** |Enter the database account of the target instance. |
||**Database password** |Enter the password corresponding to the database account of the target instance. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
|**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source?_vtm_=a106466.b106468.0_0.0_0.0.4567_7694130500017817107&lang=en).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
||**Instance type** |Select **PostgreSQL**. |
||**Access method** |Select **BytePlus RDS for PostgreSQL**. |
||**region** |Select the region where the target instance is located. |
||**PostgreSQL instance** |Select the target instance of **RDS for PostgreSQL** from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
||**Database name** |Enter the database name. |
||**Database account** |Enter the database account of the target instance. |
||**Database password** |Enter the password corresponding to the database account of the target instance. |
||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
|**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project.  <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
||**Tag**<br><br> |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of volc:, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview?_vtm_=a106466.b106468.0_0.0_0.0.4575_7694130500017817107&lang=en).<br> |
||**Subscription duration** |Select the duration of the subscription as needed.<br><br>> **tip**<br><br><br>> When selecting **Subscription** in **Billing method**, you can set the purchase time and also check **Automatic renewal**. The system automatically renews before task expiration.<br> |

6. Click **Next: configure synchronization object**.

7. On the **Configure synchronization object** wizard page, configure the related parameter information as shown in the table below.

|**Name** ||**Description** |
|---|---|---|
|**Synchronization type** ||Select the synchronization type as needed. Currently, **Schema initialization**, **Full initialization**, and **Incremental synchronization** are supported. including:<br><br>> **tip**<br><br><br><br>* > Incremental synchronization is selected by default and cannot be deselected.<br><br><br>* > When you select **Schema initialization** or **Full initialization**, after the pre\-check is completed, DTS will initialize the data of the objects to be synchronized from the source instance in the target instance, which serves as the basis for subsequent incremental data synchronization.<br><br><br>* > If you need to perform no\-downtime synchronization, you can select **Structure initialization**, **Full initialization**, and **Incremental synchronization** at the same time.<br> |
|**Synchronization starting point** ||Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify GTID**: Enter the specified GTID in the input box, formatted as `source_id:transaction_id`.<br><br>* **Set GTID**_**EXECUTED**: Enter the specified GTID_EXECUTED in the input box, formatted as `source_id:transaction_id`. If multiple exist, separate them with commas (,). For how to obtain the instance's GTID_EXECUTED, refer to [How to obtain the GTID_EXECUTED of the instance](https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance?_vtm_=a106466.b106468.0_0.0_0.0.4581_7694130500017817107&lang=en).<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**.<br><br><br>> **tip**<br><br><br><br>* > When **Synchronization type** selects **Full initialization**, this step is not supported.<br><br><br>* > GTID and GTID_EXECUTED must be legal values from the source end. Otherwise, pre\-check reports an error.<br><br><br>* > When **Synchronization type** selects both **Full initiation** and **Incremental synchronization**, the **Starting timestamp** defaults to the current time point and can not be modified.<br><br><br>* > When selecting **Specify timestamp**, the time you set must be later than the earliest Binlog time on the source end. If there is no corresponding time Binlog, the closest Binlog starting point will be selected.<br> |
|**Synchronization statement type**<br><br> ||Select the operation types to synchronize. Currently, DML and DDL operation statements are supported for synchronization. The details are as follows:<br><br><br>* **DML**: Currently supports `Delete`, `Insert`, and `Update`. All DML operation statements are selected by default and can be adjusted as needed.<br><br>* **DDL**: All supported DDL operations are synchronized by default. You can also click **custom DDL** to select the DDL types that need synchronization as required. If the task captures unsupported DDL during operation, the destination will not execute the operation, synchronization progress will stop, and the task will report an error. For DDL operation statements supported by DTS during data synchronization, refer to [supported synchronized SQL operations](https://docs.byteplus.com/en/docs/DTS/Synchronize-to-volcano-engine-postgresql-for-express?TagIDs=2&lang=en#jKu2ArB0). |
|**Synchronization object** ||In the **Synchronize object** area, select the objects you want to synchronize, and in the **Selected object** area, confirm the objects you want to synchronize.<br><br><br>* Set schema, table, or column mapping: click the pencil icon behind the target database or table to rename the database or table. If the entire database is selected in the **Synchronization object ** area, only the database name can be modified in the **Selected object ** area, and the database cannot be expanded. Click **Batch mapping** to modify database or table names in bulk. For more information, refer to [Database and table batch mapping](https://docs.byteplus.com/en/docs/DTS/Database_and_table_mapping).<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets.<br><br>* Filter data in tables: Check **Filter data** enables filtering of data within the table.<br><br><br>> **tip**<br><br><br><br>* > If new tables are expected later, choose whole database synchronization first; if only some tables are synchronized, confirm that new tables will not be automatically included in the current task.<br><br><br>* > Currently only supported: synchronization at the database, table, and column levels.<br><br><br>* > Supports mapping the source MySQL database to the destination PostgreSQL schema, with support for table name and column name mapping. If the primary key or unique key column is involved in column mapping, the mapped target columns must still form the same set of non\-null primary key or unique key.<br> |
|**Filter condition** ||When filtering conditions are enabled, data filtering can begin during the full data scan phase to improve synchronization performance. You can set the filter condition in the **filter condition** column of the table and then click **verification statement** to check if the filter condition is met.<br><br>> **tip**<br><br><br><br>* > This feature is currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.<br><br><br>* > This field supports configuration only when **filter data** is checked for the database and tables of the **synchronization objects**.<br><br><br>* > The filter condition currently supports the `=`, `!=`, <code><</code>, `>`, <code><=</code>, `>=`, `in`, `is null`, `and`, and `or` operators.<br> |
|**Advanced configuration** |**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The front end default value is 600 seconds. |
||**Full synchronization rate** |Set the full synchronization rate as needed. To prevent high synchronization rates from affecting the source database's performance, adjust the following parameters based on the read and write pressure of the source and target databases accordingly:<br><br><br>* **Rows synchronized per second**: Enable and set the rows synchronized per second as needed. The default value is 100000, and the value range is 1\-100000.<br><br>* **Data volume to synchronize per second**: Enable this option and set the data volume as needed. The default value is 100,000, and the value range is 1\-100,000, unit: KB.<br><br>* **Synchronization task concurrency**: Set the concurrency of synchronization tasks as needed. The default value is 8, and the valid range is 1 to 64.<br><br><br>> **tip**<br><br><br><br>* > You can configure this parameter when selecting **Synchronization type** as **Full initiation**.<br><br><br>* > An excessively high synchronization rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases.<br> |

8. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the synchronization task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the synchronization task. You can also click **Ignore all** to ignore all alert messages with one click.

      * If you choose to **Ignore** the alert and start the synchronization task, it may cause data inconsistencies and business risks.

      * for detailed instructions on pre\-checks, refer to [Pre-check items (MySQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mysql?lang=en) and [Pre-check items (PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql?lang=en).

11. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

12. Select the configuration method according to the billing method of the task creation:

   * Pay\-as\-you\-go

      On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm order information** configuration wizard page, confirm the billing information of the task.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

         Once the **Payment is completed** on the configuration wizard page, a **Successful payment** message means your task has been created.

After successfully creating the data synchronization task, you can return to the DTS console to view the data synchronization task information on the data synchronization task list.

## Related APIs

|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask?_vtm_=a106466.b106468.0_0.0_0.0.4581_7694130500017817107&lang=en) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask?_vtm_=a106466.b106468.0_0.0_0.0.4581_7694130500017817107&lang=en) |Call the ModifyTransmissionTask API to modify the transmission task. |
