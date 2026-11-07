---
title: "How to troubleshoot and resolve connection failures caused by connection exhaustion in sharding instances?"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/how_to_troubleshoot_and_resolve_connection_failures_caused_by_connection_exhaustion"
---

When a sharding instance of Document Database for MongoDB reaches its maximum connection limit, it will no longer accept new connections, causing business connection failures. This topic describes how to troubleshoot and resolve these issues.

<span id="860ozs4z"></span>
## Problem

When connection exhaustion occurs, it typically manifests as one or more of the following phenomena.


* Business applications (such as Java, Python, and other services) report errors, indicating connection timeouts or connection refusals. The error message is as follows:

   ```JSON
   {"t":{"$date":"2026-06-30T15:35:37.256+08:00"},"s":"I",  "c":"NETWORK",  "id":22942,   "ctx":"listener","msg":"Connection refused because there are too many open connections","attr":{"remote":"11.189.107.83:59512","connectionCount":24000}}
   ```
   

* The allowlist is correctly configured, but the instance still cannot be connected using MongoDB Shell or other client tools.

* In the console monitoring charts, the current number of connections consistently approaches or reaches the recommended maximum limit for the instance specification.


<span id="8ttvMrXV"></span>
## Cause analysis

Check the monitoring charts in the console to confirm whether the connection limit has been exhausted.


1. Log in to the [MongoDB Console](https://console.byteplus.com/db/region:db+cn-beijing/mongodb/shardList), and in the upper\-left corner of the top menu bar, select the project and region for the instance.

2. In the left navigation bar, select **Sharding instances**, and click the target instance name to access the instance details page.

3. On the instance details page, click the **Alerts and monitoring** tab, then switch to the **Mongos** and **Shards** tabs to view the current number of connections for each node.


If the current number of connections continuously approaches or reaches the recommended maximum for the specification, it can be confirmed that the connections are exhausted.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For the recommended maximum connections for each specification, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/product-specification?lang=en">Product specifications</a>.</div>


* <div data-tips="true" data-tips-type="default">The number of connections for sharding instances may be concentrated in Mongos nodes (business entry point) or Shard nodes (data storage). Check these two types of nodes separately. ConfigServer nodes only store cluster metadata and do not handle business connections, so they can be temporarily ignored during troubleshooting.</div>



<span id="v9iyVHh8"></span>
## Solution

You can temporarily release all connections by [restarting Mongos nodes](https://docs.byteplus.com/en/docs/mongodb/restart-instance?lang=en#.5pON5L2c5q2l6aqk) to quickly restore business. After the restart, promptly investigate the cause of connection exhaustion to prevent the problem from recurring.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A restart will cause a temporary disconnection of approximately 30 seconds on the node. Plan your business operations and ensure your application has a reconnection mechanism.</div>



* You can check for long\-running operations or an IP address consuming too many connections by executing `db.currentOp()`. If any are found, terminate them by executing `db.killOp(<opid>)`. For connection methods, refer to [Connecting to instance via MongoDB shell tool](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell?_vtm_=a106466.b106468.0_0.0_0.0.2423_7615838008780801546&lang=en). For command usage, refer to [db.currentOp()](https://www.mongodb.com/docs/v4.0/reference/method/db.currentOp/) and [db.killOp()](https://www.mongodb.com/docs/v4.0/reference/method/db.killOp/).

* If all connections are normal business requests, you can try the following methods sequentially.

   * Adjust the client connection pool: Ensure that the number of application instances × [maxPoolSize](https://www.mongodb.com/docs/manual/reference/connection-string-options/#mongodb-urioption-urioption.maxPoolSize) (default 100) is less than the recommended number of connections per instance. Set [maxIdleTimeMS](https://www.mongodb.com/zh-cn/docs/manual/reference/connection-string-options/#mongodb-urioption-urioption.maxPoolSize) (default 0, meaning unlimited) to automatically close idle connections. For more connection pool tuning suggestions, refer to [Tuning your connection pool settings](https://www.mongodb.com/docs/manual/tutorial/connection-pool-performance-tuning/).

   * Increase the server connection limit: Appropriately increase the `net.maxIncomingConnections` parameter value in the console. For parameter descriptions, refer to [Supported parameters](https://docs.byteplus.com/en/docs/mongodb/supported-parameter?_vtm_=a106466.b106468.0_0.0_0.0.2466_7615838008780801546&lang=en). For modification methods, refer to [Modifying instance parameters](https://docs.byteplus.com/en/docs/mongodb/modify-parameter?_vtm_=a106466.b106468.0_0.0_0.0.2466_7615838008780801546&lang=en).

   * Upgrade instance specifications: If business demands still exceed the specification limit, you can [upgrade Mongos node specifications or increase the number of Mongos nodes](https://docs.byteplus.com/en/docs/mongodb/modify-mongos-config?lang=en).

      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">Upgrading instance specifications will incur additional costs. Refer to <a href="https://docs.byteplus.com/en/docs/mongodb/billing-item-price?lang=en">Billing items and prices</a> for details, and assess your business requirements accordingly.      </div>
