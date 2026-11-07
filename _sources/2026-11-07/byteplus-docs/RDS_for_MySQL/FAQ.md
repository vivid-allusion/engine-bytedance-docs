---
title: "FAQ"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
section: "Document"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/faq_overview"
---

This topic summarizes the FAQs for using RDS for MySQL.

<span id=".5pyN5Yqh5LiO5pSv5oyB"></span>
## Service and support

<span id=".5Li65LuA5LmI5LqR5pWw5o2u5bqTLW15c3FsLeeJiOS4jeaUr-aMgS1teWlzYW0t5byV5pOO44CBLW1lbW9yeS3lvJXmk47vvJ8="></span>
### Why doesn't RDS for MySQL support the MyISAM and Memory engines?

RDS for MySQL defaults to the InnoDB engine for MySQL 5.7 and later versions. It no longer supports MyISAM, Memory, or Archive engines for the following main reasons:


* RDS for MySQL has implemented numerous kernel optimizations for InnoDB, giving it a significant performance advantage.

* MyISAM uses a table\-level locking mechanism, while InnoDB uses a row\-level locking mechanism. Therefore, InnoDB typically offers higher write efficiency.

* MyISAM's data integrity protection is flawed, which can lead to data corruption or even loss. Most of these flaws are design issues that cannot be fixed without breaking compatibility.

* Migrating from MyISAM and Memory to InnoDB is low\-cost, as most applications only need to modify their table creation code to complete the migration.

* The development of MySQL is shifting toward InnoDB. In the latest official version of MySQL 8.0, all system tables use InnoDB.

* The Memory engine cannot guarantee data integrity. All data in its tables is lost when the instance restarts or during a switch between primary and secondary nodes.


