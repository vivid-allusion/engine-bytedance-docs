---
title: "Guide to configuring MongoDB connection address"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/Guide_to_configuring_MongoDB_connection_address"
---

The connection address is the fundamental configuration that enables applications to establish communication with Document Database for MongoDB instances. With correct connection address configuration, application requests can be precisely routed to cluster primary nodes, secondary nodes, read\-only nodes, or Mongos nodes, providing foundational support for stable instance access, high availability, and read/write splitting. This topic describes the configuration methods and recommendations for MongoDB connection addresses.

<span id="s7nTdg2R"></span>
## Background information

<span id="AbrDQeoL"></span>
### **Connection address type**

Document Database for MongoDB provides two types of connection addresses, private and public, which support replica set and sharding cluster architectures. For details on connection address differences, viewing methods, application and release operations, and connection addresses supported by various instances, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction?lang=en).

<span id="meAVERSS"></span>
### **Connection address format**

The format, parameter descriptions, and examples for each connection address are as follows.


* **Replica set instance**



<Tabs>
<Tab zoneid="d4A18RK5Wp" title="Private network address">
<TabTitle>Private network address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<host1>:<port>,<host2>:<port>,...,<hostN>:<port>/<database>?replicaSet=<replicaSetName>&authSource=admin[&readPreference=<value>][&retryWrites=true]
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<host1>:<port>,<host2>:<port>,...,<hostN>:<port>` |Required. The domain name and port information for the primary and secondary nodes of the replica set instance. Separate multiple nodes with commas (,). The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en). |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`replicaSet=<replicaSetName>` |Required. The replica set name. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |
|`readPreference=<value>` |Optional. Customize the read preference policy. You can prioritize reading from primary or secondary nodes. |
|`retryWrites=true` |Optional. Recommended for production environments. Automatically retries write requests during minor network fluctuations to improve access stability. |


Example

```Plain Text
mongodb://root:****@mongod-01.ivolces.com:3717,mongod-02.ivolces.com:3717/admin?replicaSet=rs-xxxx&authSource=admin&retryWrites=true
```



</Tab>
<Tab zoneid="QDmlbr62im" title="Private network address (read-only)">
<TabTitle>Private network address (read-only)</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<host1>:<port>,<host2>:<port>,<hostN>:<port>/admin?replicaSet=<replicaSetName>&authSource=admin&readPreference=secondary&readPreferenceTags=role:readonly[&retryWrites=true]
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<host1>:<port>,<host2>:<port>,<hostN>:<port>` |Required. The domain name and port information for read\-only nodes of the replica set instance. Separate multiple nodes with commas (,). The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en). |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`replicaSet=<replicaSetName>` |Required. The replica set name. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |
|`readPreference=secondary` |Required. Specifies that read requests are preferentially routed to secondary and read\-only nodes.<br><br> |
|`readPreferenceTags=role:readonly` |Required. Precisely route read requests to dedicated read\-only nodes, ensuring only read operations are performed. |
|`retryWrites=true` |Optional. Recommended for production environments to improve the stability of specific write operations and prevent write failures due to network fluctuations. |


Example

```Plain Text
mongodb://root:****@mongod-01.ivolces.com:3717,mongod-02.ivolces.com:3717/admin?replicaSet=rs-xxxx123&authSource=admin&readPreference=secondary&readPreferenceTags=role:readonly&retryWrites=true
```



