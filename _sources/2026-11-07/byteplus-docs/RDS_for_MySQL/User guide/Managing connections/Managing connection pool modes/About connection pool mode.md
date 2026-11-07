---
title: "About connection pool mode"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/about_connection_pool_mode"
---

A database connection pool is responsible for allocating, managing, and releasing database connections. By selecting the corresponding connection pool mode based on specific business scenarios, you can improve the performance of the database and improve the utilization of database resources. RDS for MySQL provides direct connection pools and transaction\-level connection pools.

<span id="introduction-to-connection-pool-modes"></span>
## Introduction to connection pool modes


|**Connection pool mode** |**Mode introduction** |**Usage Scenario** |
|---|---|---|
|Transaction\-level connection pool (default) |It supports connection reuse to reduce the number of direct connections to the database and the load caused by frequent new connections in scenarios with a large number of short connections. |* This applies to businesses with a large number of short connections. Native MySQL is not good at short connection scenarios.<br><br>* Connection convergence, supports higher concurrent connections. |
|Direct connection pool |It is also known as the no connection pool mode, where the connection pool of Proxy no longer performs connection reuse, that is, a new connection is synchronized every time a client creates a new connection to Proxy. |* This is applicable to businesses that mainly use long connections.<br><br>* The user application layer supports the connection pool.<br><br>* The connection status must be queried. For example, `14493` is executed.<br><br>* The accuracy of the `FOUND_ROWS()` function can be guaranteed without read/write splitting. |


&nbsp;

<span id="limits"></span>
## Limits

<span id="restrictions-on-the-use-of-transaction-level-connection-pools"></span>
### Restrictions on the use of transaction\-level connection pools


* When the following operations are performed, a connection is locked until it ends (that is, the connection is no longer placed in the connection pool for other users to use).

   * Execute a `PREPARE` statement or execute `COM_STMT_PREPARE` related protocols.

   * Create a temporary table.

   * Modify user variables.

   * Use `lock table`.

   * Create a temporary table.

   * Multiple statements.

   * Call the stored procedure.

* Calling `FOUND_ROWS`, `ROW_COUNT`, and `LAST_INSERT_ID` functions is not supported. These functions can be called successfully, but the call results may not be correct.

* For a connection with `wait_timeout` set, `wait_timeout` may not take effect on the client because each request gets a connection from the connection pool, and only backend connections in the connection pool are disconnected in case of `wait_timeout`. The disconnection of backend connections does not cause the client disconnection.

* If the business depends on session\-level system variables other than the four variables of `sql_mode`, `character_set_server`, `collation_server`, and `time_zone`, the `set` statement must be explicitly executed after the client connection is established, otherwise the connection pool may reuse the connection for which system variables have been changed.

* Since connections may be reused, you can use `select connection_id()` to query the thread ID of the current connection.

* Since connections may be reused, the IP address and port displayed by `show processlist` may not match the actual IP address and port of the client.

* The database proxy responds after merging `show processlist` results on all nodes. The thread IDs of the frontend and backend connections cannot be matched after the transaction\-level connection pool is enabled. As a result, the `kill` command may report an error even though the `kill`' command has actually been executed successfully. You can determine whether the corresponding connection is disconnected based on `show processlist`.

* Do not set different permissions for the same database account under different IP addresses because it can cause permission errors during connection reuse. For example, if the database_01 permission is set for user@192.168.1.1, but user@192.168.1.2 does not have the database_01 permission, a permission error may occur when the connection pool is enabled.


<span id="restrictions-on-the-use-of-the-direct-connection-pool"></span>
### FOUND_ROWS


* Since the frontend and backend Proxy connections are inconsistent, you can use `select connection_id()` to query the thread ID of the current connection.processlist

* Since the frontend and backend Proxy connections are inconsistent, the IP address and port displayed by `show processlist` may not match the actual IP address and port of the client.

* The database proxy responds after merging `show processlist` results on all nodes. The thread IDs of the frontend and backend Proxy connections cannot currently be matched. As a result, the `kill` command may report an error even though the `kill` command has actually been executed successfully. You can determine whether the corresponding connection is disconnected based on `show processlist`.


<span id="comparison-of-connection-pool-modes"></span>
## Comparison of connection pool modes

<span id="comparison-of-structures"></span>
### Comparison of structures


* Transaction\-level connection pool: The same client can use multiple proxy connections.

* Direct connection pool: The same client can use only one backend connection.


<span id="comparison-of-functions"></span>
### Comparison of functions

Most of the functions of the direct connection pool and transaction\-level connection pool are the same. Because the direct connection pool is directly associated with the user, these two connection pool modes are somewhat different when the immediate connection update function is involved.


|**Function** |**Transaction\-level connection pool** |**Direct connection mode** |
|---|---|---|
|Read/Write Splitting |Supported |Supported |
|Read/Write weight |Supported |Supported |
|Delay threshold |Supported |Supported |
|Failover of read/write splitting |Supported |Supported |
|Parameters modified through the console take effect immediately |Supported |Not supported. Modified parameters take effect only after the user disconnects in the direct connection mode. |
|Connection reuse |Supported |Not supported |
