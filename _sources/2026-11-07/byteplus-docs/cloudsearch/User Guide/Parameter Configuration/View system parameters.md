---
title: "View system parameters"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/View_system_parameters"
---

This article introduces the system parameters supported by different versions of instances.

<span id="79e4b285"></span>
## Procedure


1. Log on to the [Cloud Search console](https://console.byteplus.com/es).

2. In the top navigation bar, select the target project and region.

3. On the **Instances** page, click the target instance name to enter the instance details page.

4. In the left navigation bar, select **Instance management \> Parameter management**, then view system parameters.

   
   <Tabs>
   <Tab zoneid="lgcsEND2MB" title="OpenSearch 3.3.0">
   <TabTitle>OpenSearch 3.3.0</TabTitle>
   
   
   |**Category** |**Parameter name** |**Description** |
   |---|---|---|
   |Index management |ActionAutoCreateIndex |whether to create the index automatically. default value is `true`, with the following value selection description:<br><br><br>* true: create the index automatically.<br><br>* false: do not create the index automatically. |
   ||ActionDestructiveRequiresName |Whether deleting an index requires specifying the full index name. Default value is `false`, value selection description as follows:<br><br><br>* true: requires specifying the full index name.<br><br>* false: does not require specifying the full index name. |
   ||ActionIndicesCloseEnable |Whether turning off the index is supported. default value is `true`, with the following value selection description:<br><br><br>* true: supports turning off the index.<br><br>* false: does not support turning off the index. |
   ||IndexingPressureMemoryLimit |Maximum JVM memory size available for write requests. The node will reject requests once the limit is reached. Value range: [1%, 100%]. |
   ||IndicesMemoryIndexBufferSize |Accept percentage. The default value is 10%, which means 10% of the total heap memory allocated to the node is used as the index buffer when writing shards. The value range is [1%, 100%]. |
   |cluster management |ClusterPublishTimeout |Cluster release status timeout, a positive integer in seconds. Default value is `30s`.<br><br>This is an expert\-level setting and should be configured with caution. |
   ||FollowerFaultDetectionTimeout |Data node heartbeat timeout, a positive integer in seconds. Default value is `30s`.<br><br>This is an expert\-level setting and should be configured with caution. |
   ||FollowerLagTimeout |When the node receives metadata, it tolerates a maximum time during which it cannot be removed. The value is a positive integer in seconds, with a default of `90s`.<br><br>This is an expert\-level setting; configure it carefully. |
   ||LeaderFaultDetectionTimeout |Active node heartbeat timeout, a positive integer in seconds; default value is `30s`<br><br>This is an expert\-level configuration; set with caution. |
   |HttpCors |HttpCorsAllowCredentials |Whether to return the header `Access-Control-Allow-Credentials` for HttpCors. Default value is `false`, value selection description as follows:<br><br><br>* true: returns the header `Access-Control-Allow-Credentials`.<br><br>* false: does not return the header `Access-Control-Allow-Credentials`. |
   ||HttpCorsAllowHeaders |Allowed Headers for HttpCors, separated by English commas. Default value: `X-Requested-With, Content-Type, Content-Length`. |
   ||HttpCorsAllowMethods |Allowed HTTP methods for HttpCors, separated by commas. Default value: OPTIONS, HEAD, GET, POST, PUT, DELETE. |
   ||HttpCorsAllowOrigin |Source addresses allowed for HttpCors, configured as `http://host:port`. supports regular expressions. |
   ||HttpCorsEnabled |Whether to allow cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: allow cross\-origin access.<br><br>* false: do not allow cross\-origin access. |
   ||HttpCorsMaxAge |Default cache time for browser preflight request results, configurable within [1, 1728000] seconds.<br><br>Default value is `1728000` (20 days). |
   |HTTP |HttpMaxContentLength |Maximum size of HTTP request body, expressed as a positive integer in MB.<br><br>Default value is `100`. |
   ||HttpMaxHeaderSize |maximum HTTP request header size, value is a positive integer in KB.<br><br>default value is `8`. |
   ||HttpMaxInitialLineLength |Maximum HTTP request line size, positive integer in KB<br><br>Default value is `4` |
   |Cache |IndicesFielddataCacheSize |Cache ratio of field data in Java heap space, range [1%, 100%], default 100%. |
   ||IndicesQueriesCacheSize |Cache size during the query phase. The value can be a percentage or a specific value, within the range<br><br>[512 MB, 2048 MB] or [5%, 20%].<br><br>Default value is `10%`. |
   ||IndicesRequestsCacheSize |Request and response result cache ratio in the Java heap space, with a value range of [1%, 100%], default value is 1%. |
   |Query |IndicesQueryBoolMaxClauseCount |The maximum number of clauses allowed in a Lucene BooleanQuery ranges from 16 to 100,000, with a default value of 1024. |
   ||SearchAllowExpensiveQueries |Allow queries that consume high resources, including script queries, Join queries, regex queries, wildcard queries, fuzzy queries, etc. default value is `true`, with the following value selection description:<br><br><br>* true: allowed<br><br>* false: not allowed |
   |ThreadPool |ThreadPoolForceMergeQueueSize |Request queue size for force\-merge operations, with a value range of \-1 to 10000. Setting to 0 or \-1 disables this queue.<br><br>Default value is `-1`. |
   ||ThreadPoolWriteQueueSize |Request wait queue size for index, delete, update, and bulk operations on a single document. Value range: \-1 to 10,000. Setting to `0` or `-1` disables this queue.<br><br>Default value is 1,000. |
   |Reindex |ReindexRemoteWhitelist |Add remote cluster access address whitelist, supporting host and port combinations, separated by commas for multiple host configurations, e.g. `node1:9200,127.0.0.1:9200`. |
   |Shard allocation |ClusterRoutingAllocationNodeConcurrentIncomingRecoveries |Number of incoming shard recoveries allowed to occur simultaneously on one node. Incoming recovery refers to the recovery operation assigned to the target shard (usually a replica shard, unless the shard is relocating) on this node. Default value is `2`. |
   ||ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries |Number of outgoing shard recoveries allowed simultaneously on one node. Outgoing recovery refers to recovery operations assigned to this node on the source shard (usually the active shard unless the shard is migrating). Default value is `2`. |
   ||ClusterRoutingAllocationNodeConcurrentRecoveries |Set `ClusterRoutingAllocationNodeConcurrentIncomingRecoveries` and `ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries` parameters simultaneously. This parameter only takes effect if the above parameters are not configured. Default value is `2`. |
   ||ClusterRoutingAllocationNodeInitialPrimariesRecoveries |Replica shard recovery occurs over the network, while recovery of primary shards that are unassigned after node restart uses data on the local disk. This recovery usually completes quickly, allowing more initial primary shard recoveries to run in parallel on each node. Default value is `4`. |
   |Index recovery |IndicesRecoveryMaxBytesPerSec |Limit total inbound and outbound recovery traffic per node. This limit applies to both inter\-node recoveries and snapshot recoveries. Default value is `40 MB`. |
   
   
   
   </Tab>
   <Tab zoneid="sinvWGLmnl" title="OpenSearch 2.9.0">
   <TabTitle>OpenSearch 2.9.0</TabTitle>
   
   
   |**Category** |**Parameter name** |**Description** |
   |---|---|---|
   |Index management |ActionAutoCreateIndex |whether to create the index automatically. default value is `true`, with the following value selection description:<br><br><br>* true: create the index automatically.<br><br>* false: do not create the index automatically. |
   ||ActionDestructiveRequiresName |Deleting an index requires specifying the full index name. Default value is `false`, value selection description as follows:<br><br><br>* true: requires specifying the full index name.<br><br>* false: does not require specifying the full index name. |
   ||ActionIndicesCloseEnable |whether to support turning off the index. default value is `true`, with the following value selection description:<br><br><br>* true: supports turning off the index.<br><br>* false: does not support turning off the index. |
   |Cluster management |ClusterPublishTimeout |Cluster release status timeout in seconds. The value must be a positive integer. Default is `30s`.<br><br>This is an expert\-level configuration; adjust with caution. |
   ||FollowerFaultDetectionTimeout |Data node heartbeat timeout, value must be a positive integer in seconds, default is `30s`.<br><br>This is an expert\-level configuration; set it carefully. |
   ||FollowerLagTimeout |Maximum tolerated time in seconds for a node to accept metadata without being removed. The value must be a positive integer. Default is `90s`.<br><br>This is an expert\-level configuration; adjust with caution. |
   ||LeaderFaultDetectionTimeout |Master node heartbeat timeout, value is a positive integer in seconds, default is `30s`.<br><br>This is an expert\-level configuration. Adjust with caution. |
   |HttpCors |HttpCorsAllowCredentials |Whether to return the header `Access-Control-Allow-Credentials` for cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: returns the header `Access-Control-Allow-Credentials`.<br><br>* false: does not return the header `Access-Control-Allow-Credentials`. |
   ||HttpCorsAllowHeaders |Allowed Headers for HttpCors, separated by English commas. Default value: `X-Requested-With, Content-Type, Content-Length`. |
   ||HttpCorsAllowMethods |Allowed HTTP methods for HttpCors, separated by English commas. Default value: OPTIONS, HEAD, GET, POST, PUT, DELETE. |
   ||HttpCorsAllowOrigin |HttpCors allowed source addresses, configuration format: `http://host:port`. supports regular expressions. |
   ||HttpCorsEnabled |Whether to allow cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: allow cross\-origin access.<br><br>* false: do not allow cross\-origin access. |
   ||HttpCorsMaxAge |Default cache duration for the browser preflight request response, configurable from 1 to 1,728,000 seconds.<br><br>Default value is `1728000` (20 days). |
   |HTTP |HttpMaxContentLength |Maximum HTTP request body size, set as a positive integer in MB.<br><br>Default value is `100`. |
   ||HttpMaxHeaderSize |Maximum limit for HTTP request headers, expressed as a positive integer in KB.<br><br>Default value is `8`. |
   ||HttpMaxInitialLineLength |Maximum limit for HTTP request line, in KB, must be a positive integer.<br><br>Default value is `4`. |
   |Cache |IndicesFielddataCacheSize |The cache proportion of field data in the Java heap space ranges from 1% to 100%, with a default value of 100%. |
   ||IndicesQueriesCacheSize |Cache size during the query phase. The value can be a percentage or a specific value, with a range of<br><br>[512 MB, 2048 MB] or [5%, 20%].<br><br>Default value is `10%`. |
   ||IndicesRequestsCacheSize |Cache ratio of request response results in Java heap space, ranging from [1%, 100%], default is 1%. |
   |Query |IndicesQueryBoolMaxClauseCount |Maximum number of subclauses allowed in Lucene BooleanQuery, range [16, 100000], default 1024 |
   ||SearchAllowExpensiveQueries |Allow queries with high resource consumption, including script queries, join queries, regex queries, wildcard queries, and fuzzy queries. default value is `true`, with the following value selection description:<br><br><br>* true: Allowed<br><br>* false: Not allowed |
   |ThreadPool |ThreadPoolForceMergeQueueSize |Request queue size for force\-merge operations, ranging from \-1 to 10000. Setting to 0 or \-1 disables this queue.<br><br>Default value is `-1`. |
   ||ThreadPoolWriteQueueSize |Request wait queue size for index, delete, update, and bulk operations on a single document. Value range: \-1 to 10000. Setting to `0` or `-1` disables this queue.<br><br>Default value is 1000. |
   |Reindex |ReindexRemoteWhitelist |Add remote cluster access address whitelist, supporting host and port combinations separated by commas, e.g., `node1:9200,127.0.0.1:9200`. |
   |Shard allocation |ClusterRoutingAllocationNodeConcurrentIncomingRecoveries |Number of incoming shard recoveries allowed simultaneously on one node. Incoming recovery refers to the recovery operation of the target shard (usually a replica shard, unless the shard is relocating) assigned to that node. Default value is `2`. |
   ||ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries |Allow the number of outgoing shard recoveries occurring simultaneously on a node. Outgoing recovery refers to the recovery operation of a source shard (usually the active shard unless the shard is relocating) assigned to that node. Default value is `2`. |
   ||ClusterRoutingAllocationNodeConcurrentRecoveries |Set both `ClusterRoutingAllocationNodeConcurrentIncomingRecoveries` and `ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries` parameters simultaneously. This parameter only takes effect if the above parameters are not configured. Default value is `2`. |
   ||ClusterRoutingAllocationNodeInitialPrimariesRecoveries |Replica shard recovery uses the network, while recovery of unassigned primary shards after node restart uses local disk data. This recovery usually happens quickly, allowing more initial primary shard recoveries to run concurrently on each node. Default value is `4`. |
   |Index Recover |IndicesRecoveryMaxBytesPerSec |Limit the total inbound and outbound recovery traffic for each node. This limit applies to both inter\-node recovery and snapshot recovery. Default value is `40 MB`. |
   
   
   
   </Tab>
   <Tab zoneid="EPkNz6dKW4" title="Elasticsearch 7.10.2">
   <TabTitle>Elasticsearch 7.10.2</TabTitle>
   
   
   |**Category** |**Parameter name** |**Description** |
   |---|---|---|
   |<div style="text-align: center"><br>Index management</div><br> |ActionAutoCreateIndex |whether to create the index automatically. default value is `true`, with the following value selection description:<br><br><br>* true: create the index automatically.<br><br>* false: do not create the index automatically. |
   ||ActionDestructiveRequiresName |Whether deleting an index requires specifying the full index name. Default value is `false`, value selection description as follows:<br><br><br>* true: requires specifying the full index name.<br><br>* false: does not require specifying the full index name. |
   ||ActionIndicesCloseEnable |Whether to support turning off the index. default value is `true`, with the following value selection description:<br><br><br>* true: supports turning off the index.<br><br>* false: does not support turning off the index. |
   ||IndexingPressureMemoryLimit |Set the maximum JVM memory size available for requests. The node will reject requests when the limit is reached. Value range is [1%, 100%]. |
   ||IndicesMemoryIndexBufferSize |Accepts percentage. Default value is 10%, which means 10% of the total heap memory allocated to the node is used as the index buffer during shard writing. Value range is [1%, 100%]. |
   |Cluster management |ClusterPublishTimeout |cluster deployment timeout, a positive integer in seconds, default value is `30`.<br><br>this is an expert\-level configuration; set carefully. |
   ||FollowerFaultDetectionTimeout |Data node heartbeat timeout, a positive integer in seconds, default `30`.<br><br>This is an expert\-level configuration. Set it carefully. |
   ||FollowerLagTimeout |maximum tolerance time in seconds for node metadata acceptance without removal, positive integer, default is `90`.<br><br>this is an expert\-level setting; configure carefully. |
   ||LeaderFaultDetectionTimeout |Master node heartbeat timeout, value must be a positive integer in seconds, default is `30`.<br><br>This is an expert\-level configuration; set it carefully. |
   |HttpCors |HttpCorsAllowCredentials |Whether to return the header `Access-Control-Allow-Credentials` for cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: returns the header `Access-Control-Allow-Credentials`.<br><br>* false: does not return the header `Access-Control-Allow-Credentials`. |
   ||HttpCorsAllowHeaders |Allowed Headers for HttpCors, separated by English commas. Default value: `X-Requested-With, Content-Type, Content-Length`. |
   ||HttpCorsAllowMethods |Allowed HTTP methods for HttpCors, separated by English commas. Default value: `OPTIONS, HEAD, GET, POST, PUT, DELETE`. |
   ||HttpCorsAllowOrigin |source addresses allowed for HttpCors, configured as `http://host:port`. supports regular expressions. |
   ||HttpCorsEnabled |Whether to allow cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: allow cross\-origin access.<br><br>* false: do not allow cross\-origin access. |
   ||HttpCorsMaxAge |Default cache duration for the browser preflight request response, configurable between [1, 1728000] seconds.<br><br>Default value is `1728000` (20 days). |
   |HTTP |HttpMaxContentLength |Maximum limit for the HTTP request body, a positive integer in MB.<br><br>Default value is `100`. |
   ||HttpMaxHeaderSize |Maximum HTTP request header size, a positive integer value in KB.<br><br>Default value is `8`. |
   ||HttpMaxInitialLineLength |Maximum limit for HTTP request line, set as a positive integer in KB.<br><br>default value is `4`. |
   |Cache |IndicesFielddataCacheSize |Cache ratio of fields data in Java heap space, with a value range of [1%, 100%], default value is `100%`. |
   ||IndicesQueriesCacheSize |Cache size during the query phase. The value can be a percentage or a specific value, with a range of<br><br>[512 MB, 2048 MB] or [5%, 20%].<br><br>Default value is `10%`. |
   ||IndicesRequestsCacheSize |The cache proportion of the request response result in the Java heap space, with a value range of [1%, 100%], default is `1%`. |
   |Query |IndicesQueryBoolMaxClauseCount |The maximum number of clauses Lucene BooleanQuery can contain, range [16, 100000], default `1024`. |
   ||SearchAllowExpensiveQueries |Allow resource\-intensive queries including scripted queries, join queries, regex queries, wildcard queries, and fuzzy queries. default value is `true`, with the following value selection description:<br><br><br>* true: allowed<br><br>* false: not allowed |
   |ThreadPool |ThreadPoolForceMergeQueueSize |Request queue size for force\-merge operations, range is \-1 to 10000. Setting to `0` or `-1` disables this queue.<br><br>Default value is \-1. |
   ||ThreadPoolSearchSize |ThreadPool size used for query requests. Default value is calculated automatically, usually about 1.5 times the number of CPU cores. |
   ||ThreadPoolWriteQueueSize |Request wait queue size for index, delete, update, and bulk operations on a single document. Value range: \-1~10000. Setting to `0` or `-1` disables this queue.<br><br>default value is `1000`. |
   |Reindex |ReindexRemoteWhitelist |Add a whitelist of access addresses for remote clusters. Supports host and port combinations, separated by commas for multiple hosts, e.g., `node1:9200,127.0.0.1:9200`. |
   |shard allocation |ClusterRoutingAllocationNodeConcurrentIncomingRecoveries |Number of incoming shard recoveries allowed simultaneously on a single node. Incoming recovery refers to a recovery operation assigned to the target shard (usually a replica shard unless the shard is relocating) on that node. Default value is `2`. |
   ||ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries |Allow the number of outgoing shard recoveries to occur simultaneously on a single node. Outgoing recovery refers to the recovery operations of source shards (usually active shards unless shards are relocating) assigned to that node. Default value is `2`. |
   ||ClusterRoutingAllocationNodeConcurrentRecoveries |Set both `ClusterRoutingAllocationNodeConcurrentIncomingRecoveries` and `ClusterRoutingAllocationNodeConcurrentOutgoingRecoveries` parameters simultaneously. This parameter takes effect only when the above parameters are not configured. The default value is `2`. |
   ||ClusterRoutingAllocationNodeInitialPrimariesRecoveries |Replica shard recovery happens over the network, whereas active shard recovery after a node restart uses data on the local disk. This recovery usually completes quickly, allowing more initial active shard recoveries to run in parallel on each node. Default value is `4`. |
   |Index recovery |IndicesRecoveryMaxBytesPerSec |Limit the total incoming and outgoing recovery traffic for each node. This limit applies to both inter\-node recovery and snapshot recovery. Default value is `40 MB`. |
   
   
   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="tip">Increasing the value of parameters under the <strong>shard allocation</strong> category may impact the cluster’s overall activity performance during shard movements, but it does not necessarily speed up shard movement completion significantly. Changing the default value is not recommended.</div>
   
   
   
   </Tab>
   <Tab zoneid="rOz17myWHv" title="Elasticsearch 6.7.1 and 6.8.23">
   <TabTitle>Elasticsearch 6.7.1 and 6.8.23</TabTitle>
   
   
   |**Category** |**Parameter name** |**Description** |
   |---|---|---|
   |Index management |ActionAutoCreateIndex |whether to create the index automatically. default value is `true`, with the following value selection description:<br><br><br>* true: create the index automatically.<br><br>* false: do not create the index automatically. |
   ||ActionDestructiveRequiresName |Whether deleting an index requires specifying the full index name. Default value is `false`, value selection description as follows:<br><br><br>* true: requires specifying the full index name.<br><br>* false: does not require specifying the full index name. |
   ||ActionIndicesCloseEnable |Whether the index supports turning off. default value is `true`, with the following value selection description:<br><br><br>* true: supports turning off the index.<br><br>* false: does not support turning off the index. |
   |HttpCors |HttpCorsAllowCredentials |Whether to return the header `Access-Control-Allow-Credentials` for cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: returns the header `Access-Control-Allow-Credentials`.<br><br>* false: does not return the header `Access-Control-Allow-Credentials`. |
   ||HttpCorsAllowHeaders |Allowed Headers for HttpCors, separated by English commas. Default value: `X-Requested-With, Content-Type, Content-Length`. |
   ||HttpCorsAllowMethods |Allowed HTTP methods for HttpCors, separated by English commas. Default value: `OPTIONS, HEAD, GET, POST, PUT, DELETE`. |
   ||HttpCorsAllowOrigin |allowed source addresses for HttpCors, configured in the format `http://host:port`. supports regular expressions. |
   ||HttpCorsEnabled |Whether to allow cross\-origin requests. Default value is `false`, value selection description as follows:<br><br><br>* true: allow cross\-origin access.<br><br>* false: do not allow cross\-origin access. |
   ||HttpCorsMaxAge |Default cache duration for the browser preflight request response, configurable within [1, 1728000] seconds.<br><br>Default value is `1728000` (20 days). |
   |HTTP |HttpMaxContentLength |Maximum limit for HTTP request body, must be a positive integer in MB.<br><br>Default value is `100`. |
   ||HttpMaxHeaderSize |Maximum limit for HTTP request header, valid positive integer in KB.<br><br>Default value is `8`. |
   ||HttpMaxInitialLineLength |The maximum limit for the HTTP request line, set as a positive integer, unit in KB.<br><br>Default value is `4`. |
   |Cache |IndicesFielddataCacheSize |The cached proportion of field data in the Java heap space ranges from [1%, 100%], with a default value of 100%. |
   ||IndicesQueriesCacheSize |Cache size during the query phase. The value can be a percentage or a specific number, with a range of<br><br>[512 MB, 2048 MB] or [5%, 20%].<br><br>Default value is 10%. |
   ||IndicesRequestsCacheSize |Cache ratio of request response in Java heap space, range [1%, 100%], default 1%. |
   |Query |*IndicesQueryBoolMaxClauseCount* |The maximum number of clauses Lucene BooleanQuery can contain ranges from 16 to 100,000, with a default value of 1,024. |
   |ThreadPool |ThreadPoolWriteQueueSize |Request wait queue size for index, delete, update, and bulk operations on a single document. Value range: \-1 to 10000. Setting to `0` or `-1` disables this queue.<br><br>Default value is `1000`. |
   ||ThreadPoolBulkQueueSize |Request wait queue size for bulk operations on a single document. Value range: \-1 to 10000. Setting to `0` or `-1` disables this queue.<br><br>Default value is 1000. |
   |Reindex |ReindexRemoteWhitelist |Add access address whitelist for remote clusters, supporting host and port combinations, separated by commas for multiple hosts, e.g., `node1:9200,127.0.0.1:9200`. |
   
   
   
   </Tab>
   </Tabs>
   


&nbsp;