</Tab>
<Tab zoneid="n7yqAjW3MP" title="Primary address">
<TabTitle>Primary address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<primaryHost>:<port>/<database>?authSource=admin&directConnection=true
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<primaryHost>:<port>` |Required. The domain name and port information for the replica set instance's primary node. The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en). |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |
|`directConnection=true` |Required. Forces a fixed connection to the primary node, where all read and write requests are executed.<br><br><br>* If this parameter is specified and set to `true`, all read and write requests are routed to the primary node.<br><br>* If this parameter is not specified or is set to `false`, read requests may be forwarded to other nodes. |


Example

```Plain Text
mongodb://root:****@mongod-primary.ivolces.com:3717/admin?authSource=admin&directConnection=true
```



</Tab>
<Tab zoneid="FwZT6lnHsE" title="Secondary address">
<TabTitle>Secondary address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<secondaryHost>:<port>/<database>?authSource=admin&directConnection=true[&readPreference=secondary]
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<secondaryHost>:<port>` |Required. The domain and port information for the replica set instance's secondary nodes. The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en). |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |
|`directConnection=true`<br><br> |Required. Forces a fixed connection to secondary nodes and does not participate in automatic cluster failover.<br><br><br>* If this parameter is specified and set to `true`, only read requests are supported, and write requests are rejected.<br><br>* If this parameter is not specified or its value is set to `false`, write requests will be forwarded to the primary node. |
|`readPreference=secondary` |Optional. Configure the read preference policy to read data from secondary nodes without affecting write operations. |


Example

```Plain Text
mongodb://root:****@mongod-secondary.ivolces.com:3717/admin?authSource=admin&directConnection=true&readPreference=secondary
```



