---
title: "Connection pool"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Connection_pool"
---

NDB for MySQL provide session\-level and transaction\-level connection pools, which effectively reduce the database load caused by a large number of connections. This topic describes the working principles of the two connection pool types to help you select a suitable connection pool based on your business scenarios.

<span id="mq9AXLpJ"></span>
## Precautions


* Connection pool is currently invite\-only features. If you need to use it, please [submit a ticket](https://console.volcengine.com/workorder/create) to contact technical support.

* Changes to the connection pool configuration apply only to new connections. To modify connection pool settings, refer to [Editing connection endpoints](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Editing_connection_endpoints).

* After you enable the connection pool, permission errors may occur if the same username is configured with different permissions for different hosts. For example, if userA@hostA has permissions for DB_A but userA@hostB does not, unexpected permission issues may occur during connection reuse after you enable the connection pool.

* After you enable the connection pool, a frontend user does not immediately establish a connection with the backend. Instead, when a request is initiated, an idle connection is retrieved from the connection pool or a new one is created. If no connections are available (for example, if the backend database has reached its connection limit or does not exist), the proxy disconnects from the frontend user when executing the request.


<span id="AriElq4G"></span>
## Session\-level connection pool

<span id="1fsUFu29"></span>
### How it works

<div style="text-align: center">
<img src="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c5ff25e1a78b43241deaea8f820a51e4.png" /></div>


A session\-level connection pool is used to reduce the instance load caused by frequent new connections from short\-lived user connections. When the session\-level connection pool is enabled, the NDB for MySQL proxy checks if the backend database connection is idle and reusable after a frontend user disconnects. If the connection is reusable, it is returned to the connection pool and retained for a period. When a new frontend connection is requested, an available idle connection from the pool is reused. If no available idle connections exist, a new connection is created.

<span id="EttqXRqo"></span>
### Limitations


* A session\-level connection pool is unable to reduce the number of concurrent active connections on a database node. Instead, it reuses connections to reduce the scheduling overhead on the database's main thread during connection establishment. Idle connections waiting for reuse in the connection pool temporarily occupy database connection slots.

* A session\-level connection pool is unable to resolve the issue where slow SQL queries prevent short\-lived connections from being released promptly. In such cases, prioritize resolving the slow SQL issues.


<span id="MoishSNm"></span>
## Transaction\-level connection pool

<span id="jIM2aBMx"></span>
### How it works

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_dd178f5d235316644f2bd51c2db83b98.png) </span>

Transaction\-level connection pools are primarily used to reduce the total number of backend database connections and alleviate the database load caused by frequent establishments of short\-lived connections.

When a front\-end User establishes a connection, it first authenticates with the NDB for MySQL proxy. At this stage, no connection is established with the backend database. When a User sends a request, the proxy searches the connection pool for a connection that meets the requirements, including username and Client Capabilities. If a suitable connection exists, it is retrieved and reused. During this process, the system checks for consistency in session variables and schema state. If they are inconsistent, the state is synchronized before the request is sent. If no suitable connection is found, a new connection is created. After the transaction on the current connection ends, the connection is returned to the connection pool to be used by other requests. The connection reuse mechanism of the transaction\-level connection pool can significantly reduce the total number of connections between the proxy and the database in scenarios where there are many front\-end User connections but few concurrent requests.

<span id="UQZQMbDm"></span>
### Limitations


* After a User executes the following types of requests, the acquired connection is not returned to the connection pool. Instead, it remains bound to that front\-end connection and is destroyed after the front\-end connection is terminated.

   * Executing a `PREPARE` statement

   * Creating a temporary table

   * Modifying user variables

   * Use `lock table`

   * Multiple statements

   * Stored procedure call

* Statements related to the previous context, such as the `FOUND_ROWS`, `ROW_COUNT`, and `LAST_INSERT_ID` functions, can be called successfully, but their results are not guaranteed to be accurate.

* The following differences exist between connection pooling and direct connections:

   * The connection ID received by the client does not match the one on the backend, and the thread ID may change when queried multiple times using `select connection_id()`. Executing the `KILL` command may result in the `ERROR 1094 (HY000): Unknown thread id`. To kill a running database request, perform the action in [Session management](https://docs.byteplus.com/en/docs/DBW/Session_information_management).

   * The IP address and port displayed in `show processlist` or [Full SQL insights](https://docs.byteplus.com/en/docs/DBW/Full_SQL_insight_management) may not match the client's actual IP address and port.


<span id="bcTRsIpy"></span>
## Connection pool scenario selection


1. If the user client already supports connection pools or most User connections are persistent, do not enable the connection pool on the NDB for MySQL proxy side.

2. Consider enabling the transaction\-level connection pool if there are a large number of frontend User connections and the business use case does not involve the usage restrictions of the transaction\-level connection pool.

3. Consider using the session\-level connection pool if the business scenario involves short\-lived connections and is subject to the restrictions of the transaction\-level connection pool.
