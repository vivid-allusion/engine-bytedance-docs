---
title: "Network connection"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/network-connection"
---

This topic summarizes network connection FAQs for Document Database for MongoDB.

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5piv5ZCm5pSv5oyB5YWs572R6K6_6Zeu77yf"></span>
### Does Document Database for MongoDB support public network access?

Yes. You can apply for a public address for a MongoDB instance, so that devices outside the VPC can access the MongoDB instance through the public address. For more information about how to apply for a public address, refer to [Applying for public address](https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address).

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5pSv5oyB5ZOq5Lqb6K-t6KiA55qE5a6i5oi356uv6L-b6KGM6L-e5o6l77yf"></span>
### What languages does MongoDB support for client connection?

Document Database for MongoDB is fully compatible with the official MongoDB protocol, so it supports the same clients as MongoDB (such as Node.js, PHP, Java, Python, C, C++, Scala, Golang, .NET Core). For more details about clients for various languages, refer to [MongoDB Drivers](https://www.mongodb.com/docs/drivers/).

<span id=".5aaC5L2V6YCa6L-H6Ieq5bu66LSm5Y-377yI5Y2z6Z2eLXJvb3Qt6LSm5Y-377yJ6L-e5o6l5a6e5L6L77yf"></span>
### How can I connect to MongoDB instance via a non\-root account?

When you create a MongoDB instance, the system will, by default, create an administrator account root in the admin database. Therefore, the value of `authSource` in MongoDB's default connection address is `admin` (that is, it will connect to the `admin` database by default).

If the account you created yourself belongs to another database (such as `testdb1`), you need to change `admin` after `authSource` to the database where the self\-created account is located (such as `testdb1`). For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

<span id=".bW9uZ29kYi3lrp7kvovnmoTmnIDlpKfov57mjqXmlbDmmK_lpJrlsJHvvJ8="></span>
### What is the maximum number of connections for a MongoDB instance?

The specification of each node in a MongoDB instance has a default max connections value. For more information, refer to [Product specifications](https://docs.byteplus.com/en/docs/mongodb/product-specification).

The recommended number of connections refers to the default upper limit of connections for a single node in the instance. For example, the default max connections for a single node of 2 core 4 GiB replica set instance is 2,000, which means that the default max connections for both the primary node and the secondary node of the instance is 2000 (hidden nodes are only used to guarantee high availability and do not allow connections).

When the number of connections reaches the upper limit, the system will reject new connections. If you need to use more connections, you can modify the maximum number of concurrent connections per node of the instance through the `net.maxIncomingConnections` parameter. For more information about this parameter, refer to [Supported parameter](https://docs.byteplus.com/en/docs/mongodb/supported-parameter). You can also obtain a larger number of connections by upgrading the node specifications.

<span id=".5aaC5L2V5p-l55yLLW1vbmdvZGIt5a6e5L6L55qE6L-e5o6l5L2_55So5oOF5Ya177yf"></span>
### How to check the connection usage of a MongoDB instance?

You can check the number of connections currently used by a MongoDB instance as follows:


1. Connect to a MongoDB instance through the MongoDB shell tool on a local server or ECS instance with MongoDB shell installed. For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

2. Run the following command to check the usage of the instance's connection count.

   ```JavaScript
   db.serverStatus().connections
   ```
   

   Example of return results is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can focus on the parameters of <code>current</code> and <code>available</code>. The maximum number of connections for an instance = the number of currently established connections + the number of remaining available connections.   </div>
   

   ```JavaScript
   {
           "current" : 14,   // Number of existing connections
           "available" : 386,  // Number of available connections
           "totalCreated" : 65, 
           "internalCurrent" : 15,
           "internalTotalCreated" : 618540,
           "active" : 3
   }
   ```
   


<span id=".5aaC5L2V5p-l55yL6L-e5o6lLW1vbmdvZGIt5a6e5L6L55qE5a6i5oi356uv5p2l5rqQ77yf"></span>
### How to view the client source of connections to a MongoDB instance?

You can view the client source (including IP address and port number information) of connections to a MongoDB instance through the following steps.


1. Connect to a MongoDB instance through the MongoDB shell tool on a local server or ECS instance with MongoDB shell installed. For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

2. Run the following command to view the statements running in the database.

   ```JavaScript
   db.currentOp({"active" : true})
   ```
   

   Example of a partial return result is as follows.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can focus on the <code>client</code> parameter in the query results (which is the client information corresponding to the current connection) to confirm the number of connections established between each client and the MongoDB instance. For more information about the <code>db.currentOp()</code> command, refer to <a href="https://www.mongodb.com/docs/v4.4/reference/method/db.currentOp/">db.currentOp()</a>.   </div>
   

   ```JavaScript
   {
                           ...
                           "client" : "192.168.***.***:****", // Client information for current connection
                           "appName" : "MongoDB Shell",
                           "active" : true,
                           "currentOpTime" : "2023-01-28T16:45:51.243+0800",
                           "opid" : 7339****,
                           ...
                           "secs_running" : NumberLong(0),
                           "microsecs_running" : NumberLong(137),
                           "op" : "command",
                           "ns" : "admin.$cmd.aggregate",
                           "command" : {
                                   "currentOp" : 1,
                                   ...
                                   "$db" : "admin"
                           },
                           "numYields" : 0,
                           "locks" : {
                           },
                           "waitingForLock" : false,
                           "lockStats" : {
                           },
                           ...
                           
   }
   ```
   


<span id=".5aaC5L2V6ZmQ5Yi26K6_6ZeuLW1vbmdvZGIt5a6e5L6L55qE5a6i5oi356uv6L-e5o6l5pWw77yf"></span>
### How to limit the number of client connections accessing a MongoDB instance?

You can set the maximum number of connections for the client connection pool by using the `&maxPoolSize=[$Integer]` parameter when connecting to a MongoDB instance.

For example, when connecting to a MongoDB instance with the MongoDB shell tool, you can add the `&maxPoolSize=[$Integer]` parameter to the end of the address string. An example is provided below. Here, we use the private address of a replica set instance as an example, and the connection pool value is 2000.

```JavaScript
"mongodb://<user>:<password>@mongoreplicae9d7d321****0.mongodb.ibytepluses.com:3717,mongoreplicae9d7d321****1.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-e9d7d321****&retryWrites=true&maxPoolSize=2000
```


For limits on the connection pools for clients in different languages, refer to [MongoDB Drivers](https://www.mongodb.com/docs/drivers/).

<span id=".5Li65Ymv5pys6ZuG5a6e5L6L5paw5aKe6IqC54K55oiW5Li65YiG54mH6ZuG576k5paw5aKeLW1vbmdvcy3oioLngrnlkI7vvIzpnIDopoHkv67mlLnlupTnlKjnqIvluo_nmoTov57mjqXlnLDlnYDku6PnoIHmiY3og73ov57kuIrmlrDlop7oioLngrnlkJfvvJ8="></span>
### After adding a new node to a replica set instance (or a new Mongos node to a sharding cluster instance), is it necessary to modify the connection address of the application to connect to the new node?

After adding a node to a replica set instance (or a Mongos node to a sharding cluster instance), MongoDB can automatically discover and connect to the new node without modifying the client's connection string.

However, to ensure the effectiveness of failover and load balancing, it is recommended that after adding a new node, you replace the connection address string code on the client with the **new complete connection address string code** (as shown in the figure below) to connect to the MongoDB instance. For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ae6f38453ca6a76ca2646fb7b2cc7bb5.png) </span>

<span id=".5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5piv5ZCm5pSv5oyBLXNydi3nmoTov57mjqXmlrnlvI_vvJ8="></span>
### Does MongoDB support the SRV connection method?

First of all, not all clients (such as older versions of MongoDB clients) support SRV records; in addition, using SRV records requires additional DNS resolution costs, which will have a certain impact on performance. Due to the above compatibility and performance considerations, the Document Database for MongoDB does not support the SRV connection method. It is recommended that you directly use the standard complete connection address string to access the MongoDB instance. For specific procedures, refer to [Connecting to instance via MongoDB shell](https://docs.byteplus.com/en/docs/mongodb/connect-instance-via-mongo-shell).

<span id=".5aaC5L2V5p-l55yLLW1vbmdvZGIt6L-e5o6l5Zyw5Z2A5a-55bqU55qELWlwLeWcsOWdgA=="></span>
### How to check the IP address corresponding to the MongoDB connection address?


<Tabs>
<Tab zoneid="ed62r3Ytvm" title="Method 1: Check directly in console">
<TabTitle>Method 1: Check directly in console</TabTitle>

For specific procedures, refer to [View connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).


</Tab>
<Tab zoneid="mPN4a5JACf" title="Method 2: Query via API interface">
<TabTitle>Method 2: Query via API interface</TabTitle>

You can call the [DescribeDBEndpoint](https://docs.byteplus.com/en/docs/mongodb/describedbendpoint) interface to query the connection address information of a specified MongoDB instance, including the IP address information corresponding to different connection addresses of the instance. That is, the `AddressIP` information in the `DBAddresses` structure of the return result.

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_0953de1d09eeb6ad6866bd21ba22f2c2.png) </span>


</Tab>
<Tab zoneid="HHztyWM9im" title="Method 3: Query via PING command">
<TabTitle>Method 3: Query via PING command</TabTitle>

You can refer to the following steps to check the IP address corresponding to the MongoDB connection address:


1. Obtain connection address of the MongoDB instance. For specific procedures, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).

2. Log in to the ECS instance where the client is located and execute the PING command in the command line.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">This topic takes the MongoDB shell client as example. For the detailed procedure on connecting to MongoDB instance using the MongoDB shell tool, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/ug-connect-instance-via-mongo-shell">Connecting to instance via MongoDB shell</a>.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The PING command can be used in both Windows and Linux systems.   </div>
   

   Example is as follows.

   ```Bash
   ping mongoreplicac1a11ecf5****.mongodb.ibytepluses.com
   ```
   

   Example of return results is as follows.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5a42cbea41c53aa772815ea573140550.png) </span>


</Tab>
</Tabs>


<span id=".5piv5ZCm5pSv5oyB5L-u5pS5LW1vbmdvZGIt6L-e5o6l5Zyw5Z2A55qE5Z-f5ZCN77yf"></span>
### Does it support modifying the domain name of the MongoDB connection address?

Currently, only the private network or public network connection address domain names of the **replica set instances** and the **Mongos node** in sharding cluster instances and can be modified, but the connection address domain names of Shard or ConfigServer nodes in sharding cluster instances cannot be modified. For specific procedures, refer to [Modifying connection address](https://docs.byteplus.com/en/docs/mongodb/modify-connection-address).

<span id="W961Nm5x"></span>
### Does MongoDB support read/write splitting feature?

Yes. You can set the `readPreference` and `readPreferenceTags` parameters in the high\-availability address of the MongoDB instance according to your business needs to meet the read/write splitting requirements in different scenarios. For more details, refer to[ Read/write splitting](https://docs.byteplus.com/en/docs/mongodb/read_write_splitting).
