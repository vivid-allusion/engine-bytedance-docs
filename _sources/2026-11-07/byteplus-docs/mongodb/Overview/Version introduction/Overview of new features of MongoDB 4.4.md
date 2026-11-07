---
title: "Overview of new features of MongoDB 4.4"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/mongodb-4-4-features"
---

This topic introduces the main new features of MongoDB version 4.4.

<span id=".5YWo5pe26K-K5pat5pWw5o2u6YeH6ZuG77yIZnVsbC10aW1lLWRpYWdub3N0aWMtZGF0YS1jYXB0dXJl77yJ"></span>
## Full time diagnostic data capture

Starting from MongoDB 4.4, the initiation process will be terminated when the Full Time Diagnostic Data Capture (FTDC) thread in mongod or mongos fails. For more details, refer to [Full Time Diagnostic Data Capture (FTDC)](https://www.mongodb.com/docs/v4.4/administration/analyzing-mongodb-performance/#std-label-ftdc-stub).

<span id=".6YeN5a6a5LmJ5YiG54mH6ZSu77yIcmVmaW5hYmxlLXNoYXJkLWtleXPvvIk="></span>
## Refinable shard keys

MongoDB version 4.4 introduces the `refineCollectionShardKey` command to optimize a collection's shard key, allowing you to add one or more suffix fields to an existing shard key via the `refineCollectionShardKey` command to achieve finer\-grained data distribution. For more details, refer to [refineCollectionShardKey](https://www.mongodb.com/docs/v4.4/reference/command/refineCollectionShardKey/#mongodb-dbcommand-dbcmd.refineCollectionShardKey).

<span id=".5a-55Yay6K-777yIaGVkZ2VkLXJlYWRz77yJ"></span>
## Hedged reads

To reduce data read latency, MongoDB version 4.4 supports the Hedged Reads feature, where, in a sharding cluster scenario, the mongos node routes a read request concurrently to multiple nodes within the queried shard and returns the fastest query result to the client. You can set the parameter `readHedgingMode` to `on` in the `Read Preference` field of the sharding cluster. For more details, refer to [hedged reads](https://www.mongodb.com/docs/v4.4/core/sharded-cluster-query-router/#std-label-mongos-hedged-reads) and [Read Preference for Sharded Clusters](https://www.mongodb.com/docs/v4.4/core/read-preference-mechanics/#std-label-replica-set-read-preference-behavior-mongos).

<span id=".5aSN5ZCI5ZOI5biM5YiG54mH6ZSu77yIY29tcG91bmQtaGFzaGVkLXNoYXJkLWtleXPvvIk="></span>
## Compound hashed shard keys

MongoDB 4.4 introduces compound hashed indexes, allowing the specification of a single hash field in a compound index, thereby supporting compound hashed shard keys to help distribute collection data evenly among shards and simplify business logic complexity. For more details, refer to [Compound Hashed Indexes](https://www.mongodb.com/docs/v4.4/core/index-hashed/#create-a-compound-hashed-index).

<span id=".6ZqQ6JeP57Si5byV77yIaGlkZGVuLWluZGV4ZXPvvIk="></span>
## Hidden indexes

MongoDB 4.4 supports the Hidden Indexes feature. You can hide existing indexes using the `collMod` command. Once hidden, these indexes will not be chosen by the query planner, helping you assess the impact of deleting the index. If hiding the index affects online services, you can unhide it, and the index will be immediately available. For more details, refer to [Hidden Indexes](https://www.mongodb.com/docs/v4.4/core/index-hidden/).

<span id=".5rWB5byP5aSN5Yi277yIc3RyZWFtaW5nLXJlcGxpY2F0aW9u77yJ"></span>
## Streaming replication

Before MongoDB 4.4, secondary nodes had to send a read request to the primary node and wait for its response before they could retrieve a batch of Oplog data. With this method, retrieving Oplog data required a complete network round\-trip time (RTT) for each operation. However, starting from MongoDB 4.4, secondary nodes do not need to initiate requests; the primary node can continuously send Oplog to them. This Oplog synchronization method is called streaming replication. Streaming replication can reduce replication latency in high\-load and high\-latency network environments. You can enable streaming replication using the `oplogFetcherUsesExhaust` parameter. For more details, refer to [Streaming Replication](https://www.mongodb.com/docs/v4.4/core/replica-set-sync/#std-label-replica-set-streaming-replication).

<span id=".5ZCM5q2l5bu657Si5byV77yIc2ltdWx0YW5lb3VzLWluZGV4aW5n77yJ"></span>
## Simultaneous indexing

Before MongoDB 4.4, indexes could only be created on secondary nodes after index creation on the primary node was complete. Starting from MongoDB 4.4, primary and secondary nodes can perform index creation operations simultaneously. This significantly reduces primary\-secondary latency events and ensures that secondary nodes can still access the latest data even during index creation. For more details, refer to [Index Builds in Replicated Environments](https://www.mongodb.com/docs/v4.4/core/index-creation/#std-label-index-operations-replicated-build).

<span id=".6ZWc5YOP6K-75Y-W77yIbWlycm9yZWQtcmVhZHPvvIk="></span>
## Mirrored reads

MongoDB 4.4 introduces the Mirrored Reads feature, where the primary node replicates a certain proportion of read traffic to secondary nodes for execution, helping them pre\-warm their cache. This is not a "Fire and Forgot" behavior; it does not substantially affect the primary node's performance, but it does increase the load on secondary nodes to some extent. You can set the traffic replication ratio using the `samplingRate` and `maxTimeMS` parameters. For more details, refer to [mirrorReads](https://docs.mongodb.com/master/reference/parameters/#param.mirrorReads).

<span id=".5Y-v5oGi5aSN55qE5YWo6YeP5ZCM5q2l77yIcmVzdW1hYmxlLWluaXRpYWwtc3luY--8iQ=="></span>
## Resumable initial sync

In versions prior to MongoDB 4.4, if a secondary node's initial sync was interrupted by network fluctuations, it had to restart the entire process. This severely impacted operations, especially with large data volumes. However, starting with MongoDB 4.4, it supports resuming synchronization from the point of interruption. If it cannot successfully reconnect after an interruption, the system reselects an available sync source to perform a new initial sync. You can set the timeout period for this process using the `replication.initialSyncTransientErrorRetryPeriodSeconds` parameter. For more details about this parameter, refer to [MongoDB Server Parameters](https://www.mongodb.com/docs/upcoming/reference/parameters/#mongodb-parameter-param.initialSyncTransientErrorRetryPeriodSeconds).

<span id=".b3Bsb2ct5pyA5bCP5L-d55WZ5pe26Ze077yIbWluaW11bS1vcGxvZy1yZXRlbnRpb24tcGVyaW9k77yJ"></span>
## Minimum oplog retention period

The oplog in MongoDB records all data change details and can be used for data synchronization, incremental backups, data migration, data subscription, and other scenarios. Starting from MongoDB 4.4, define the minimum oplog retention period using the `storage.oplogMinRetentionHours` parameter in the mongod configuration file, or modify it online with the `oplogMinRetentionHours` command. For more details, refer to [Minimum Oplog Retention Period](https://www.mongodb.com/docs/v4.4/release-notes/4.4/#minimum-oplog-retention-period).

<span id=".5aSa6KGo6IGU5ZCI5aKe5by677yIdW5pb24tYWxs77yJ"></span>
## Union all

MongoDB 4.4 supported adding the `$unionWith` stage in multi\-table union queries to aggregate data from two collections into a single result. `$unionWith stage` supports sharded collections. Use multiple `$unionWith stage`s in an Aggregate Pipeline to aggregate data from multiple collections. For more details, refer to [$unionWith](https://www.mongodb.com/docs/v4.4/reference/operator/aggregation/unionWith/#mongodb-pipeline-pipe.-unionWith).

<span id=".6Ieq5a6a5LmJLWFnZ3JlZ2F0aW9uLeihqOi-vuW8j--8iGN1c3RvbS1hZ2dyZWdhdGlvbi1leHByZXNzaW9uc--8iQ=="></span>
## Custom aggregation expressions

MongoDB 4.4 introduces two new operators: `$accumulator` and `$function`. With these two operators, you can write custom JavaScript scripts using aggregation to achieve more complex query capabilities. For more details, refer to [Map-Reduce to Aggregation Pipeline](https://www.mongodb.com/docs/v4.4/reference/map-reduce-to-aggregation-pipeline/).
