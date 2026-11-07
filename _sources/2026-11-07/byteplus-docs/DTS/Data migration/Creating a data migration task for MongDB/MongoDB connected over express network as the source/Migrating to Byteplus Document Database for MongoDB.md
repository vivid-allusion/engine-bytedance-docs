---
title: "Migrating to Byteplus Document Database for MongoDB"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_documentdb_for_mongodb_expressmongodb"
---

This topic describes how to create a task for migrating the MongoDB connected over express network to the BytePlus MongoDB on the Database Transmission Service (DTS) console.

## Prerequisites

* A database and an account for Document Database for MongoDB have been created. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/mongodb/create-instance) and [Creating an account](https://docs.byteplus.com/en/docs/mongodb/create-account).

* Set the source information as needed, as detailed below:

   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

* When your instance connects via the express network, the subnet of the express network must communicate with the source or target database. To allow DTS to access instances in the express network normally, add the subnet CIDR block to the source or target database allowlist or security group rules. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.65.32/28,101.47.65.48/28`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* The network connectivity and service availability of the source and destination have been confirmed.

* Optional. Check each migration object in the source and target databases according to the instructions in the pre\-check items. For more information, refer to [Pre-check items (MongoDB)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mongodb).

## Precautions

* Do not write new data to the source instance during data migration when incremental migration is not selected to ensure data consistency.

* To ensure real\-time data consistency, it is recommended to select schema migration, full data migration, and incremental data migration.

* Since full data migration performs concurrent insert operations, the collection in the target database generates fragments. Therefore, the storage space of the collection in the target database will be larger than that of the collection in the source database after the full migration is complete.

* During migration, if there are `CREATE TABLE` or `RENAME TABLE` operations on the source end, select the entire database containing the table or the entire database where the table is renamed to when configuring the migration object. Otherwise, the newly created or renamed table will not migrate to the destination.

* When creating a VPC data migration task, the system creates several network cards by default in your selected VPC, and the network cards are mounted by default to the subnet you selected. The network card name format is `dts_shuttle_********`.

## Limits

### Application limits

|**Type** |**Description** |
|---|---|
|Source database and target database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* If the migration object is at the collection level and needs to be edited (e.g., collection name mapping), each migration task only supports migrating up to 1,000 collections. If this limit is exceeded, an error will appear after task submission. In this case, it is recommended to split the collections to be migrated and configure the task in batches.<br><br>* To perform incremental migration, complete the following configuration:<br><br>   * Enable `Oplog` logs. Otherwise, an error will be reported during the pre\-check phase, and the migration task can not start.<br><br>   * It is recommended that the `Oplog` be retained for at least 7 days during full migration. To adjust the `Oplog` size, refer to [Change the size of the Oplog](https://www.mongodb.com/docs/v4.0/tutorial/change-oplog-size/). You can also clean the `Oplog` generated by the DTS source database after the full migration completes and the task runs.<br><br>* Incremental data migration is not supported for single node MongoDB source databases. If you need to use incremental migration, convert the single node MongoDB to a replica set. For more information, refer to [How to achieve incremental migration or synchronization if the source database is a single node MongoDB instance](https://docs.byteplus.com/en/docs/DTS/how_to_perform_incremental_migration_or_incremental_synchronization).<br><br>* Ensure no orphaned documents exist in the source and destination instances, as they may cause inconsistent data or task failure. For more information, refer to [orphan documents](https://www.mongodb.com/zh-cn/docs/v7.0/reference/glossary/#std-term-orphaned-document) and [how to clean orphaned documents in MongoDB (sharded cluster architecture)](https://docs.byteplus.com/en/docs/DTS/how-to-clean-orphaned-documents-in-MongoDB-sharding-cluster-architecture?lang=zh). |
|Other limits |* It is recommended that the source and target Document Database for MongoDB be the same version, or migrate from a lower version to a higher one to ensure compatibility. If migrating from a higher version to a lower version, there may be database compatibility issues.<br><br>* Migrating data from admin and local databases is not supported.<br><br>* Transaction information is not retained, that is, transactions in the source database are converted into single records when migrated to the target database.<br><br>* Prior to executing data migration, assess the performance of both source and target databases. It is advised to perform the migration during off\-peak business hours. Otherwise, during full migration, DTS consumes certain read/write resources on both source and target databases, which may lead to an increase in database load.<br><br>* The storage space of the target Document Database for MongoDB database must be greater than the storage space occupied by the source Document Database for MongoDB database.<br><br>* DTS uses `ROUND(COLUMN,PRECISION)` to read the migration precision of `FLOAT` and `DOUBLE` columns. The default migration precision is 38 digits for `FLOAT` and 308 digits for `DOUBLE`. [Submit a ticket](https://console.byteplus.com/workorder/create) if requirements are not met. |

### Operation limits

Operation limits of the source database:

* During the schema and full migration phases, do not perform schema changes to databases or collections. Otherwise, the data migration task will fail.

* If only full data migration is performed, do not write new data to the source database, or the source and target data will be inconsistent.

## Database account minimum permission policy

The account used for data migration must have the following permissions:

* If the source database is a sharded cluster instance, `root` permissions on the source database are required.

   > **tip**

   > When incrementally migrating sharded cluster data and the incremental data acquisition method is `ChangeStream`, the source database account needs the `ChangeStream` permission.

* If the source database is a replica set instance, the following permissions are required.

   * `FIND`, `buildInfo`, `serverStatus`, and `listDatabases` permissions of the object to be migrated from the source database.

   * The source database account must have read permissions for the database to be synchronized, the `Config` database, the `admin` database, and the `local `database.

* The target database account must have read and write permissions for the target database, and read permissions for the `local` database.

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**None** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br><br>> **tip**<br><br><br>> If not set, the system generates a random task name based on the naming rules, prefixed with **`dts-`**.<br> |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MongoDB**. |
   ||**Access method** |Select **MongoDB connected over express network**. |
   ||**Region** |Select the region of the virtual private cloud. |
   ||**Architecture** |Select the architecture type of the target MongoDB instance as needed, currently supporting **Replica set**, **Sharded cluster**, and **Single node**.<br><br>> **tip**<br><br><br>> Incremental data migration is not supported for single node MongoDB source databases. If you need to use incremental migration, convert the single node MongoDB to a replica set. For more information, refer to [How to achieve incremental migration or synchronization if the source database is a single node MongoDB instance](https://docs.byteplus.com/en/docs/DTS/how_to_perform_incremental_migration_or_incremental_synchronization).<br> |
   ||**Incremental data acquisition method** |When selecting **Architecture** as **Sharded cluster**, you can set the **Incremental data acquisition method** Select the incremental data acquisition method as needed. The following options are supported:<br><br><br>* **ChangeStream**: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* **Oplog**: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to **ChangeStream**.<br><br>* **None**: After selecting None, incremental migration is not available. Only full migration can be selected. |
   ||When **Incremental data acquisition method** is set to **ChangeStream** or **None**, configure the parameters of **Address**, **Account verification database**, **VPC**, **Subnet**, **Database account**, and **Database password**. ||
   ||**Address** |Enter the host address and port of the target self\-managed instance in the format of `IP:Port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>> **tip**<br><br><br>> Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br> |
   ||**Account verification database** |Enter the database name to which the account belongs. |
   ||**Virtual private cloud** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select the subnet connected to the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When migrating a MongoDB instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||When **Incremental data acquisition method** is set to **Oplog**, configure the parameters of **VPC**, **Subnet**, **Mongos information** and **Sharding information**. ||
   ||**Virtual private cloud** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When migrating a MongoDB instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||**Mongos information** |1. Click **Modify mongos information**.<br><br>2. In the **Modify mongos information** control panel.<br><br>3. Configure the following parameters:<br><br>   * **Address**: Enter the mongos address, for example, `IP: port` or `Domain name: port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>   > **tip**<br>   <br><br>   > Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br>   <br><br>   * **Account verification database**: Enter the database name to which the account belongs.<br><br>   * **Database account**: Enter the database account of the target instance.<br><br>   * **Database password**: Enter the password corresponding to the database account of the target instance.<br><br>4. Click **OK**. |
   ||**Sharding information** |1. Click **Modify sharding information**.<br><br>2. In the **Modify sharding information** control panel, configure the shard's address, account verification database, account, and password.<br><br>   * **Address**: Enter the sharding address, for example, `IP: port` or `Domain: port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>   > **tip**<br>   <br><br>   > Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br>   <br><br>   * **Account verification database**: Enter the database name to which the account belongs.<br><br>   * **Account**: Enter the target sharding account information.<br><br>   * **Password**: Enter the password corresponding to the target sharding account.<br><br>3. Optional. Click **Add a row** to add up to 32 sharding information entries to set more sharding details.<br><br>4. Click **OK**. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MongoDB**. |
   ||**Access method** |Select **BytePlus Database for MongoDB**. |
   ||**Architecture** |Select the architecture type of the target MongoDB instance as needed. currently supported options are **replica set** and **sharded cluster**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**MongoDB instance** |Select the target instance of Document Database for MongoDB from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
   ||**Tag** |Optional. Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |

6. Click **Next step: configure migration object**.

7. On the **Configure migration object** wizard page, configure the related parameter information as shown in the table below.

   > **tip**

   * > If you do not need to start the migration task immediately, click **Save** in the lower\-right corner of the page after configuring the migration object.

   * > After saving, you will be redirected to the **Migration task list** page. The task status will be **To be started**, and you can configure the migration task at a suitable time. For configuration methods, refer to [Configuring a migration task](https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task).

   |**Parameter** |**Description** |
   |---|---|
   |**Migration type** |Select the migration type based on business needs, including:<br><br><br>* If only full migration is required, select both **Schema migration** and **Full migration**.<br><br>* If online migration is needed, select **Schema migration**, **Full migration**, and **Incremental migration** simultaneously.<br><br><br>> **tip**<br><br><br>> Do not write new data to the source instance during data migration when **incremental migration** is not selected to ensure data consistency.<br> |
   |**Migration object** |Check the objects to migrate in the **Migration object** area. You can use **Normal search** and **Global search** to find target objects. At the same time, you can perform the following operations in the **Selected object** area:<br><br><br>* Rename databases or tables: Click the pencil icon next to the target database, table, or view to rename them. If you select entire databases in the **Migration object** area, you can only modify the database name in the **Selected object** area, and can not expand the database. Click **Batch mapping** to modify database or table names in bulk. For more information, refer to [Database and table batch mapping](https://docs.byteplus.com/en/docs/DTS/Database_and_table_mapping).<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets. |
   |**Error retry time** |If a migration task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   |**Full migration rate** |Set the full migration rate as needed. To prevent high migration rates from affecting the source database's performance, adjust the following parameters based on the read and write pressure of the source and target databases accordingly:<br><br><br>* **Rows migrated per second**: Enable and set the rows migrated per second as needed. The default value is 100,000, and the value range is 1 to 100,000.<br><br>* **Data volume migrated per second**: Enable and set the data volume migrated per second as needed. The default value is 25,000. The value range is 1 to 25,000, and the unit is KB.<br><br>* **Migration task concurrency**: Set the concurrency of migration tasks as needed. The default value is 8, and the value range is 8 to 64.<br><br><br>> **tip**<br><br><br><br>* > You can configure this parameter when selecting **Migration type** as **Full migration**.<br><br><br>* > An excessively high migration rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases. For more information, refer to [Migration rate settings for MongoDB](https://docs.byteplus.com/en/docs/mongodb/data-migration-guide).<br> |

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
