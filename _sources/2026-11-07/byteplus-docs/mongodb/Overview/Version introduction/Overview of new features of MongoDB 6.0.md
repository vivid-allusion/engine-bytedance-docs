---
title: "Overview of new features of MongoDB 6.0"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/mongodb-6-features"
---

This topic introduces the main new features of MongoDB version 6.0.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details on MongoDB 6.0 features, refer to <a href="https://www.mongodb.com/docs/manual/release-notes/6.0/">MongoDB 6.0 release notes</a>.</div>


<span id=".6IGa5ZCILe-8iGFnZ3JlZ2F0aW9u77yJ"></span>
## Aggregation

MongoDB's aggregation feature supports filtering, grouping, sorting data, calculating statistics, and performing other operations via an aggregation pipeline, aiding in the analysis and processing of data from multiple documents.

MongoDB 6.0 includes the following updates for the aggregation feature:


* Added support for more aggregation stages, including [$densify](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/densify/#mongodb-pipeline-pipe.-densify), [$documents](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/documents/#mongodb-pipeline-pipe.-documents), [$fill](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/fill/#mongodb-pipeline-pipe.-fill), and [$shardedDataDistribution](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/shardedDataDistribution/#mongodb-pipeline-pipe.-shardedDataDistribution).

* Added support for more aggregation operators, e.g., [$bottomN](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/bottomN/#mongodb-group-grp.-bottomN)/[$topN](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/topN/#mongodb-group-grp.-topN), [$firstN](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/firstN/#mongodb-group-grp.-firstN)/[$lastN](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/lastN/#mongodb-group-grp.-lastN), [$linearFill](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/linearFill/#mongodb-group-grp.-linearFill), [$locf](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/locf/#mongodb-group-grp.-locf), [$maxN](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/maxN/#mongodb-group-grp.-maxN)/[$minN](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/minN/#mongodb-group-grp.-minN), [$sortArray](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/sortArray/#mongodb-expression-exp.-sortArray), [$tsIncrement](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/tsIncrement/#mongodb-expression-exp.-tsIncrement), and [$tsSecond](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/tsSecond/#mongodb-expression-exp.-tsSecond). You can combine these aggregation operators to form complex aggregation pipelines to meet various data analysis needs.

* Aggregation stages now offer optimized support for sharded collections. MongoDB 6.0 adds support for using sharded collections in the `from` field of [$lookup](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/lookup/#mongodb-pipeline-pipe.-lookup) and [$graphLookup](https://www.mongodb.com/docs/v6.0/reference/operator/aggregation/graphLookup/#mongodb-pipeline-pipe.-graphLookup) aggregation stages.


<span id=".5Y-Y5pu05rWB77yIY2hhbmdlLXN0cmVhbXPvvIk="></span>
## Change streams

The change stream feature, supported since MongoDB 3.6, can be used to monitor modification operations on MongoDB collections, databases, or deployments. When a monitored resource changes, the change stream returns a change event notification document containing information about the operation and the changes made.

For the change stream feature, MongoDB 6.0 includes the following updates:


* Adds support for viewing document versions before and after changes (that is, Pre\-image and Post\-image). Versions prior to MongoDB 6.0 only supported viewing the post\-change version. For more details, refer to [Change Streams with Document Pre- and Post-Images](https://www.mongodb.com/docs/v6.0/reference/method/db.collection.watch/#std-label-db.collection.watch-change-streams-pre-and-post-images-example).

* Change stream events ([change stream events](https://www.mongodb.com/docs/manual/reference/change-events/#std-label-change-stream-output)) now support DDL statements such as [create](https://www.mongodb.com/docs/manual/reference/change-events/create/), [createIndexes](https://www.mongodb.com/docs/manual/reference/change-events/createIndexes/), [dropIndexes](https://www.mongodb.com/docs/manual/reference/change-events/dropIndexes/), [modify](https://www.mongodb.com/docs/manual/reference/change-events/modify/), and [shardCollection](https://www.mongodb.com/docs/manual/reference/change-events/shardCollection/).

* Change stream events ([change stream events](https://www.mongodb.com/docs/manual/reference/change-events/#std-label-change-stream-output)) add the `wallTime` field to determine the server date and time of database operations.


<span id=".57Si5byV77yIaW5kZXjvvIk="></span>
## Index

Since MongoDB 5.0, index\-related features have been optimized as follows:


* Starting from MongoDB 5.1, you can convert a regular single\-field index to a TTL index by adding the `expireAfterSeconds` field in the [collMod](https://www.mongodb.com/docs/v6.0/reference/command/collMod/#mongodb-dbcommand-dbcmd.collMod) command.

* MongoDB 5.3 adds support for using clustered indexes ([Clustered index](https://www.mongodb.com/docs/v6.0/reference/method/db.createCollection/#std-label-db.createCollection.clusteredIndex)) when creating collections. Collections using clustered indexes (that is, [Clustered Collections](https://www.mongodb.com/docs/v6.0/core/clustered-collections/#std-label-clustered-collections)) offer the following advantages:

   * Clustered collections have additional performance improvements in CRUD scenarios. The reasons are as follows:

      * When creating collections, MongoDB automatically creates a unique index on the `_id` field to prevent clients from inserting duplicate data with the same `_id`. Non\-clustered collections need to store data and the `_id` index separately, which means modification or read operations require writing or reading data twice.

      * Clustered collections store data and the `_id` index together in `_id` order. Therefore, modification or read operations only require writing or reading data once, enabling faster queries without relying on secondary indexes (for example, range and equality queries on clustered index keys).

   * Clustered collections use less storage space, which helps improve query and bulk insertion performance.

   * Clustered indexes can serve as TTL indexes (requiring a format compliant with supported date types), which can enhance TTL deletion efficiency and reduce data storage space.

* MongoDB 6.0 supported using the prep`areUnique and` uniq`ue opt`ions with the coll[Mod com](https://www.mongodb.com/docs/v6.0/reference/command/collMod/#mongodb-dbcommand-dbcmd.collMod)mand to convert an existing standard index to a unique index. For a specific example of index conversion, refer to [Convert an Existing Index to a Unique Index](https://www.mongodb.com/docs/v6.0/core/index-unique/convert-to-unique/#convert-an-existing-index-to-a-unique-index).


<span id=".5YiG54mH6ZuG5LyY5YyW77yIc2hhcmRpbmfvvIk="></span>
## Optimizations for Sharding

MongoDB 6.0 has implemented the following optimizations for sharding clusters:

Adjustment of balancing strategy: Starting from MongoDB version 6.0, the data distribution strategy in sharded clusters is no longer based on the number of chunks but on data size. This optimization has the following effects:


* The Balancer focuses more on balancing data distribution rather than chunk distribution.

* Chunks only split when being moved between shards; they do not automatically split at other times.

* Chunks are now called ranges, and the [moveRange](https://www.mongodb.com/docs/manual/reference/command/moveRange/) command replaces the original [moveChunk](https://www.mongodb.com/docs/manual/reference/command/moveChunk/).


<span id=".5pe25bqP6ZuG5ZCI77yIdGltZS1zZXJpZXMtY29sbGVjdGlvbnPvvIk="></span>
## Time series collections

Since MongoDB 5.0, the following optimizations have been made to time series collection features:


* MongoDB 5.1 added support for sharding time series collections, providing them with the ability to horizontally scale capacity and read/write performance. For more details, refer to [Shard a Time Series Collection](https://www.mongodb.com/docs/v6.0/core/timeseries/timeseries-shard-collection/#shard-a-time-series-collection).

* Since MongoDB 5.2, time series collections have begun using column compression to help reduce overall data storage on disk and improve read performance.

* MongoDB 6.0 added support for compressing array type data. For more details, refer to [Time Series Compression](https://www.mongodb.com/docs/v6.0/core/timeseries/timeseries-compression/).
