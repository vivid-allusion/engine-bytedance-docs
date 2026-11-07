---
title: "Migrating to Redis connected over public network"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/migrating_to_public_network_publicredis"
---

This topic describes how to create a task for migrating the Redis connected over public network to another Redis connected over public network on the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A self\-managed instance for Cache for Redis has been set up in the public network environment, with the database account and password configured.

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* The network connectivity and service availability of the source and target databases have been confirmed.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The migration task performs full migration and incremental migration by default. In Redis data migration, when the source database lacks SYNC or PSYNC permissions, DTS supports selecting full migration only. Full migration only uses the Scan method, migrating data by traversing the entire source database to the target. The Scan method causes a high load on the source database. Perform it during off\-peak hours.

* When the source database is a self\-managed Cache for Redis, do not restart or switch the source or target database between primary and secondary during migration, as this will cause the migration task to fail.

* To migrate data from the Alibaba Cloud Redis to BytePlus Cache for Redis, the Alibaba Cloud database account must have replication permissions.

* In full and incremental migration tasks of Stream, do not perform double\-write operations on the target database instance, as this may cause the migration task to fail.

* Migrating instances with SSL enabled is not supported.

* DTS currently does not support migrating data from Alibaba Cloud's cloud\-native in\-memory database Tair to BytePlus Cache for Redis. To migrate, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.

* If different DBs map to the same DB and the same Key exists in different DBs, it may cause unpredictable results including data inconsistency or task failure during migration.

* During migration, do not change the instance configuration. Otherwise, the migration task will fail.

* You can migrate cluster edition instances by shard\-to\-shard migration.

* During data migration, if duplicate key values are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination.

* This feature is currently in beta testing. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/).

