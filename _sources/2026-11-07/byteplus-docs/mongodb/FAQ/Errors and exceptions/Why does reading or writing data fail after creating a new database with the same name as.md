---
title: "Why does reading or writing data fail after creating a new database with the same name as a deleted one?"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/rw-failure-with-same-name-new-db-created"
---

<span id=".6Zeu6aKY546w6LGh"></span>
## Problem

After creating a new database with the same name as a deleted one, you cannot read the latest data from the new database or write data to it.

<span id=".5Y-X5b2x5ZON55qE5a6e5L6L"></span>
## Affected instances

MongoDB sharding cluster instances with database version 4.2.

<span id=".5Y6f5Zug"></span>
## Possible cause

Since instances of MongoDB versions prior to 4.4 use the `dropDatabase` command to delete the target database and do not automatically execute the `flushRouterConfig` command, nodes in sharded cluster instances may not refresh the metadata cache. For more details, refer to [MongoDB issues](https://jira.mongodb.org/browse/SERVER-17397).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Starting from MongoDB 4.4, when executing the <code>dropDatabase</code> command, the system automatically refreshes the sharding cluster's routing table as needed. Therefore, for MongoDB sharding instances of version 4.4 and later, it is no longer necessary to run <code>flushRouterConfig</code> after deleting the target database using the <code>dropDatabase</code> command. For more details, refer to <a href="https://www.mongodb.com/docs/v4.4/reference/command/flushRouterConfig/">flushRouterConfig</a>.</div>


<span id=".5bu66K6u"></span>
## Solution

You can follow these suggestions to avoid the above issues:


* After deleting target database, you must execute the `flushRouterConfig` command on the Mongos node before performing read or write operations to ensure that all nodes in the sharding cluster have flushed the metadata cache. To completely delete the MongoDB database, refer to [db.dropDatabase()](https://www.mongodb.com/docs/manual/reference/method/db.dropDatabase/#replica-set-and-sharded-clusters).

* Enable the sharding function of the sharding cluster instance database with the `sh.enableSharding` command, and convert unsharded collections to sharded collections with the `sh.shardCollection` command.

* After deleting target database, restart the MongoDB instance before performing data read and write operations. For instance restart procedure, refer to [Restarting instance](https://docs.byteplus.com/en/docs/mongodb/restart-instance).

* For databases without sharding enabled, we do not recommend creating a database or collection with the same name as a deleted one.

   If you have to create a database or collection with the same name, be sure to flush the route table on the Mongos node before creating it.
