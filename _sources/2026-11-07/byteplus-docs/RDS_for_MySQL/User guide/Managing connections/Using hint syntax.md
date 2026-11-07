---
title: "Using hint syntax"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/using_hint_syntax"
---

This topic describes how to enable the specified nodes to execute SQL requests by Hint syntax.

<span id="background"></span>
## Background

Using Hint syntax can force SQL requests to execute on specified nodes. Hints have the highest routing priority and are not limited by consistency and transactions. However, the Hint function depends on the Proxy link, and read/write splitting must be enabled and take effect on all connections. Evaluate whether it is suitable for your business before using it.

<span id="hint-syntax-supported"></span>
### Hint syntax supported


* The following three Hints are currently supported:

   * Assign execution to the primary node.

      ```shell
      /* FORCE_MASTER */
      ```
      

   * Assign execution to the read\-only node.

      ```shell
      /* FORCE_SLAVE */
      ```
      

   * Assign execution to a specific node. Get the node ID under the connection management menu of the target instance.

      ```shell
      /* FORCE_NODE='<id>' */
      ```
      


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When there is no specified node/the node is temporarily unavailable, the error <code>specific node[<id>] not found</code> will be reported when forced routing of Hints is used.</div>


<span id="sql-statements-supported"></span>
### SQL statements supported

The following types of single SQL statements are supported:


* SHOW STATEMENT

* SELECT STATEMENT

* EXPLAIN STATEMENT

* UNION STATEMENT

* KILL STATEMENT


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Supports mixed case (for example, <code>/* FORCE_master */ show databases;</code>).</div>


* <div data-tips="true" data-tips-type="tip">Supports use in SDKs.</div>



<span id="forwarding-policy"></span>
### Forwarding policy

When the weights of each node are specified by the read/write splitting policy, requests with Hints are forwarded according to the following policy:


* Assign execution to the primary node (`/* FORCE_MASTER */`)

   You can forcibly route the SQL statement to the primary node when the weight of the primary node is 0.

* Assign execution to the read\-only node (`/* FORCE_SLAVE */`)

   First, try to forward to read\-only nodes according to weight. If the weights of read\-only nodes are 0, the statement will be routed to the primary node.

* Assign execution to a specific node (`/* FORCE_NODE='<id>' */`)

   You can forcibly route the statement to a node when the weight of the specific node is 0.


<span id="limits"></span>
## Limits


* When connecting through the command line in the MySQL client and using the Hint statement, you must add the `-c` option in the command. Otherwise, Hints are filtered by the MySQL command line tool.

* Hint comments are limited to the beginning of SQL statements, such as `/* FORCE_MASTER */ show databases;`. Comments in statements are not analyzed, such as `show /* FORCE_MASTER */ databases;`.

* You cannot add multiple Hints to one SQL statement, such as `/* FORCE_MASTER FORCE_SLAVE */`.

* Forwarding a `PREPARE` statement or multiple statements based on Hints is temporarily not supported, such as `show databases;` or `use test;`.
