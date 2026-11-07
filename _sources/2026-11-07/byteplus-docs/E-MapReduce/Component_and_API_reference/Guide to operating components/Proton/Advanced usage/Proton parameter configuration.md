---
title: "Proton parameter configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_parameter_configuration"
---

<span id="_1-proton-sdk相关参数"></span>
## Proton SDK related parameters


|Parameter name |Parameter value |Note |
|---|---|---|
|fs.tos.http.maxConnections |1024 |Maximum number of connections in the TOS Client connection pool. Default is 1024. |
|fs.tos.http.idleConnectionTimeMills |60000 |Maximum idle HTTP connection time in the TOS Client connection pool. Default is 60000 (Unit: milliseconds). |
|fs.tos.http.connectTimeoutMills |10000 |Connection timeout for establishing a TOS Client connection. Default is 10000 (Unit: milliseconds). |
|fs.tos.http.readTimeoutMills |30000 |Read timeout for TOS Client. Default is 30000 (Unit: milliseconds). |
|fs.tos.http.writeTimeoutMills |30000 |Write timeout for TOS Client. Default is 30000 (Unit: milliseconds). |
|fs.tos.http.enableVerifySSL |true |Whether SSL certificate verification is enabled for TOS Client. Default is true. |
|fs.tos.http.dnsCacheTimeMinutes |0 |DNS cache validity period for TOS Client. A value less than or equal to 0 disables DNS cache. Default is 0. |
|fs.tos.request.max.retry.times |20 |Number of retry attempts for access errors, including rate limiting. Default value is 20. For large data volumes and low bandwidth, keep a relatively large parameter value. |
|fs.tos.client.disable.cache |false |Whether to disable the TOS client cache. Default is false. To ensure that each TOS access uses a completely new client, set this parameter to true to disable the cache. |
|fs.tos.multipart.size |5242880 |MPU part size. Default is 5242880 (Unit: bytes), that is, 5 MB. |
|fs.tos.multipart.threshold |10485760 |When uploading a file, MPU is used only if the file size exceeds this threshold; otherwise, PUT is used. Default is 10485760 (Unit: bytes), that is, 10 MB. |
|fs.tos.multipart.copy\-threshold |5242880 |When renaming a file, the [UploadPartCopy](https://www.volcengine.com/docs/6349/74872) API is used only if the file size exceeds this threshold; otherwise, the [CopyObject](https://www.volcengine.com/docs/6349/74859) API is used. Default is 5242880 (Unit: bytes), that is, 5 MB. |
|fs.tos.multipart.staging\-dir |${java.io.tmpdir}/multipart\-staging\-dir |When writing large files, local disk is used to store staging data for writing, which facilitates parallel data upload. Multiple directories can be configured to fully utilize the write capabilities of multiple data disks, for example: /data01/data, /data02/data. |
|fs.tos.multipart.staging\-buffer\-size |4096 |When writing files, staging data is temporarily stored in memory. If its size exceeds this value, it will be written to local disk. When increasing this value, make sure to adjust the total JVM memory size accordingly; otherwise, OOM issues may occur. |
|fs.tos.task.thread\-pool\-size |Number of CPUs on the current machine |Must be a positive integer. Indicates the number of threads in the thread pool for executing tasks (such as concurrent file copy). |
|fs.tos.multipart.thread\-pool\-size |Number of CPUs on the current machine |Must be a positive integer. Indicates the number of threads in the thread pool for asynchronous uploading of TOS data parts. |
|fs.tos.list.batch\-size |1000 |Must be a positive integer. Indicates the maximum number of objects returned per call to the TOS Client's list object function. Default is 1000. |
|fs.job.committer.summary.report.directory |None |When a value is set, the logs for each stage of the Job Committer's commit operation will be written to the specified directory for analysis and troubleshooting. Example: tos://test\-bucket/report\-dir |
|fs.job.committer.threads |Number of CPUs on the current machine |Requires a positive integer, indicating the thread pool size used to specify commit tasks |
|fs.tos.access\-key\-id |None |Access Key of the IAM user or role used when accessing TOS |
|fs.tos.secret\-access\-key |None |Secret Key of the IAM user or role used when accessing TOS |
|fs.tos.session\-token |None |Security Session Token of the temporary IAM role used when accessing TOS |
|fs.tos.bucket.%s.access\-key\-id |None |You can set a specific Access Key for a particular Bucket when accessing that Bucket. If not set, the default global configuration fs.tos.access\-key\-id will be used. |
|fs.tos.bucket.%s.secret\-access\-key |None |You can set a specific Secret Key for a particular Bucket when accessing that Bucket. If not set, the default global configuration fs.tos.secret\-access\-key will be used. |
|fs.tos.bucket.%s.session\-token |None |You can set a specific Secret Key for a particular Bucket when accessing that Bucket. If not set, the default global configuration fs.tos.session\-token will be used. |
|fs.tos.endpoint |None |The Endpoint where the Bucket to be accessed is located. Refer to [TOS Endpoint list](https://www.volcengine.com/docs/6349/107356). In the Volcengine EMR environment, a default value has already been set based on the Region where the EMR cluster is located, such as tos\-cn\-beijing.ivolces.com |
|fs.tos.region |None |The Region where the Bucket to be accessed is located. If not set, region information will be obtained from the configured fs.tos.endpoint, such as cn\-beijing. |
|fs.tos.bucket.%s.endpoint |None |Set the Endpoint for a specific Bucket. If not set, the value of fs.tos.endpoint will be used. This value is mainly applicable to cross\-Region access scenarios. For example, to copy data from an object in Region A to an object in Region B, you can set different Endpoints for different Buckets. |
|fs.tos.bucket.%s.region |None |Set the Region for a specific Bucket. If not set, the value of fs.tos.bucket.%s.endpoint will be used. |
|fs.tos.rename.enabled |false |Whether to enable the atomic rename capability for a single object in a TOS flat bucket. Before enabling, you must activate the RenameObject capability for the corresponding flat bucket. In the TOS hierarchical bucket scenario, atomic rename capability for files and directories is supported by default and is not affected by this parameter. |
|fs.tos.read\-ahead.buffer\-size |0 |Read\-ahead buffer size when reading data. If the parameter value is less than or equal to 0, read\-ahead is not enabled. The size should be adjusted based on business requirements. The recommended value is 64k. Setting it too large may lead to excessive read amplification. |
|fs.tos.user.agent.prefix |EMR |Custom User Agent prefix, which will ultimately appear in the access log when accessing TOS. It is mainly used to analyze the source of requests, facilitate issue troubleshooting and analysis, profile analysis, and more. You can set it according to actual business requirements, such as Serverless Spark. |


<span id="_2-有缓存参数"></span>
## Cached parameters

<span id="_2-1-client配置项"></span>
### **Client configuration items**


|**Parameter name** |**Parameter value** |**Note** |
|---|---|---|
|proton.metaserver.addresses |_ |MetaServer RPC address list. Multiple MetaServer addresses are separated by commas. For example: ip1:port1,ip2:port2 |
|proton.client.data.read\-timeout\-ms |60000 (Unit: milliseconds) |Data read timeout |
|proton.client.data.conn\-pool\-size |256 |TCP connection pool size for connecting to DataServer |
|proton.client.data.conn\-pool\-ttl |10000 (Unit: milliseconds) |Connection expiration time in the connection pool |
|proton.client.fallback.enabled |true |Allows fallback to other DataServers or underlying storage systems when read fails |
|proton.rpc.client.timeout\-ms |2147483647 (Unit: milliseconds) |RPC timeout duration |
|proton.rpc.client.debug.enabled |false |Returns detailed error information from MetaServer to the client, suitable for developers and advanced users |
|proton.rpc.client.pool.max\-connections |128 |Maximum number of client RPC connections |
|proton.rpc.client.netty.eventloop\-num |4 |Number of client RPC Netty threads |


<span id="_2-2-metaserver配置项"></span>
### **MetaServer configuration items**


|**Parameter name** |**Parameter value** |**Note** |
|---|---|---|
|proton.rpc.server.call\-queues.num |100 |Number of RPC call queues |
|proton.rpc.server.call\-queue.length |1024 |RPC call queue length |
|proton.rpc.server.runner.threads |24 |Number of RPC call processing threads |
|proton.metaserver.metastore.kvstore.rocksdb.data\-dir |_ |MetaServer RocksDB storage path |
|proton.metaserver.bind\-address |0.0.0.0 |MetaServer bind address |
|proton.metaserver.port |10100 |MetaServer RPC port |
|proton.metaserver.http.port |10110 |MetaServer HTTP port |
|proton.metaserver.tos.{bucket name}.data\-cache.allowlist |_ |Allows caching data to directories within the cluster. Data present in these directories will be cached within the cluster. By default, all files will be cached. |
|proton.metaserver.tos..{bucket name}.data\-cache.blocklist |Empty |Does not allow caching data to directories within the cluster. Data present in these directories will not be cached within the cluster. |


<span id="_2-3-dataserver配置项"></span>
### **DataServer configuration items**


|**Parameter name** |**Parameter value** |**Note** |
|---|---|---|
|proton.dataserver.bind\-address |0.0.0.0 |DataServer bind address |
|proton.dataserver.port |10200 |DataServer data transfer port |
|proton.dataserver.http.port |10210 |DataServer HTTP port |
|proton.dataserver.ipc.port |10220 |DataServer RPC port |
|proton.dataserver.max\-session\-timeout |30000 (Unit: milliseconds) |DataServer heartbeat timeout duration |
|proton.dataserver.check\-expire\-interval |10000 (Unit: milliseconds) |DataServer heartbeat timeout check interval |
|proton.dataserver.tick\-time |3000 (Unit: milliseconds) |DataServer heartbeat interval |
|proton.dataserver.transfer\-io.enabled |true |Uses Java NIO for cached data transfer. Enabled by default for higher transfer efficiency. |
|proton.dataserver.blockio.impl |io.proton.core.data.io.CacheBlockIO |BlockIO implementation class. Local caching is enabled by default. |
|proton.dataserver.blockio.async\-cache |true |Asynchronously caches block data to local disks |
|proton.dataserver.io.socket.read\-timeout\-ms |60000 (Unit: milliseconds) |Timeout for DataServer data transfer threads reading requests from the client |
|proton.dataserver.io.socket.write\-timeout\-ms |240000 (Unit: milliseconds) |Timeout for DataServer data transfer threads writing data to the client |
|proton.dataserver.io.max\-transfer\-threads |4096 |Maximum number of DataServer data transfer threads |
|proton.dataserver.blockcache.impl |io.proton.core.data.cache.disk.MultiDiskBlockCache |Cache type. Local disk is used for caching by default. |
|proton.dataserver.blockcache.max\-cache\-size |268435456 |Total local disk cache size. Default is 256 MB. Cache space is allocated proportionally to each local disk. |
|proton.dataserver.blockcache.disk.data\-dirs |_ |Paths for cache disks. Each path corresponds to a disk. Multiple paths are separated by commas. For example: /data01/block,/data02/block |
|proton.dataserver.blockcache.data\-dirs\-ratio |_ |Configure the proportion of cache space allocated to each disk. The sum must equal 1. By default, each disk is allocated evenly. For example: 0.5,0.5 or 0.2,0.2,0.6 |
|proton.dataserver.blockcache.max\-used\-ratio |0.9 |Maximum cache usage ratio. Exceeding this value triggers cache eviction. |
|proton.dataserver.blockcache.min\-used\-ratio |0.85 |Minimum cache usage ratio. Eviction stops when usage falls below this value. |
|proton.dataserver.blockcache.reserved\-ratio |0.05 |Cache reserved ratio. When remaining space is less than this ratio, caching new data stops. |
|proton.dataserver.blockcache.async\-eviction |true |Enable asynchronous eviction |
|proton.dataserver.blockcache.flush\-threads |2 |Number of cache flush threads, used for asynchronously flushing cache data |
|proton.dataserver.blockcache.max\-retry\-times |5 |Maximum retry attempts for asynchronous cache operations |
