---
title: "Overview of new features of MongoDB 7.0"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/mongodb-7-features"
---

This topic introduces the main new features of MongoDB version 7.0.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details of MongoDB 7.0 features, refer to <a href="https://www.mongodb.com/docs/manual/release-notes/7.0/">MongoDB 7.0 release notes</a>.</div>


<span id="LQEVEltb"></span>
## Enhanced observability and diagnostic capabilities

<span id="ZukifJkD"></span>
### Improvements to slow query logs


* Slow query log messages ([log messages for slow queries](https://www.mongodb.com/docs/v7.0/reference/log-messages/#std-label-log-message-slow-ops)) now include the [Cache refresh times](https://www.mongodb.com/docs/v7.0/reference/log-messages/#std-label-log-messages-cache-refresh-times) metric, which provides detailed information on the time spent refreshing the cache during query execution.

* The slow query log messages have added the `queryFramework` field to identify the engine type executing the query.

* Optimized concurrent commit monitoring: `totalOplogSlotDurationMicros` accurately measures the delay between commit operations and timestamp acquisition, reflecting the coordination efficiency of parallel writes.

* The `totalOplogSlotDurationMicros` field in slow query log messages indicates the time taken to acquire a commit timestamp from a write operation, specifically the duration between the storage engine's write commit and the actual commit, thereby optimizing concurrent commit monitoring.


<span id="MofjAWDv"></span>
### Expanded serverStatus output

The serverStatus output now includes key metrics related to plan cache (planCache), query analyzers (queryAnalyzers), and others. For more details, refer to [serverStatus Output Change](https://www.mongodb.com/docs/manual/release-notes/7.0/#serverstatus-output-change).

<span id="XLdRp2Zv"></span>
### Enhancements to the currentOp command

The currentOp now includes metrics such as `admissionPriority` (operation priority), `collUuid` (collection identifier), `startTime` (operation start time), and sampled data metrics (such as `samplesPerSecond`). For more details, refer to [currentOp Metrics](https://www.mongodb.com/docs/manual/release-notes/7.0/#currentop-metrics).

<span id="3HElgfae"></span>
### Enhancements to $currentOp aggregation pipeline

New metrics have been added that are fully consistent with the [currentOp](https://bytedance.larkoffice.com/docx/NPc8dCNSQoOxmQxrV9jc9hjWnHW#share-E3AsdxYWJom3qSxe3IpcImLpnLh) command (such as `collUuid`, `startTime`, and sampled metrics), facilitating real\-time analysis of operation status within the aggregation framework. For more details, refer to [$currentOp (aggregation) Metrics](https://www.mongodb.com/docs/manual/release-notes/7.0/#-currentop--aggregation--metrics).

<span id="5fj7fMG0"></span>
## Enhancements to sharding cluster O&M

<span id="sLsXeXQJ"></span>
### Sharding metadata diagnostics

MongoDB 7.0 added support for the `checkMetadataConsistency` command, which can be used to check for inconsistencies in sharding metadata at the cluster, database, and collection levels. If errors occur during the upgrade process or if manual intervention damages the cluster directory, this will lead to inconsistent sharding metadata. It is recommended to add this inspection item to database O&M tasks to detect metadata inconsistency risks early. For more details, refer to [checkMetadataConsistency](https://www.mongodb.com/docs/manual/reference/command/checkMetadataConsistency/#mongodb-dbcommand-dbcmd.checkMetadataConsistency).

<span id="LZvDLNPv"></span>
### Refined data migration monitoring

Starting with MongoDB 7.0, more data migration\-related metrics have been added (such as `shardingStatistics.countDonorMoveChunkCommitted`, and `shardingStatistics.totalDonorMoveChunkTimeMillis`), enabling more granular monitoring of the data migration process. For more details, refer to [Sharding Metadata Diagnostics](https://www.mongodb.com/docs/manual/release-notes/7.0/#sharding-metadata-diagnostics).

<span id="eT6y7lLV"></span>
### Support for AutoMerger

Starting with MongoDB 7.0, the AutoMerger ([AutoMerger](https://www.mongodb.com/docs/manual/core/automerger-concept/#std-label-automerger-concept)) has been enabled in the load balancer, which can automatically merge qualifying chunks. Additionally, MongoDB 7.0 supports configuring the AutoMerger using the `autoMergerIntervalSecs` and `autoMergerThrottlingMS` parameters to balance data and improve performance.

<span id="amlZxzob"></span>
### Balancer throttling

MongoDB 7.0 introduces the [balancerMigrationsThrottlingMs](https://www.mongodb.com/zh-cn/docs/v7.0/reference/parameters/#mongodb-parameter-param.balancerMigrationsThrottlingMs) parameter to limit the balancing rate of the load balancer.

<span id="fm3TSw03"></span>
## Security and permission management

<span id="3vbaoF6s"></span>
### Queryable encryption

MongoDB 7.0 optimizes Queryable encryption, building upon the 6.0 preview release to launch its generally available (GA) version. For more details, refer to [Queryable Encryption](https://www.mongodb.com/docs/v7.0/core/queryable-encryption/#std-label-qe-manual-feature-qe).

<span id="AwpL6pWW"></span>
### Security compliance

MongoDB 7.0 adds support for KMIP 1.0 and 1.1, as well as OpenSSL and FIPS.

<span id="xrnXni2x"></span>
### New system variables

MongoDB 7.0 now supports the [USER_ROLES](https://www.mongodb.com/zh-cn/docs/v7.0/reference/aggregation-variables/#mongodb-variable-variable.USER_ROLES) system variable, which returns the current user's role information.

<span id="3YhaKz9f"></span>
## More optimizations

<span id="DWQvY5sm"></span>
### Indexing and query optimization

MongoDB 7.0 supports creating compound wildcard indexes. The core advantage of compound wildcard indexes is their ability to cover many potential queries with a single wildcard index, significantly reducing the number of indexes, optimizing storage and write performance, and addressing the challenge of maintaining a large number of independent indexes. For more information, refer to [Compound wildcard indexes](https://www.mongodb.com/docs/v7.0/core/indexes/index-types/index-wildcard/index-wildcard-compound/#std-label-wildcard-index-compound).

<span id="ARNMC3Sm"></span>
### Change stream enhancements

MongoDB 7.0 introduces the `$changeStreamSplitLargeEvent` operator, which can be used to split large change events exceeding 16 MB into smaller fragments. For more details, refer to [Large Change Stream Events](https://www.mongodb.com/docs/manual/release-notes/7.0/#large-change-stream-events).

<span id="YWQjJ4TX"></span>
### New parameters

MongoDB 7.0 introduces new query analyzer parameters (including [queryAnalysisWriterIntervalSecs](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.queryAnalysisWriterIntervalSecs) and [queryAnalysisSampleExpirationSecs](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.queryAnalysisSampleExpirationSecs)), shard key analysis parameters (including [analyzeShardKeyNumRanges](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.analyzeShardKeyNumRanges) and [analyzeShardKeyMonotonicityCorrelationCoefficientThreshold](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.analyzeShardKeyMonotonicityCorrelationCoefficientThreshold)), and other key parameters (such as [enableDetailedConnectionHealthMetricLogLines](https://www.mongodb.com/docs/v7.0/reference/parameters/#mongodb-parameter-param.enableDetailedConnectionHealthMetricLogLines), and [oidcIdentityProviders](https://www.mongodb.com/docs/manual/reference/parameters/#mongodb-parameter-param.oidcIdentityProviders)), to meet diverse configuration requirements for scenarios such as query analysis and shard key analysis.

<span id="SiuEqRkW"></span>
### Aggregation operators

MongoDB 7.0 adds support for using the [$median](https://www.mongodb.com/docs/manual/reference/operator/aggregation/median/#mongodb-group-grp.-median) and [$percentile](https://www.mongodb.com/docs/manual/reference/operator/aggregation/percentile/#mongodb-group-grp.-percentile) operators in aggregation operations, which can be used respectively to return the approximate median (equivalent to the 50th percentile) and specified percentiles. Additionally, the [$dateToString](https://www.mongodb.com/docs/manual/reference/operator/aggregation/dateToString/#mongodb-expression-exp.-dateToString) operator now supports two month formats: `%b` and `%B`.

<span id="9e5MSTOJ"></span>
### Time series collection optimization

MongoDB 7.0 removes time series restrictions on DELETE\-related commands (including [delete](https://www.mongodb.com/docs/manual/reference/command/delete/#mongodb-dbcommand-dbcmd.delete), [deleteOne()](https://www.mongodb.com/docs/manual/reference/method/db.collection.deleteOne/#mongodb-method-db.collection.deleteOne), [deleteMany()](https://www.mongodb.com/docs/manual/reference/method/db.collection.deleteMany/#mongodb-method-db.collection.deleteMany), [Bulk.find.delete()](https://www.mongodb.com/docs/manual/reference/method/Bulk.find.delete/#mongodb-method-Bulk.find.delete), and [Bulk.find.deleteOne()](https://www.mongodb.com/docs/manual/reference/method/Bulk.find.deleteOne/#mongodb-method-Bulk.find.deleteOne)). For more details, refer to [Timeseries limitations](https://www.mongodb.com/docs/v7.0/core/timeseries/timeseries-limitations/#std-label-timeseries-limitations-deletes).
