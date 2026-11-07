---
title: "MongoDB maximum connections best practices"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/MongoDB_maximum_connections_best_practices"
---

Connections are a critical resource affecting MongoDB instance stability. Properly configuring client connection pools and server\-side connection limits is essential for ensuring normal business operations. When connections reach their limit or show abnormal growth, quickly identifying the root cause and taking effective measures is a critical aspect of operations and maintenance. This topic systematically explains connection management methods, focusing on configuration, Monitoring, and troubleshooting, to help you effectively manage connection resources and improve instance stability.

<span id="WbAtYufj"></span>
## Background information

Connection management involves coordinated configuration at both the client and server levels. Understanding the following two core parameters and their relationship is fundamental to properly planning connection resources.


|**Dimension** |**Client** |**Server** |
|---|---|---|
|Parameter name |[maxPoolSize](https://www.mongodb.com/docs/manual/reference/connection-string-options/#mongodb-urioption-urioption.maxPoolSize) |`net.maxIncomingConnections` |
|Scope of policy |Limit the maximum number of connections for a single client to each MongoDB node. |Limit the maximum total concurrent connections allowed for a single MongoDB instance. |
|Configuration method |Set as a configuration item in drivers (e.g., Java, Python). |Modify through the console. |
|Purpose |Prevents a single client from monopolizing too many connection resources, while also reusing established connections. |Protect server resources to prevent performance degradation or system crashes due to excessively high connection counts. |
|Default value |None |MongoDB defaults to 65536, but the actual value might be lower due to operating system limitations. |


The core relationship between them is that the sum of all client connection pools should not exceed the server's connection limit. Once the limit is reached, new connection requests will be rejected.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For recommended connections for each specification, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/product-specification">Product specifications</a>.</div>


* <div data-tips="true" data-tips-type="default">For more information about the net.maxIncomingConnections parameter, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/supported-parameter">Supported parameters</a>.</div>


* <div data-tips="true" data-tips-type="default">For specific parameter modification procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-parameter">Modifying instance parameters</a>.</div>



<span id="wkM5rbd6"></span>
## Configuration recommendations

&nbsp;


<Tabs>
<Tab zoneid="wiRt6U5qEg" title="Client connection pool configuration">
<TabTitle>Client connection pool configuration</TabTitle>

You can set this in the connection URL using the `maxPoolSize` parameter (parameter names may vary by driver; refer to the corresponding driver's official documentation for specifics).

**Core principles**


* Connections in the connection pool can be reused by multiple requests, eliminating the need to create a new connection for each request. Excessively large settings will consume too many server resources, while excessively small settings may cause requests to queue and wait.

* Recommended value for a single client: ≤ `Server connection limit ÷ Expected number of clients`


**Typical scenarios**


|**Typical scenarios** |**Connection Pool Recommendations** |**Description** |
|---|---|---|
|High\-concurrency short transactions<br><br>(e.g., major e\-commerce promotions, flash sales) |Increase appropriately |Reduce the overhead of frequently establishing/closing connections. |
|Long transactions or resource\-constrained scenarios (e.g., Data analytics, batch import) |Adjust downwards |Avoid connection backlog. |
|Replica Set instance or Sharding Cluster instance |Calculated by node count |Each node establishes a pool independently. The actual number of connections = maxPoolSize × number of nodes. |


**Configuration example**

```Plain Text
mongodb://user:password@host:3717/admin?maxPoolSize=100
```



</Tab>
<Tab zoneid="zcATFZnLEN" title="Server connection count configuration">
<TabTitle>Server connection count configuration</TabTitle>

Server configurations apply universally, regardless of business scenarios, and adhere to the following principles.

**Core principles**

The server's maximum connection limit should exceed the sum of all client connection pools: `net.maxIncomingConnections ≥ Σ(each client's maxPoolSize)`

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The actual effective value of the <code>net.maxIncomingConnections</code> parameter is also limited by the operating system's <code>ulimit -n</code> (the maximum number of files a single process can open). Therefore, if this value is too low, increasing <code>net.maxIncomingConnections</code> will not achieve the desired effect.</div>


&nbsp;

**Configuration examples**

With 10 application clients, each connection pool set to 100, the total client demand is 10 × 100 = 1000. If the server limit is 500, the total demand will exceed this limit, causing some clients to fail to connect and receive a `TooManyConnections` error.


</Tab>
</Tabs>


<span id="XvpyNtHo"></span>
## Monitoring and alerting

Monitoring metrics are fundamental for determining if the connection configuration is reasonable and for timely detection of anomalies. You can view the instance's connection\-related metrics through the console. For specific procedures, refer to [Viewing monitoring data](https://docs.byteplus.com/en/docs/mongodb/view-monitoring-data). For a detailed description of monitoring metrics, refer to [Monitoring metrics](https://docs.byteplus.com/en/docs/mongodb/monitoring-metric).

<span id="SC87x1Kw"></span>
### View connections

You can quickly understand the current connection usage of the instance by executing the following command in the MongoDB Shell. For connection methods, see [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell?_vtm_=a106466.b106468.0_0.0_0.0.2423_7615838008780801546&lang=en). For command usage, see [db.serverStatus()](https://www.mongodb.com/docs/manual/reference/method/db.serverStatus/).

```Plain Text
db.serverStatus().connections
```


Example of return results is as follows.

```Plain Text
{
  "current" : 14,      // 当前已建立的连接数
  "available" : 386,   // 剩余可用连接数
  "totalCreated" : 65,
  "active" : 3         // 当前活跃连接数
}
```


You are advised to pay close attention to the current and available parameters. If available remains low, or current sharply increases at a certain point, it indicates abnormal connection resources, and further investigation is required.

<span id="tWCYs4I0"></span>
### Locate the Source of Abnormal Connections

When there is an abnormal increase in connections or insufficient available connections, you need to identify which client is consuming too many connections by executing the following command. For command usage, see [db.currentOp()](https://www.mongodb.com/docs/v4.0/reference/method/db.currentOp/).

```Plain Text
db.currentOp({"active" : true})
```


The `client` field in the return results displays the client's IP address and port number, facilitating the identification of the specific client source.

<span id="zBw4bZDM"></span>
### Configure Alert Rules

You can configure alert rules for connection utilization in the console to be promptly notified of abnormal increases in connection count. Refer to the following settings for alert thresholds:


* Connection utilization ≥ 80%: Triggers a warning. It is recommended to monitor the growth trend.

* Connection utilization ≥ 90%: Triggers an urgent alert. It is recommended to address immediately.


You can also customize thresholds based on your specific business requirements. For detailed procedures, see [Setting alerts](https://docs.byteplus.com/en/docs/mongodb/set-alert).

<span id="kUc0p3rP"></span>
## Handle connection limit exceedance

<span id="IaRrmBom"></span>
### Sharding cluster instance

For troubleshooting and handling methods for sharding cluster instance connection limit exceedance, see [How to troubleshoot and resolve connection failures caused by connection exhaustion in sharding cluster instances?](https://docs.byteplus.com/en/docs/mongodb/how_to_troubleshoot_and_resolve_connection_failures_caused_by_connection_exhaustion?lang=zh).

<span id="AP5k5eIL"></span>
### Replica set instance

The processing logic for replica set instances is largely consistent with sharding clusters, with the difference that replica sets do not have Mongos nodes, and connections directly reach the primary node or Secondary node.

You can temporarily release all connections and quickly restore business by [Restarting node](https://docs.byteplus.com/en/docs/mongodb/restart-instance?lang=en#.5pON5L2c5q2l6aqk). After restarting, promptly investigate the reason for the connection limit being exceeded to prevent the issue from recurring.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">A restart will cause a temporary disconnection of approximately 30 seconds on the node. Plan your business operations in advance and ensure your application has a reconnection mechanism.</div>



* You can also execute the [db.currentOp()](https://www.mongodb.com/docs/v4.0/reference/method/db.currentOp/)` ` command in the MongoDB Shell to check for long\-running operations or if a certain IP is occupying too many connections. If so, execute [db.killOp(<opid>)](https://www.mongodb.com/docs/v4.0/reference/method/db.killOp/) to terminate them.

* If all connections are normal business requests, you can try the following methods sequentially.

   * Adjust the client connection pool: Ensure that `number of application instances × maxPoolSize` (default 100) is less than the instance's recommended connection count. Under a replica set architecture, [MongoClient](https://www.mongodb.com/zh-cn/docs/drivers/java/sync/current/connection/mongoclient/)` ` creates a separate pool for each node. The actual connection count = `maxPoolSize × number of nodes` (refer to typical scenario descriptions). You can set` `[maxIdleTimeMS](https://www.mongodb.com/zh-cn/docs/manual/reference/connection-string-options/#mongodb-urioption-urioption.maxPoolSize) (default 0, meaning no limit) to automatically close idle connections. For more connection pool tuning suggestions, refer to [Tuning your connection pool settings](https://www.mongodb.com/zh-cn/docs/manual/tutorial/connection-pool-performance-tuning/).

   * Increase the server connection limit: Appropriately increase the `net.maxIncomingConnections` parameter value in the console.

   * Upgrade instance specifications: If business demands exceed the current specification limit, you can upgrade node specifications by changing the configuration. For specific operations, refer to [Modifying instance configurations](https://docs.byteplus.com/en/docs/mongodb/change-instance-config?lang=en).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Upgrading instance specifications will incur additional costs. Refer to <a href="https://docs.byteplus.com/en/docs/mongodb/billing-item-price">Billing items and prices</a> for details, and assess your business requirements accordingly.   </div>
