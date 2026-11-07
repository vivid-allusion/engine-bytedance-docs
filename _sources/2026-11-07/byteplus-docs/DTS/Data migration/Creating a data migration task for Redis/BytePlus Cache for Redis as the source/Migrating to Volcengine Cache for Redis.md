---
title: "Migrating to Volcengine Cache for Redis"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_redis"
---

This topic describes how to create a task for migrating the BytePlus Cache for Redis to BytePlus Cache for Redis on the Database Transmission Service (DTS) console.

## Prerequisites

* A database for Cache for Redis has been created, and the account password has been set. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and [Setting an account password](https://docs.byteplus.com/en/docs/redis/create-manage-account).

* Confirm the network connectivity and service availability of the source and target databases before creating a data migration task.

* Optional. Check each migration object in the source and target databases according to the instructions in the pre\-check items. For more information, refer to [Pre-check items (Redis)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_redis).

## Precautions

* The migration task performs full migration and incremental migration by default. In Redis data migration, when the source database lacks `SYNC` or `PSYNC` permissions, DTS supports selecting full migration only. Full migration only uses the Scan method, migrating data by traversing the entire source database to the target. The Scan method causes a high load on the source database. Perform it during off\-peak hours.

* During the pre\-check, if you ignore the alert and start the migration task, it may lead to data inconsistencies and pose business risks. Proceed with caution.

* Because the single\-node instance of Cache for Redis does not have AOF persistence enabled, it can not be migrated using DTS.

* In full and incremental migration tasks of Stream, do not perform double\-write operations on the target database instance, as this may cause the migration task to fail.

* Migrating instances with SSL enabled is not supported.

* During migration, do not change the instance configuration. Otherwise, the migration task will fail.

* If different DBs map to the same DB and the same Key exists in different DBs, it may cause unpredictable results including data inconsistency or task failure during migration.

* During data migration, if duplicate key values are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination.

* In full migration scenarios only, if the source end contains large keys or the network environment is poor, the dump operation may timeout and fail. It is recommended to split or delete large keys and then retry. If the task does not recover for a long time, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.

* Migration tasks from BytePlus Cache for Redis to another BytePlus Cache for Redis are not supported in China (Shanghai) and China (Beijing). To create such tasks, [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support.

## Limits

|**Type** |**Description** |
|---|---|
|Source and target database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal migration performance.<br><br>* When certain keys in the source database use an expiration (expire) policy, a situation may arise where expired keys are not deleted promptly. This can result in the target database appearing to have fewer keys than the source database.<br><br>* During migration, if the source database undergoes scaling such as adding or removing shards, or changes in specifications like memory expansion, you need to reconfigure the task. To ensure consistent data, it is recommended to clear data that has been migrated to the target Cache for Redis instance before reconfiguring the task.<br><br>* During migration, if the source database connection address changes and causes the task to fail, you need to reconfigure the task. If it fails, you can [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support. If it is not processed for a long time, the source database will reset the AOF file.<br><br>* The target database account used for data migration must have permissions to execute write commands.<br><br>* The storage space of the target Cache for Redis database must be greater than the storage space occupied by the source Cache for Redis database.<br><br>* If the target database's data eviction policy parameter `maxmemory-policy` is configured to a value other than `noeviction`, it may cause the target database's data to be inconsistent with the source database. |
|Other limits |* It is recommended that the source and target Cache for Redis databases be the same version, or migrate from a lower version to a higher one to ensure compatibility. If you migrate from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* During incremental migration, because the target database does not explicitly return the execution result when running scripts, DTS cannot confirm whether Lua scripts called through `EVAL` or `EVALSHA` execute successfully.<br><br>* DTS will occupy some resources of the source and target databases during full migration, which may increase the database server load. When the database workload is heavy or server specifications are low, it may increase database pressure, even causing the database service to become unavailable and the data migration task to fail.<br><br>   It is recommended to perform data migration during off\-peak hours. You can also increase the parameter value of the source database's `client-output-buffer-limit` to prevent buffer overflow when migrating large Keys.<br><br>* When DTS transmits data using the `psync` and `sync` commands, it overwrites data on the target database. If the target contains the same key, DTS deletes it first using the `del` operation.<br><br>* In the event of a transient connection failure on the source or target instance, a full data re\-migration may be triggered, potentially leading to data inconsistency. |

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

> **tip**

> Cache for Redis 7.0 does not support `Function` commands.

## Procedure

1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data migration**.

4. On the **Migration task list** page, click **Create task**.

5. On the **Create migration task** page, locate the **Configure source and target database** wizard, and configure the following parameters.

   |**Type** |**Parameter** |**Description** |
   |---|---|---|
   |**None** |**Task name** |Optional. Customize the task name. Naming rules are as follows: <br><br><br>* Must start with a Chinese character or letter.<br><br>* Must be 64 characters or less.<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-). |
   ||**Link specification** |Select the link specification for the migration task. **Compact**, **Medium** and **Standard** are supported.<br><br>> **tip**<br><br><br>> The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to [Product specifications](https://docs.byteplus.com/en/docs/DTS/product_specifications).<br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **BytePlus Cache for Redis**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**Cross\-BytePlus account?**  |Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts.<br><br>   > **tip**<br>   <br><br>   * > When transmitting data across accounts, log on to the Database Transmission Service (DTS) console through the account of the destination.<br>   <br><br>   * > Before cross\-account data transmission, create and authorize an IAM role in the source root user. For detailed steps, refer to [How to authorize users for cross\-account data transmission](https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission).<br>    |
   ||**Cross\-account ID** |Enter the BytePlus account ID to which the source database belongs. |
   ||**Cross\-account roles** |Enter the IAM role authorized for DTS to access cross\-account resources. |
   ||**Redis Instance** |Select the target instance of Cache for Redis from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database account** |The default account is **default**, and you can set the database account on a case\-by\-case basis. |
   ||**Database password** |Enter the password corresponding to the database account of the source instance.<br><br>> **tip**<br><br><br>> When password\-free access is enabled for Cache for Redis instances, access the target instance without entering a password. For steps on enabling password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **BytePlus Cache for Redis**. |
   ||**Region** |Select the region where the target instance is located. |
   ||**Redis Instance** |Select the target instance of Cache for Redis from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database account** |The default account is **default**, and you can set the database account on a case\-by\-case basis. |
   ||**Database password** |Enter the password corresponding to the database account of the source instance.<br><br>> **tip**<br><br><br>> When password\-free access is enabled for Cache for Redis instances, access the target instance without entering a password. For steps on enabling password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. For more information, refer to [Creating a new project](https://docs.byteplus.com/en/docs/6649/94336#%E6%96%B0%E5%BB%BA%E9%A1%B9%E7%9B%AE).<br><br>> **tip**<br><br><br><br>* > To grant sub\-user privileges to access resources in a specific project, refer to [Modifying project privileges](https://docs.byteplus.com/en/docs/6649/173422#%E4%BF%AE%E6%94%B9%E9%A1%B9%E7%9B%AE%E6%9D%83%E9%99%90).<br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing method** |Currently, only **Pay\-as\-you\-go** is supported. No selection is required.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |

6. Click **Next step: configure migration object**.

7. On the **Configure migration object** wizard page, configure the related parameter information as shown in the table below.

   > **tip**

   * > The migration task performs **Full migration** and **Incremental migration** by default.

   * > If you do not need to start the migration task immediately, click **Save** in the lower\-right corner of the page after configuring the migration object.

   * > After saving, you will be redirected to the **Migration task list** page. The task status will be **To be started**, and you can configure the migration task at a suitable time. For configuration methods, refer to [Configuring a migration task](https://docs.byteplus.com/en/docs/DTS/configuring_a_migration_task).

   |**Parameter** |**Description** |
   |---|---|
   |**Migration type**<br><br> |Select the migration type as needed. Currently supported types are **Full migration**, and **Incremental migration**. By default, **Full migration** and **Incremental migration** are enabled, and **Full migration** can not be checked.<br><br><br>* If only full migration is required, you can deselect **Incremental migration**.<br><br>* If online migration is needed, select **Full migration** and **Incremental migration** simultaneously.<br><br><br>> **tip**<br><br><br><br>* > In Redis data migration, when the source database lacks SYNC or PSYNC permissions, DTS supports selecting full migration only. Full migration only uses the Scan method, migrating data by traversing the entire source database to the target. The Scan method causes a high load on the source database. Perform it during off\-peak hours.<br><br><br>* > In full migration scenarios only, if the source end contains large keys or the network environment is poor, the dump operation may timeout and fail. It is recommended to split or delete large keys and then retry. If the task does not recover for a long time, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br><br><br>* > If only **Full migration** is selected and the source database keeps writing, consistency between source and target data is not guaranteed.<br> |
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
