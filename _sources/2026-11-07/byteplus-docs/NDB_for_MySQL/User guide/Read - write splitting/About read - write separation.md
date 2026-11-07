---
title: "About read/write separation"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/About_read_write_separation"
---

NDB for MySQL instances support read\-write splitting by default. The client only needs to connect to the instance through the address of the connection endpoint. The database agent will automatically send write requests to the primary node and send read requests to the primary node or read\-only node according to the load balancing strategy.

<span id=".5Y6f55CG5LuL57uN"></span>
## Principle introduction

NDB for MySQL uses a primary\-replica architecture and scales read capabilities horizontally by adding multiple read\-only nodes. To help applications adapt to this architecture, the proxy offers a read\-write splitting feature that automatically identifies read and write requests and routes them to different nodes for transparent scaling of read capabilities.

The read\-write separation function of NDB for MySQL disperses the request traffic to different nodes. Write operations such as `UPDATE`, `DELETE`, `INSERT`, and `CREATE` are only processed by the primary node, while `SELECT` read operations are automatically distributed to all nodes for processing, thus achieving read\-write separation. Each NDB for MySQL instance contains only one primary node and supports up to 15 read\-only nodes, which can greatly improve query efficiency and reduce the pressure on the primary node.

<span id=".6K-75YaZ5YiG56a7562W55Wl"></span>
## Read/Write splitting strategy


|Endpoint mode |Forwarding strategy |Request type |
|---|---|---|
|**Read/Write endpoint** |Requests sent only to the primary node |* All DDL and DML operations.<br><br>* Requests in all transactions.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">All read requests before the first write request after transaction splitting is enabled will be sent to the read\-only node.   </div><br>   <br><br>* Custom function.<br><br>* Stored procedure.<br><br>* EXECUTE statement.<br><br>* Requests that use temporary tables.<br><br>* `SELECT 1494838`. |
||Requests sent to both the primary and read\-only nodes |* Non\-transactional read requests.<br><br>* `COM_STMT_EXECUTE` command (Execute preprocessed SQL).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After enabling the <strong>Primary node accepts read requests</strong>, requests are sent to both the primary node and the read\-only node.</div><br> |
||Always send requests to all nodes |* Change requests for all system variables.<br><br>* `USE` command.<br><br>* Query and modify user variables.<br><br>* `KILL` (Terminates the database connection or cancels the running SQL).<br><br>* `COM_STMT_PREPARE` command.<br><br>* `COM_CHANGE_USER`, `COM_QUIT`, `COM_SET_OPTION` and other commands. |
|**Read\-only endpoint** |No write requests are allowed to be processed, and all read requests are sent to read\-only nodes based on the number of active requests. ||


<span id=".5Yqf6IO954m55oCn"></span>
## Precautions


* NDB for MySQL does not support the compression protocol.

* When connecting with the default endpoint, all requests within a transaction are routed to the primary node if transaction splitting is disabled.

* When you execute the `SHOW PROCESSLIST` command while connected to the default endpoint, the system returns the merged results from all nodes.

* If you execute multiple statements or call a stored procedure, all subsequent requests on the current connection are routed to the primary node. You must disconnect and reconnect to restore the read/write splitting feature.

* The endpoint itself does not have a maximum connection limit. The backend DBengine limits the number of connections, and the default maximum varies by instance specification. For specific numbers, refer to [Product specifications](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Product_specifications).

* Do not modify environment variables while running multi\-statements or calling stored procedures, for example, `set names utf8mb4;select * from t1;`. Otherwise, data queried from read\-only nodes may be inconsistent with data from the primary node.

* When establishing a URL connection with an application connection pool, add the `connectTimeout` and `socketTimeout` parameters to the URL to prevent the pool from hanging due to packet loss from network issues or other unexpected scenarios. Refer to the [MySQL documentation](https://dev.mysql.com/doc/connector-j/en/connector-j-connp-props-networking.html) for parameter descriptions. Example: `java url: jdbc:mysql://ip:port/db?connectTimeout=60000&socketTimeout=300000;`.


<span id=".5Yqf6IO954m55oCn"></span>
## Functional features

The read\-write separation function of NDB for MySQL mainly includes the following features:


* [Load balancing](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Load_balancing)

* [Transaction splitting](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Transaction_splitting)

* [Consistency levels](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Consistency_levels)
