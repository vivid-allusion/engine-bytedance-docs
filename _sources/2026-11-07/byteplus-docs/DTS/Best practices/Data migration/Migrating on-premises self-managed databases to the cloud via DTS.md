---
title: "Migrating on-premises self-managed databases to the cloud via DTS"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Migrating_on-premises_self-managed_databases_to_the_cloud_via_DTS"
---

In the scenario of business migration, after the local database is migrated to the cloud, you need to cut the traffic to switch the business to the cloud. To avoid exceptions in the database on the cloud after the business traffic is cut, it is recommended to use the DTS data migration function to configure a reverse migration link. When a business exception occurs, you can immediately switch the business to the local self\-managed database. This topic uses an on\-premises self\-managed MySQL database instance and a BytePlus RDS for MySQL as examples to introduce how to use DTS to migrate on\-premises data to the cloud, switch services, migrate data back, and roll back services.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The local self\-built database and the VPC of BytePlus have been connected. Select a configuration method as needed according to the actual situation:

   * When using VPN to perform data migration, the local network where the self\-managed database is located has been connected to BytePlus via VPN gateway. For detailed steps, refer to [Building a cloud VPC and on-premises multi-data-center network interconnection](https://docs.byteplus.com/en/docs/vpn/Connecting-a-virtual-private-cloud-to-multiple-data-centers).

   * If data migration requires a dedicated line connection, you need to establish a dedicated line connection between a single cloud VPC and a single on\-premises data center network.   For more information, refer to [Configuring direct connections](https://docs.byteplus.com/en/docs/directconnect/Quick-start#.6YWN572u5LiT57q_6L-e5o6l).

* An instance and database for RDS for MySQL have been created. Used to migrate local self\-built data to the cloud. For details, refer to [Creating an instance (RDS for MySQL)](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and [Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database).

* When the database instance’s access method is VPC and access restrictions are enabled, add the subnet segment of the VPC connected by the dedicated line to the database instance’s allowlist or security group before creating the database transmission task. For more information, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* Ensure that the servers to which the source and target ends belong have sufficient outbound bandwidth. Otherwise, the data migration rate will be affected.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Forward migration and reverse migration are two independent unidirectional migration tasks. Each independent task's constraints, operational restrictions, and other requirements must meet the basic requirements of the migration task. For precautions during the data migration process, please refer to [Migrating MySQL connected over express network to BytePlus RDS for MySQL](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_rds_for_mysql_expressmysql#.5rOo5oSP5LqL6aG5), and [Migrating BytePlus RDS for MySQL to MySQL connected over express network.](https://docs.byteplus.com/en/docs/DTS/synchronizing_to_express_network_rdsmysql#.5rOo5oSP5LqL6aG5)

* During the full migration process, the target database will generate a large number of Binlog files, resulting in the target database's disk usage being much greater than that of the original instance. We recommend that you modify the target database Binlog storage strategy before performing a full migration.

* Before starting the reverse migration task, the forward migration task must be paused first; otherwise, data loops may occur.

* Since performing a business switching operation requires stopping database writes and pausing business operations, it is recommended to perform the operation during off\-peak hours to minimize the impact on business operations.


<span id=".5pWw5o2u5bqT6LSm5Y-35pyA5bCP5p2D6ZmQ562W55Wl"></span>
## Database account minimum permission policy


|**Database** |**Schema migration** |**Full migration** |**Incremental migration** |
|---|---|---|---|
|Source |`SELECT` permission |`SELECT` permission |`REPLICATION SLAVE`, `REPLICATION CLIENT`, and `SELECT` permissions. |
|Target |`SELECT` permission |`SELECT` permission |`REPLICATION SLAVE`, `REPLICATION CLIENT`, and `SELECT` permissions. |


<span id=".5pON5L2c5rWB56iL"></span>
## Operation process

In the scenario of business relocation, after the local database is migrated to the cloud, business switching is required. To avoid exceptions in the cloud database after the business is switched, it is recommended to use the Database Transmission Service (DTS) data migration feature to configure a reverse migration link. When a business exception occurs, you can immediately switch the business to the local database. The main procedure is as follows:

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9b4bbc71133f485a5c8324d3f2d7e892.png) </span>


1. Create and start a forward migration task

   For the forward task, select **Schema migration** + **Full migration** + **Incremental migration** to migrate the local self\-built database to the cloud database.

2. Create a reverse migration task, but do not start it

   For the reverse task, select **Incremental migration**. Create the task but do not start it to avoid data loopbacks.

3. Switch the business to the cloud database

   Pause business writes to the source local self\-built database and switch the business to the cloud database.

4. Pause the forward migration task and start the reverse migration task

   Migrate incremental data generated by the destination cloud database to the local self\-built database to provide a rollback solution for the business.

5. (Optional) Business rollback

   If an exception occurs in the cloud service, you can switch the service to the local self\-built database.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5Yib5bu65q2j5ZCR6L-B56e75Lu75Yqh"></span>
### Step 1: Create a forward migration task


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   
   |**Type** |**Name** |**Description** |
   |---|---|---|
   |**None** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div><br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MySQL**. |
   ||**Access method** |Select **MySQL connected over express network**. |
   ||**Region** |Select the region of the virtual private cloud. |
   ||**Host address** |Enter the host address of the MySQL instance connected over express network. |
   ||**Port** |Enter the port of the MySQL instance connected over express network. |
   ||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When migrating a MySQL instance connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MySQL**. |
   ||**Access method** |Select **BytePlus RDS for MySQL**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**MySQL instance** |Select the target instance of RDS for MySQL from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The drop\-down list only shows the first 10 instances. You can also search for the target instance by instance ID or name.</div><br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project. For more information, refer to <a href="https://docs.byteplus.com/en/docs/6649/94337#%E8%B5%84%E6%BA%90%E8%BD%AC%E5%85%A5%E9%A1%B9%E7%9B%AE">Moving resources to a project</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   

6. Click **Next step: configure migration object**.

7. On the **Configure migration object** wizard page, configure the related parameter information as shown in the table below.

   
   |**Name** |**Description** |
   |---|---|
   |**Migration type** |Check **Structural migration**, **Full migration**, and **Incremental migration**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If <strong>User migration</strong> is needed, user and permission migration must be handled separately. If some source database accounts do not support migration, ensure that business operations are not affected by the absence of these accounts.</div><br> |
   |**Migration user** |Select the target accounts as needed, and set a new password in the **New password (Optional)**  column. When migrating multiple users, click **Batch change passwords** to change all their passwords at once. Otherwise, the target account passwords will be the same as the source passwords.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This configuration is supported when <strong>Migration type</strong> is set to <strong>User migration</strong>.</div><br> |
   |**Migration starting point** |Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify GTID**: Enter the specified GTID in the input box, formatted as `source_id:transaction_id`.<br><br>* **Set GTID**_**EXECUTED**: Enter the specified GTID_EXECUTED in the input box, formatted as `source_id:transaction_id`. If multiple exist, separate them with commas (,). For how to obtain the instance's GTID_EXECUTED, refer to [How to obtain the GTID_EXECUTED of the instance](https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance).<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can configure this parameter when selecting <strong>Migration type</strong> as <strong>Incremental migration</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When <strong>Migration type</strong> selects both <strong>Full migration</strong> and <strong>Incremental migration</strong>, migration defaults to the current time point.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">GTID and GTID_EXECUTED must be legal values from the source end. Otherwise, pre\-check reports an error.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When selecting <strong>Specify timestamp</strong>, the time you set must be later than the earliest Binlog time on the source end. If there is no corresponding time Binlog, the closest Binlog starting point will be selected.</div><br> |
   |**Whether to enable foreign key check?**  |Select whether to enable foreign key check as needed. When enabled, the tool supports migrating cascading updates and deletes of foreign keys from the source, ensuring data integrity and consistency throughout the migration. |
   |**Migration object** |Check the objects to migrate in the **Migration object** area. You can use **Normal search** and **Global search** to find target objects. At the same time, you can perform the following operations in the **Selected object** area:<br><br><br>* Rename databases or tables: Click the pencil icon next to the target database, table, or view to rename them. If you select entire databases in the **Migration object** area, you can only modify the database name in the **Selected object** area, and can not expand the database.<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases, tables, and other targets.<br><br>* Filter data in tables: Check **Filter data** enables filtering of data within the table.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Regular expression search for target objects is supported in the <strong>Migration object</strong> or <strong>Selected object</strong> areas.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When the migration object is not the entire database, OnlineDDL operations are not supported. Meanwhile, incremental migration does not automatically migrate newly added objects and their changes.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">The migration object granularity can be either database or table. If tables are selected as the migration objects, other objects such as views, triggers, functions, or stored procedures will not be migrated to the target database.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">To ensure data migration performance and task stability, the source TRIGGER and EVENT will migrate only after the incremental migration completes.</div><br> |
   |**Filter condition** |Optional. Filtering data during a full data scan improves migration performance. Click the pen icon in the **Filter condition** column for the target database, table, or view, set the filter condition, then click **Verification statement ** to validate the condition.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This feature is currently in beta testing. To use it, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">This field can be configured only if <strong>Filter data </strong>is selected for the <strong>Migration object</strong>'s database, table, or view.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Filter condition currently supported <code>=</code>, <code>!=</code>,  <code><</code>, <code>></code>, <code><=</code>, <code>>=</code>, <code>in</code>, <code>is null</code>, <code>and</code> , <code>or</code>.</div><br> |
   |**Error retry time** |If a migration task fails due to a disconnection between the source and target ends, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86,400, in seconds (s). The default value is 600 seconds. |
   |**Full migration rate** |Set the full migration rate as needed. To prevent high migration rates from affecting the source database's performance, adjust the following parameters based on the read and write pressure of the source and target databases accordingly:<br><br><br>* **Rows migrated per second**: Enable and set the rows migrated per second as needed. The default value is 100,000, and the value range is 1 to 100,000.<br><br>* **Data volume migrated per second**: Enable and set the data volume migrated per second as needed. The default value is 25,000. The value range is 1 to 25,000, and the unit is KB.<br><br>* **Migration task concurrency**: Set the concurrency of migration tasks as needed. The default value is 8, the value range is 1\-64.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">You can configure this parameter when selecting <strong>Migration type</strong> as <strong>Full migration</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you apply to enable the full\-incremental feature of the DTS, you can not set the migration task concurrency individually. To enable the full\-incremental feature of DTS, <a href="https://console.byteplus.com/workorder/create">submit a ticket</a> for technical support.</div><br> |
   

8. Click **Data validation configuration**.

9. On the **Create migration task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   
   |**Name** |**Description** |
   |---|---|
   |**Data verification**<br><br> |Select whether to configure the data verification function directly when creating a migration task (built\-in).<br><br><br>* **Enable**: Configure data verification tasks directly when creating a data migration task.<br><br>* **Disable**: Do not configure data verification tasks when creating a data migration task. |
   |**Validation type** |DTS automatically generates validation types based on the database type and migration type, and does not support modification. For more information on validation types, refer to [Background](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation#.6IOM5pmv5L-h5oGv). |
   |**Validation object** |Select the object to be verified as needed.<br><br><br>* **Consistent with the migration task**: The object to be verified matches the object to be migrated, meaning all migration objects are verified.<br><br>* **Custom**: Select the object to be verified as needed. |
   |**Startup settings** |Configure the timing of data verification in the migration task.<br><br><br>* **Automatic start**: The data verification task starts automatically along with the progress of the migration task. Automatic start occurs when full migration (if any) is complete and the delay of incremental migration is 0.<br><br>* **Manually start**: The data verification task does not start automatically with the migration task progress. You must manually start the data verification at the appropriate time. It is recommended to manually start data verification only after full migration (if any) is complete and the delay of incremental migration is 0. Otherwise, verification results may be inaccurate. |
   |**Billing type** |Currently, only **Pay\-as\-you\-go** is supported and can not be modified. |
   

10. Click **Pre\-check**.

9. Optional. If a pre\-check has been performed for the created task, you can confirm whether to restart the pre\-check based on the prompts. If you need to restart, click **OK** in the **Whether to restart the pre\-check** dialog box.

   1. If the instances of the source and target databases are not modified, there is no need to restart the pre\-check.

   2. If you modify the source and target database instance information or the migration task parameters, it is recommended to restart the pre\-check to avoid task startup failures or interruptions.

10. On the **Pre\-check** configuration wizard page, perform the following actions based on the check result:

   1. Click **Details** in the **Actions** column of the pre\-check results to view detailed alert and failure messages. After modifying the databases and tables accordingly, click **Retry**.

   2. Click **Ignore** in the **Actions** column to ignore the alert and continue starting the migration task. You can also click **Ignore all** to ignore all alert messages with one click.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the migration task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoints">Pre\-check items</a>.      </div>
      

11. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

12. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.


After successfully creating the data migration task, you can return to the DTS console to view the data migration task information on the data migration task list. For more information, refer to [Viewing migration tasks](https://docs.byteplus.com/en/docs/DTS/viewing_a_migration_task).

<span id=".5q2l6aqk5LqM77ya5Yib5bu65Y-N5ZCR6L-B56e75Lu75Yqh"></span>
### Step 2: Create a reverse migration task

The reverse migration task provides a rollback solution for your business. After the business is restored, you can immediately switch the business to the original local self\-built database if data exceptions occur.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For a reverse migration task, you only need to select incremental migration for the migration type. You can create a reverse migration task according to the following guidance, but do not start the reverse migration task.</div>



1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   
   |**Type** |**Name** |**Description** |
   |---|---|---|
   |**None** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div><br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Access method** |Select **BytePlus RDS for MySQL**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**Cross\-BytePlus account?**  |Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When transmitting data across accounts, log on to the Database Transmission Service (DTS) console through the account of the destination.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Before cross\-account data transmission, create and authorize an IAM role in the source root user. For detailed steps, refer to <a href="https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission">How to authorize users for cross\-account data transmission</a>.</div><br> |
   ||**Cross\-account ID** |Enter the BytePlus account ID to which the source database belongs. |
   ||**Cross\-account roles** |Enter the IAM role authorized for DTS to access cross\-account resources. |
   ||**MySQL instance** |Select the target instance of RDS for MySQL from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also search for the target instance by instance ID or name.</div><br> |
   ||**Node type** |Select node types as needed, currently supporting **Primary node** and **Read\-only node**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Select read\-only nodes when read\-only nodes are created within the instance. For specific steps on creating a read\-only node, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_read-only_nodes">Read\-only node overview</a>.</div><br> |
   ||**MySQL read\-only node** |Select the target read\-only node from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When a read\-only node is created in the instance and <strong>Node type</strong> selects <strong>Read\-only node</strong>, this parameter can be configured.</div><br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **MySQL**. |
   ||**Access method** |Select **MySQL connected over express network**. |
   ||**Region** |Select the region of the virtual private cloud. |
   ||**Host address** |Enter the host address of the MySQL instance connected over express network. |
   ||**Port** |Enter the port of the MySQL instance connected over express network. |
   ||**VPC** |Select the target VPC from the drop\-down list as follows:<br><br><br>* Direct connect: Select any VPC under the CEN when achieving data connectivity through a dedicated line CEN.<br><br>* VPN connection: Select the VPC bound to the VPN gateway when achieving data connectivity through VPN. |
   ||**Subnet** |Select a subnet within the VPC from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When migrating a MySQL instance connected over express network, you need to add subnet CIDR block access permissions to the allowlist or security group policy on the source end in advance. Click <strong>View subnet CIDR blocks</strong> to view and copy CIDR blocks.</div><br> |
   ||**Database account** |Enter the database account of the target instance. |
   ||**Database password** |Enter the password corresponding to the database account of the target instance. |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address.<br><br>* **The Express network requires the subnet to have \* available IPs. The current number of available IPs in the subnet is insufficient, and the task can not be created. Check the subnet resources in the VPC**: When this error prompt appears, adjust the number of available IPs in the VPC subnet to ensure enough IPs in the target VPC subnet. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project. For more information, refer to <a href="https://docs.byteplus.com/en/docs/6649/94337#%E8%B5%84%E6%BA%90%E8%BD%AC%E5%85%A5%E9%A1%B9%E7%9B%AE">Moving resources to a project</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   

6. Click **Next step: configure migration object**.

7. On the **Configure migration object** wizard page, configure the related parameter information as shown in the table below.

   
   |**Name** |**Description** |
   |---|---|
   |**Migration type** |For reverse migration tasks, you only need to migrate the newly added data in the cloud to the local database as storage backup. Therefore, you only need to select **Incremental migration**. |
   |**Migration starting point** |Set to pull Binlog logs from a specified position or timestamp. The values are as follows:<br><br><br>* **System default**: The default is the task start time.<br><br>* **Specify GTID**: Enter the specified GTID in the input box, formatted as `source_id:transaction_id`.<br><br>* **Set GTID**_**EXECUTED**: Enter the specified GTID_EXECUTED in the input box, formatted as `source_id:transaction_id`. If multiple exist, separate them with commas (,). For how to obtain the instance's GTID_EXECUTED, refer to [How to obtain the GTID_EXECUTED of the instance](https://docs.byteplus.com/en/docs/DTS/how_can_I_retrieve_the_GTID_EXECUTED_of_an_instance).<br><br>* **Specify timestamp**: Click the input box to select a date, click **Select time** to set the time point, then click **OK**. |
   |**Whether to enable foreign key check?**  |Select whether to enable foreign key check as needed. When enabled, the tool supports migrating cascading updates and deletes of foreign keys from the source, ensuring data integrity and consistency throughout the migration. |
   |**Migration object** |In the **Migration object** area, check the objects selected in the forward migration task. You can use **Normal search** and **Global search** to find target objects. |
   |**Error retry time** |If a migration task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   

8. Click **Save**.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">To create a reverse migration task, simply click Save without starting the reverse migration task.   </div>
   

<span id=".5q2l6aqk5LiJ77ya5Lia5Yqh5YiH5o2i6Iez5LqR5LiK5pWw5o2u5bqT"></span>
### Step 3: Switch business to cloud database

When the forward task completes full migration and schema migration and enters the incremental migration stage, you can complete the service cut\-over operation according to the following configurations.


1. (Optional) Log in to the source database and execute the following command according to the database type to view the session information, and ensure that no new sessions perform write operations.



<Tabs>
<Tab zoneid="FFl9RhPneJ" title="MySQL & veDB MySQL">
<TabTitle>MySQL & veDB MySQL</TabTitle>

```SQL
show processlist;
```



</Tab>
<Tab zoneid="Gxbs3DJMVi" title="Redis">
<TabTitle>Redis</TabTitle>

```SQL
CLIENT LIST
```



</Tab>
<Tab zoneid="rtzArappG6" title="MongoDB">
<TabTitle>MongoDB</TabTitle>

```SQL
use admin
db.runCommand({currentOp: 1, $all:[{"active" : true}]})
```



</Tab>
<Tab zoneid="da3rVWF0MR" title="PostgreSQL">
<TabTitle>PostgreSQL</TabTitle>

```SQL
select * from pg_stat_activity;
```



</Tab>
</Tabs>



2. (Optional) Before switching services, you can perform data verification to verify whether the source and destination data are consistent.

   You need to create a full validation task and a schema verification task. For details, refer to [Creating a data verification task](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation).

3. Switch the service to the cloud database.

   1. Suspend business writes to the local self\-built database on the source end.

   2. Switch the service to the cloud database.


<span id=".5q2l6aqk5Zub77ya5pqC5YGc5q2j5ZCR6L-B56e75Lu75Yqh77yM5ZCv5Yqo5Y-N5ZCR6L-B56e75Lu75Yqh"></span>
### Step 4: Pause the forward migration task and start the reverse migration task


1. Pause the forward migration task.Task For details, refer to [Pausing a migration task](https://docs.byteplus.com/en/docs/DTS/suspending_a_migration_task).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When the migration task is suspended, do not start the task at will; otherwise, data inconsistency may occur.   </div>
   

2. Start the reverse migration task. For details, refer to [Starting a migration task](https://docs.byteplus.com/en/docs/DTS/initiating_a_migration_task).

3. Start writing cloud business.

4. Test business functions.


<span id=".5q2l6aqk5LqU77ya77yI5Y-v6YCJ77yJ5Lia5Yqh5Zue6YCA"></span>
### Step 5: (optional) Service rollback

If an exception occurs in the cloud business, refer to the following operation prompts to reduce the impact of data migration on the business.


1. Pause the business and prohibit the writing of new data.

2. Switch the service to the source on\-premises self\-built database.

3. Resume writing business data.
