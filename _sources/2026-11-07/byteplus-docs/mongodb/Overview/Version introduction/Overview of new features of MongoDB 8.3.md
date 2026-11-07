---
title: "Overview of new features of MongoDB 8.3"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/overviw_of_new_features_of_mongodb_83"
---

This topic introduces the main new features of MongoDB 8.3.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">MongoDB 8.3 is currently in canary release. If you need to use the vector search feature, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical staff for applying.</div>


* <div data-tips="true" data-tips-type="default">For more information on MongoDB 8.3 changes, see <a href="https://www.mongodb.com/docs/manual/release-notes/8.3/">Release notes</a>.</div>



<span id="BcGSFlEv"></span>
## Sharding cluster enhancements

<span id="FNu6YGtw"></span>
### Shard removal process refactoring

Deprecates the [removeShard](https://www.mongodb.com/zh-cn/docs/manual/reference/command/removeShard/#mongodb-dbcommand-dbcmd.removeShard)` `command, introducing four new commands—[startShardDraining](https://www.mongodb.com/zh-cn/docs/manual/reference/command/startShardDraining/#mongodb-dbcommand-dbcmd.startShardDraining), [stopShardDraining](https://www.mongodb.com/zh-cn/docs/manual/reference/command/stopShardDraining/#mongodb-dbcommand-dbcmd.stopShardDraining), [shardDrainingStatus](https://www.mongodb.com/zh-cn/docs/manual/reference/command/shardDrainingStatus/#mongodb-dbcommand-dbcmd.shardDrainingStatus), and [commitShardRemoval](https://www.mongodb.com/zh-cn/docs/manual/reference/command/commitShardRemoval/#mongodb-dbcommand-dbcmd.commitShardRemoval)—that support fine\-grained control over the shard removal and deletion process, effectively reducing the risk of accidental operations and enhancing the determinism and security of shard removal operations.

<span id="lZ9TG1Pd"></span>
### DDL operation routing restrictions

All [DDL operations](https://www.mongodb.com/zh-cn/docs/manual/reference/ddl-operations/#std-label-ddl-operations) and [applyOps](https://www.mongodb.com/zh-cn/docs/manual/reference/command/applyOps/#mongodb-dbcommand-dbcmd.applyOps) commands can only be executed via mongos, standardizing the entry point for DDL operations in sharding clusters and mitigating the risk of bypassing metadata management specifications.

<span id="QUQlK224"></span>
### Shard query statistics enhancements

After enabling [queryStats](https://www.mongodb.com/zh-cn/docs/manual/reference/command/serverStatus/#mongodb-serverstatus-serverstatus.queryStats), Shard includes queries originating from `mongos` in its statistics, facilitating comprehensive diagnostic analysis in a sharding cluster environment.

<span id="XjErkELf"></span>
### Orphaned document cleanup optimization

Optimizes the orphaned document cleanup mechanism after Chunk migration and enhances data consistency through the [terminateSecondaryReadsOnOrphanCleanup](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.terminateSecondaryReadsOnOrphanCleanup) parameter (enabled by default) and the [orphanCleanupDelaySecs](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.orphanCleanupDelaySecs) parameter (default value is 3,600 seconds).

<span id="g0RtfRXo"></span>
## Performance and monitoring

<span id="RsP8yxX9"></span>
### In\-progress slow query logs

Introduces an in\-progress slow query logging feature that supports real\-time recording of slow logs during query execution, without waiting for query completion. Set the threshold using the [--defaultSlowInProgMS](https://www.mongodb.com/zh-cn/docs/manual/reference/program/mongod/#std-option-mongod.--defaultSlowInProgMS) startup parameter or [db.setProfilingLevel()](https://www.mongodb.com/zh-cn/docs/manual/reference/method/db.setProfilingLevel/#mongodb-method-db.setProfilingLevel) parameter at runtime. The `originalQueryShapeHash` field in the logs facilitates associating Shard slow logs with original mongos requests, enabling end\-to\-end diagnosis in a sharding cluster environment.

<span id="181cBWKU"></span>
### Query\-level memory tracking

Adds the `inUseTrackedMemBytes` and `peakTrackedMemBytes` fields to track a query's current and peak memory consumption. This facilitates identifying operations with abnormal memory consumption and provides precise data for optimizing query statements or adjusting memory parameters.

<span id="UUbBMBxu"></span>
### serverStatus on\-demand output

Supports masking all optional fields via `none: 1`, and then selectively adding them as needed, simplifying monitoring data collection and reducing the burden of network transmission and client parsing. The `service` field has been removed.

<span id="R1rJ1bOm"></span>
### Standardize explain output

Explain output ([Explain results](https://www.mongodb.com/docs/manual/reference/explain-results/#std-label-explain-results)) in the spill to disk phase uniformly uses standard fields such as `spills` and `spilledBytes`, facilitating the analysis of disk usage for high\-memory operations.

<span id="mGN8gPwo"></span>
### New queryStats metrics

New metrics related to delinquent tickets ([Delinquent tickets](https://www.mongodb.com/docs/manual/core/wiredtiger/#std-label-storage-wiredtiger-concurrency)) have been added to the [$queryStats](https://www.mongodb.com/docs/manual/reference/operator/aggregation/queryStats/#mongodb-pipeline-pipe.-queryStats) output to monitor resource contention and queuing issues caused by slow execution ticket acquisition.

<span id="StspZcyj"></span>
### New currentOp field

A new `versionContext` field has been added to the output of the [$currentOp](https://www.mongodb.com/docs/manual/reference/operator/aggregation/currentOp/#mongodb-pipeline-pipe.-currentOp) aggregation stage to display the feature compatibility version information of operations, facilitating troubleshooting during upgrades.

<span id="oqNmXa7k"></span>
## Indexing, aggregation, and retrieval

<span id="2Sw1bOLj"></span>
### 2dsphere default version upgrade

The [2dsphereIndexVersion](https://www.mongodb.com/zh-cn/docs/manual/core/indexes/index-types/geospatial/2dsphere/2dsphere-index-versions/#std-label-2dsphere-index-versions) default value has been upgraded from 3 to 4, and newly created geospatial indexes will default to using more efficient storage and query algorithms.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">If you need to downgrade the <a href="https://www.mongodb.com/zh-cn/docs/manual/reference/command/setFeatureCompatibilityVersion/#std-label-view-fcv">feature compatibility version</a> below 8.3, you must first delete 2dsphere version 4 indexes.</div>


<span id="u87I20Nx"></span>
### Enhanced array index access

[$map](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/map/#mongodb-expression-exp.-map), [$filter](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/filter/#mongodb-expression-exp.-filter), and [$reduce](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/reduce/#mongodb-expression-exp.-reduce) expressions now support direct retrieval of the current element's index value. You can specify a custom variable name for the index using the arrayIndexAs field, or directly reference it using the built\-in [$IDX](https://www.mongodb.com/zh-cn/docs/manual/reference/aggregation-variables/#mongodb-variable-variable.IDX) variable. Access positional information within array processing logic without additional coding, simplifying the operational process.

<span id="5aLefzH6"></span>
### New aggregation expressions

New expressions such as [$subtype](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/subtype/#mongodb-expression-exp.-subtype), [$createObjectId](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/createObjectId/#mongodb-expression-exp.-createObjectId), [$hash](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/hash/#mongodb-expression-exp.-hash)/[$hexHash](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/hexHash/#mongodb-expression-exp.-hexHash), [$serializeEJSON](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/serializeEJSON/#mongodb-expression-exp.-serializeEJSON) /[$deserializeEJSON](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/deserializeEJSON/#mongodb-expression-exp.-deserializeEJSON), and [$scoreFusion](https://www.mongodb.com/zh-cn/docs/manual/reference/operator/aggregation/scoreFusion/#mongodb-pipeline-pipe.-scoreFusion) (now generally available) have been introduced, enriching data processing and type conversion capabilities and reducing the data processing burden on the application layer.

<span id="tnf8P6gS"></span>
### Vector search and full\-text search

MongoDB 8.3 has built\-in vector search and full\-text search capabilities. Vector search is based on semantic similarity and is suitable for unstructured data search in AI applications (e.g., searching for similar pictures in an image library, finding semantically related paragraphs in a document library); full\-text search is based on keyword matching and is suitable for document search and log analysis. You can create vector or full\-text indexes for collections in the console to accelerate retrieval. Both search methods can be used in combination.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The retrieval feature is currently only available for MongoDB 8.3 and later versions.</div>


<span id="cVr1nhny"></span>
### Run rankFusion on views

The [$rankFusion](https://www.mongodb.com/docs/manual/reference/operator/aggregation/rankFusion/#mongodb-pipeline-pipe.-rankFusion) stage, used for hybrid search, supports running directly on [views](https://www.mongodb.com/docs/manual/core/views/#std-label-views-landing-page).

<span id="zbKeYKZy"></span>
### Supports $currentDate

In the [aggregate()](https://www.mongodb.com/docs/manual/reference/method/db.collection.aggregate/#mongodb-method-db.collection.aggregate) pipeline, you can use `$currentDate` to return the server's current time.

<span id="p0eopKzo"></span>
## Connection and behavior changes

<span id="k4IuD3Wz"></span>
### New performance tuning parameters


*  [cachePressureQueryPeriodMilliseconds](https://www.mongodb.com/zh-cn/docs/manual/reference/parameters/#mongodb-parameter-param.cachePressureQueryPeriodMilliseconds)

   Controls the frequency of checking cache pressure; upon detection, the oldest transactions are automatically aborted to free up cache.

* [overloadAwareServerSelectionEnabled](https://www.mongodb.com/zh-cn/docs/manual/reference/parameters/#mongodb-parameter-param.overloadAwareServerSelectionEnabled)

   When enabled, clients automatically switch to other nodes to retry upon receiving a SystemOverloadedError, providing applications with fault avoidance capabilities and effectively reducing overall request latency and failure rates.

* [ingressRequestRateLimiterApplicationExemptions](https://www.mongodb.com/zh-cn/docs/manual/reference/parameters/#mongodb-parameter-param.ingressRequestRateLimiterApplicationExemptions)

   Allows specifying applications to be exempt from ingress rate limiting, ensuring the availability of critical business applications during peak traffic.


<span id="aXkHQwAK"></span>
### Behavior changes


* Upsert Error Code Changes

   When an Upsert generates an oversized [BSON object](https://www.mongodb.com/zh-cn/docs/manual/reference/bson-types/#std-label-bson-types), the error code changes to `10334` (originally `17419`/`17420`), making the error type more accurate and facilitating precise capture and handling by clients.

* Validate command update

   `validate(full=true)` no longer automatically enables `checkBSONConformance`, but adds checks for documents exceeding 16 MB, making the validation process more controllable.