</Tab>
<Tab zoneid="s1hXh2F5WC" title="ReadOnly address">
<TabTitle>ReadOnly address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<readonlyHost>:<port>/<database>?authSource=admin&directConnection=true[&readPreference=secondary]
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<readonlyHost>:<port>` |Required. The domain and port information for the replica set instance's read\-only nodes. The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en). |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |
|`directConnection=true`<br><br> |Required. Forces a fixed connection to read\-only nodes and does not participate in automatic cluster failover.<br><br><br>* If this parameter is specified and set to `true`, only read requests are supported, and write requests are rejected.<br><br>* If this parameter is not specified or its value is set to `false`, write requests will be forwarded to the Primary node. |
|`readPreference=secondary` |Optional. Configure the read preference policy to read data from secondary nodes without affecting write operations. |


Example

```Plain Text
mongodb://root:****@mongod-readonly.ivolces.com:3717/admin?authSource=admin&directConnection=true&readPreference=secondary
```



</Tab>
</Tabs>



* **Sharding cluster instance**



<Tabs>
<Tab zoneid="sjU7S1Rc0I" title="Private network address">
<TabTitle>Private network address</TabTitle>

The high\-availability access address for multiple Mongos nodes in a sharding cluster is the **standard recommended entry point for business applications to access the sharding cluster.** 

Format

```Plain Text
mongodb://<username>:<password>@<mongos1>:<port>,<mongos2>:<port>.../<database>?authSource=admin[&retryWrites=true]
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<mongos1>:<port>,<mongos2>:<port>...` |Required. The domain name and port information for multiple Mongos nodes in the sharding cluster. Separate multiple nodes with commas (,). The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en). |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |
|`retryWrites=true`<br><br> |Optional. Recommended for production environments. Automatically retries write requests during minor network fluctuations to improve access stability. |


Example

```Plain Text
mongodb://root:****@mongos-01.ivolces.com:3717,mongos-02.ivolces.com:3717/admin?authSource=admin&retryWrites=true
```



</Tab>
<Tab zoneid="Ed1NPDIlOo" title="Mongos address">
<TabTitle>Mongos address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<mongos>:<port>/<database>?authSource=admin
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<mongos>:<port>` |Required. The domain name and port information for a single Mongos node in the sharding cluster. The default port is 3717. The modifiable range for port numbers is `1,000~65,535`. For specific operations, refer to [Modifying port](https://docs.byteplus.com/en/docs/mongodb/modifying_ports?lang=en).<br><br> |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |


Example

```Plain Text
mongodb://root:****@mongos-01.ivolces.com:3717/admin?authSource=admin
```



</Tab>
<Tab zoneid="NdjkDrdGKd" title="Shard address">
<TabTitle>Shard address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<shard1>:<port>,<shard2>:<port>/<database>?replicaSet=<shardReplicaSet>&authSource=admin
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<shard1>:<port>,<shard2>:<port>` |Required. The domain name and port information for the sharding cluster's Shard nodes. Separate multiple nodes with commas (,). The default port is 3717. |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`replicaSet=<shardReplicaSet>` |Required. The name of the replica set to which the Shard node belongs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>replicaSet</code> parameter here does not indicate an independent replica set instance, but rather the high\-availability deployment configuration for Shard nodes. Each Shard node is deployed in replica set mode to ensure sharded data safety. The overall still belongs to a sharding cluster.</div><br> |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |


Example

```Plain Text
mongodb://root:****@shard-01.ivolces.com:3717,shard-02.ivolces.com:3717/admin?replicaSet=shard-rs-01&authSource=admin
```



</Tab>
<Tab zoneid="lDu4er9cem" title="ConfigServer address">
<TabTitle>ConfigServer address</TabTitle>

Format

```Plain Text
mongodb://<username>:<password>@<cfg1>:<port>,<cfg2>:<port>,<cfg3>:<port>/<database>?replicaSet=<configReplicaSet>&authSource=admin
```


Parameter description


|**Parameter** |**Description** |
|---|---|
|`mongodb://` |A fixed prefix used to identify the MongoDB connection protocol. It cannot be modified. |
|`<username>` |Required. Database account name, defaults to root. |
|`<password>` |Required. Password for the database account. |
|`<cfg1>:<port>,<cfg2>:<port>,<cfg3>:<port>` |Required. The domain name and port information for the sharding cluster's ConfigServer nodes. Separate multiple nodes with commas (,). The default port is 3717.<br><br> |
|`<database>` |Optional. The database used for authentication, defaults to `admin`. |
|`replicaSet=<configReplicaSet>` |Required. The name of the replica set to which the ConfigServer node belongs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The <code>replicaSet</code> parameter here does not indicate an independent replica set instance, but rather the high\-availability deployment configuration for ConfigServer nodes. ConfigServer is deployed in a 3\-node replica set mode to ensure the security of cluster metadata.</div><br> |
|`authSource=admin` |Required. Must be `admin`, and used for database account authentication. |


Example

```Plain Text
mongodb://root:****@config-01.ivolces.com:3717,config-02.ivolces.com:3717,config-03.ivolces.com:3717/admin?replicaSet=config-rs&authSource=admin
```



</Tab>
</Tabs>


<span id="8VGahTcs"></span>
### **Read/write splitting parameters**

When your business accesses the database, to offload read pressure from the primary node and improve query performance and cluster stability, you can configure `readPreference` and `readPreferenceTags` in the connection address to achieve read/write splitting. To learn about basic parameter descriptions and the configuration method for read/write splitting connection addresses, refer to [Read/Write splitting](https://docs.byteplus.com/en/docs/mongodb/read_write_splitting?lang=en).

<span id="HCCvrsXg"></span>
## **Configuration schemes and applicable scenarios**

You can select a suitable connection address configuration scheme based on your business scenarios. Specific scenarios and configuration details are as follows:


|No. |Applicable scenarios<br><br> |Configuration description |Single\-node failure impact<br><br> |Connection address configuration |Core configuration parameters<br><br> |
|---|---|---|---|---|---|
|1<br><br> |Core scenarios such as e\-commerce order placement, payment settlement, and user login and authentication. No read/write splitting is required. It focuses on strong data consistency and high availability. |Default high\-availability configuration (recommended). All read and write requests access the primary node.<br><br> |Primary node failure: The instance automatically performs a primary/secondary failover, allowing normal read/write operations afterward.<br><br>Secondary node failure: No impact.<br><br> |`mongodb://<user>:<password>@host0,host1/?authSource=admin&replicaSet=rs-mongo-replica-xxx&retryWrites=true`<br><br> |`retryWrites=true`<br><br> |
|2 |Small and medium\-sized e\-commerce and content platforms. To control node deployment costs, achieve zero\-cost read/write splitting (without adding new nodes) for tasks such as product detail queries and article list loading. |Read/write splitting configuration (recommended). **Read requests prioritize accessing secondary nodes and access primary nodes in case of failure**, with zero\-cost traffic offloading.<br><br> |Primary node failure: Normal read/write operations are possible after primary/secondary failover.<br><br>Secondary node failure: No impact.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">No new nodes are required. Data synchronization delays between primary and secondary nodes can affect the accuracy of business data reads.</div><br> |`mongodb://<user>:<password>@host0,host1/?authSource=admin&replicaSet=rs-mongo-replica-xxx&retryWrites=true` **`&readPreference=secondaryPreferred`**<br><br> |`readPreference=secondaryPreferred`<br><br> |
|3 |Large e\-commerce and big data platforms that heavily rely on read\-write splitting and demand high availability. Functions such as real\-time data analytics, user behavior statistics, and high\-frequency product queries require stable read request routing. |Read/write splitting configuration (recommended). **Read requests prioritize accessing read\-only nodes and access the primary node if no read\-only nodes are available**.<br><br> |Primary node failure: Normal read/write operations are possible after primary/secondary failover.<br><br>Partial read\-only node failure: No impact.<br><br>All read\-only node failures: No impact.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">It is recommended to add 2 or more read\-only nodes.</div><br> |`mongodb://<user>:<password>@host0,host1,readonly-host0,readonly-host1/?authSource=admin&replicaSet=rs-mongo-replica-xxx&retryWrites=true` **`&readPreference=secondaryPreferred&readPreferenceTags=role:readonly`** |`readPreference=secondaryPreferred&readPreferenceTags=role:readonly` |
|4 |Read\-write splitting scenarios for non\-core links, such as product review list queries and historical order queries (non\-core pages). Read requests are only allowed to access secondary nodes. |Read/write splitting configuration. **Read requests only access secondary nodes**. **Avoid using it in core online links**.<br><br> |Primary node failure: After primary/secondary failover, write requests are normal, but read requests fail.<br><br>Secondary node failure: Read requests fail.<br><br> |`mongodb://<user>:<password>@host0,host1/?authSource=admin&replicaSet=rs-mongo-replica-xxx&retryWrites=true` **`&readPreference=secondary`** |`readPreference=secondary`<br><br> |
|5 |Read/write splitting where read requests are only allowed to access read\-only nodes (without downgrade requirements), such as report statistics for fixed periods and non\-real\-time data queries. |Read/write splitting configuration, where **read requests only access read\-only nodes** and do not downgrade if no nodes are available.<br><br> |Primary node failure: Normal read/write operations are possible after primary/secondary failover.<br><br>Partial read\-only node failure: No impact.<br><br>All read\-only node failures: Read requests will fail.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Plan and deploy read\-only nodes in advance to ensure available nodes can handle read requests.</div><br> |`mongodb://<user>:<password>@host0,host1,readonly-host0,readonly-host1/?authSource=admin&replicaSet=rs-mongo-replica-xxx&retryWrites=true` **`&readPreference=secondary&readPreferenceTags=role:readonly`** |`readPreference=secondary&readPreferenceTags=role:readonly` |
|6 |For temporary debugging and troubleshooting by O&M personnel, such as database performance monitoring and data anomaly troubleshooting, where high availability is not required. |Single\-node access. **Avoid using it in production environments**.<br><br> |Node failure: All read/write requests fail.<br><br> |`mongodb://<user>:<password>@host0/?directConnection=true`<br><br> |`directConnection=true`<br><br> |


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">If you need to adjust connection address information based on the above schemes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/modify-connection-address?lang=en">Modifying connection address</a>.</div>


**Configuration selection summary**:


* Zero\-cost read/write splitting (no new nodes): Configuration scheme 2 is recommended.

* High\-concurrency read scaling (add read\-only nodes): Configuration scheme 3 is recommended. Add 2 or more read\-only nodes to avoid a single\-node failure.

* Prohibited for use in production environments: configuration scheme 4 (risk of core link read request failure) and configuration scheme 6 (no high\-availability guarantee).


<span id="YBmElNfT"></span>
## Configuration verification and troubleshooting

<span id="IFf5M3kE"></span>
### **Configuration connectivity verification**

After configuring the connection address, you can quickly verify connectivity in the following ways to confirm that the configuration takes effect.


* Elastic Compute Service (ECS) test (recommended)

   Install the MongoDB Shell tool on the BytePlus ECS server where your business is deployed, and execute the following command to connect to the instance.

   ```Plain Text
   mongosh "mongodb://<username>:<password>@<host>:<port>/admin?authSource=admin"
   ```
   

   Replace the placeholders in the command with your actual database account, password, instance domain name, and port. If you can successfully enter the database interactive interface without errors, the configuration is correct.

* Client tool verification

   Enter the standard connection address, account password, and authentication parameters in visual clients such as MongoDB Compass and Navicat. If a connection can be successfully established and database and table data can be viewed, the configuration is correct.

* Business application verification

   Enter the connection address into the business project configuration file and restart the application. If there are no database connection errors and data read/write operations can be completed normally, the configuration is effective and usable.


<span id="5LKuRzHl"></span>
### **FAQs and troubleshooting**

When configuring the connection address and verifying connectivity, if you encounter connection, login, or access\-related exceptions, refer to the table below to troubleshoot and resolve them yourself. If you encounter other network\-related issues, refer to the documentation titled [Network connection](https://docs.byteplus.com/en/docs/mongodb/network-connection?lang=en#.5aaC5L2V6ZmQ5Yi26K6_6ZeuLW1vbmdvZGIt5a6e5L6L55qE5a6i5oi356uv6L-e5o6l5pWw77yf). If the problem cannot be resolved, you can [submit a ticket](https://console.byteplus.com/workorder/create) to contact technical staff for assistance.


|**Problem** |**Common reasons**<br><br> |**Solution**<br><br> |
|---|---|---|
|Instance access failed due to a connection timeout. |Not configure IP allowlist, not open port 3717, or not select the correct network address.<br><br> |1. Add the client IP to the allowlist in the console <br><br>2. Allow port 3717 <br><br>3. Prioritize connecting using a private network address.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For specific operations to add the client IP to the allowlist, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/create-allowlist?lang=en">Creating allowlist</a>.</div><br> |
|Authentication failure during login. |Incorrect account and password, or incorrect connection authentication parameter configuration. |Verify the account and password, and ensure the `authSource=admin` parameter in the connection configuration is correct. |
|Write errors due to direct connection to a secondary/read\-only node. |Not use a unified cluster connection address. Connects only to secondary nodes/read\-only nodes individually. |Use the unified cluster connection address. Do not directly connect to secondary/read\-only nodes separately. |
|Routing failure due to an abnormal replica set connection.<br><br> |Not configure the `replicaSet` parameter, or enter an incorrect node domain name. |Add the `replicaSet` parameter and enter the node domain names exactly as shown in the console. |
|Sharding cluster connection failure. |Incorrect node address string. The `replicaSet` parameter is not configured when connecting to Shard or ConfigServer nodes (this parameter is not required when connecting to Mongos nodes). |Assemble node addresses following the standard format, and add the `replicaSet` parameter for both Shard and ConfigServer nodes.<br><br> |
|Frequent connection disconnections and write failures due to an unstable network. |Not enable the write retry feature. |Enable the write retry feature (configuring the `retryWrites=true` parameter) to avoid write failures caused by connection interruptions. |