* In full migration only scenarios, export (dump) timeout failures may occur if there are large keys on the source end or if the network environment is poor. It is recommended to split or delete large keys and then retry. If the task does not recover for a long time, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* When certain keys in the source database use an expiration (expire) policy, a situation may arise where expired keys are not deleted promptly. This can result in the target database appearing to have fewer keys than the source database.<br><br>* During migration, if scaling operations occur, such as adding or removing shards, or specification changes, such as memory expansion, you need to reconfigure the task. To ensure consistent data, it is recommended to clear data that has been migrated to the target Cache for Redis instance before reconfiguring the task.<br><br>* During migration, if the source database connection address changes and causes the task to fail, you need to reconfigure the task. If it fails, you can [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support. If it is not processed for a long time, the source database will reset the AOF file.<br><br>* The account used for data migration must have the following permissions:<br><br>   * The source database can execute `sync`, `psync`, and `config get` commands.<br><br>   * The target database can execute write commands. |
|Other limits |* Self\-managed Cache for Redis supports the open\-source PSync protocol.<br><br>* It is recommended that the source and target Cache for Redis databases be the same version, or migrate from a lower version to a higher one to ensure compatibility. If you migrate from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* During incremental data migration, DTS cannot confirm the execution success of Lua scripts called via `EVAL` or `EVALSHA`, as the target database does not explicitly return execution results for scripts.<br><br>* During full data migration, DTS consumes certain read/write resources on both the source and target databases, which may lead to an increased load on the database servers. When the database workload is heavy or server specifications are low, it may increase database pressure, even causing the database service to become unavailable and the data migration task to fail.<br><br>* It is recommended to perform data migration during off\-peak hours. You can also increase the parameter value of the source database's `client-output-buffer-limit` to prevent buffer overflow when migrating large Keys.<br><br>* The storage space of the target Cache for Redis database must be greater than the storage space occupied by the source Cache for Redis database.<br><br>* When DTS transfers data using the `psync` and `sync` commands, it overwrites data in the target database. If the target database already contains the same Key, it will first execute the `del` operation.<br><br>* In the event of a transient connection failure on the source or target instance, a full data re\-migration may be triggered, potentially leading to data inconsistency.<br><br>* If the target database's data eviction policy parameter `maxmemory-policy` is configured to a value other than `noeviction`, it may cause the target database's data to be inconsistent with the source database. |


<span id=".5aKe6YeP6L-B56e75pSv5oyB55qE5ZG95Luk"></span>
## Commands supported by incremental migration


* `APPEND`

* `BITOP`, `BLPOP,` `BRPOP,` `BRPOPLPUSH`

* `DECR`, `DECRBY,` `DEL`

* `EVAL`, `EVALSHA,` `EXPIRE,` `EXPIREAT`

* `GEOADD`, `GETSET`

* `HDEL`, `HINCRBY,` `HINCRBYFLOAT,` `HMSET,` `HSET,` `HSETNX`

* `INCR`, `INCRBY,` `INCRBYFLOAT`

* `LINSERT`, `LPOP,` `LPUSH,` `LPUSHX,` `LREM,` L`SET,` `LTRIM`

* `MOVE`, `MSET,` `MSETNX`

* `PERSIST`, `PEXPIRE,` `PEXPIREAT,` `PFADD,` `PFMERGE,` `PSETEX`

* `RENAME`, `RENAMENX,` `RESTORE,` `RPOP,` `RPOPLPUSH,` `RPUSH,` `RPUSHX`

* `SADD`, `SDIFFSTORE,` `SELECT,` `SET,` `SETBIT,` `SETEX,` S`ETNX,` `SETRANGE,` `SINTERSTORE, `S`MOVE, S`P`OP, `S`REM,` `SUNIONSTORE`

* `ZADD`, `ZINCRBY,` `ZINTERSTORE,` `ZREM,` `ZREMRANGEBYLEX,` `ZUNIONSTORE,` `ZREMRANGEBYRANK,` `ZREMRANGEBYSCORE`


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cache for Redis 7.0 does not support <code>Function</code> commands.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   
   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**None** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div><br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **Redis connected over public network**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When synchronizing a Redis connected over public network, you need to add access permissions for the DTS CIDR blocks to the allowlist or security group policy on the source end in advance. Click <strong>View DTS CIDR blocks</strong> to view and copy the CIDR block.</div><br> |
   ||**Host address** |Enter the host address of the self\-managed instance. |
   ||**Port** |Enter the port number of the self\-managed instance. |
   ||**Database account** |The default account is **default**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the version of Redis connected over public network is above 6.0, you can set the database account on a case\-by\-case basis.</div><br> |
   ||**Database password** |Enter the password corresponding to the database account of the self\-managed instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the Redis instance connected over public network enables passwordless login, you do not need to enter the password for the instance database account.</div><br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **Redis connected over public network**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When synchronizing a Redis connected over public network, you need to add access permissions for the DTS CIDR blocks to the allowlist or security group policy on the source end in advance. Click <strong>View DTS CIDR blocks</strong> to view and copy the CIDR block.</div><br> |
   ||**Host address** |Enter the host address of the self\-managed instance. |
   ||**Port** |Enter the port number of the self\-managed instance. |
   ||**Database account** |The default account is **default**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the version of Redis connected over public network is above 6.0, you can set the database account on a case\-by\-case basis.</div><br> |
   ||**Database password** |Enter the password corresponding to the database account of the self\-managed instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the Redis instance connected over public network enables passwordless login, you do not need to enter the password for the instance database account.</div><br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">To grant sub\-user privileges to access resources in a specific project, refer to <a href="https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90">Modifying project privileges</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |Optional. Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   

6. Click **Next step: configure migration object**.

7. On the **Configure migration object** wizard page, configure the related parameter information as shown in the table below.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The migration task performs <strong>Full migration</strong> and <strong>Incremental migration</strong> by default.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you do not need to start the migration task immediately, click <strong>Save</strong> in the lower\-right corner of the page after configuring the migration object.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">After saving, you will be redirected to the <strong>Migration task list</strong> page. The task status will be <strong>To be started</strong>, and you can configure the migration task at a suitable time. For configuration methods, refer to <a href="https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task">Configuring a migration task</a>.   </div>
   

   
   |**Parameter** |**Description** |
   |---|---|
   |**Migration type**<br><br> |Select the migration type as needed. Currently supported types are **Full migration**, and **Incremental migration**. By default, **Full migration** and **Incremental migration** are enabled, and **Full migration** can not be checked.<br><br><br>* If only full migration is required, you can deselect **Incremental migration**.<br><br>* If online migration is needed, select **Full migration** and **Incremental migration** simultaneously.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">In Redis data migration, when the source database lacks SYNC or PSYNC permissions, DTS supports selecting full migration only. Full migration only uses the Scan method, migrating data by traversing the entire source database to the target. The Scan method causes a high load on the source database. Perform it during off\-peak hours.</div><br><br><br>* <div data-tips="true" data-tips-type="default">In full migration scenarios only, if the source end contains large keys or the network environment is poor, the dump operation may timeout and fail. It is recommended to split or delete large keys and then retry. If the task does not recover for a long time, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If only <strong>Full migration</strong> is selected and the source database keeps writing, consistency between source and target data is not guaranteed.</div><br> |
   |**Migration object** |In the **Migration object** area, check the objects to migrate. You can confirm the objects to migrate again in the **Selected object** area.<br><br>Meanwhile, you can perform the following actions in the **Selected object** area:<br><br><br>* Rename databases or tables: Click the pencil icon next to the target databases to rename them. If you select entire databases in the **Migration object** area, you can only modify the database name in the **Selected object** area, and can not expand the database. Click **Batch mapping** to modify database names in bulk. For more information, refer to [Database and table batch mapping](https://docs.byteplus.com/en/docs/DTS/Database_and_table_mapping).<br><br>* Filter and delete unnecessary targets: The search box in the **Selected object** area supports fuzzy search to batch delete unwanted databases and other targets. |
   |**Error retry time** |If a migration task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600 \- 86400, in seconds (s). The default value is 600 seconds. |
   

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

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the migration task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoints">Pre\-check items</a>.      </div>
      

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**. Then perform the following operations.

   * Click **Create and start a task**. After successfully creating the data migration task, data migration starts immediately.

   * Click **Create task**. After successfully creating the data migration task, you need to manually start data migration at the right time.


After successfully creating the data migration task, you can return to the DTS console to view the data migration task information on the data migration task list. For more information, refer to [Viewing migration tasks](https://docs.byteplus.com/en/docs/DTS/viewing_a_migration_task).

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|**API** |**Description** |
|---|---|
|[CreateTransmissionTask](https://docs.byteplus.com/en/docs/DTS/CreateTransmissionTask) |Call the CreateTransmissionTask API to create a DTS task. |
|[ModifyTransmissionTask](https://docs.byteplus.com/en/docs/DTS/modifytransmissiontask) |Call the ModifyTransmissionTask API to modify the transmission task. |
