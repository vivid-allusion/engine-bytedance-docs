---
title: "Synchronizing to Volcano Engine RDS for PostgreSQL"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_postgresql_expresspostgresql"
---

This topic describes how to create a task for synchronizing the PostgreSQL connected over express network to the BytePlus PostgreSQL on the Database Transmission Service (DTS) console.

## Prerequisites

* Set the source information as needed, as detailed below:

   * When using VPN to perform data synchronization, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to[ Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data synchronization requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

* An instance, a database, and an account for RDS for PostgreSQL have been created. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance) and [Creating a database and an account](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_databases_and_accounts).

* When your instance connects via the VPC, the subnet of the VPC must communicate with the source or target database. To allow DTS to access instances in the VPC normally, add the subnet CIDR block to the source or target database allowlist or security group rules. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* The network connectivity and service availability of the source and destination have been confirmed.

## Precautions

* To ensure data consistency in real time, it is recommended to select structure initialization, full initialization, and incremental synchronization.

* If the created task is a bidirectional synchronization task, it is not recommended to use sequence as the auto\-increment ID, otherwise data inconsistencies may result.

* The synchronization object granularity can be either database or table. If tables are selected as synchronization objects, other objects such as views, triggers, functions, or stored procedures will not be synchronized to the target database. If you need to synchronize other objects, create a new synchronization task.

* Only data from the primary database supports synchronization. Data from the secondary database is not supported.

* Since full initialization performs INSERT operations concurrently, the collection of the target database generates fragments. Therefore, the collection storage space of the target database is larger than that of the source database after full initialization is complete.

* For RDS for PostgreSQL synchronization tasks, the source database account must create triggers, functions, and other objects in the source database. Therefore, during the synchronization process, do not modify the access permissions of objects such as triggers, functions, or internal tables created by this account in the source database.

* During the pre\-check, if you ignore the alert and start the synchronization task, it may lead to data inconsistencies and pose business risks.

* During data synchronization, if duplicate primary keys or unique keys are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination. When a conflict overwrite occurs, if there is a table with the same name in the target database, it may cause data inconsistency issues or task failures as detailed below.

   * When the table structure is consistent, data from full synchronization overwrites records in the target table with the same primary key or unique key values as in the source database.

   * When the table structure is inconsistent, initialization of data may fail, and only partial column data can be synchronized or synchronization may fail.

* During synchronization, if there are `CREATE TABLE` or `RENAME TABLE` operations on the source end, select the entire database containing the table or the entire database where the table is renamed to when configuring the synchronization object. Otherwise, the newly created or renamed table will not synchronize to the destination.

* When creating a data synchronization task via express network, the system creates several network cards by default in your selected VPC, and the network cards are mounted by default to the subnet you selected. The network card name format is `dts_shuttle_********`.

* You need to ensure the availability of the logical replication slot of the source instance after switching the primary node. If it is unavailable, the task will be interrupted and cannot be recovered after switching the primary node, and a new task needs to be created.

## Limits

### Application limits

|**Type** |**Description** |
|---|---|
|Source |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal synchronization performance.<br><br>* Tables to be synchronized must have a primary key or a unique non\-null constraint, and their fields must be unique. Otherwise, data inconsistency may occur.<br><br>* It is recommended that the number of tables in a single task should not exceed 20,000, and the number of schemas should not exceed 50. When a large number of databases and tables need to be synchronized, it is recommended to split them into multiple tasks.<br><br>* The database or table name of the object to be synchronized can not contain question marks (?). Otherwise, the task will fail.<br><br>* For incremental synchronization, the requirements for WAL logs are as follows:<br><br>   * You must enable WAL logs, that is, set the value of the `wal_level` parameter to `logical`.<br><br>   * WAL logs must be retained for at least 24 hours, and a retention period of more than seven days is recommended. Otherwise, the DTS task may fail because it can not obtain the logs, potentially leading to data loss. |
|others |* A single synchronization task can only synchronize one database. To synchronize multiple databases, configure a synchronization task for each one.<br><br>* During the incremental data synchronization process, if the granularity of the synchronization object is schema, ensure that the table\-level replication identity `REPLICA IDENTITY` is set to `FULL`. If a new table is created in the schema to be synchronized, or the table to be synchronized is reconstructed using the `RENAME` command, you need to execute the `ALTER TABLE schema.table REPLICA IDENTITY FULL;` command before writing data to the table.<br><br>   > **tip**<br>   <br><br>   > When executing the `ALTER TABLE schema.table REPLICA IDENTITY FULL;` command, replace schema and table with the actual `schema` and `table` names.<br>   <br><br>* During incremental data synchronization, DTS creates a replication slot with the prefix `dts_sync_` in the source database to replicate data. DTS automatically cleans up historical replication slots every 5 to 10 minutes to prevent them from continuously accumulating and taking up disk space.<br><br>   > **tip**<br>   <br><br>   * > When a synchronization task is released or fails, DTS actively cleans up the replication slot.<br>   <br><br>   * > If a primary/secondary switchover occurs in RDS for PostgreSQL, you need to log in to the secondary database to manually clean up the replication slot.<br>   <br><br>* Prior to executing data synchronization, assess the performance of both source and target databases. It is also advised to perform synchronization during off\-peak business hours. Otherwise, during full data synchronization, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* Since full data synchronization performs concurrent insert operations, the table in the target database generates fragments. Therefore, the storage space of the table in the target database will be larger than that of the table in the source database after the full synchronization is complete.<br><br>* Verify that the character sets of the source and target databases are consistent before synchronization. Otherwise, pre\-check may fail. |

