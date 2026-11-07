---
title: "Synchronizing to Volcano Engine Cache for Redis"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/Synchronizing_to_Volcano_Engine_Cache_for_Redis"
---

This topic describes how to create a public network Redis synchronization task to Volcengine Cache for Redis in the Database Transmission Service (DTS) console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A self\-managed instance for Cache for Redis has been set up in the public network environment, with the database account and password configured.

* A database for Cache for Redis has been created, and the account password has been set. For detailed steps, refer to [Creating an instance](https://docs.byteplus.com/en/docs/redis/create-instance) and [Setting an account password](https://docs.byteplus.com/en/docs/redis/create-manage-account).

* When the access method of the database instance is self\-managed over the Internet and access restrictions are enabled, add the DTS server IP addresses to the allowlist or security group of the database instance before creating the database transmission task. DTS server IP addresses vary by region, as detailed below:

   * DTS server IP addresses in China (Guangzhou), China (Shanghai), and China (Beijing) are `221.194.189.0/27,157.148.90.32/27,180.184.132.64/27,61.129.54.64/27,220.196.172.32/27,117.135.143.32/27,220.196.168.32/27,116.132.250.32/27,111.45.13.32/27,125.88.248.32/27,180.153.35.32/27,220.181.65.32/27,220.181.65.64/27`.

   * DTS server IP addresses in Asia Pacific (Johor) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

   * DTS server IP addresses in Asia Pacific (Jakarta) are `221.194.189.0/27,157.148.90.32/27`.

   * DTS server IP addresses in China (Hong Kong) are `101.47.0.32/27,220.181.65.32/27,220.181.65.64/27,101.47.65.192/27,101.47.65.32/27`.

      For more information on the CIDR block of DTS servers, refer to [Adding the CIDR block of the DTS server](https://docs.byteplus.com/en/docs/DTS/Adding_the_CIDR_block_of_the_DTS_server).

* Confirm the network connectivity and service availability of the source and target databases before creating a data synchronization task.

* You can also refer to the descriptions in the pre\-check items to prepare the synchronization objects in the source and target databases. For more information, refer to [Pre-check items (Redis)](https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_redis).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The synchronization task performs incremental synchronization by default.

* When the source database is a self\-managed Cache for Redis, do not restart or switch the source or target database between primary and secondary during synchronization, as this will cause the synchronization task to fail.

* In full and incremental synchronization tasks of Stream, do not perform double\-write operations on the target database instance, as this may cause the synchronization task to fail.

* Synchronizing instances with SSL enabled is not supported.

* During synchronization, do not change the instance configuration. Otherwise, the synchronization task will fail.

* If different DBs map to the same DB and the same Key exists in different DBs, it may cause unpredictable results including data inconsistency or task failure during synchronization.

* To Synchronize data from the Alibaba Cloud Redis to BytePlus Cache for Redis, the Alibaba Cloud database account must have replication permissions.

* Database Transmission Service (DTS) currently does not support synchronizing data from Alibaba Cloud's cloud\-native in\-memory Database Tair to BytePlus Cache for Redis. To synchronize, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support.

* During data synchronization, if duplicate key values are encountered in the target database, DTS will not retain the conflicting data at the destination. Instead, the data from the source will overwrite the data at the destination.

* Cache for Redis Enterprise Edition is currently in beta testing. to synchronize to Cache for Redis Enterprise Edition, [submit a ticket](https://console.byteplus.com/workorder/create/) to request the service. For more information on Cache for Redis Enterprise Edition, refer to [What is Cache for Redis Enterprise Edition](https://docs.byteplus.com/en/docs/84772/1258077).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|**Type** |**Description** |
|---|---|
|Source database limits |* Bandwidth requirements: Adequate egress bandwidth is required on the source database server. Failure to meet this prerequisite will lead to suboptimal synchronization performance.<br><br>* When certain keys in the source database use an expiration (expire) policy, a situation may arise where expired keys are not deleted promptly. This can result in the target database appearing to have fewer keys than the source database.<br><br>* During synchronization, if the source database undergoes scaling such as adding or removing shards, or changes in specifications like memory expansion, you need to reconfigure the task. To ensure consistent data, it is recommended to clear data that has been synchronized to the target Cache for Redis instance before reconfiguring the task.<br><br>* During synchronization, if the source database connection address changes and causes the task to fail, you need to reconfigure the task. If it fails, you can [submit a ticket](https://console.byteplus.com/workorder/create/) for technical support. If it is not processed for a long time, the source database will reset the AOF file. |
|Other limits |* It is recommended that the source and target Cache for Redis databases be the same version, or synchronize from a lower version to a higher one to ensure compatibility. If you synchronize from a higher version to a lower version, there may be database compatibility or data loss issues.<br><br>* During incremental data synchronization, DTS cannot confirm the execution success of Lua scripts called via `EVAL` or `EVALSHA`, as the target database does not explicitly return execution results for scripts.<br><br>* During full data synchronization, DTS consumes certain read/write resources on both the source and target databases, which may lead to an increased load on the database servers. When the database workload is heavy or server specifications are low, it may increase database pressure, even causing the database service to become unavailable and the data synchronization task to fail.<br><br>* It is recommended to perform data synchronization during off\-peak hours. You can also increase the parameter value of the source database's `client-output-buffer-limit` to prevent buffer overflow when synchronizing large Keys.<br><br>* The storage space of the target Cache for Redis database must be greater than the storage space occupied by the source Cache for Redis database.<br><br>* When DTS transfers data using the `psync` and `sync` commands, it overwrites data in the target database. If the target database already contains the same Key, it will first execute the `del` operation.<br><br>* In the event of a transient connection failure on the source or target instance, a full data re\-synchronization may be triggered, potentially leading to data inconsistency.<br><br>* If the target database's data eviction policy parameter `maxmemory-policy` is configured to a value other than `noeviction`, it may cause the target database's data to be inconsistent with the source database. |


<span id=".5pSv5oyB55qE5ZCM5q2l5p625p6E"></span>
## Supported synchronization architectures


* One\-to\-one unidirectional synchronization

* One\-to\-many unidirectional synchronization

* Many\-to\-one unidirectional synchronization

* Cascading unidirectional synchronization


For information on the types and usage of synchronization topology supported by DTS, refer to [Data synchronization topology](https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology).

<span id=".5pSv5oyB55qE5ZG95Luk"></span>
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


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Cache for Redis 7.0 does not support <code>Function</code> commands.</div>


<span id=".5pWw5o2u5bqT6LSm5Y-35pyA5bCP5p2D6ZmQ562W55Wl"></span>
## Database account minimum permission policy


|**Database** |**Privilege** |
|---|---|
|Source database |You can execute the `sync`, `psync`, and `config get` commands. |
|Target database |You can execute write commands. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [DTS console](https://console.byteplus.com/dts).

2. On the top menu bar, select the project and region.

3. In the left navigation bar, click **Data synchronization**.

4. On the **Synchronization task list** page, click **Create task**.

5. On the **Create synchronization task** page, locate the **Configure source and target database** wizard, and configure the following parameters information.

   
   |**Type** |**Name** |**Description** |
   |---|---|---|
   |**Basic information** |**Task name** |Optional. Customize the task name. The length must be within 256 characters.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If not set, the system generates a task name by default according to the naming rule, starting with <code>dts-</code>.</div><br> |
   ||**Link specification** |Select the link specifications for the synchronization task as needed. **Compact**,  **Medium**, and **Standard** are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The link specification can not be modified after the task is successfully created. For details on the link specifications, refer to <a href="https://docs.byteplus.com/en/docs/DTS/product_specifications">Product specifications</a>.</div><br> |
   ||**Synchronization topology** |Currently only **unidirectional synchronization** is supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information about the synchronization topology, refer to <a href="https://docs.byteplus.com/en/docs/DTS/data_synchronization_topology">Data synchronization topology</a>.</div><br> |
   |**Source database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |select **Redis connected over public network**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When synchronizing Redis connected over public network instances, you must add DTS IP segment access permissions in the source end's allowlist or security group policy in advance. Click <strong>View DTS CIDR blocks</strong> to view and copy the CIDR block.</div><br> |
   ||**Host address** |Enter the host address of the self\-managed instance. |
   ||**Port** |Enter the port number of the self\-managed instance. |
   ||**Database account** |The default account is **default**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">when the version of public network Redis is above 6.0, you can set the database account number based on actual conditions.</div><br> |
   ||**Database password** |Enter the password corresponding to the database account of the self\-managed instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the Redis connected over public network enables passwordless login, you do not need to enter the password for the instance database account.</div><br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check the network**: When this error prompt appears, confirm network connectivity.<br><br>* **Connection authentication failed. Check the username and password**: When this error prompt appears, verify your username and password.<br><br>* **Invalid IP address**: When this error prompt appears, verify the accuracy of the IP address. |
   |**Target database configuration** |**Select an existing data source** |You can choose whether to use an existing instance as needed:<br><br><br>* Use existing instances: Click **Select an existing data source**, then in the **Select data source** control panel, choose the target region from the **Region** drop\-down list, and select the target data source. Supports selecting data sources by data source name and ID. For methods to create data sources, refer to [Data source management](https://docs.byteplus.com/en/docs/DTS/Data_source).<br><br>* Do not use existing instances: If not using an existing instance, you need to configure the following database instance information. |
   ||**Instance type** |Select **Redis**. |
   ||**Access method** |Select **BytePlus Cache for Redis**. |
   ||**Redis Instance** |Select the target instance of Cache for Redis from the drop\-down list.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can also search for the target instance by instance ID or name.</div><br> |
   ||**Database account** |The default account is **default**, and you can set the database account on a case\-by\-case basis. |
   ||**Database password** |Enter the password corresponding to the database account of the source instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When password\-free access is enabled for Cache for Redis instances, access the target instance without entering a password. For steps on enabling password\-free access, refer to <a href="https://docs.byteplus.com/en/docs/redis/pwd-free-access">Password\-free access</a>.</div><br> |
   ||**Test connection** |Click **Test connection** to verify the connection to the instance. If the test connection fails, modify the configuration based on the failure prompt, and then click **Test connection** again to verify the connection. The details are as follows:<br><br><br>* **Connection authentication failed. Check if the username and password are correct**: When this error prompt appears, verify your username and password.<br><br>* **Connection authentication failed, unable to create connection normally, contact customer service**: When this error prompt appears, [submit a ticket](https://console.byteplus.com/workorder/create) for technical support. |
   |**None** |**Project** |Optional. Select the affiliated project for the task from the drop\-down list. By default, it is under **default (default project)** . You can also click **Create new project** to create a new project. <br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">After a task is created successfully, if you need to change its affiliated project, you can move the resource to another project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A project is a virtual concept that includes a set of resources, users, and roles. A project allows for a unified view and management of a set of resources, and controls the permissions of users and roles within the project for those resources.</div><br> |
   ||**Tag** |(Optional) Click **Add tag** to add a tag to the instance. Tags can help you categorize cloud resources, control access to them, and allocate bills and costs. A tag is a key\-value pair that identifies a cloud resource. You can use tags to categorize resources with the same characteristics from different dimensions, such as purpose or owner, making it easier to filter, aggregate, and manage your cloud resources. For more details about tags, refer to [Tag overview](https://docs.byteplus.com/en/docs/6649/189377). The rules for tag key\-value pairs are as follows:<br><br><br>* Key<br><br>   * Supports any language, characters, numbers, spaces, or symbols (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 1 to 128 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br>   * Keys cannot start with any form of `volc:`, such as `Volc:` or `VOLC:`.<br><br>* (Optional) Value<br><br>   * Supports any language, character, digit, space, or symbol (`_.:/=+-@`).<br><br>   * Case\-sensitive, and the length is 0 to 256 characters.<br><br>   * In UTF\-8 encoded Unicode format.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Support fuzzy search for selecting existing tag keys and tag values.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A maximum of 20 tags can be associated with a task in a single operation. A maximum of 50 tags can be associated with a single task.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">For a single resource, tag keys must be unique, and each tag key can have only one value.</div><br> |
   ||**Billing method** |Select a billing method: **Pay\-as\-you\-go** or **Subscription**.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For detailed billing information, refer to <a href="https://docs.byteplus.com/en/docs/DTS/billing_overview">Billing instructions</a>.</div><br> |
   ||**Subscription duration** |Select the duration of the subscription as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When selecting <strong>Subscription</strong> in <strong>Billing method</strong>, you can set the purchase time and also check <strong>Automatic renewal</strong>. The system automatically renews before task expiration.</div><br> |
   

6. Click **Next: configure synchronization object**.

7. On the Configure synchronization objects wizard page, configure the following parameter information.

   
   |**Name** ||**Description** |
   |---|---|---|
   |**Synchronization type** ||Select the synchronize type as needed. Currently, **Full initialization** and **Incremental synchronization** are supported.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip"><strong>Incremental synchronization</strong> is selected by default.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">A forward synchronization task can select only incremental synchronization. In this case, the historical full data of the source end is not initialized to the destination. Reverse Synchronization does not currently support selecting Full initialization.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you select <strong>Full initialization</strong>, after the pre\-check is completed, DTS will initialize the data of the objects to be synchronized from the source instance in the target instance, which serves as the basis for subsequent incremental data synchronization.</div><br> |
   |**Synchronization object** ||In the **Synchronize object ** area, select the objects you want to synchronize, and in the **Selected object** area, confirm the objects you want to synchronize. |
   |**Advanced configuration** |**Error retry time** |If a synchronization task fails due to a disconnection between the source and target databases, the system immediately retries connecting to them multiple times within the specified time. Value range: 600–86400, in seconds (s). The default value is 600 seconds. |
   ||**Enable key filtering** |In a data synchronization task, if you only need to synchronize data that meets the conditions to the target database, you can achieve this by using the key filtering function.<br><br>Select whether to enable the key filtering function.<br><br><br>* **Yes**: Indicates that the key filtering function is enabled.<br><br>   * After Key filtering is enabled, you must configure **Filter rules**.<br><br>      * **Allowlist**: If you select **Allowlist** for filtering **rule**, you must enter a regular expression. Indicates that the Keys matched by the regular expression will be synchronized to the Target.<br><br>      * **Blocklist**: If you select **Blocklist** for the filtering rule, you must enter a regular expression. Indicates that the Keys matched by the regular expression will be filtered out, that is, they will not be synchronized to the target.<br><br>   * After Key filtering is enabled, to ensure the accuracy of the synchronized data, click **Online test**. On the **VolcDTSRedisKeyFilter** page, test whether the regular expression you entered completely meets your filtering requirements online. Based on the test results, you can confirm whether the regular expression has the correct syntax and whether it can meet the filtering requirements, so as to reduce the risk of data loss or synchronization errors during data synchronization.<br><br>* **No**: Indicates that the key filtering function is not enabled. |
   ||**Use KSN for incremental**<br><br> |Enable KSN for incremental synchronization as needed. After enabling, DTS will use Redis keyspace notification to capture incremental data changes that Redis native replication protocol cannot transmit.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Because the KSN mechanism depends on Redis service's real\-time message push, it is highly sensitive to performance. Before enabling this feature, consider the following risks:</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">High performance overhead: KSN increases CPU and network load on the source database, which may put significant pressure on online business operations.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Prohibited in large key scenarios: Frequent operations on large keys can easily cause KSN message backlog or timeout, leading to synchronization task failure.</div><br><br><br>* <div data-tips="true" data-tips-type="default">Data consistency risk: KSN cannot guarantee 100% reliable message delivery. Network fluctuations or high source database load may cause message loss, resulting in inconsistent primary and standby data.</div><br><br><br>* <div data-tips="true" data-tips-type="default">SLA not guaranteed: Due to the above instabilities, synchronization links enabled with this feature are not covered by standard SLA protection.</div><br> |
   

8. Click **Data validation configuration**.

9. On the **Create synchronization task** page, locate the **Configure data verification** wizard, and configure the following parameters.

   
   |**Name** |**Description** |
   |---|---|
   |**Data verification**<br><br> |Select whether to configure the data verification function directly when creating a synchronization task (built\-in).<br><br><br>* **Enable**: Configure data verification tasks directly when creating a data synchronization task.<br><br>* **Disable**: (Default) Do not configure data verification tasks when creating data synchronization tasks. |
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

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you choose to <strong>Ignore</strong> the alert and start the synchronization task, it may cause data inconsistencies and business risks.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For details about the pre\-check, refer to <a href="https://docs.byteplus.com/en/docs/DTS/consumption_checkpoint_items_redis">Pre\-check items</a>.      </div>
      

13. At the bottom\-right of the **Pre\-check** page, click **Confirm order**.

14. Select the configuration method according to the billing method of the task creation:

   * For pay\-as\-you\-go, reconfirm the configuration on the **Confirm order** wizard page. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

   * Subscription

      1. On the **Confirm order** configuration wizard page, confirm the configuration information again. Read the Service\-Specific Terms for BytePlus Database Products and Services and check **I have read and agree to Service\-Specific Terms for BytePlus Database Products and Services**, and click **Create and start a task**.

      2. On the **Confirm billing information** configuration wizard page, verify the instance’s billing information.

      3. Optional. Click **Voucher redemption**. In the **Voucher redemption** dialog box, enter the voucher code and click **Redeem**.

      4. Optional. In the voucher area, select an available voucher as needed. Only one voucher can be selected at a time to offset part of the cost. You can also choose not to use a voucher.

      5. Click **Next step**.

         <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="3">tip         </div>
         

         <div data-tips="true" data-tips-type="tip" data-wrapper-indent="3">Once the <strong>Payment is completed</strong> on the configuration wizard page, a <strong>Successful payment</strong> message means your task has been created.         </div>
         

After successfully creating the data synchronization task, you can return to the DTS console to view the data synchronization task information on the data synchronization task list.
