---
title: "Migrating to PostgreSQL connected over public network"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/migrating_to_public_network_postgresql"
---

This topic introduces how to create a Volcengine RDS for PostgreSQL migration task to PostgreSQL connected over public network in the Database Transmission Service (DTS) console.

## Prerequisites

* An instance, a database, and an account for PostgreSQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance) and [Creating a database and an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts).

* A self\-managed instance and its database for PostgreSQL have been set up in the public network environment.

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* If you need to migrate data from the PostgreSQL engine instance managed in the AI native database management platform (AIDAP):

   * AIDAP\-managed Supabase engine instance:

      * Create workspace. For detailed steps, refer to [Create workspace](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_workspace?lang=en).

      * Create database branch. For detailed steps, refer to [Creating branch](https://docs.byteplus.com/en/docs/aidap/Supabase-Creating_a_branch?lang=en).

      * Obtain the connection information required by DTS, such as host address, port, account number, and password. refer to [Obtaining the connection information of computing power](https://docs.byteplus.com/en/docs/aidap/Supabase-Getting_compute_connection_information?lang=en) for detailed steps.

   * AIDAP\-managed standard PostgreSQL engine instance:

      * Create workspace. For detailed steps, refer to [Create workspace](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_workspace?lang=en).

      * Create database branch. For detailed steps, refer to [Creating branch](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Creating_a_branch?lang=en).

      * Obtain the connection information required by DTS, such as host address, port, account number, and password. refer to [Obtaining the connection information of computing power](https://docs.byteplus.com/en/docs/aidap/PostgreSQL-Getting_compute_connection_information?lang=en) for detailed steps.

* Confirm the network connectivity and service availability of the source and target databases before creating a data migration task.

* You can also prepare the migration objects in the source and target databases according to the instructions in the Pre\-check items. For more information, refer to [Pre-check items (PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql).

* If you use the major version upgrade function of the BytePlus RDS for PostgreSQL database, the logical replication slot in existing RDS for PostgreSQL migration tasks may be lost after the upgrade, resulting in the failure of RDS for PostgreSQL migration tasks. If this occurs, you need to recreate the PostgreSQL migration task.

## Precautions

* When **Incremental migration** is not selected, do not write new data to the source database instance during data migration to ensure data consistency.

* To ensure real\-time data consistency, it is recommended to select schema migration, full data migration, and incremental data migration.

* The migration object granularity can be either database or table. If tables are selected as the migration objects, other objects such as views, triggers, functions, or stored procedures will not be migrated to the target database.

* If you do not need to start the migration task immediately, click **Save** in the lower\-right corner of the page after configuring the migration object. After saving, you will be redirected to the **Migration task list** page. The task status will be **To be started**, and you can configure the migration task at a suitable time. For configuration methods, refer to [Configuring a migration task](https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task).

* During the pre\-check, if you **Ignore** the alert and start the migration task, it may lead to data inconsistencies and pose business risks. For details about the pre\-check, refer to [Pre-check items (RDS for PostgreSQL)](https://docs.byteplus.com/en/docs/DTS/limits_postgresql_as_source_database).

* During migration, if there are `CREATE TABLE` or `RENAME TABLE` operations on the source end, select the entire database containing the table or the entire database where the table is renamed to when configuring the migration object. Otherwise, the newly created or renamed table will not migrate to the destination.

* Since full data migration performs concurrent insert operations, the collection in the target database generates fragments. Therefore, the storage space of the collection in the target database will be larger than that of the collection in the source database after the full migration is complete.

* To ensure data migration performance and task stability, ordinary triggers, event triggers, RULE, exclusion constraints, foreign key constraints, check constraints, constraints on DOMAIN, and Sequence value settings in RDS for PostgreSQL will migrate only after incremental migration completes.

* During data migration, if duplicate primary key values or unique key values are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination. When a conflict overwrite occurs, if there is a table with the same name in the target database, it may cause data inconsistency issues as detailed below. It is recommended to use table name mapping or delete or rename the table with the same name in the target database to avoid data inconsistency and reduce business risks.

   * When the table structure is consistent, the migrated data overwrites records in the target table with the same primary key or unique key values as in the source database.

   * When the table structure is inconsistent, initialization of data may fail, and only partial column data can be migrated.

* Only data from the primary database supports migration. Data from the secondary database is not supported.

* For RDS for PostgreSQL migration tasks, the source database account must create triggers, functions, and other objects in the source database. Therefore, during the migration process, do not modify the access permissions of objects such as triggers, functions, or internal tables created by this account in the source database.

* If you use the major version upgrade function of the BytePlus RDS for PostgreSQL database, the logical replication slot in existing RDS for PostgreSQL migration tasks may be lost after the upgrade, resulting in the failure of RDS for PostgreSQL migration tasks. If this occurs, you need to recreate the RDS for PostgreSQL migration task.

## Limits

### Application limits

|**Type** |**Description** |
|---|---|
|Source database |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* Tables to be migrated must have a primary key or a unique non\-null constraint, and their fields must be unique. Otherwise, data inconsistency may occur.<br><br>* It is recommended that the number of tables in a single task should not exceed 20,000, and the number of databases should not exceed 50. When a large number of databases and tables need to be migrated, it is recommended to split them into multiple tasks.<br><br>* The database or table name of the object to be migrated can not contain question marks (?). Otherwise, the migration task will fail.<br><br>* For incremental migration, the requirements for WAL logs are as follows:<br><br>   * You must enable WAL logs, that is, set the value of the` wal_level` parameter to `logical`.<br><br>   * WAL logs must be retained for at least 24 hours, and a retention period of more than seven days is recommended. Otherwise, the DTS task may fail because it can not obtain the logs, potentially leading to data loss. |
|Others |* A single migration task can only migrate one database. To migrate multiple databases, configure a migration task for each one.<br><br>* It is recommended that the source and target RDS for PostgreSQL databases be the same version, or migrate from a lower version to a higher one to ensure compatibility. If you migrate from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* During the incremental data migration process, if the granularity of the migration object is schema, ensure that the table\-level replication identity `REPLICA IDENTITY` is set to `FULL`. If a new table is created in the schema to be migrated, or the table to be migrated is reconstructed using the `RENAME` command, you need to execute the `ALTER TABLE schema.table REPLICA IDENTITY FULL;` command before writing data to the table.<br><br>   > **tip**<br>   <br><br>   > When executing the `ALTER TABLE schema.table REPLICA IDENTITY FULL;` command, replace `schema` and `table` with the actual schema and table names.<br>   <br><br>* During incremental data migration, DTS creates a replication slot with the prefix `dts_sync_` in the source database to replicate data. DTS automatically cleans up historical replication slots every 5 to 10 minutes to prevent them from continuously accumulating and taking up disk space.<br><br>   > **tip**<br>   <br><br>   * > When a migration task is released or fails, DTS actively cleans up the replication slot.<br>   <br><br>   * > If a primary/secondary switchover occurs in RDS for PostgreSQL, you need to log in to the secondary database to manually clean up the replication slot.<br>   <br><br>* Prior to executing data migration, assess the performance of both source and target databases. It is also advised to perform the migration during off\-peak business hours. Otherwise, during full data migration, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* Since full data migration performs concurrent insert operations, the table in the target database generates fragments. Therefore, the storage space of the table in the target database will be larger than that of the table in the source database after the full migration is complete.<br><br>* Verify that the character sets of the source and target databases are consistent before migration. Otherwise, pre\-check may fail. |

### Operation limits

* During the schema migration and full migration stages, do not perform DDL operations that change the database or table structure, or the data migration task will fail.

* If only full data migration is performed, do not write new data to the source database, or the source and target data will be inconsistent. To maintain real\-time data consistency, it is recommended to select schema migration, full data migration, and incremental data migration.

## Minimum database permission policy

The account used for data migration must have the following permissions:

* The source database account needs to have `superuser` permissions to create logical replication slots.

* The target database account needs to have permissions to create a `schema`. If the target database `schema` already exists, the migration account must be the target schema owner.

## Supported SQL statements

|**Operation type** |**SQL operation statements** |
|---|---|
|DML |INSERT, UPDATE, DELETE |
|DDL |* CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE<br><br>* CREAT INDEX, DROP INDEX<br><br>* CREATE SEQUENCE, ALTER SEQUENCE, DROP SEQUENCE<br><br>* DROP RULE<br><br>* CREATE TYPE<br><br>   > **tip**<br>   <br><br>   > TYPE supports SHELL, ENUM, RANGE, or COMPOSE.<br>    |

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   |**Type** |**Name** |**Description** |
   |---|---|---|
   |**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task named with `dts-` by default.<br> |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **PostgreSQL**. |
   ||**Access method** |Select **BytePlus RDS for PostgreSQL**. |
   ||**region** |Select the region where the target instance is located. |
   ||**Cross\-BytePlus account?**  |Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts.<br><br>   > **tip**<br>   <br><br>   * > When transmitting data across accounts, log on to the Database Transmission Service (DTS) console through the account of the destination.<br>   <br><br>   * > Before cross\-account data transmission, create and authorize an IAM role in the source root user. For detailed steps, refer to [How to authorize users for cross\-account data transmission](https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission).<br>    |
   ||**Cross\-account ID** |Enter the BytePlus account ID to which the source database belongs. |
   ||**Cross\-account roles** |Enter the IAM role authorized for DTS to access cross\-account resources. |
   ||**PostgreSQL instance** |Select the target instance of **RDS for PostgreSQL** from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database name** |Enter the database name. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **PostgreSQL**. |
   ||**Access method** |Select **PostgreSQL connected over public network**.<br><br>> **tip**<br><br><br>> When migrating PostgreSQL connected over public network instances, add the DTS IP segment access permission in the source end's allowlist or security group policy in advance. Click **View DTS CIDR blocks** to view and copy the CIDR block.<br> |
   ||**region** |Select the region where the target instance is located. |
   ||**Host address** |Enter the host address of the target self\-managed instance. |
   ||**Port** |Enter the port number of the target self\-hosted instance. |
   ||**Database name** |Enter the database name. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Connection method**<br><br> |Select whether to enable the encryption protocol as needed to establish a secure connection between the client and the database instance, preventing data interception, tampering, or forgery during transmission. Option:<br><br><br>* **Unencrypted connection**: suitable for self\-built PostgreSQL instances deployed in a public network environment. This method carries security risks and is recommended only for testing environments or controlled networks.<br><br>* **SSL secure connection**: Recommended for production environments, supports connections to PostgreSQL instances hosted on the AI native database management platform (AIDAP), and can also be used for self\-built instances configured with SSL. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify your IP address. |
   |**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project.  <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |

6. Click **Next step: configure migration object**.

7. On the **Configure migration object** wizard page, configure the related parameter information as shown in the table below.

   > **tip**

   * > If you do not need to start the migration task immediately, click **Save** in the lower\-right corner of the page after configuring the migration object.

   * > After saving, you will be redirected to the **Migration task list** page. The task status will be **To be started**, and you can configure the migration task at a suitable time. For configuration instructions, refer to Configure migration task.

   |**Name** ||**Description** |
   |---|---|---|
   |**Migration type** ||Select the migration type as needed. Currently supported types are **Schema migration**, **Full migration**, and **Incremental migration**. including:<br><br><br>* If only full migration is required, select both **Schema migration** and **Full migration**.<br><br>* If online migration is needed, select **Schema migration**, **Full migration**, and **Incremental migration** simultaneously.<br><br><br>> **tip**<br><br><br><br>* > When **Incremental migration** is not selected, do not write new data to the source database instance during data migration to ensure data consistency.<br><br><br>* > To ensure real\-time data consistency, it is recommended to select schema migration, full data migration, and incremental data migration.<br> |
   |**Migration object** ||In the **Migration object** area, check the objects to migrate. You can confirm the objects to migrate in the **Selected object** area.<br><br>> **tip**<br><br><br><br>* > The migration object granularity can be either database or table. If tables are selected as the migration objects, other objects such as views, triggers, functions, or stored procedures will not be migrated to the target database.<br><br><br>* > To ensure data migration performance and task stability, TRIGGER, RULE, FOREIGN KEY, SEQUENCE, and other objects of RDS for PostgreSQL will migrate only after the incremental migration completes.<br><br><br>* > The search box in the **Selected object** area supports fuzzy search to batch delete unwanted targets.<br> |
   |**Advanced configuration**<br><br> |**Enable millisecond\-level delay monitoring**<br><br> |When **migration type** selects **incremental migration**, millisecond\-level latency monitoring is enabled by default. Enabling this feature provides high\-precision, full\-link, and proactive end\-to\-end latency measurement that improves monitoring stability and effectively detects abnormal scenarios such as network interruptions and idle disconnects.<br><br>Enabling this feature requires DTS to write heartbeats to the source database. The source end account must have SELECT, INSERT, and UPDATE permissions. For more information about the heartbeat table, refer to [Manually creating the heartbeat table](https://docs.byteplus.com/en/docs/DTS/Why_is_a_heartbeat_table_required_when_enabling_millisecond-level_latency_monitoring?lang=en). |
   ||**Skip post\-schema migration** |When selecting schema migration in migration type, DTS automatically migrates post\-schema after the incremental migration ends. You may also skip post\-schema migration, meaning DTS will not migrate post\-schema objects.<br><br>RDS for PostgreSQL database post\-schema migration objects include ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.<br><br><br>* **Yes**: Represent skipping post\-schema migration, i.e., DTS does not migrate post\-schema objects.<br><br>* **No**: Represent not skipping post\-schema migration, i.e., DTS migrates post\-schema objects.<br><br><br>> **tip**<br><br><br>> The configuration of whether to skip post\-schema migration is only supported when the migration type includes **Schema migration**.<br> |
   ||**Error retry time** |If a migration task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   ||**Full migration rate** |Set the full migration rate as needed. To prevent high migration rates from affecting the source database's performance, adjust the following parameters based on the read and write pressure of the source and target databases accordingly:<br><br><br>* **Rows migrated per second**: Enable and set the rows migrated per second as needed. The default value is 100,000, and the value range is 1 to 100,000.<br><br>* **Data volume migrated per second**: Enable and set the data volume migrated per second as needed. The default value is 25000, and the value range is 1\-100000, in KB.<br><br>* **Migration task concurrency**: Set the concurrency of migration tasks as needed. The default value is 8, the value range is 1\-64.<br><br><br>> **tip**<br><br><br><br>* > You can configure this parameter when selecting **Migration type** as **Full migration**.<br><br><br>* > An excessively high migration rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases.<br> |

8. Click **Data validation configuration**.

9. On the **Create migration task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   |**Parameter** |**Description** |
   |---|---|
   |**Data verification**<br><br> |Select whether to configure the data verification function directly when creating a migration task (built\-in).<br><br><br>* **Enable**: Configure data verification tasks directly when creating a data migration task.<br><br>* **Disable**: Do not configure data verification tasks when creating a data migration task. |
   |**Validation type** |DTS automatically generates validation types based on the database type and migration type, and does not support modification. For more information on validation types, refer to [Background](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation#.6IOM5pmv5L-h5oGv). |
   |**Validation object** |Select the object to be verified as needed.<br><br><br>* **Consistent with the migration task**: The object to be verified matches the object to be migrated, meaning all migration objects are verified.<br><br>* **Custom**: Select the object to be verified as needed. |
   |**Startup settings** |Configure the timing of data verification in the migration task.<br><br><br>* **Automatic start**: The data verification task starts automatically along with the progress of the migration task. Automatic start occurs when full migration (if any) is complete and the delay of incremental migration is 0.<br><br>* **Manually start**: The data verification task does not start automatically with the migration task progress. You must manually start the data verification at the appropriate time. It is recommended to manually start data verification only after full migration (if any) is complete and the delay of incremental migration is 0. Otherwise, verification results may be inaccurate. |
   |**Billing type** |Currently, only **Pay\-as\-you\-go** is supported and can not be modified. |

10. Click **Pre\-check**.

11. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   * If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   * If you modify the source and target database instance information or the migration task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

12. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   * Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   * Click **Ignore** in the **Actions** column to ignore the alert and continue starting the migration task. You can also click **Ignore all** to ignore all alert messages with one click.

      > **tip**

      * > If you choose to **Ignore** the alert and start the migration task, it may cause data inconsistencies and business risks.

      * > For details about the pre\-check, refer to [Pre\-check items](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoints).

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**. Then perform the following operations.

   * Click **Create and start a task**. After successfully creating the data migration task, data migration starts immediately.

   * Click **Create task**. After successfully creating the data migration task, you need to manually start data migration at the right time.

After successfully creating the data migration task, you can return to the DTS console to view the data migration task information on the data migration task list. For more information, refer to [Viewing migration tasks](https://docs.byteplus.com/en/docs/DTS/viewing_a_migration_task).

## Related APIs

|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