### Operation limits

* Do not perform DDL operations on library or table structure changes during the database & table structure initialization and full initialization phases, or the data synchronization task will fail.

* If only full initialization is performed, do not write new data to the source database, or the source and target data will be inconsistent. To ensure data consistency in real time, it is recommended to select structure initialization, full initialization, and incremental synchronization.

## Minimum database permission policy

The account used for data synchronization must have the following permissions:

* The source database account needs to have `superuser` permissions to create logical replication slots.

* The target database account needs to have permissions to create a `schema`. If the target database `schema` already exists, the synchronization account must be the target schema owner.

## Supported SQL statements

|**Operation type** |**SQL operation statements** |
|---|---|
|DML |INSERT, UPDATE, DELETE |
|DDL |* CREATE TABLE, ALTER TABLE, DROP TABLE, TRUNCATE TABLE<br><br>* CREAT INDEX, DROP INDEX<br><br>* CREATE SEQUENCE, ALTER SEQUENCE, DROP SEQUENCE<br><br>* DROP RULE<br><br>* CREATE TYPE<br><br>   > **tip**<br>   <br><br>   > TYPE supports SHELL, ENUM, RANGE, or COMPOSE.<br>    |

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Synchronization task list** page, click **Create task**.

5. On the **Create synchronization task** page, locate the **Configure source and target database** wizard, and configure the following parameters information.

   |**Type** |**Name** |**Description** |
   |---|---|---|
   |**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br>> **tip**<br><br><br>> If not set, the system generates a task name by default according to the naming rule, starting with `dts-`.<br> |
   ||**Link specification** |Select the link specifications for the synchronization task as needed **Compact**, **Medium**, and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br> |
   ||**Synchronization topology** |Select a synchronous topology based on your business needs. **Unidirectional synchronization** and **Bidirectional synchronization** are currently supported.<br><br>> **tip**<br><br><br><br>* > For more information about the synchronization topology, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).<br><br><br>* > When you select bidirectional synchronization for the synchronous topology, it is not recommended to use a sequence as the auto\-increment ID.<br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **PostgreSQL**. |
   ||**Access method** |Select **PostgreSQL connected over express network**. |
   ||**region** |Select the region of the virtual private cloud. |
   ||**Host address** |Enter the host address of the target self\-managed instance.<br><br>> **tip**<br><br><br>> Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br> |
   ||**Port** |Enter the port number of the target self\-hosted instance. |
   ||**Database name** |Enter the database name of the target self\-managed instance. |
   ||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When synchronizing a PostgreSQL connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Connection method**<br><br> |Select whether to enable the encryption protocol as needed to establish a secure connection between the client and the database instance, preventing data interception, tampering, or forgery during transmission. Option:<br><br><br>* **Unencrypted connection**: Suitable for self\-managed PostgreSQL instances deployed in a virtual private cloud environment. This method carries security risks and is recommended only for testing environments or controlled networks.<br><br>* **SSL secure connection**: Recommended for production environments, supports connections to PostgreSQL instances hosted on the AI native database management platform (AIDAP), and can also be used for self\-built instances configured with SSL. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **PostgreSQL**. |
   ||**Access method** |Select **BytePlus RDS for PostgreSQL**. |
   ||**region** |Select the region where the target instance is located. |
   ||**PostgreSQL instance** |Select the target instance of **RDS for PostgreSQL** from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database name** |Enter the database name. |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project.  <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |
   ||**Subscription duration** |Select the duration of the subscription as needed.<br><br>> **tip**<br><br><br>> When selecting **Subscription** in **Billing method**, you can set the purchase time and also check **Automatic renewal**. The system automatically renews before task expiration.<br> |