If you have specific requirements for the MyISAM and Memory engines, you can [submit a ticket](https://console.byteplus.com/workorder/create/) to contact RDS for MySQL technical support.

<span id=".5aaC5L2V5oqK5p-l6K-i57uT5p6c5a-85Ye65Yiw5paH5Lu277yf"></span>
### How to export query results to a file?

RDS for MySQL is connected with the Database Workshop, providing relevant capabilities. For more details, refer to [Creating an SQL result set export task](https://docs.byteplus.com/en/docs/DBW/creating-a-sql-result-set-export-task-for-mysql).

<span id=".5aaC5L2V5Y2H57qnLW15c3FsLTUtNy3lrp7kvovliLAtbXlzcWwtOC0wLeWunuS-i--8nw=="></span>
### How to upgrade a MySQL 5.7 instance to a MySQL 8.0 instance?

A MySQL 5.7 instance cannot be directly upgraded to a MySQL 8.0 instance. To upgrade the instance version, you can first create a MySQL 8.0 instance and use Database Transmission Service (DTS) to migrate data from MySQL 5.7 to the MySQL 8.0 instance. For detailed information about migrating data using DTS, refer to [About Database Transmission Service](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service).

<span id="DAJF6OLq"></span>
### When creating an RDS for MySQL instance, can the database kernel minor version be specified?

Not supported.

<span id="9qKVqie2"></span>
### After an RDS for MySQL instance is created, can the time zone be switched?

Switching the time zone is supported. After you create an instance, log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql). On the **Parameters** tab, modify the time zone by changing the default_time_zone parameter.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">After the time zone is switched, issues such as invalid partial time‑related fields in data tables may occur. Proceed with caution.</div>


<span id=".572R57uc6L-e5o6l"></span>
## Network connection

<span id=".5Li65LuA5LmI5peg5rOV6L-e5o6l5pWw5o2u5bqT77yf"></span>
### Why can't I connect to the database?

If you cannot access a database, please conduct troubleshooting as recommended:


* Confirm that the MySQL instance is **Running**.

* Confirm whether an [account has been created](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3) for the instance.

* Confirm that an [IP allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist_1) has been configured.

* If connecting via a private network, confirm that the ECS instance and the MySQL instance are in the same VPC.


If you still cannot connect to the MySQL instance after troubleshooting, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5ZyoLWVjcy3lrp7kvovkvb_nlKgtbXlzcWwt5a6i5oi356uv6L-e5o6lLW15c3FsLeWunuS-i-aXtuaUtuWIsOmUmeivr-aPkOekui1hY2Nlc3MtZGVuaWVk44CC"></span>
### Receiving an `Access denied` error when connecting to a MySQL instance from an ECS instance using a MySQL client.

If you receive the following error message when connecting to a MySQL instance from an ECS instance using a MySQL client, first confirm whether the address of the ECS instance has been added to the allowlist of the MySQL instance. For more information on creating an allowlist, refer to [Creating an allowlist](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_allowlist_1).

```sql
ERROR 1045 (28000): Access denied for user 'example'@'[192.168.xxx.xxx]' (using password: IP NOT IN white List)
```


<span id=".5Y-v5Lul6I635b6XLW15c3FsLeWunuS-i-WFrOe9kei_nuaOpeaIluengee9kei_nuaOpeeahC1pcC3lkJfvvJ8="></span>
### Can I get the IP address for the public or private network connection of a MySQL instance?

No. MySQL connection addresses are provided as domain names.

<span id=".bXlzcWwt5a6e5L6L5YWs572R6L-e5o6l5oiW56eB572R6L-e5o6l55qELWlwLeS8muWPmOWMluWQl--8nw=="></span>
### Will the IP address for a MySQL instance's public or private network connection change?

Typically, the IP address of the connection does not change if the associated Virtual Private Cloud or subnet is not modified. Each connection endpoint corresponds to an ENI network interface address. However, it is recommended to access the instance via the domain name to hide the actual IP address and improve availability. For more information about viewing domain names, refer to [View connection addresses and ports](https://docs.byteplus.com/en/docs/RDS_for_MySQL/viewing_address_and_port).

<span id=".6YeN5ZCv5a6e5L6L5oiW5YiH5o2i5Li75aSH6IqC54K55ZCO77yM5pS25Yiw6ZSZ6K-v5o-Q56S6LWVycm9yLTMzMDAtaHkwMDAtYmFja2VuZC1uZXR3b3JrLWVycm9y44CC"></span>
### After restarting the instance or switching between primary and secondary nodes, the error message `ERROR 3300 (HY000): Backend NetWork Error` is received.

After restarting the instance or switching between primary and secondary nodes, you might receive the `ERROR 3300 (HY000): Backend NetWork Error` prompt. This error indicates a network problem with the database proxy and can be resolved by retrying.

<span id="V1docuqe"></span>
### Does RDS for MySQL support connections from a local device using public and private keys?

Not supported. When you create a database account, you can set the account's **Verification method** to **IAM verification**. In this case, you do not need to set a password for the account. When connecting, the system uses the obtained temporary token instead of a password for verification and login.

<span id="F1wneAlI"></span>
### How to resolve the error `Public Key Retrieval is not allowed` when connecting to a MySQL instance via a client?

Reason: This error occurs because the MySQL instance uses the more‑secure caching_sha2_password password authentication plugin, while the client driver used by your business is an older version incompatible with this authentication method.

Solution: Configure client parameters to allow the client to retrieve the public key from the server. The configuration items for different clients are as follows:


* MySQL command line: `--get-server-public-key`.

* JDBC connection string: `allowPublicKeyRetrieval=true`.

* Python（mysql‑connector‑python）：`allow_public_key_retrieval=True`.


<span id="mup0X5mL"></span>
## Account privileges

<span id=".6auY5p2D6ZmQ6LSm5Y-35ZKM5pmu6YCa6LSm5Y-35pyJ5LuA5LmI5Yy65Yir77yf"></span>
### What are the differences between a super account and a normal account?

Super account: You can create only one super account for each instance. It can manage all normal accounts and databases.

Normal account: You can create multiple normal accounts for an instance. You must manually grant specific database privileges to them.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific information on account privileges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3">Creating an account</a>.</div>


<span id=".6auY5p2D6ZmQ6LSm5Y-36IO95ZCm5L-u5pS55oyH5a6a5p2D6ZmQ77yf"></span>
### Can I modify a specific permission of a super account?

The super account can only be reset to the initial status, not modified to specific permissions.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For specific information on account privileges, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#.5Yib5bu66LSm5Y-3">Creating an account</a>.</div>


<span id=".5pWw5o2u5bqT5piv5ZCm5Y-v5Lul57uR5a6a5aSa5Liq6LSm5Y-377yf"></span>
### Can a database be associated with multiple accounts?

Yes.

<span id=".5Li65LuA5LmI6LSm5Y-355qE54q25oCB5pi-56S64oCc5LiN5Y-v55So4oCd77yf"></span>
### Why is the account state 'Unavailable'?

Reason: If a database account is deleted from the command line after it has been created, its state is displayed as **Unavailable** in the account list on the console.

Solution: Reset the password for the account in the console to restore it to an available state. For details about resetting the password, refer to [Resetting account password](https://docs.byteplus.com/en/docs/RDS_for_MySQL/resetting_an_account_password). We recommend performing account management operations in the console to prevent the account from becoming **Unavailable**.

<span id=".5Y-q6K-76IqC54K5"></span>
## Read\-only node

<span id=".5LuA5LmI5piv5Y-q6K-76IqC54K577yf"></span>
### What is a read\-only node?

For applications with a large number of read requests, you can create one or more read\-only nodes to meet the high demand for database reads and increase application throughput. For detail, refer to [Read-only node overview](https://docs.byteplus.com/en/docs/RDS_for_MySQL/overview_of_read-only_nodes).

<span id=".5aaC5L2V6YCJ5oup5Y-q6K-76IqC54K555qE6KeE5qC877yf"></span>
### How to choose the node specification for a read\-only node?

They can be different from the primary node specification, and can also be modified at any time. We recommend that the specification of a read\-only node be higher than that of the primary node, or else it can easily result in high delays and high load on the read\-only node.

<span id=".5Y-q6K-76IqC54K555qE6LSm5Y-35ZKM5Li76IqC54K55LiA5qC35ZCX77yf"></span>
### Is the account of the read\-only node the same as the primary node?

A read\-only node can be accessed through the account of the primary node.

<span id=".5LiA5Liq5a6e5L6L5LiL5pyA5aSa5Y-v5Lul5Yib5bu65aSa5bCR5Liq5Y-q6K-76IqC54K577yf"></span>
### How many read\-only nodes can be created under one instance at most?

10.

<span id=".5Y-q6K-76IqC54K55Li65L2V5rKh5pyJ5aSH5Lu95Yqf6IO977yf"></span>
### Why do read\-only nodes have no backup function?

Because the primary node already has backups, read\-only nodes currently do not support backup settings or manual backup initiation.

<span id=".5Y-v5Lul5bCG5bey5pyJ55qE6IqC54K55YiH5o2i5Li65Y-q6K-76IqC54K55ZCX77yf"></span>
### Can an existing node be switched to a read\-only node?

You can only add new read\-only nodes to an instance and cannot switch an existing node to a read\-only node.

<span id=".5Yib5bu65Y-q6K-76IqC54K55Lya5b2x5ZON5Li76IqC54K55ZCX77yf"></span>
### Will creating a read\-only node affect the primary node?

When adding a read\-only node, migration of primary and secondary nodes or connection interruptions may occur depending on the resource pool where the cluster resides or the migration method suitable for the current instance. The specific impact is subject to the estimated impact displayed on the Modify configuration page. If you only add a read\-only node in the Modify configuration settings and set the execution time to Execute now, there is a slight chance of causing a migration of the primary and secondary nodes or a connection interruption.

<span id="VEqlXNts"></span>
### After a read‑only node is added, does application code need to be modified?


* Scenarios where no modification to application code is required: If a proxy endpoint is used, read‑write splitting is enabled, and the auto‑add new node feature of the proxy endpoint is turned on, newly added read‑only nodes are automatically associated with the proxy endpoint. Read requests are automatically distributed to new read‑only nodes based on weights, and no modification to application code is required.

* Scenarios where modification to application code is required:

   * If no proxy endpoint is used and only the direct connection endpoint is adopted to access the Primary Node, modification to application code configuration is required after a new read‑only node is added. Read requests must point to the direct connection endpoint address corresponding to the newly added read‑only node to offload requests to the read‑only node.

   * If a proxy endpoint is used but read‑write splitting is not enabled, or the auto‑add new node feature is disabled, the newly added read‑only node needs to be manually associated with the proxy endpoint and read‑write splitting rules must be configured. If the service previously did not use the proxy address, the application connection address needs to be modified to the proxy endpoint address.


<span id="fj8lh1Vo"></span>
### After a read‑only node fails, can read requests be automatically routed to the Primary Node?

Connections endpoints that satisfy both of the following conditions will automatically route read requests to the Primary Node when a read‑only node fails:


* The connection endpoint is a proxy endpoint, and read‑write splitting is enabled.

* The proxy endpoint is associated with the primary node.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If overload protection is not enabled for the connection endpoint, all read requests are automatically routed to the associated primary node after all read‑only nodes fail or are removed due to latency exceeding the threshold, ensuring the availability of business read requests.</div>


* <div data-tips="true" data-tips-type="default">If overload protection is enabled for the connection endpoint, the system triggers the primary node protection mechanism upon overall anomalies of read‑only nodes. Within the configured overload protection duration, read requests are not routed to the primary node to prevent the primary node from being overwhelmed by burst traffic. After the protection duration expires, read requests are automatically switched to the primary node.</div>



<span id=".6K-75YaZ5YiG56a7"></span>
## Read/Write separation

<span id=".5Li65L2V6YCJ5oup6K-75YaZ5YiG56a75Lya5oql6ZSZ77yf"></span>
### Why does choosing read/write separation report an error?

Before enabling read/write separation, confirm a read\-only node is created. If you encounter errors with read/write separation, troubleshoot using the following suggestions:


* Confirm that the MySQL instance is **Running**.

* Confirm that a [read-only node has been created](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1) and the instance is in a **Running** state.


If errors with read/write separation persist after troubleshooting, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".6K-75YaZ5YiG56a755qE5L2c55So5piv5LuA5LmI77yf"></span>
### What is the function of Read/Write separation?

After enabling Read/Write separation, eligible read requests can be forwarded to read\-only nodes for execution, reducing the read load on the primary node. For detailed information about the request forwarding logic after enabling Read/Write separation, refer to [Enabling Read/Write separation](https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_read-write_splitting#.6IOM5pmv5L-h5oGv).

<span id=".5LuA5LmI5piv5YWo5bGA5Y-q6K-777yf"></span>
### What is global read\-only?

After enabling global read\-only, you can set a MySQL instance to be read\-only, preventing writes.

<span id=".5byA5ZCv5YWo5bGA5Y-q6K-75ZCO77yM5piv5ZCm5Lya6KaG55uW6LSm5Y-35p2D6ZmQ77yf"></span>
### Does enabling global read\-only override account privileges?

After global read\-only is enabled, only read permission is available.

<span id=".5aSH5Lu95oGi5aSN"></span>
## Backups

<span id=".5Li65LuA5LmI5peg5rOV6L-b6KGM5aSH5Lu95pON5L2c77yf"></span>
### Why can't I perform a backup?

If you are unable to perform a backup operation, check the following:


* Confirm that the MySQL instance is **Running**.

* Confirm that no DDL operations are ongoing during the backup period to avoid table locks that may cause a backup failure.

* You cannot create backups for an instance with more than 600,000 tables. When there are too many tables, splitting the instance is recommended.


If the problem persists, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5aSH5Lu957G75Z6L5piv5ZCm5pSv5oyB6YC76L6R5aSH5Lu977yf"></span>
### Does the backup type support logical backup?

Support.

<span id=".5LqR5pWw5o2u5bqTLW15c3FsLeeJiOacieWTquS6m-WuueeBvuaWueahiO-8nw=="></span>
### What disaster recovery solutions are available for RDS for MySQL?


1. RDS for MySQL provides an online, high\-availability architecture with primary and secondary nodes to ensure service availability. If the primary node fails, it automatically detects the failure and switches over to the secondary node within seconds.

2. Supports multi\-availability zone deployment. When creating or restoring a new instance, you can assign the primary, standby, and read\-only nodes to different availability zones within the same region to enable cross\-availability zone disaster recovery.

3. Supports cross\-regional backups and restores.

4. You can achieve online cross\-regional disaster recovery by configuring synchronization tasks with Database Transmission Service. For more details, refer to [Synchronization solution overview](https://docs.byteplus.com/en/docs/DTS/overview_of_synchronization_solutions).


<span id="HKTzZcuA"></span>
## Service availability

<span id="ZpRAXLZ1"></span>
### What are the precautions for switching primary node?


* A primary/secondary switchover may cause one or two transient disconnections. Ensure your applications have automatic reconnection mechanisms.

* If an instance has read\-only nodes, data on these nodes will experience a period of latency after a primary/secondary switchover. This is due to factors such as rebuilding the replication link and synchronizing incremental data.

* Switchover can be completed within 5 seconds without a delay in primary/secondary replication.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note for more details on primary/secondary switchover, refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_MySQL/switching_primary_nodes">Switching primary node</a>.</div>


<span id="j1PP6ERi"></span>
### Do I need to update the connection address in my service after a primary/secondary switchover?

The primary and secondary addresses are the same. You do not need to change the address after a primary/secondary switchover, but be aware that a transient disconnection may occur during the process.

<span id="wxpjwWzB"></span>
## Data interaction

<span id="1ylXxX8H"></span>
### How does the RDS for MySQL example execute the initialization SQL script?

You can execute the initialization SQL script through the SQL window of the [Database Workshop](https://docs.byteplus.com/en/docs/DBW/logging-on-to-the-data-interaction-platform-for-rds-for-mysql?lang=en). For more information, refer to [SQL window](https://docs.byteplus.com/en/docs/DBW/Introduction_to_SQL_window?lang=en).

<span id="GtY9r7Cy"></span>
### How can successful data migration be confirmed?


* If you perform migration via Data Transmission Service (DTS), you can view the DTS task results. In the migration task list, click the migration task name, and then click Data Validation to view the validation results.

* If you migrate the data via other methods, you can log in to the database and execute the following SQL statements to count and compare row numbers of each table and check whether the number of tables is consistent.

   ```SQL
   SELECT COUNT(*) FROM <原表名>; 
   SELECT COUNT(*) FROM <迁移后的表名>; 
   ```
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Executing the COUNT command will increase CPU and memory usage, so it is not recommended to run it during business peak hours.   </div>
   

      * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can run the query after executing <code>ANALYZE TABLE oneapi_eye</code>.   </div>
   


<span id="Hef33c5K"></span>
## Security

<span id=".bXlzcWwt5a6e5L6L5b-F6aG76K6-572u55m95ZCN5Y2V5ZCX77yf"></span>
### Do MySQL instances require an allowlist?

If a default allowlist is configured in the current region, the MySQL instance is associated with the default allowlist after it is created. IP addresses or address ranges within the default allowlist can access the instance. If no default allowlist is configured in the current region, the MySQL instance is not associated with any allowlists after it is created, and cannot be accessed by any IP address.

<span id=".5Y2V5Liq5a6e5L6L5pyA5aSa5Y-v5Lul57uR5a6a5aSa5bCR5Liq55m95ZCN5Y2V77yf"></span>
### How many allowlists can a single instance associate?

A single instance can associate up to 100 allowlists.

<span id=".5q-P5Liq55m95ZCN5Y2V5pyA5aSa5pSv5oyB5aSa5bCRLWlwLeaIluiAhS1pcC3mrrXvvJ8="></span>
### How many IP addresses or IP address ranges can an allowlist support?

An allowlist can support up to 300 IP addresses or IP address ranges.

<span id=".5LiA5Liq55m95ZCN5Y2V5pSv5oyB57uR5a6a5Yiw5aSa5Liq5a6e5L6L5ZCX77yf"></span>
### Can an allowlist be associated with multiple instances?

Support. An allowlist can be associated with up to 500 instances.

<span id="82lFGGYg"></span>
### Does RDS for MySQL support setting a denylist?

Not supported. After an RDS for MySQL instance is created, no allowlists or IP addresses are bound, and access to the instance is denied for all IP addresses by default. You can configure the instance allowlist as needed later. Within the IP addresses bound to the instance allowlist, the presence of [0.0.0.0/0](http://0.0.0.0/0) means access is permitted for all addresses. If only the [127.0.0.1](http://127.0.0.1/) address is bound to the instance, access to the instance is denied for all addresses.

<span id=".5pel5b-X"></span>
## Log

<span id=".5oWi5pel5b-X5piO57uG5Y-v5L-d55WZ5aSa5LmF77yf"></span>
### How long can I store the slow log details?

Slow log details can be stored for 30 days.

<span id=".6KKr6K6w5b2V5Zyo5oWi5pel5b-XLXNxbC3or63lj6XnmoTpu5jorqTml7bplb_mmK_vvJ_og73lkKboh6rlrprkuYnvvJ8="></span>
### What is the default duration for SQL statements to be recorded in the slow log? Can it be customized?

By default, SQL statements with an execution time exceeding 1 second are recorded in the slow log. You can change this duration by modifying the `long_query_time` parameter in Parameter setting. For details, refer to [Modifying parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

<span id="GZPukFPe"></span>
### How are SQL execution records viewed for an RDS for MySQL instance?


* You can view the execution history records of SQL statements in the Execution History area of the SQL Window in Database Workshop (DBW). However, Database Workshop (DBW) only records SQL operations performed by the currently‑logged‑in account within DBW and cannot record operations executed through other clients.

* If you have enabled the [database audit](https://docs.byteplus.com/en/docs/DBW/database-audit-management-for-mysql?lang=en) feature, you can view the execution history records of SQL statements on the Database Audit tab of Database Workshop (DBW).

* If you have not enabled the database audit feature, you can [download Binlog logs](https://docs.byteplus.com/en/docs/RDS_for_MySQL/downloading_binlog_backups?lang=en) on the console for parsing and view the execution history records of SQL statements. However, Binlog logs only record operations such as insertion, deletion and modification, and do not record query operations.


<span id=".5Y-C5pWw"></span>
## Parameter

<span id=".5Zyo5Y-C5pWw566h55CG5Lit5Li65LuA5LmI5om-5LiN5Yiw6ZyA6KaB5L-u5pS555qE5Y-C5pWw77yf"></span>
### Why can't I find the parameter I need to modify in parameter management?

For security and stability reasons, only some parameters can be modified. For a list of modifiable parameters, refer to [List of modifiable parameters in MySQL 5.7](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_5_7) and [List of modifiable parameters in MySQL 8.0](https://docs.byteplus.com/en/docs/RDS_for_MySQL/list_of_modifiable_parameters_in_mysql_8_0). If you cannot find the parameter you need to modify, [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical support.

<span id=".5L-u5pS55Y-C5pWw5ZCO77yM6ZyA6KaB6YeN5ZCv5a6e5L6L5ZCX77yf"></span>
### Does the instance need to be restarted after modification of parameters?

Some parameters require restarting the instance after modification. You can check the **Need restart?**  column under **Parameter configuration** \> **MySQL parameters** to see if you need to [restart the instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/restarting_an_instance). For details, refer to [Modifing parameters](https://docs.byteplus.com/en/docs/RDS_for_MySQL/modifying_parameters).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Operate during business off\-peak hours and ensure the application has a reconnection mechanism.</div>


<span id=".5pSv5oyB5L-u5pS557O757uf5Y-C5pWw5qih5p2_5ZCX77yf"></span>
### Is it possible to modify the system parameter template?

The system parameter template cannot be modified. You can modify the c[ustom template](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_parameter_template) instead.

<span id=".5aaC5L2V5p-l6K-i5LqR5pWw5o2u5bqTLW15c3FsLeeJiOS4jeaUr-aMgeS_ruaUueeahOWPguaVsOeahOiuvuWumuWAvO-8nw=="></span>
### How do I check the values of parameters that cannot be modified in RDS for MySQL?

Log on to [Database Workshop](https://console.byteplus.com/dbw) and use the SQL statement `SHOW variables like 'Parameter name'` to check.

<span id="fz9u5PkW"></span>
## Storage

<span id="pK11Sfh4"></span>
### How to solve the error "**PrecheckFailed_DiskSpaceInsufficient" (insufficient disk space)**  when executing the statement "alter table operator_log engine=innodb"?


* (Recommended) [Expand the storage space](https://docs.byteplus.com/en/docs/RDS_for_MySQL/standard_instance_specification_modification?lang=en). The remaining disk space of the instance must be greater than twice the storage space occupied by the current table.

* If you change the table structure using a non‑locking method, it will not affect the business read and write operations during the process, but it will occupy some storage space. It is recommended that you clear the table space at an off‑peak business period.


<span id="8UrSvYcF"></span>
### Why is the space not released after deleting the database data?

After you delete data by using the DELETE command, storage space is not released immediately. You need to run the `OPTIMIZE TABLE <table_name>;` command to reclaim table space for the storage space to be released.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Running the <code>OPTIMIZE TABLE <table_name>;</code> command rebuilds the table. Exercise caution when performing this operation for large‑volume data. It is recommended to perform the operation during business off‑peak hours to avoid long‑term blocking that affects normal business operations.</div>
