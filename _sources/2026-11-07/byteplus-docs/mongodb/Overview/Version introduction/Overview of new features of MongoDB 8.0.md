---
title: "Overview of new features of MongoDB 8.0"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/mongodb-8-features"
---

This topic introduces the main new features of MongoDB version 8.0.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">For more details of MongoDB 8.0 features, refer to <a href="https://www.mongodb.com/docs/manual/release-notes/8.0/">MongoDB 8.0 release notes</a>.</div>



<span id="Gar90Guo"></span>
## Sharding cluster enhancements

MongoDB version 8.0 has enhancements in sharding cluster management, operations, and performance:


* **Collection management actions**

   * Move unsharded collections: Added the [moveCollection](https://www.mongodb.com/docs/manual/reference/command/moveCollection/#mongodb-dbcommand-dbcmd.moveCollection) and [sh.moveCollection()](https://www.mongodb.com/docs/manual/reference/method/sh.moveCollection/#mongodb-method-sh.moveCollection) commands, which can move unsharded collections between shards, and support using [abortMoveCollection](https://www.mongodb.com/docs/manual/reference/command/abortMoveCollection/#mongodb-dbcommand-dbcmd.abortMoveCollection) or [sh.abortMoveCollection()](https://www.mongodb.com/docs/manual/reference/method/sh.abortMoveCollection/#mongodb-method-sh.abortMoveCollection) to abort the move operation.

   * Unshard collections: Added the [unshardCollection](https://www.mongodb.com/docs/manual/reference/command/unshardCollection/#mongodb-dbcommand-dbcmd.unshardCollection) and [sh.unshardCollection()](https://www.mongodb.com/docs/manual/reference/method/sh.unshardCollection/#mongodb-method-sh.unshardCollection) commands, which can convert sharded collections into unsharded collections. The data will be migrated to the specified shard or the shard with the least amount of data, and supported using [abortUnshardCollection](https://www.mongodb.com/docs/manual/reference/command/abortUnshardCollection/#mongodb-dbcommand-dbcmd.abortUnshardCollection) or [sh.abortUnshardCollection()](https://www.mongodb.com/docs/manual/reference/method/sh.abortUnshardCollection/#mongodb-method-sh.abortUnshardCollection) to abort the conversion operation.

* **Sharding operation performance and elasticity**

   * Resharding optimization: Optimized the performance of the [reshardCollection](https://www.mongodb.com/docs/manual/reference/command/reshardCollection/#mongodb-dbcommand-dbcmd.reshardCollection) operation to reduce its runtime. Added the `forceRedistribution` option to redistribute data to the new shard. For more details, refer to [Reshard a Collection](https://www.mongodb.com/docs/manual/reference/command/reshardCollection/#reshard-a-collection).

   * Adjusted the default number of chunks: For hash sharding, the default number of initial chunks created per shard has been reduced from 2 to 1.

* **Query and data management**

   * Partial shard key query: When executing the [findAndModify](https://www.mongodb.com/docs/manual/reference/command/findAndModify/#mongodb-dbcommand-dbcmd.findAndModify) or [deleteOne()](https://www.mongodb.com/docs/manual/reference/method/db.collection.deleteOne/#mongodb-method-db.collection.deleteOne) command, the query condition only needs to contain part of the shard key (previously, the complete shard key was usually required).

   * Sharded collection update/insert optimization: When executing the [updateOne()](https://www.mongodb.com/docs/manual/reference/method/db.collection.updateOne/#mongodb-method-db.collection.updateOne) command with [upsert: true](https://www.mongodb.com/docs/manual/reference/method/db.collection.update/#std-label-update-upsert) on a sharded collection, the complete shard key is no longer required in the query condition. Additionally, the sort field is supported in [updateOne()](https://www.mongodb.com/docs/manual/reference/method/db.collection.updateOne/#mongodb-method-db.collection.updateOne), [replaceOne()](https://www.mongodb.com/docs/manual/reference/method/db.collection.replaceOne/#mongodb-method-db.collection.replaceOne), and [update](https://www.mongodb.com/docs/manual/reference/command/update/#mongodb-dbcommand-dbcmd.update) commands.

* **Data verification diagnostics**

   Directly run dbHash: Supports running the [dbHash](https://www.mongodb.com/docs/manual/reference/command/dbHash/#mongodb-dbcommand-dbcmd.dbHash) command directly on each shard for easy data verification and diagnosis.


<span id="WpLQG7Aj"></span>
## Performance efficiency improvements

MongoDB 8.0 has been optimized in terms of the performance and efficiency of database core actions:


* **Write performance optimization**

   * Majority write confirm mechanism change: When `writeConcern` is set to `"majority"`, only a majority of nodes need to write the operation to their Oplog before a confirm is returned, without waiting for the operation to be applied. This significantly improves write performance, but aware of potential delays when reading from a secondary node.

   * Support batch writing: Added support for the [bulkWrite](https://www.mongodb.com/docs/manual/reference/command/bulkWrite/#mongodb-dbcommand-dbcmd.bulkWrite) bulk write command, which allows you to perform bulk insert, update, and delete actions on multiple collections in a single request.

   * Bulk insert optimization: Non\-transactional bulk multi\-document insert operations are merged into a single entry in the Oplog, which significantly reduces replication latency and improves insert performance. These inserted documents have the same `clusterTime` in change stream events.

* **Memory management optimization**

   Upgraded TCMalloc: The new version of the TCMalloc memory allocator, which is based on per\-CPU cache instead of per\-thread cache, effectively reduces memory fragmentation and improves performance and stability under high\-stress loads. For more details, refer to [TCMalloc performance optimization](https://www.mongodb.com/docs/manual/administration/tcmalloc-performance/#std-label-tcmalloc-performance).

* **Concurrency control**

   DDL operation concurrency: Supports the concurrent execution of multiple [DDL operations](https://www.mongodb.com/docs/manual/reference/glossary/#std-term-DDL--Data-Definition-Language-) on different collections within the same database, increasing the efficiency of management operations.


<span id="aRw0aozX"></span>
## Vector search

MongoD 8.0 provides vector search capability. Vector Search supports querying data based on semantics rather than just keyword matching, helping to obtain more relevant search results. For more details, refer to [Vector search](https://docs.byteplus.com/en/docs/mongodb/vector_index).

<span id="iwj0C6wE"></span>
## Query, aggregation, and index optimization

MongoDB version 8.0 enhances the data query, processing, and index building capabilities and flexibility in the following aspects:


* Aggregation pipeline enhancement

   * Binary data conversion: Supported converting between strings and binary data (binData) using the [$convert](https://www.mongodb.com/docs/manual/reference/operator/aggregation/convert/#mongodb-expression-exp.-convert) operator. Added the [$toUUID](https://www.mongodb.com/docs/manual/reference/operator/aggregation/toUUID/#mongodb-expression-exp.-toUUID) expression to simplify the syntax for converting strings to UUIDs.

   * Sorting operation optimization: In the [$denseRank](https://www.mongodb.com/docs/manual/reference/operator/aggregation/denseRank/#mongodb-group-grp.-denseRank) and [$rank](https://www.mongodb.com/docs/manual/reference/operator/aggregation/rank/#mongodb-group-grp.-rank) operators, the handling of null and missing fields by `sortBy` `null`is consistent with that of the [$sort](https://www.mongodb.com/docs/manual/reference/operator/aggregation/sort/#mongodb-pipeline-pipe.-sort) operator.

* Index building and query optimization

   * Index build error reporting: Improved the speed of error reporting during [index builds](https://www.mongodb.com/docs/manual/reference/method/db.collection.createIndex/#std-label-create-index-builds) and enhanced fault tolerance.

   * Query settings: Introduced a new [query shape](https://www.mongodb.com/docs/manual/core/query-shapes/#std-label-query-shapes) and supported using the [setQuerySettings](https://www.mongodb.com/docs/manual/reference/command/setQuerySettings/#mongodb-dbcommand-dbcmd.setQuerySettings) command to configure query settings for it to influence the query optimizer's plan selection.


<span id="lenFOrUh"></span>
## Operations and diagnosis

MongoDB 8.0 version enhances the maintainability and observability of the database in the following aspects:


* Slow query logs filtering: Supported filtering and recording slow query logs based on `workingMillis` (actual operation execution time) rather than `durationMillis` (total operation delay), which can more accurately reflect the performance bottlenecks of the database itself. For more details, refer to [db.setProfilingLevel()](https://www.mongodb.com/docs/manual/reference/method/db.setProfilingLevel/#mongodb-method-db.setProfilingLevel).

* Compression operations enhancement

   * Compression command parameters: The [compact](https://www.mongodb.com/docs/manual/reference/command/compact/#mongodb-dbcommand-dbcmd.compact) command added the `freeSpaceTargetMB` parameter to specify the minimum space to be reclaimed, and the `dryRun` parameter for trial runs, which returns only the estimated results without actually performing any compression.

   * Background compression: Supported performing background compression via the [autoCompact](https://www.mongodb.com/docs/manual/reference/command/autoCompact/#mongodb-dbcommand-dbcmd.autoCompact) command.


<span id="920rR2bx"></span>
## More optimizations


* Security and query encryption: When performing [queryable encryption](https://www.mongodb.com/docs/manual/core/queryable-encryption/#std-label-qe-manual-feature-qe), you can use the [$lt](https://www.mongodb.com/docs/manual/reference/operator/query/lt/#mongodb-query-op.-lt), [$lte](https://www.mongodb.com/docs/manual/reference/operator/query/lte/#mongodb-query-op.-lte), [$gt](https://www.mongodb.com/docs/manual/reference/operator/query/gt/#mongodb-query-op.-gt), and [$gte](https://www.mongodb.com/docs/manual/reference/operator/query/gte/#mongodb-query-op.-gte) operators for range queries on encrypted fields, which greatly enhances the query capabilities on encrypted data.

* Capped collections update: TTL indexes can now be created on capped collections, and read concern ["snapshot"](https://www.mongodb.com/docs/manual/reference/read-concern-snapshot/#mongodb-readconcern-readconcern.-snapshot-) is supported.

* DDL and adding/removing shard operations are mutually exclusive: During a DDL operation (such as `reshardCollection`) on a cluster, adding or removing shards will be blocked until the DDL operation is complete.
