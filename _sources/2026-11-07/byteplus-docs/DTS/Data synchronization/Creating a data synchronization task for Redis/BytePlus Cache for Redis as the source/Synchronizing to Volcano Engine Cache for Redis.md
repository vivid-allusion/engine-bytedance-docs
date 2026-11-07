---
title: "Synchronizing to Volcano Engine Cache for Redis"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/synchronizing_to_byteplus_cache_for_redis_redis"
---

This topic describes how to create a task for synchronizing the BytePlus Cache for Redis to BytePlus Cache for Redis on the Database Transmission Service (DTS) console.

## Prerequisites

* A database for Cache for Redis has been created, and the default account password has been set. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and Setting the [default account password](https://docs.byteplus.com/en/docs/redis/create-manage-account).

* The network connectivity and service availability of the source and destination have been confirmed.

* Optional. Check each synchronization object in the source and target databases according to the instructions in the pre\-check items. For more information, refer to [Pre-check items (Redis)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_redis).

## Precautions

* A forward synchronization task can select only incremental synchronization. In this case, the historical full data of the source end is not initialized to the destination. Reverse Synchronization does not currently support selecting Full initialization.

* Because the single\-node instance of Cache for Redis does not have AOF persistence enabled, it can not be synchronized using DTS.

* During synchronization, do not change the instance configuration. Otherwise, the synchronization task will fail.

* During data synchronization, if duplicate key values are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination.

* In full and incremental synchronization tasks of Stream, do not perform double\-write operations on the target database instance, as this may cause the synchronization task to fail.

* Synchronizing instances with SSL enabled is not supported.

* When you want to achieve data synchronization through a dedicated line, you can [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.

## Limits

|**Type** |**Description** |
|---|---|
|Source database limits |* Database version: Cache for Redis 4.0, 5.0, 6.0, and 7.0 instances are supported.<br><br>* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal synchronization performance.<br><br>* When certain keys in the source database use an expiration (expire) policy, a situation may arise where expired keys are not deleted promptly. This can result in the target database appearing to have fewer keys than the source database.<br><br>* During full initialization, DTS consumes certain read/write resources on both the source and target databases, which may lead to an increased load on the database servers. When database workload is high or server specifications are insufficient, it can increase pressure on the database and even lead to service unavailability. It is recommended to perform data synchronization during off\-peak hours. You can also increase the parameter value of the `client-output-buffer-limit` of the source database.<br><br>* During synchronization, if the source database undergoes scaling such as adding or removing shards, or changes in specifications like memory expansion, you need to reconfigure the task. To ensure consistent data, it is recommended to clear data that has been synchronized to the target Cache for Redis instance before reconfiguring the task.<br><br>* During synchronization, if the source database connection address changes and causes the task to fail, you need to reconfigure the task. If it fails, you can [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support. If it is not processed for a long time, the source database will reset the AOF file. |
|Target database limits |* Database version: Cache for Redis 4.0, 5.0, 6.0, and 7.0 instances are supported.<br><br>* If the target database's data eviction policy parameter `maxmemory-policy` is configured to a value other than `noeviction`, it may cause the target database's data to be inconsistent with the source database. |
|Other limits |* In the bidirectional synchronization process, only synchronization between two Redis Instances is supported, and multiple Redis loops are not supported, nor are cascades supported.<br><br>* During incremental data synchronization, DTS cannot confirm the execution success of Lua scripts called via `EVAL` or `EVALSHA`, as the target database does not explicitly return execution results for scripts.<br><br>* Two\-way synchronization does not solve the CRDT problem. You need to ensure that there are no operations on the same Key in the source and target databases.<br><br>* In the event of a transient connection failure on the source or target instance, a full data re\-synchronization may be triggered, potentially leading to data inconsistency.<br><br>* Prior to executing data synchronization, assess the performance of both source and target databases. It is also advised to perform synchronization during off\-peak business hours. Otherwise, during full initialization, DTS consumes certain read/write resources on both source database and target database, which may lead to an increase in database load. Synchronization may fail if the source database has a large write volume.<br><br>* It is recommended that the source and target Cache for Redis databases be the same version, or synchronize from a lower version to a higher one to ensure compatibility. If you synchronize from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* The storage space of the target Cache for Redis database must be greater than the storage space occupied by the source Cache for Redis database.<br><br>* When DTS calls the `psync` and `sync` commands to transmit data, it will overwrite the data in the target database. That is, if the same Key exists in the target database, a `del` operation will be performed first. |

## Supported synchronization architectures

* One\-to\-one unidirectional synchronization

* One\-to\-many unidirectional synchronization

* Many\-to\-one unidirectional synchronization

* Cascading unidirectional synchronization

* One\-to\-one bidirectional synchronization

For information on the types and usage of synchronization topology supported by DTS, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).

## Supported commands

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

## Database account minimum permission policy

|**Database** |**Privilege** |
|---|---|
|Source database |You can execute the `sync`, `psync`, and `config get` commands. |
|Target database |You can execute write commands. |

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
   ||**Synchronization topology** |Select a synchronization topology based on your business needs. **Unidirectional synchronization** and **Bidirectional synchronization** are currently supported.<br><br>> **tip**<br><br><br>> For more information about the synchronization topology, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).<br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **BytePlus Cache for Redis**. |
   ||**region** |Select the region where the target instance is located. |
   ||**Cross\-BytePlus account?**  |Select whether to transmit data cross\-account as needed, with the following options:<br><br><br>* **This account**: Selecting this means data transmission occurs only within this account.<br><br>* **Cross\-account**: Selecting this means data transmission occurs between two accounts.<br><br>   > **tip**<br>   <br><br>   * > When transmitting data across accounts, log on to the Database Transmission Service (DTS) console through the account of the destination.<br>   <br><br>   * > Before cross\-account data transmission, create and authorize an IAM role in the source root user. For detailed steps, refer to [How to authorize users for cross\-account data transmission](https://docs.byteplus.com/en/docs/DTS/How_to_authorize_users_for_cross-account_data_transmission).<br>   <br><br>   * > If you need to implement cross\-account data transmission, you also need to configure the **Cross\-account ID** and **Cross\-account roles** parameters.<br>    |
   ||**Cross\-account ID** |Enter the BytePlus account ID to which the source database belongs. |
   ||**Cross\-account roles** |Enter the IAM role authorized for DTS to access cross\-account resources. |
   ||**Redis Instance** |Select the target instance of Cache for Redis from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database account** |The default account is **default**, and you can set the database account on a case\-by\-case basis. |
   ||**Database password** |Enter the password corresponding to the database account of the source instance.<br><br>> **tip**<br><br><br>> When password\-free access is enabled for Cache for Redis instances, access the target instance without entering a password. For steps on enabling password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **BytePlus Cache for Redis**. |
   ||**region** |Select the region where the target instance is located. |
   ||**Redis Instance** |Select the target instance of Cache for Redis from the drop\-down list.<br><br>> **tip**<br><br><br>> You can also search for the target instance by instance ID or name.<br> |
   ||**Database account** |The default account is **default**, and you can set the database account on a case\-by\-case basis. |
   ||**Database password** |Enter the password corresponding to the database account of the source instance.<br><br>> **tip**<br><br><br>> When password\-free access is enabled for Cache for Redis instances, access the target instance without entering a password. For steps on enabling password\-free access, refer to [Password\-free access](https://docs.byteplus.com/en/docs/redis/pwd-free-access).<br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance.<br><br>If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The specific prompts are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project.  <br><br>> **tip**<br><br><br><br>* > After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.<br><br><br>* > A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.<br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources.   The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br>> **tip**<br><br><br><br>* > Support fuzzy search for selecting existing tag keys and tag values.<br><br><br>* > A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.<br><br><br>* > For a single resource, tag keys must be unique, and each tag key can have only one value.<br> |
   ||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br>> **tip**<br><br><br>> For detailed billing information, refer to [Billing instructions](https://docs.byteplus.com/en/docs/DTS/billing_overview).<br> |
   ||**Subscription duration** |Select the duration of the subscription as needed.<br><br>> **tip**<br><br><br>> When selecting **Subscription** in **Billing method**, you can set the purchase time and also check **Automatic renewal**. The system automatically renews before task expiration.<br> |

6. Click **Next: configure synchronization object**.

7. On the **Configure synchronization object** wizard page, configure the related parameter information as shown in the table below.

   > **tip**

   * > If you do not need to start the synchronization task immediately, click **Save** in the lower\-right corner of the page after configuring the synchronization object.

   * > After saving, you will be redirected to the **Synchronization task list** page. The task status will be **To be started**, and you can configure the synchronization task at a suitable time. For configuration methods, refer to [Configuring a synchronization task](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).

|**Name** | |**Description** |
|---|---|---|
|**Synchronization type** ||Select the synchronize type as needed. Currently, **Full initialization** and **Incremental synchronization** are supported.<br><br>> **tip**<br><br><br><br>* > **Incremental synchronization** is selected by default.<br><br><br>* > A forward synchronization task can select only incremental synchronization. In this case, the historical full data of the source end is not initialized to the destination. Reverse Synchronization does not currently support selecting Full initialization.<br><br><br>* > When you select Full initialization, after the pre\-check is completed, DTS will initialize the data of the objects to be synchronized from the source instance in the target instance, which serves as the basis for subsequent incremental data synchronization.<br> |
|**Synchronization object** ||In the Synchronization objects area, select the objects to be synchronized, and in the Selected object area, confirm the objects to be synchronized. |
|**Advanced configuration** |**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
||**Enable key filtering** |In a data synchronization task, if you only need to synchronize data that meets the conditions to the target database, you can achieve this by using the key filtering function.<br><br>Select whether to enable the key filtering function.<br><br><br>* **Yes**: Indicates that the key filtering function is enabled.<br><br>   * After Key filtering is enabled, you must configure **Filter rules**.<br><br>      * **Allowlist**: If you select **Allowlist** for filtering **rule**, you must enter a regular expression. Indicates that the Keys matched by the regular expression will be synchronized to the Target.<br><br>      * **Blocklist**: If you select **Blocklist** for the filtering rule, you must enter a regular expression. Indicates that the Keys matched by the regular expression will be filtered out, that is, they will not be synchronized to the target.<br><br>   * After Key filtering is enabled, to ensure the accuracy of the synchronized data, click **Online test**. On the **VolcDTSRedisKeyFilter** page, test whether the regular expression you entered completely meets your filtering requirements online. Based on the test results, you can confirm whether the regular expression has the correct syntax and whether it can meet the filtering requirements, so as to reduce the risk of data loss or synchronization errors during data synchronization.<br><br>* **No**: Indicates that the key filtering function is not enabled. |
||**Increment using KSN**<br><br> |Enable KSN for incremental synchronization as needed. After enabling, DTS will use Redis keyspace notification to capture incremental data changes that Redis native replication protocol cannot transmit.<br><br>> **tip**<br><br><br>> Because the KSN mechanism depends on Redis service's real\-time message push, it is highly sensitive to performance. Before enabling this feature, consider the following risks:<br><br><br><br>* > High performance overhead: KSN increases CPU and network load on the source database, which may put significant pressure on online business operations.<br><br><br>* > Prohibited in large key scenarios: Frequent operations on large keys can easily cause KSN message backlog or timeout, leading to synchronization task failure.<br><br><br>* > Data consistency risk: KSN cannot guarantee 100% reliable message delivery. Network fluctuations or high source database load may cause message loss, resulting in inconsistent primary and standby data.<br><br><br>* > SLA not guaranteed: Due to the above instabilities, synchronization links enabled with this feature are not covered by standard SLA protection.<br> |

8. Click **Data validation configuration**.

9. On the **Create synchronization task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   |**Name** |**Description** |
   |---|---|
   |**Data verification**<br><br> |Select whether to configure the data verification function directly when creating a synchronization task (built\-in).<br><br><br>* **Enable**: Configure data verification tasks directly when creating a data synchronization task.<br><br>* **Disable**: (Default) Do not configure data verification tasks when creating data synchronization tasks. |
   |**Validation type** |DTS automatically generates validation types based on the database type and synchronization type, and does not support modification. For more information on validation types, refer to [Background](https://docs.byteplus.com/en/docs/DTS/configuring_data_validation#.6IOM5pmv5L-h5oGv). |
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

   * > For details about the pre\-check, refer to [Pre\-check items](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_redis).

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. Select the configuration method according to the billing method of the task creation:

   * Pay\-as\-you\-go

      On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm billing information** configuration wizard page, verify the instance’s billing information.

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
