---
title: "How to perform incremental migration or incremental synchronization when the source database is a single node MongoDB instance?"
product: "Database Transmission Service"
product_code: "DTS"
source: "https://docs.byteplus.com/en/docs/DTS/how_to_perform_incremental_migration_or_incremental_synchronization"
---

DTS does not support data synchronization or incremental migration when the source database is a single node MongoDB instance. To use incremental data synchronization, you need to convert the single node MongoDB to a replica set as follows.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">Single node MongoDB instances do not have an oplog, so incremental migration or incremental synchronization cannot be achieved. When a single node MongoDB instance is converted to a replica set, there will be an oplog, and the oplog can be used to implement incremental migration or incremental synchronization. Refer to <a href="https://www.mongodb.com/zh-cn/docs/v6.0/tutorial/convert-standalone-to-replica-set/">Convert a standalone self\-managed mongod to a replica set</a> for more information.</div>


* <div data-tips="true" data-tips-type="default">After a single node MongoDB instance is converted to a replica set, since there are no other nodes, the write operation does not have node confirmation from the node.</div>


1. Close the running MongoDB service.

2. Restart the MongoDB instance and specify the replica set name.

   * Method 1: Set the `replSetName` parameter in the configuration file, as shown below.

      ```Java
      replication:
      replSetName: "rs0"
      ```
      

   * Method 2: Specify it when you start MongoDB by the command line: `mongod --replSet rs0`.

3. After starting the MongoDB instance, connect to it. Then, use the following command to initialize the replica set.

   ```Java
   rs.initiate()
   ```
   

5. After initializing the replica set, use the following command to see if oplog is present. If the oplog.rs collection exists, it indicates that the oplog can be used for incremental migration or incremental synchronization.

   ```Java
   use local
   show collections
   ```
