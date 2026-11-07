---
title: "Read/write splitting"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/read_write_splitting"
---

Document Database for MongoDB supports read/write splitting by specifying parameters in the instance connection address. This topic describes how to configure the relevant parameters to implement read/write splitting.

<span id="uLktNKTW"></span>
## Background information

Document Database for MongoDB provides high\-availability addresses by default for the replica set instances and Mongos components in sharding cluster instances. This address includes all node addresses of replica set instances or all Mongos node addresses in sharding clusters. After a primary\-secondary switchover, write requests are routed to the new primary node or other Mongos nodes, ensuring write operations are always performed successfully. For more details about MongoDB instance connection address, refer to [Viewing connection address](https://docs.byteplus.com/en/docs/mongodb/addresses-introduction).

<span id="yA5e52Hu"></span>
## Introduction to read/write splitting parameters

Document Database for MongoDB supports using the `readPreference` and `readPreferenceTags` parameters in high\-availability addresses to implement read/write splitting.


|Parameter |Description |Connection address types that support corresponding parameters |
|---|---|---|
|`readPreference` |Used to implement read/write splitting and load balancing for highly available addresses. This parameter can send write requests to the primary node and randomly send read requests to secondary nodes and read\-only nodes. The available values are as follows:<br><br><br>* `readPreference=primary`: Read requests are only sent to the primary node.<br><br>* `readPreference=primaryPreferred`: Prefer reading from the primary node. If the primary node fails, send read requests to the secondary nodes and read\-only nodes.<br><br>* `readPreference=secondary`: Only read from secondary nodes and read\-only nodes. If both secondary nodes and read\-only nodes fail, the read request fails and will not be sent to the primary node.<br><br>* `readPreference=secondaryPreferred`: Preferentially read from secondary and read\-only nodes. If both secondary nodes and read\-only nodes fail, this parameter sends the read request to the primary node.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more details about the <code>readPreference</code> parameter, refer to <a href="https://www.mongodb.com/docs/v6.0/core/read-preference/">Read Preference</a>.</div><br> |* Replica set instance connection address.<br><br>* Connection addresses for Mongos, Shard, and ConfigServer components in a sharding cluster instance.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The connection addresses of Shard or ConfigServer components in a sharding cluster instance are primarily used for testing or other special scenarios. In production environment, it is not recommended to directly connect to Shard or ConfigServer addresses for read/write operations. Instead, connect via the Mongos address to achieve load balancing and read/write splitting.   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">Document Database for MongoDB only provides Mongos private network addresses by default. If you need to use Shard or ConfigServer component connection addresses, you must apply for them separately. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/apply-private-address">Applying for private address</a> and <a href="https://docs.byteplus.com/en/docs/mongodb/ug-apply-public-address">Applying for public address</a>.   </div><br>    |
|`readPreferenceTags`<br><br> |This parameter can send read requests to the node corresponding to the tag. The available values are as follows:<br><br><br>* `readPreferenceTags=role:electable`: Read requests are sent to secondary node.<br><br>* `readPreferenceTags=role:readonly`: Read requests are sent to read\-only node.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">For instances created before November 27, 2025, if you need to set <code>readPreferenceTags=role:electable</code>, you must first enable <strong>Read/write splitting enhancement</strong> feature on the <strong>Connectivity</strong> tab of the instance. <strong>Read/write splitting enhancement</strong> feature switch once been enabled, it cannot be disabled.</div><br><br><br>* <div data-tips="true" data-tips-type="default">MongoDB instances created on or after November 27, 2025, support setting <code>readPreferenceTags=role:electable</code> by default. You can directly set this parameter in the connection address.</div><br><br><br>* <div data-tips="true" data-tips-type="default">This parameter is usually used together with the <code>readPreference</code> parameter to implement read\-write separation functionality, but it is incompatible with the <code>primary</code> mode.</div><br><br><br>* <div data-tips="true" data-tips-type="default">The setting of <code>readPreferenceTags=role:readonly</code> will only take effect when there is read\-only node in the instance. For specific procedures on using read\-only nodes, refer to <a href="https://docs.byteplus.com/en/docs/mongodb/add-or-remove-read-only-node">Adding or deleting read\-only nodes</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="default">For more details about the <code>readPreferenceTags</code> parameter, refer to <a href="https://www.mongodb.com/docs/v6.0/reference/connection-string-options/#mongodb-urioption-urioption.readPreferenceTags">readPreferenceTags</a>.</div><br> |* Replica set instance connection address.<br><br>* Mongos and Shard component connection addresses in a sharding cluster instance. |


<span id="4UKUrTSP"></span>
## Setting read/write splitting connection address

You can set the `readPreference` and `readPreferenceTags` parameters in the high\-availability address of the MongoDB instance according to your business needs to meet the read/write splitting requirements in different scenarios.


<Tabs>
<Tab zoneid="GEqRcy4a2p" title="Read requests are sent to primary node when secondary or read-only nodes fail">
<TabTitle>Read requests are sent to primary node when secondary or read-only nodes fail</TabTitle>

* Read request routing strategy and suggestions for Read/write splitting parameter settings.

   
   |**Read request distribution strategy** |**Parameter setting suggestions** |
   |---|---|
   |Preferentially read from primary node. |`readPreference=primaryPreferred` |
   |Preferentially read from secondary and read\-only nodes. |`readPreference=secondaryPreferred` |
   |Preferentially read from secondary node.<br><br>If secondary node fails, read requests will be sent to primary node and not to read\-only nodes. |`readPreference=secondaryPreferred&readPreferenceTags=role:electable` |
   |Preferentially read from read\-only nodes.<br><br>If read\-only node fails, read requests will be sent to primary node, not to secondary node. |`readPreference=secondaryPreferred&readPreferenceTags=role:readonly` |
   

* Example of Read/write splitting connection address

   The following example uses the connection address of a MongoDB replica set instance. It configures the instance to preferentially read from read\-only nodes. If read\-only nodes fail, read requests are sent to primary node.

   ```Bash
   mongodb://root:Pwd_123456@mongoreplicab338d0d1****0.mongodb.ibytepluses.com:3717,mongoreplicab338d0d1****1.mongodb.ibytepluses.com:3717,mongoreplicab338d0d1****100.mongodb.ibytepluses.com:3717/?authSource=admin&replicaSet=rs-mongo-replica-b338d0d1a007&readPreference=secondaryPreferred&readPreferenceTags=role:readonly&retryWrites=true
   ```
   


</Tab>
<Tab zoneid="e0Ye4J8Vcj" title="Read requests are not sent to primary node when secondary or read-only nodes fail">
<TabTitle>Read requests are not sent to primary node when secondary or read-only nodes fail</TabTitle>

* Read request routing strategy and suggestions for read/write splitting parameter settings.

   
   |**Read request distribution strategy** |**Parameter setting suggestions** |
   |---|---|
   |Only read from secondary nodes and read\-only nodes. |`readPreference=secondary` |
   |Only read from secondary node. If secondary node fails, read request fails. |`readPreference=secondary&readPreferenceTags=role:electable` |
   |Only read from read\-only nodes. If read\-only nodes fail, the read operation fails. |`readPreference=secondary&readPreferenceTags=role:readonly` |
   

* Example of Read/write splitting connection address

   The following example uses the Mongos connection address of MongoDB sharding cluster instance. It configures instance to only read from secondary node. If secondary node fails, read request will also fail.

   ```Bash
   mongodb://root:Pwd_123456@mongoshardcd671c46****0.mongodb.ibytepluses.com:3717,mongoshardcd671c46****1.mongodb.ibytepluses.com:3717,mongoshardcd671c46****2.mongodb.ibytepluses.com:3717/?authSource=admin&readPreference=secondary&readPreferenceTags=role:electable&retryWrites=true
   ```
   


</Tab>
</Tabs>


<span id="vvecpttj"></span>
## FAQs


* [How to check the connection usage of a MongoDB instance?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5aaC5L2V5p-l55yLLW1vbmdvZGIt5a6e5L6L55qE6L-e5o6l5L2_55So5oOF5Ya177yf)

* [How to view the client source of connections to a MongoDB instance?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5aaC5L2V5p-l55yL6L-e5o6lLW1vbmdvZGIt5a6e5L6L55qE5a6i5oi356uv5p2l5rqQ77yf)

* [How to limit the number of client connections accessing a MongoDB instance?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5aaC5L2V6ZmQ5Yi26K6_6ZeuLW1vbmdvZGIt5a6e5L6L55qE5a6i5oi356uv6L-e5o6l5pWw77yf)

* [After adding a new node to a replica set instance (or a new Mongos node to a sharding cluster instance), is it necessary to modify the connection address of the application to connect to the new node?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5Li65Ymv5pys6ZuG5a6e5L6L5paw5aKe6IqC54K55oiW5Li65YiG54mH6ZuG576k5paw5aKeLW1vbmdvcy3oioLngrnlkI7vvIzpnIDopoHkv67mlLnlupTnlKjnqIvluo_nmoTov57mjqXlnLDlnYDku6PnoIHmiY3og73ov57kuIrmlrDlop7oioLngrnlkJfvvJ8=)

* [Does MongoDB support the SRV connection method?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5paH5qGj5pWw5o2u5bqTLW1vbmdvZGIt54mI5piv5ZCm5pSv5oyBLXNydi3nmoTov57mjqXmlrnlvI_vvJ8=)

* [How to check the IP address corresponding to the MongoDB connection address?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5aaC5L2V5p-l55yLLW1vbmdvZGIt6L-e5o6l5Zyw5Z2A5a-55bqU55qELWlwLeWcsOWdgA==)

* [Does it support modifying the domain name of the MongoDB connection address?](https://docs.byteplus.com/en/docs/mongodb/network-connection#.5piv5ZCm5pSv5oyB5L-u5pS5LW1vbmdvZGIt6L-e5o6l5Zyw5Z2A55qE5Z-f5ZCN77yf)

* [Does MongoDB support read/write splitting feature?](https://docs.byteplus.com/en/docs/mongodb/network-connection#W961Nm5x)