6. Click **Next: configure synchronization object**.

7. On the **Configure synchronization object** wizard page, configure the related parameter information as shown in the table below.

   > **tip**

   * > If you do not need to start the synchronization task immediately, click **Save** in the lower\-right corner of the page after configuring the synchronization object.

   * > After saving, you will be redirected to the **Synchronization task list** page. The task status will be **To be started**, and you can configure the synchronization task at a suitable time. For configuration methods, refer to [Configuring a synchronization task](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

   |**Name** |**Description** |
   |---|---|
   |**Synchronization type** |Select the synchronization type as needed. Currently, **Schema initialization**, **Full initialization**, and **Incremental synchronization** are supported. including:<br><br><br>* If only full initialization is required, you can select both **Schema initialization** and **Full initialization**.<br><br>* If you need to perform no\-downtime synchronization, you can select **Structure initialization**, **Full initialization**, and **Incremental synchronization** at the same time.<br><br><br>> **tip**<br><br><br><br>* > Do not write new data to the source instance during data synchronization when **Incremental synchronization** is not selected to ensure data consistency.<br><br><br>* > To ensure data consistency in real time, it is recommended to select structure initialization, full data initialization, and incremental data synchronization.<br> |
   |**Synchronization object** |In the **Synchronize object** area, select the objects you want to synchronize, and in the **Selected object** area, confirm the objects you want to synchronize.<br><br>> **tip**<br><br><br><br>* > If a table is selected as the synchronization object, other dependent objects, such as views, triggers, functions, or stored procedures, must be manually selected to be synchronized to the target database. Otherwise, a warning prompt will appear during the pre\-check.<br><br><br>* > To ensure data synchronization performance and task stability, TRIGGER, RULE, FOREIGN KEY, SEQUENCE, and other objects of RDS for PostgreSQL will synchronize only after the incremental synchronization completes.<br><br><br>* > Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets.<br> |
   |**Skip post\-schema synchronization**<br><br> |When selecting schema initialization in synchronization type, DTS automatically synchronizes post\-schema after the incremental synchronization ends. You may also skip post\-schema synchronization, meaning DTS will not synchronize post\-schema objects.<br><br>PostgreSQL database post\-schema synchronization objects include ordinary trigger, event trigger, RULE, exclusive constraint, foreign key constraint, check constraint, Domain constraint, and Sequence value setting.<br><br><br>* **Yes**: Represent skipping post\-schema synchronization, i.e., DTS does not synchronize post\-schema objects.<br><br>* **No**: Represent not skipping post\-schema synchronization, i.e., DTS synchronizes post\-schema objects.<br><br><br>> **tip**<br><br><br>> Whether to skip post\-schema synchronization is supported only when the synchronization topology is **Unidirectional synchronization** and the migration type includes **Schema initialization**.<br> |
   |**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   |**Full synchronization rate** |Set the full synchronization rate as needed. To prevent high synchronization rates from affecting the source database's performance, adjust the following parameters based on the read and write pressure of the source and target databases accordingly:<br><br><br>* **Rows synchronized per second**: Enable and set the rows synchronized per second as needed. The default value is 100000, and the value range is 1\-100000.<br><br>* **Data volume to synchronize per second**: Enable this option and set the data volume as needed. The default value is 25000, the value range is 1\-100000, and the unit is KB.<br><br>* **Synchronization task concurrency**: Set the concurrency of synchronization tasks as needed. The default value is 8, and the valid range is 1 to 64.<br><br><br>> **tip**<br><br><br><br>* > You can configure this parameter when selecting **Synchronization type** as **Full initiation**.<br><br><br>* > An excessively high synchronization rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases.<br> |

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

         * > For details about the pre\-check, refer to [Pre\-check items](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_postgresql).

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
