---
title: "Synchronizing to MongoDB connected over express network"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_MongoDB_connected_over_express_network"
---

This topic describes how to create a task for synchronizing the MongoDB connected over express network to another MongoDB connected over express network on the Database Transmission Service (DTS) console.

## Prerequisites

* When the source and target are deployed in IDC or ECS and connected through the public network, you need to add the server IP address of DTS to the allowlist of the self\-built database.

* Set the source and target information as needed, as detailed below:

   * When using VPN to perform data synchronization, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to[ Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data synchronization requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network. For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

* When your instance connects via the VPC, the subnet of the VPC must communicate with the source or target database. To allow DTS to access instances in the VPC normally, add the subnet CIDR block to the source or target database allowlist or security group rules. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* The network connectivity and service availability of the source and destination have been confirmed.

* Optional. Check each synchronization object in the source and target databases according to the instructions in the pre\-check items. For more details, refer to [Pre-check items (MongoDB)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mongodb).

## Precautions

* To ensure data consistency in real time, it is recommended to select structure initialization, full initialization, and incremental synchronization.

* Since full initialization performs INSERT operations concurrently, the collection of the target database generates fragments. Therefore, the collection storage space of the target database is larger than that of the source database after full initialization is complete.

* During data synchronization, if duplicate primary key values or unique key values are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination. When a conflict overwrite occurs, if there is a table with the same name in the target database, it may cause data inconsistency issues as detailed below. It is recommended to use table name mapping or delete or rename the table with the same name in the target database to avoid data inconsistency and reduce business risks.

   * When the table structure is consistent, the synchronized data overwrites records in the target table with the same primary key or unique key values as in the source database.

   * When the table structure is inconsistent, initialization of data may fail, and only partial column data can be synchronized.

* During the pre\-check, if you **ignore** the alert and start the synchronization task, it may lead to data inconsistencies and pose business risks. For details about the pre\-check, refer to [Pre-check items (MongoDB)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mongodb).

* During synchronization, if there are `CREATE TABLE` or `RENAME TABLE` operations on the source end, select the entire database containing the table or the entire database where the table is renamed to when configuring the synchronization object. Otherwise, the newly created or renamed table will not synchronize to the destination.

* Do not write new data to the source instance during data synchronization when **Incremental synchronization** is not selected to ensure data consistency.

* During incremental synchronization, MongoDB's DDL operations (such as `createIndexes`) are executed asynchronously on the destination and do not block DML synchronization. If you plan to switch business to the target, confirm the DDL has completed and all indexes are ready on the target before switching to avoid performance or data consistency issues due to indexes not being ready.

## Limits

|**Type** ||**Description** |
|---|---|---|
|Application limits |Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal synchronization performance.<br><br>* The collection of objects to be synchronized must contain a primary key or unique constraint, and the fields must be unique. Otherwise, duplicate data may occur in the target database.<br><br>* If the synchronization object is at the collection level and needs to be edited (e.g., collection name mapping), each synchronization task only supports synchronizing up to 1,000 collections. If this limit is exceeded, an error will appear after task submission. In this case, it is recommended to split the collections to be synchronized and configure the task in batches.<br><br>* User initialization only supports replica set instances, not sharded cluster instances, and does not support cross\-version synchronization. This feature is currently in the invitation\-only testing phase. To use this feature, [submit tickets](https://console.byteplus.com/workorder/create) to contact technical support to apply for usage.<br><br>* To perform incremental synchronization, complete the following configuration:<br><br>   * Enable Oplog logs. Otherwise, an error will be reported during the pre\-check phase, and the synchronization task can not start.<br><br>   * It is recommended that the Oplog be retained for at least 7 days during full initialization. To adjust the Oplog size, refer to [Changing the size of the Oplog](https://www.mongodb.com/docs/v4.0/tutorial/change-oplog-size/). You can also clean the oplog generated by the DTS source database after the full initialization completes and the task runs.<br><br>* Incremental data synchronization is not supported when the source database is a MongoDB single\-node instance. To use incremental synchronization, convert the single\-node MongoDB to a replica set. For more information, refer to [How to achieve incremental migration or incremental synchronization if the source database is a single-node MongoDB instance](https://docs.byteplus.com/en/docs/DTS/how_to_perform_incremental_migration_or_incremental_synchronization). |
| |Other limits |* It is recommended that the source and target Document Database for MongoDB databases be the same version, or synchronize from a lower version to a higher one to ensure compatibility. If you synchronize from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* Synchronizing data from admin and local databases is not supported.<br><br>* Transaction information is not retained, that is, transactions in the source database are converted into single records when synchronized to the target database.<br><br>* Prior to executing data synchronization, assess the performance of both source and target databases. It is also advised to perform synchronization during off\-peak business hours. Otherwise, during full initialization, DTS consumes certain read/write resources on both source database and target database, which may lead to an increase in database load.<br><br>* The storage space of the target Document Database for MongoDB database must be greater than the storage space occupied by the source Document Database for MongoDB database.<br><br>* DTS reads the synchronization precision of the FLOAT and DOUBLE `ROUND(COLUMN,PRECISION)` columns. The default synchronization precision of FLOAT is 38 bits and that of DOUBLE is 308 bits. [Submit a ticket](https://console.byteplus.com/workorder/create) if requirements are not met. |
|Operation limits ||Operation limits of the source database:<br><br><br>* Do not perform structural changes to libraries or collections during the structure initialization and full initialization phases, or the data synchronization task will fail.<br><br>* If only full initialization is performed, do not write new data to the source database, or the source and target data will be inconsistent. |

## **Minimum database permission policy**

The account used for data synchronization must have the following permissions:

* If the source database is a sharded cluster instance, you need to have the root account privileges of the source database.

* If the source database is a replica set instance, you need to have the `FIND` permission of the synchronization objects of the source database.

* The target database has the `INSERT`, `UPDATE`, `REMOVE`, `DROPDATABASE`, and `DROPCOLLECTION` permissions.

## Synchronize type **instructions**

|**Synchronization type** |**Description** |
|---|---|
|Schema initialization |Initialize the structure of synchronized objects in the source MongoDB connected over express network to the target MongoDB connected over express network. |
|Full initialization |Initialize all existing data of the source MongoDB connected over express network synchronization objects into the target MongoDB connected over express network.<br><br>> **tip**<br><br><br>> Full initialization of DATABASE and COLLECTION is supported.<br> |
|Incremental synchronization |Based on full initialization, incremental updates from the source MongoDB connected over express network are synchronized to the target MongoDB connected over express network.<br><br>> **tip**<br><br><br>> Incremental synchronization of databases created after the task starts running is not supported.<br> |

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
   ||**Synchronization topology** |Select a synchronization topology based on your business needs. Only **Unidirectional synchronization** is currently supported.<br><br>> **tip**<br><br><br>> For more information about the synchronization topology, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).<br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MongoDB**. |
   ||**Access method** |Select **MongoDB connected over express network**. |
   ||**region** |Select the region of the virtual private cloud. |
   ||**Architecture** |Select the architecture type of the target MongoDB instance as needed, currently supporting **Replica set**, **Sharded cluster**, and **Single node**.<br><br>> **tip**<br><br><br>> MongoDB instances with a single\-node source database do not support incremental synchronization. To use incremental synchronization, convert the single\-node MongoDB to a replica set. For more information, refer to [How to achieve incremental migration or incremental synchronization if the source database is a single\-node MongoDB instance](https://docs.byteplus.com/en/docs/DTS/how_to_perform_incremental_migration_or_incremental_synchronization).<br> |
   ||**Incremental data acquisition method** |When selecting **Architecture** as **Sharded cluster**, you can set the **Incremental data acquisition method** Select the incremental data acquisition method as needed. The following options are supported:<br><br><br>* **ChangeStream**: This method provides a way to obtain change events of specific types of modified data from a data set (database, collection, or pipeline). For example, insert, update, or delete events. If this acquisition method is selected, the instance version must be 3.6 or higher.<br><br>* **Oplog**: This acquisition method means directly obtaining the operation log of the MongoDB. For MongoDB sharded clusters, all sharding addresses must be entered after selecting this acquisition method. This method offers better synchronization performance compared to **ChangeStream**. |
   ||When **Incremental data acquisition method** is set to **ChangeStream** or **None**, configure the parameters of **Address**, **Account verification database**, **VPC**, **Subnet**, **Database account**, and **Database password**. ||
   ||**Address** |Enter the host address and port of the target self\-managed instance in the format of `IP:Port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>> **tip**<br><br><br>> Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br> |
   ||**Account verification database** |Enter the database name to which the account belongs. |
   ||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select the subnet connected to the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When migrating a MongoDB instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||When **Incremental data acquisition method** is set to **Oplog**, configure the parameters of **VPC**, **Subnet**, **Mongos information** and **Sharding information**. ||
   ||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When migrating a MongoDB instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||**Mongos information** |1. Click **Modify mongos information**.<br><br>2. In the **Modify mongos information** control panel.<br><br>3. Configure the following parameters:<br><br>   * **Address**: Enter the mongos address, for example, `IP: port` or `Domain name: port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>   > **tip**<br>   <br><br>   > Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br>   <br><br>   * **Account verification database**: Enter the database name to which the account belongs.<br><br>   * **Database account**: Enter the database account of the target instance.<br><br>   * **Database password**: Enter the password corresponding to the database account of the target instance.<br><br>4. Click **OK**. |
   ||**Sharding information** |1. Click **Modify sharding information**.<br><br>2. In the **Modify sharding information** control panel, configure the shard's address, account verification database, account, and password.<br><br>   * **Address**: Enter the sharding address, for example, `IP: port` or `Domain: port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>   > **tip**<br>   <br><br>   > Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br>   <br><br>   * **Account verification database**: Enter the database name to which the account belongs.<br><br>   * **Account**: Enter the target sharding account information.<br><br>   * **Password**: Enter the password corresponding to the target sharding account.<br><br>3. Optional. Click **Add a row** to add up to 32 sharding information entries to set more sharding details.<br><br>4. Click **OK**. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MongoDB**. |
   ||**Access method** |Select **MongoDB connected over express network**. |
   ||**Architecture** |Select the architecture type of the target MongoDB instance as needed. Currently supported options are **Replica set** and **Sharded cluster**. |
   ||**region** |Select the region of the virtual private cloud. |
   ||**Address** |Enter the host address and port of the target self\-managed instance in the format of `IP:Port`. If multiple addresses exist, separate them with commas (,). Up to 5 addresses are supported.<br><br>> **tip**<br><br><br>> Currently, only IPv4 addresses are supported for access. IPv6 addresses are not yet supported.<br> |
   ||**Account verification database** |Enter the database name to which the account belongs. |
   ||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br>> **tip**<br><br><br>> When synchronizing a MongoDB instance connected over express network, you need to add subnet CIDR block access permissions in the allowlist or security group policy on the source end in advance. Click **View subnet CIDR blocks** to view and copy CIDR blocks.<br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**Project and billing** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project.  <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |
   ||**Subscription duration** |Select the duration of the subscription as needed.<br><br>> **tip**<br><br><br>> When selecting **Subscription** in **Billing method**, you can set the purchase time and also check **Automatic renewal**. The system automatically renews before task expiration.<br> |

6. Click **Next: configure synchronization object**.

7. On the **Configure synchronization objects** wizard page, configure the following parameter information.

   > **tip**

   * > If you do not need to start the synchronization task immediately, click **Save** in the lower\-right corner of the page after configuring the synchronization object.

   * > After saving, you will be redirected to the **Synchronization task list** page. The task status will be **To be started**, and you can configure the synchronization task at a suitable time. For configuration methods, refer to [Configuring a synchronization task](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

   |**Name** |**Description** |
   |---|---|
   |**Synchronization type** |Select the synchronization type as needed. Currently, **User initialization**, **Schema initialization**, **Full initialization**, and **Incremental synchronization** are supported.<br><br>> **tip**<br><br><br><br>* > **Incremental synchronization** is selected by default.<br><br><br>* > When you select **Schema initialization** or **Full initialization**, after the pre\-check is completed, DTS will initialize the data of the objects to be synchronized from the source instance in the target instance, which serves as the basis for subsequent incremental data synchronization.<br> |
   |**Migration user** |Select the target account as needed, and set a new password in the **new password** column for the target account. When migrating multiple users, click **Batch change password** to change all their passwords at once. Otherwise, the target account passwords will be the same as the source passwords.Batch change password<br><br>> **tip**<br><br><br><br>* > This function is currently in invitation\-only testing. To use this feature, [submit tickets](https://console.byteplus.com/workorder/create) to contact technical support to apply for usage.<br><br><br>* > This configuration is supported when **Synchronization type** is set to **User initialization**.<br><br><br>* > During database synchronization, the synchronization of users and privileges needs to be handled separately. Ensure business operations are not affected by the absence of some source database accounts that do not support migration.<br> |
   |**Conflict resolution strategy** |Select the method to process when the unique key already exists in the target database. The values are as follows:<br><br><br>* **Conflict overwrite**: If a unique key that already exists in the target database is encountered during task running, DTS will not retain the conflicting data in the destination, that is, the data in the source will overwrite the data in the destination.<br><br>* **Conflict ignore**: During task execution, if the target database contains the unique key, Database Transmission Service (DTS) will retain the conflicting data at the destination, and the source data will not overwrite the **conflict ignore** data. |
   |**Synchronization starting point** |Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**.<br><br><br>> **tip**<br><br><br><br>* > When **Synchronization type** selects both **Full initiation** and **Incremental synchronization**, the **Starting timestamp** defaults to the current time point and can not be modified.<br><br><br>* > When selecting **Specify timestamp**, the time you set must be later than the earliest Binlog time on the source end. If there is no corresponding time Binlog, the closest Binlog starting point will be selected.<br> |
   |**Synchronization statement type** |Select the operation types to synchronize. Currently, DML and DDL operation statements are supported for synchronization. The details are as follows:<br><br><br>* **DML**: Currently supports `Delete`, `Insert`, and `Update`. All DML operation statements are selected by default and can be adjusted as needed.<br><br>* **DDL**: By default, the synchronization of **Full DDL** is supported, that is, all DDL operation statements are synchronized. You can also select to synchronize index\-related DDL statements, or not synchronize DDL\-related statements. |
   |**Synchronization object** |Select the tables to synchronize. Meanwhile, you can perform the following actions in the **Selected object** area:<br><br><br>* Rename databases or tables: Click the pencil icon next to the target database or table to rename them, supporting query of target objects via **Normal search** and **Global search** methods. If the entire database is selected in the **Synchronization object ** area, only the database name can be modified in the **Selected object ** area, and the database cannot be expanded. Click **Batch mapping** to modify database or table names in bulk. For more information, refer to [Database and table batch mapping](https://docs.byteplus.com/en/docs/DTS/Database_and_table_mapping).<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets. |
   |**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   |**Enable millisecond\-level delay monitoring** |Enable or disable millisecond\-level latency monitoring as needed. When enabled, it provides high\-precision, full\-link, proactive end\-to\-end delay measurement, effectively improving monitoring stability and awareness of abnormal scenarios such as network interruptions and idle disconnections.<br><br>When enabled, DTS writes heartbeat signals to the source database. The source end account must have  `root`, `readWriteAnyDatabase`, `dbAdminAnyDatabase`, and `cloudAdmin` permissions. You can also manually create a heartbeat table on the source database to enable millisecond\-level latency monitoring. For instructions, see [Manually create a heartbeat table](https://docs.byteplus.com/en/docs/DTS/Why_is_a_heartbeat_table_required_when_enabling_millisecond-level_latency_monitoring?lang=en). |
   |**Full synchronization rate** |Set the full synchronization rate as needed. To prevent high synchronization rates from affecting the source database's performance, adjust the following parameters based on the read and write pressure of the source and target databases accordingly:<br><br><br>* **Rows synchronized per second**: Enable and set the rows synchronized per second as needed. The default value is 100000, and the value range is 1\-100000.<br><br>* **Data volume to synchronize per second**: Enable this option and set the data volume as needed. The default value is 25000, the value range is 1\-100000, and the unit is KB.<br><br>* **Synchronization task concurrency**: Set the concurrency of synchronization tasks as needed. The default value is 8, and the valid range is 1 to 64.<br><br><br>> **tip**<br><br><br><br>* > You can configure this parameter when selecting **Synchronization type** as **Full initiation**.<br><br><br>* > An excessively high synchronization rate may affect the performance of the source database. Adjust appropriately based on the read and write pressure of the source and target databases. For more information, refer to [Migration rate settings for MongoDB](https://docs.byteplus.com/en/docs/mongodb/data-migration-guide).<br> |

8. Click **Data validation configuration**.

9. On the **Create synchronization task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   |**Name** |**Description** |
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

      * > If you choose to **Ignore** the alert and start the synchronization task, it may cause data inconsistencies and business risks.

      * > For details about the pre\-check, refer to [Pre\-check items](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_mongodb).

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. Select the configuration method according to the billing method of the task creation:

   * For pay\-as\-you\-go, reconfirm the configuration on the **Confirm order** wizard page. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm order information** configuration wizard page, confirm the billing information of the task.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

      > **tip**

      > Once the **Payment is completed** on the configuration wizard page, a **Successful payment** message means your task has been created.

After successfully creating the data synchronization task, you can return to the DTS console to view the data synchronization task information on the data synchronization task list.
