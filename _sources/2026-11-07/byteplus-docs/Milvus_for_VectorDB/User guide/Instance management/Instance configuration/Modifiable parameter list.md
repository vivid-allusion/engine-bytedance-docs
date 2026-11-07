---
title: "Modifiable parameter list"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Modifiable_parameter_list"
---

This topic describes the modifiable parameters provided by Milvus for VectorDB, including default values, types, value ranges, descriptions, and units.

## Precautions

Only Dedicated instances support modifying instance parameters.

## Modifiable parameters

|**Parameter** |**Module** |**Default value** |**Unit** |**Type** |**Value range** |**Description** |Restart scope |
|---|---|---|---|---|---|---|---|
|common.enabledJSONShredding |common |false |\- |boolean |[true\|false] |Enable JSON key statistics for Sealed Segment.<br><br>> **tip**<br><br><br>> This parameter only supports version 2.6 instances.<br> |no restart required |
|common.gracefulTime |common |5000 |Millisecond |integer |[0\-2147483647] |Time lag tolerated for data visibility under the bounded consistency policy. |no restart required |
|common.usingJSONShreddingForQuery |common |true |\- |boolean |[true\|false] |Use JSON statistics for query.<br><br>> **tip**<br><br><br>> This parameter only supports version 2.6 instances.<br> |no restart required |
|dataCoord.compaction.clustering.autoEnable |dataCoord |false |\- |boolean |[true\|false] |Specifies whether to enable automatic cluster compression. After enabled, it triggers cluster compression periodically. |no restart required |
|dataCoord.compaction.clustering.enable |dataCoord |false |\- |boolean |[true\|false] |Specifies whether to enable cluster compression. |no restart required |
|dataCoord.compaction.dropTolerance |dataCoord |86400 |Second |integer |[1\-2147483647] |Tolerant time for compaction drop.<br><br> |no restart required |
|dataCoord.import.taskRetention |dataCoord |10800 |Second |integer |[0\-2147483647] |Sets the task expiration time. Task records exceeding the threshold will be cleared. |no restart required |
|dataCoord.segment.diskSegmentMaxSize |dataCoord |2048 |MB |integer |[1\-2147483647] |Maximum capacity of the disk type index segment. |no restart required |
|dataCoord.segment.maxIdleTime |dataCoord |600 |Second |integer |[0\-2147483647] |Sets the maximum idle time for the Segment. Seal triggers when the Segment’s idle time exceeds the set value; the Segment should be larger than `datacoord.segment.minSizeFromIdleToSealed`. |Metadata service |
|dataCoord.segment.maxLife |dataCoord |86400 |Second |integer |[0\-2147483647] |Sets the maximum lifetime of a segment. When exceeded, it triggers a seal. |Metadata service |
|dataCoord.segment.maxSize |dataCoord/dataNode |1024 |MB |integer |[1\-2147483647] |Sets the maximum capacity of the segment. |Metadata service |
|dataCoord.segment.minSizeFromIdleToSealed |dataCoord |16 |MB |integer |[0\-2147483647] |Sets the minimum free seal capacity for the segment. |Metadata service |
|dataCoord.segment.sealProportion |dataCoord |0.12 |\- |double |[0\-1] |Sets the segment seal factor, which together with `dataCoord.segment.maxSize` determines when to seal a segment. |Mix Coordinator, Query node, Streaming node |
|dataCoord.slot.l0DeleteCompactionUsage |dataCoord |8 |\- |integer |[8\-128] |Number of slots used by the L0 compact task. |no restart required |
|dataCoord.slot.mixCompactionUsage |dataCoord |8 |\- |integer |[8\-128] |Number of slots used by mix compact tasks. |No restart required |
|dataCoord.slot.statsTaskSlotUsage |dataCoord |8 |\- |integer |[8\-128] |Number of slots used by the stats task. |no restart required |
|dataNode.segment.deleteBufBytes |dataNode |16777216 |B |integer |[4194304\-1073741824] |Sets the Binlog deletion buffer size. If the value is exceeded, data will be synchronized to TOS. |no restart required |
|dataNode.segment.insertBufSize |dataNode |16777216 |B |integer |[4194304\-1073741824] |Sets the size of the Binlog write buffer. If the value is exceeded, data will be synchronized to TOS. |No restart required |
|indexNode.scheduler.buildParallel |indexNode |1 |\- |integer |[1\-2147483647] |Sets the concurrency for the index. |Data node |
|metastore.maxEtcdTxnNum |metastore |64 |\- |integer |[1\-2147483647] |Maximum operations in a single ETCD transaction.<br><br>> **tip**<br><br><br>> This parameter only supports instances of version 2.5.25 or later.<br> |no restart required |
|metastore.paginationSize |metastore |100000 |\- |integer |[1\-2147483647] |Number of results returned in single metadata storage query. |Metadata service |
|proxy.maxTaskNum |proxy |1024 |\- |integer |[1\-2147483647] |Maximum number of tasks allowed in the proxy task queue. |Proxy |
|proxy.maxVarCharLength |proxy |65535 |\- |integer |[1\-2147483647] |Maximum number of characters for varchar fields. |Proxy |
|proxy.maxVectorFieldNum |proxy |4 |\- |integer |[1\-2147483647] |Maximum number of vector fields in a single collection. |no restart required |
|proxy.timeTickInterval |proxy |200 |Millisecond |integer |[10\-2147483647] |Sets the interval for synchronizing TickTime to the root coordinator. |Proxy, Mix Coordinator, Streaming Node |
|queryNode.cache.warmup |queryNode |disable |\- |enum |[disable\|sync\|async] |Specifies whether to enable chunk cache preheating. Preheating method:<br><br><br>* `disable`: no preheating. Data is loaded only when used.<br><br>* `sync`: synchronous preheating.<br><br>* `async`: asynchronous preheating. |Query Node, Streaming Node |
|queryNode.mmap.scalarField |queryNode |false |\- |boolean |[true\|false] |Whether to turn on mmap for scalar index. |Query Node, Streaming Node |
|queryNode.mmap.scalarIndex |queryNode |false |\- |boolean |[true\|false] |Whether to turn on mmap for scalar index. |Query Node, Streaming Node |
|queryNode.mmap.vectorField |queryNode |false |\- |boolean |[true\|false] |whether to turn on mmap for vector fields. |Query Node, Streaming Node |
|queryNode.scheduler.maxReadConcurrentRatio |queryNode |1.0 |\- |double |[1\-10000] |Concurrency of read tasks (search core queries): maximum concurrency = `hardware.GetCPUNum` \* `maxReadConcurrentRatio`, limited to [1, `hardware.GetCPUNum` \* 100].<br><br> |Query Node, Streaming Node |
|rootCoord.dmlChannelNum |rootCoord |16 |\- |integer |[1\-64] |Sets the maximum number of DML physical channels. |Mix Coordinator, Streaming Node |
|streaming.walBalancer.operationTimeout |streaming |30 |Second |integer |[0\-2147483647] |WAL Cloud Load Balancer operation timeout; the action will be canceled if it times out.<br><br>> **tip**<br><br><br>> This parameter supports only version 2.6 instances.<br> |no restart required |
|streaming.walRecovery.gracefulCloseTimeout |streaming |3 |Second |integer |[0\-2147483647] |WAL recovery graceful shutdown timeout. During WAL shutdown, the WAL recovery module attempts to persist recovery information to speed up the next recovery. If persistence times out, the WAL recovery module shuts down immediately. |no restart required |
