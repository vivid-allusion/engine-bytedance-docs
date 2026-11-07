---
title: "Untitled document"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Untitled_document"
---

<span id="d125cc90"></span>
## Proton 2.3.8

<span id="99cf6211"></span>
### Optimizations and improvements


* Fixed an issue where data could be mistakenly deleted when the recycle bin was not enabled for directory buckets.


<span id="eafdd5de"></span>
### Download link

[proton-2.3.8-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.8-bin.tar.gz)

<span id="7490d3ce"></span>
## Proton 2.3.7

<span id="7d7024cc"></span>
### Optimizations and improvements


* Fixed an issue where deleting objects in directory buckets would still return success even if an exception occurred.


<span id="20125fdb"></span>
### Download link

[proton-2.3.7-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.7-bin.tar.gz)

<span id="0cbe607d"></span>
## Proton 2.3.6

<span id="be187cba"></span>
### Optimizations and improvements


* Added support for Flink 1.11.

* Optimized the list operation in rate limiting scenarios.


<span id="6181a43d"></span>
### Download link

[proton-2.3.6-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.6-bin.tar.gz)

<span id="1456a4be"></span>
## Proton 2.3.5

<span id="435eb1ca"></span>
### Optimizations and improvements


* Added support for Flink 1.20.

* JobCommitter now supports tracking file size using Spark statistics.


<span id="069758e9"></span>
### Download link

[proton-2.3.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.5-bin.tar.gz)

<span id="e458d174"></span>
## Proton 2.3.4

<span id="04e9ce26"></span>
### Optimizations and improvements


* RawFileSystem and CoreFileSystem now use a cache pool thread pool, with idle threads automatically reclaimed.

* The tagging feature now supports automatic parsing of the OpenAPI endpoint.


<span id="99d53a53"></span>
### Download link

[proton-2.3.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.4-bin.tar.gz)

<span id="d369a693"></span>
## Proton 2.3.3

<span id="f35c763c"></span>
### Optimizations and improvements


* Upgraded TOS SDK to 2.9.2 and added support for adaptive directory deletion in TOS HNS.


<span id="47554703"></span>
### Download link

[proton-2.3.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.3-bin.tar.gz)

<span id="25168edc"></span>
## Proton 2.3.2

<span id="0c8c5a8b"></span>
### Optimizations and improvements


* Deployed a decentralized architecture cache cluster for Proton 2.3 using k8s.

* Tolerates the absence of the configured multipart staging directory.


<span id="8c54d4ab"></span>
### Download link

[proton-2.3.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.2-bin.tar.gz)

<span id="5f2c6e15"></span>
## Proton 2.3.1

<span id="4bb50766"></span>
### Optimizations and improvements


* The tagging API now supports setting the scheme for the request address.

* FileCredentialsProvider now supports adding retries when initially loading files.

* Proton configuration now supports key prefixes to resolve key conflicts.


<span id="65010273"></span>
### Download link

[proton-2.3.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.2-bin.tar.gz)

<span id="ec1be06b"></span>
## Proton 2.3.0

<span id="0a14ba59"></span>
### Optimizations and improvements


* Added support for load balancing during DataServer scaling.


<span id="7c87800a"></span>
### Download link

[proton-2.3.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.0-bin.tar.gz)

<span id="d8c10f55"></span>
## Proton 2.2.9

<span id="6f9e6102"></span>
### Optimizations and improvements


* TOS write operations now support flow control.

* Enhanced UserAgent information included in TOS requests.


<span id="02c2cefc"></span>
### Download link

[proton-2.2.9-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.9-bin.tar.gz)

<span id="c1043412"></span>
## Proton 2.2.8

<span id="f320610a"></span>
### Optimizations and improvements


* Job committer now supports generating a manifest file.


<span id="7bf79fbe"></span>
### Download link

[proton-2.2.8-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.8-bin.tar.gz)

<span id="d0249f4b"></span>
## Proton 2.2.7

<span id="5c0f2bb0"></span>
### Optimizations and improvements


* Removed redundant warning logs from CredentialProvider.

* Adjusted the thread pool release method for BucketTagNotifier.


<span id="f7bdec25"></span>
### Download link

[proton-2.2.7-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.7-bin.tar.gz)

<span id="4705166f"></span>
## Proton 2.2.5

<span id="77c71d29"></span>
### Optimizations and improvements


* Fixed an issue where retries of cachedRanges after DataServer failure caused slow reads.


<span id="245795e5"></span>
### Download link

[proton-2.2.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.5-bin.tar.gz)

<span id="9eff1501"></span>
## Proton 2.2.4

<span id="d321097b"></span>
### Optimizations and improvements


* Fixed secondary index leaks caused by rename operations in strong consistency scenarios.

* Added support for custom bucket domain.


<span id="c4821830"></span>
### Download link

[proton-2.2.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.4-bin.tar.gz)

<span id="39c30eb9"></span>
## Proton 2.2.3

<span id="3e5bd878"></span>
### Optimizations and improvements


* Disabled setOwner, setTime, and setAcl functions in standard bucket scenarios.


<span id="4c510b87"></span>
### Download link

[proton-2.2.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.3-bin.tar.gz)

<span id="753da076"></span>
## Proton 2.2.2

<span id="9a8e5c5a"></span>
### Optimizations and improvements


* Added more cluster monitoring metrics.

* Optimized the list operation in strong consistency scenarios.


<span id="3447e7d8"></span>
### Download link

[proton-2.2.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.2-bin.tar.gz)

<span id="87fec6ad"></span>
## Proton 2.2.1

<span id="8ed9404f"></span>
### Optimizations and improvements


* Fixed integration issues with logback.


<span id="af83ecf0"></span>
### Download link

[proton-2.2.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.1-bin.tar.gz)

<span id="09f79d04"></span>
## Proton 2.2.0

<span id="3a75ea0a"></span>
### Optimizations and improvements


* Cache mode now supports member changes.

* Improved FileSystem compatibility.

* Optimized random read scenarios.

* Enhanced support for TOS tiered buckets.


<span id="658155af"></span>
### Download link

[proton-2.2.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.0-bin.tar.gz)

<span id="5c39cb5b"></span>
## Proton 2.1.5

<span id="4507e189"></span>
### Optimizations and improvements


* When cache is missing, the client reads directly from BackendFS.


<span id="a8038237"></span>
### Download link

[proton-2.1.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.5-bin.tar.gz)

<span id="1d0c0c75"></span>
## Proton 2.1.4

<span id="94ccb818"></span>
### Optimizations and improvements


* Added support for a single application to access TOS across regions.

* In the TOS tiered bucket scenario, it supports retrieving the directory modification time.


<span id="0298aac8"></span>
### Download address

[proton-2.1.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.4-bin.tar.gz)

<span id="70901819"></span>
## Proton 2.1.3

<span id="697b9e4c"></span>
### Optimizations and improvements


* Optimized flow control issues for HeadBucket under high concurrency.


<span id="4770c768"></span>
### Download address

[proton-2.1.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.3-bin.tar.gz)

<span id="bca6a9b8"></span>
## Proton 2.1.2

<span id="ab587fd5"></span>
### Optimizations and improvements


* Optimized high latency and UpdateConflict issues when concurrently creating parent directories.


<span id="79a010fd"></span>
### Download address

[proton-2.1.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.2-bin.tar.gz)

<span id="c85d37c8"></span>
## Proton 2.1.1

<span id="dab88947"></span>
### New features


* Added ProtonAuthorizer interface.


<span id="7c95891b"></span>
### Optimizations and improvements


* Added RPC connection timeout configuration.

* RawFS supports fast rename.

* RawFS supports fast delete.

* RawFS supports fast mkdir.

* TOS requests carry more user information.

* Consistency Meta adds blocklist and allowlist.


<span id="15f52496"></span>
### Download address

[proton-2.1.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.1-bin.tar.gz)

<span id="4c95a88a"></span>
## Proton 2.1.0

<span id="2d770be8"></span>
### New features


* Added strong consistency Meta mode.

* Supports K8S deployment.

* Added showcache command to view actual file cache status.

* Added Flink 1.18 plugin.


<span id="7c7b1c06"></span>
### Optimizations and improvements


* Optimized PageCache memory allocation and improved asynchronous caching mechanism.

* Enhanced compatibility of FileSystem interface.

* Optimized client\-side connection pool.


<span id="a231de0a"></span>
### Download address

[proton-2.1.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.0-bin.tar.gz)

<span id="c7f8b0cc"></span>
## Proton 2.0.2

<span id="be0e1111"></span>
### Optimizations and improvements


* Optimized handling logic for abnormal nodes in cache mode.

* Fixed socket leak issue.

* Optimized stability of FileCredentialsProvider in VKE environment.


<span id="1a6c82e7"></span>
### Download address

[proton-2.0.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.2-bin.tar.gz)

<span id="be0dac75"></span>
## Proton 2.0.1

<span id="44904175"></span>
### New features


* Proton Flink plugin supports entropy injection.

* Supports configuring a custom user agent.


<span id="ff7cbe00"></span>
### Optimizations and improvements


* fs.listStatus performance optimization.

* Integrated TOS getFileStatus API by default to improve fs.getFileStatus performance.


<span id="a0511162"></span>
### Download address

[proton-2.0.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.1-bin.tar.gz)

<span id="2f554a49"></span>
## Proton 2.0.0

<span id="39924e0d"></span>
### New features


* Supports reading and writing TOS tiered buckets.

* Supports Flink 1.14.

* Supports accessing TOS via PyProton.


<span id="3e7533b1"></span>
### Optimizations and improvements


* Cache read performance optimization.

* MetaServer performance optimization.

* DataServer cache policy supports Two Queue.


<span id="35b381eb"></span>
### Download address

[proton-2.0.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.0-bin.tar.gz)

<span id="6a94b3d0"></span>
## Proton 1.9.0

<span id="a5c2463d"></span>
### New features


* Manages cached data in finer\-grained units, improving cache utilization.


<span id="0336bb98"></span>
### Optimizations and improvements


* Cache read performance optimization.

* MetaServer RPC performance optimization.

* RawFS listStatus performance optimization.


<span id="e4dab77b"></span>
### Download address

[proton-1.9.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.9.0-bin.tar.gz)

<span id="8d5efe1d"></span>
## Proton 1.8.5

<span id="e602b0fe"></span>
### New features


* Supports configuring authentication information using an additional configuration file.


<span id="51af7bfd"></span>
### Optimizations and improvements


* Optimized excessive logging of uncompleted mpu in JobCommitter.

* Optimized RawFileSystem listStatus performance.


<span id="aaa4753f"></span>
### Download address

[proton-1.8.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.5-bin.tar.gz)

<span id="b8b5ceed"></span>
## Proton 1.8.4

Proton 1.8.4 was released on 2024.04.16, mainly optimizing Proton SDK performance.

<span id="b09959da"></span>
### Optimizations and improvements:


* Used memory instead of disk file cache for staging data, optimizing small file write performance.

* Optimized Proton Conf copy performance, reducing performance loss during configuration copy in read and write processes.

* RawFileSystem supports Statistics functionality, allowing retrieval of read and write metrics via FileSystem Statistics.


<span id="04c03cc1"></span>
### Download address:

[proton-1.8.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.4-bin.tar.gz)

<span id="ce4adafa"></span>
## Proton 1.8.3

Proton 1.8.3 was released on 2024.04.01.

<span id="40b60b58"></span>
### Optimizations and improvements:


* Optimized Proton SDK Rename performance.


<span id="547ab641"></span>
### Download address:

[proton-1.8.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.3-bin.tar.gz)

<span id="37b079c5"></span>
## Proton 1.8.2

Proton 1.8.2 was released on 2024.03.29.

<span id="de0ea239"></span>
### Optimizations and improvements:


* Optimize the throughput and request efficiency of the file writing process.


<span id="d336c31c"></span>
### Download link:

[proton-1.8.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.2-bin.tar.gz)

<span id="de7569b4"></span>
## Proton 1.8.1

Proton 1.8.1 was released on 2024.03.23.

<span id="65bcc583"></span>
### Resolved the following issues:


* Optimized the parsing logic for endpoint and URI.


<span id="8c29db99"></span>
### Download link:

[proton-1.8.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.1-bin.tar.gz)

<span id="3adebde2"></span>
## Proton 1.8.0

Proton 1.8.0 was released on 2024.02.23.

<span id="2410fa41"></span>
### New features:


* Supports setting blocklist and allowlist for different directories, providing more flexible control over whether data needs to be cached locally.


<span id="a075281c"></span>
### Resolved the following issues:


* Optimized stability during TOS access.


<span id="200da052"></span>
### Download link:

[proton-1.8.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.0-bin.tar.gz)

<span id="c2339213"></span>
## Proton 1.7.0

Proton 1.7.0 was released on 2024.01.03.

<span id="59126621"></span>
### New features:


* Supports automatic metadata synchronization (Lazy Meta Sync), enabling synchronization of historical metadata from object storage to Proton MetaServer.

* Reuses network connections used by Proton to improve network access speed.

* Optimized random read performance in Cache mode.


<span id="2ded7c3a"></span>
### Resolved the following issues:


* Resolved occasional cache space over\-limit issues during high\-concurrency writes.


<span id="c5cfce29"></span>
### Download link:

[proton-1.7.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.7.0-bin.tar.gz)

<span id="480bfa61"></span>
## Proton 1.6.2

Proton 1.6.0 was released on 2023.11.20.

<span id="99a95541"></span>
### Resolved the following issues:


* Resolved the issue where the parent directory of the source file does not exist after rename.


<span id="20f00e37"></span>
### Download link:

[proton-1.6.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.2-bin.tar.gz)

<span id="b5d01ece"></span>
## Proton 1.6.1

<span id="5fbdaa05"></span>
### New features:


* Provides proton\-distcp, supporting cross\-filesystem operations, such as checksum verification from hdfs to tos.

* Optimized rename semantics to reduce the time consumed during rename operations.

* When using multipart write to tos, mulistage dir supports multiple directories to improve the performance of writing to tos fs.

* Added MetaServer HTTP REST API, allowing access to the meta server and viewing service status via WebUI.

* Supports mounting in Proton\-SDK mode using fuse.

* Optimized resolution of the issue where, in concurrent scenarios, caching IAM Credential information leads to local directory creation failure and an additional network request.


<span id="93b5f87f"></span>
### Download link:

[proton-1.6.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.1-bin.tar.gz)

<span id="67feb5e8"></span>
## Proton 1.6.0

Proton 1.6.0 was released on 2023.11.20.

<span id="d081369a"></span>
### New features:


* Retries issues caused by network exceptions resulting in TOS#head unexpected of stream, improving job stability.

* TOS listObjects uses the ListV2 API to improve performance.

* Proton adds new CLI operations commands (fsck, sync, evict, load data).

* Optimized MetaServer performance with 10 million files.


<span id="889797c1"></span>
### Download link:

[proton-1.6.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.0-bin.tar.gz)

<span id="07fb9a15"></span>
## Proton 1.5.5

<span id="c82ad189"></span>
### Resolved the following issues:


* Resolved the issue where logs are not displayed when Spark 3.3.x uses log4j2.

* Added retry logic for TOS rate limiting errors to improve task stability.


<span id="2fe5a2f1"></span>
### Download link:

[proton-1.5.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.5-bin.tar.gz)

<span id="858ddb6b"></span>
## Proton 1.5.4

<span id="6740c2d3"></span>
### Resolved the following issues:


* Resolved the issue where, during parallel writes, Put operations occasionally overwrite MPU results.


<span id="e73a5c44"></span>
### Download link:

[proton-1.5.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.4-bin.tar.gz)

<span id="0c1184bf"></span>
## Proton 1.5.3

Proton 1.5.3 was released on 2023.11.03.

<span id="63637f99"></span>
### New features:


* Provides the fs.tos.acl.default option, allowing users to set the ACL for subaccounts writing objects.


<span id="cd134dd8"></span>
### Fixed the following issues:


* Fixed the issue where the delete semantics in cache mode were not rigorous.


<span id="72040a86"></span>
### Download link:

[proton-1.5.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.3-bin.tar.gz)

<span id="f077c2ca"></span>
## Proton 1.5.2

Proton 1.5.2 was released on 2023.11.02.

<span id="d5e15cdc"></span>
### New features:


* Allows users to set a custom scheme for object storage.


<span id="df6fbd63"></span>
### Download link:

[proton-1.5.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.2-bin.tar.gz)

<span id="e9e0d431"></span>
## Proton 1.5.1

Proton 1.5.1 was released on 2023.10.30.

<span id="2cc325fb"></span>
### New features:


* Allows users to set a custom scheme for object storage.

* Optimized MetaServer to reduce machine resource usage.


<span id="bc928340"></span>
### Fixed the following issues:


* Fixed the issue where modifying some RPC parameters in MetaServer did not take effect.

* Fixed the issue where the number of tasks generated by Spark was three times the actual number of tasks.

* Fixed the issue where staging was not thread\-safe during the MPU process.

* Fixed the issue where JobCommitter failing to write the _SUCCESS file during the CommitJob phase did not trigger job rollback.


<span id="e265523f"></span>
### Download link:

[proton-1.5.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.1-bin.tar.gz)

<span id="8f0c0d93"></span>
## Proton 1.5.0

<span id="84278cf7"></span>
### New features:


* The client side supports automatic failover: when an error occurs while reading data from the data server, the client can easily fail over to TOS, improving the robustness of data read and write tasks.

* Added support for Fuse, allowing Proton cache to be mounted to a directory via mount.

* Added Meta server monitoring metrics, including QPS, latency, RocksDB access QPS, and RocksDB access latency, among others.

* Proton CLI supports displaying block information.

* Optimized random read performance in cache mode.

* The client and data server support verifying the file checksum when reading data from underlying storage to ensure data consistency.


<span id="993bc9a4"></span>
### Fixed the following issues:


* Ctrl\-C does not stop the load task when batch loading metadata.

* Fixed the issue where logs were not displayed when using log4j2 with Spark 3.3.x.

* Added retry logic for TOS rate limiting errors to improve task stability.

* Fixed the issue where data could not be read when the file name contained spaces.

* Fixed the permission issue that occurred when switching users during file upload.


<span id="83867c1a"></span>
### Download link:

[proton-1.5.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.0-bin.tar.gz)

<span id="7f298809"></span>
## Proton 1.4.3

<span id="52222bdd"></span>
### Fixed the following issues:


* Optimized the usage of temporary credentials for accessing TOS.


<span id="a31793dd"></span>
### Download link:

[proton-1.4.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.3-bin.tar.gz)

<span id="ab30bd72"></span>
## Proton 1.4.2

Proton 1.4.2 was released on 2023.09.26.

<span id="f583b4f4"></span>
### New features:


* Implemented socket connection reuse in the DataTransfer link, improving performance by approximately 20 percent.

* Implemented TransferIO on the DataTransfer side, significantly reducing data copying and improving data transfer performance by approximately 24 percent.


<span id="b6af14cb"></span>
### Fixed the following issues:


* Fixed the issue where the SocketListener stop thread failed.

* Fixed the issue where ObjectOutputStream did not have sufficient permissions when writing a part to the staging directory.


<span id="ec51355b"></span>
### Download link:

[proton-1.4.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.2-bin.tar.gz)

<span id="9dcf85a0"></span>
## Proton 1.4.1

<span id="c3e5ed3d"></span>
### New features:


* When performing MPU uploads using object storage, the stage directory can now be configured.

* Optimized cache performance using the ConnectionCache component.

* Added Proton meta server HA mode.

* Replaced ChunkIter with PacketIter to avoid excessive small heap objects.

* Replace ByteArray with ByteBuffer for performance optimization.


<span id="8873fbde"></span>
### Fixed the following issues:


* Fixed the issue of out\-of\-bounds data reading from RemoteBlockReader.


<span id="7b9ee540"></span>
### Download link:

[proton-1.4.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.1-bin.tar.gz)

<span id="11886907"></span>
## Proton 1.4.0

Proton 1.4.0 made the following changes based on 1.3.0:

<span id="843d0ddb"></span>
### New features:


* DataServer supports memory\-based BlockCache.

* DataServer adds Block Meta Cache when reading cache blocks.

* Optimized DataServer transfer thread model.

* DataServer loads block cache asynchronously by default.

* Optimized PositionRead by using an independent BlockReader.

* Optimized Proton internal configuration conversion logic to avoid excessive copying.

* Proton supports metrics.

* Proton command line supports conf, daemon, and loglevel options.

* Added audit log to facilitate tracking requests.


<span id="9b5b470d"></span>
### Fixed the following issues:


* Fixed incomplete cleaning of Proton Committer magic path in certain scenarios.

* Fixed the issue with controlling the upper limit of DataServer max transfer threads.

* Fixed MetaServer Chinese parsing issue.


<span id="c38e6b4b"></span>
### Download link:

[proton-1.4.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.0-bin.tar.gz)

<span id="68ad71d6"></span>
## Proton 1.3.0

Proton 1.3.0 was released on 2023.08.07, introducing the Proton cache mode, which includes Meta Server and Data Server. Users can choose to use Proton SDK mode to connect directly to TOS, or use Proton Cache mode to cache TOS data within the EMR cluster. By default, Volcano EMR clusters use Proton SDK mode. To use the cache mode, Proton service must be installed as an optional component. The following optimizations were also made based on 1.2.2:


* Improved stability when requesting temporary credentials during TOS access in job execution.

* The default value of the hdfs core\-site key `fs.tos.credential.provider.custom.classes` has been updated to: `io.proton.common.object.tos.auth.EmrSidecarCredentialProvider,io.proton.common.object.tos.auth.EnvironmentCredentialsProvider,io.proton.common.object.tos.auth.SimpleCredentialsProvider,io.proton.common.object.tos.auth.IAMInstanceCredentialsProvider`


<span id="220ab0f1"></span>
### Download link:

[proton-1.3.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.3.0-bin.tar.gz)

<span id="8d8dd035"></span>
## Proton 1.2.2

Proton 1.2.2 includes the following fixes based on 1.2.1.


* Supports checksum interface, for example, allowing consistency checks via checksum under distcp.

* Fixed inconsistent behavior between hdfs and tos when creating parent directories with mkdir \-p.

* Optimized SDK performance by caching tos client at the bucket level.


Download link:

eas\-sdk\-1.2.2.tar.gz

<span id="4068d2af"></span>
## Proton 1.2.1


* Optimized stability and fixed ineffective close of TOS newThreadpool in hook.


Download link:

eas\-sdk\-1.2.1.tar.gz

<span id="39c62553"></span>
## Proton 1.2.0


* Compatible with 1.1\-dev version parameters, allowing normal operation without modifying 1.1\-dev parameters.

* Supports integration with Flink; Flink can write to tos via eas SDK.

* Optimized TOS SDK stream close issue to improve read and write performance.


Download link:

eas\-sdk\-1.2.0.tar.gz

<span id="60b22570"></span>
## Proton 1.1\-dev

1.1\-dev is the first production\-ready version of eas, mainly including the following features:


* Compatible with HDFS FileSystem interface, enabling various compute engines such as Hive and Spark to read and write data in TOS object storage without changing user behavior.

* Provides MR and Spark Job Committer, greatly improving the write speed to object storage.

* Enhance flow control stability. Because object storage access has specific bandwidth limitations, requests may experience waiting, timeouts, and other issues once the bandwidth limit is reached. In EAS, retries are handled specially to prevent retries from occurring on the Task side of the job, thereby reducing the retry cost caused by bandwidth limitations.


<span id="73e81449"></span>
## Proton 2.0.2

<span id="65e66597"></span>
### Optimization and improvements


* Optimize the handling logic for abnormal nodes in cache mode.

* Fix socket leak issue.

* Optimize the stability of FileCredentialsProvider in the VKE environment.


<span id="386ce77c"></span>
### Download link

[proton-2.0.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.2-bin.tar.gz)

<span id="d48942b2"></span>
## Proton 2.0.1

<span id="e9edc525"></span>
### New features


* Proton Flink plugin supports entropy injection.

* Support custom user agent.


<span id="dbc874c4"></span>
### Optimization and improvements


* fs.listStatus performance optimization.

* Integrate TOS getFileStatus API by default to improve fs.getFileStatus performance.


<span id="97b6d679"></span>
### Download link

[proton-2.0.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.1-bin.tar.gz)

<span id="daa357c7"></span>
## Proton 2.0.0

<span id="b4da88e2"></span>
### New features


* Support reading and writing TOS tiered buckets.

* Support Flink 1.14.

* Support accessing TOS via PyProton.


<span id="9da13558"></span>
### Optimization and improvements


* Cache read performance optimization.

* MetaServer performance optimization.

* DataServer cache policy supports the Two Queue algorithm.


<span id="0d9e9184"></span>
### Download link

[proton-2.0.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.0-bin.tar.gz)

<span id="007c2476"></span>
## Proton 1.9.0

<span id="778b16e5"></span>
### New features


* Manage cached data in finer\-grained units to improve cache utilization.


<span id="342e725d"></span>
### Optimization and improvements


* Cache read performance optimization.

* MetaServer RPC performance optimization.

* RawFS listStatus performance optimization.


<span id="0e6e91fd"></span>
### Download link

[proton-1.9.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.9.0-bin.tar.gz)

<span id="de17d55e"></span>
## Proton 1.8.5

<span id="b6fd1f13"></span>
### New features


* Support configuring authentication information using an additional configuration file.


<span id="4abfcc85"></span>
### Optimization and improvements


* Optimize the issue of excessive logging of uncompleted MPUs in JobCommitter.

* Optimize RawFileSystem listStatus performance.


<span id="b5571cc2"></span>
### Download link

[proton-1.8.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.5-bin.tar.gz)

<span id="ddfff76a"></span>
## Proton 1.8.4

Proton 1.8.4 was released on 2024.04.16, mainly optimizing the performance of Proton SDK.

<span id="532056a0"></span>
### Optimization and improvements:


* Use memory instead of disk files to cache staging data, optimizing the performance of small file writes.

* Optimize Proton configuration file copy performance, reducing performance loss related to configuration copying during read and write operations.

* RawFileSystem supports Statistics functionality, allowing read and write metrics to be obtained via FileSystem Statistics.


<span id="54b27561"></span>
### Download link:

[proton-1.8.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.4-bin.tar.gz)

<span id="2a3258fd"></span>
## Proton 1.8.3

Proton 1.8.3 was released on 2024.04.01.

<span id="2cf57330"></span>
### Optimization and improvements:


* Optimize Proton SDK Rename performance.


<span id="eeb61ce7"></span>
### Download link:

[proton-1.8.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.3-bin.tar.gz)

<span id="577701d6"></span>
## Proton 1.8.2

Proton 1.8.2 was released on 2024.03.29.

<span id="46021858"></span>
### Optimization and improvements:


* Optimize throughput and request efficiency of the file writing process.


<span id="ada3b5f5"></span>
### Download link:

[proton-1.8.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.2-bin.tar.gz)

<span id="374e63f9"></span>
## Proton 1.8.1

Proton 1.8.1 was released on 2024.03.23.

<span id="f22a2641"></span>
### Fixed the following issues:


* Optimize the parsing logic for endpoint and uri.


<span id="d8d265ac"></span>
### Download link:

[proton-1.8.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.1-bin.tar.gz)

<span id="6531a9c7"></span>
## Proton 1.8.0

Proton 1.8.0 was released on 2024.02.23.

<span id="11b3d807"></span>
### New features:


* Support setting blocklist and allowlist for different directories, providing more flexible control over whether data needs to be cached locally.

* Proton performance optimization

   * DataServer reuses connections for reading TOS data

   * MetaServer RocksDB default parameter optimization


<span id="bb0a531e"></span>
### Download link:

[proton-1.8.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.0-bin.tar.gz)

<span id="037752dd"></span>
## Proton 1.7.0

Proton 1.7.0 was released on 2024.01.03.

<span id="97ab938e"></span>
### New features:


* Supports the automatic metadata synchronization feature (Lazy Meta Sync), which enables synchronization of historical data metadata from object storage to the Proton MetaServer.

* Reuses network connections used by Proton to improve network access speed.

* Optimizes random read performance in Cache mode.


<span id="2bb368c4"></span>
### Fixes the following issues:


* Resolves occasional cache space overrun issues under high\-concurrency write scenarios.


[proton-1.7.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.7.0-bin.tar.gz)

<span id="aca2ca57"></span>
## Proton 1.6.2

Proton 1.6.2 was released on 2023.11.20.

<span id="561b885d"></span>
### Fixes the following issues:


* Resolves the issue where the parent directory of the source file does not exist after rename.


<span id="7cf718bb"></span>
### Download link:

[proton-1.6.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.2-bin.tar.gz)

<span id="d66d188e"></span>
## Proton 1.6.1

<span id="622b5310"></span>
### New features:


* Provides proton\-distcp, supporting cross\-filesystem operations, such as checksum verification from hdfs to tos.

* Optimizes rename semantics to reduce the time consumed during rename operations.

* When performing multipart writes to TOS, mulistage dir supports multiple directories to improve write performance to the TOS filesystem.

* Adds MetaServer HTTP REST API, allowing access to the meta server and viewing service status through the WebUI.

* Supports mounting using fuse in Proton\-SDK mode.

* Optimizes the process to resolve the issue where, under concurrent scenarios, failure to create a local directory when caching IAM Credential information results in an additional network request.


<span id="c0ed6a85"></span>
### Download link:

[proton-1.6.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.1-bin.tar.gz)

<span id="a950d583"></span>
## Proton 1.6.0

Proton 1.6.0 was released on 2023.11.20.

<span id="e9faa4d8"></span>
### New features:


* Implements retries for the TOS#head unexpected of stream issue caused by network exceptions to improve job stability.

* TOS listObjects uses the ListV2 interface to improve performance.

* Proton adds new CLI commands (fsck, sync, evict, load data).

* Optimizes MetaServer performance when handling 10 million files.


<span id="4c25ae5f"></span>
### Download link:

[proton-1.6.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.0-bin.tar.gz)

<span id="e46bebe9"></span>
## Proton 1.5.5

<span id="37f49280"></span>
### Fixes the following issues:


* Fixes the issue where logs are not displayed when using log4j2 with Spark 3.3.x.

* Adds retry logic for TOS rate limiting errors to improve task stability.


<span id="fbb1d86e"></span>
### Download link:

[proton-1.5.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.5-bin.tar.gz)

<span id="17481ac2"></span>
## Proton 1.5.4

<span id="ae59df6e"></span>
### Fixes the following issues:


* Fixes the issue where, during parallel writes, the Put operation occasionally overwrites MPU results.


<span id="60a9a27c"></span>
### Download link:

[proton-1.5.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.4-bin.tar.gz)

<span id="732c1f77"></span>
## Proton 1.5.3

Proton 1.5.3 was released on 2023.11.03.

<span id="e168211d"></span>
### New features:


* Provides the fs.tos.acl.default option, allowing users to set the ACL for objects written by sub\-accounts.


<span id="47be30c6"></span>
### Fixes the following issues:


* Fixes the issue of imprecise delete semantics in cache mode.


<span id="5e6f131d"></span>
### Download link:

[proton-1.5.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.3-bin.tar.gz)

<span id="9872e63d"></span>
## Proton 1.5.2

Proton 1.5.2 was released on 2023.11.02.

<span id="96f06684"></span>
### New features:


* Supports user\-defined schemes for object storage.


<span id="54d5756d"></span>
### Download link:

[proton-1.5.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.2-bin.tar.gz)

<span id="7d0b2bfb"></span>
## Proton 1.5.1

Proton 1.5.1 was released on 2023.10.30.

<span id="2093f453"></span>
### New features:


* Supports user\-defined schemes for object storage.

* Optimizes MetaServer to reduce machine resource usage.


<span id="7a6c1632"></span>
### Fixes the following issues:


* Fixes the issue where some MetaServer RPC parameters could not take effect after modification.

* Resolves the issue where the number of Spark\-generated tasks is three times the actual number of tasks.

* Fixed the issue where staging was not thread\-safe during the MPU process.

* Fixed the issue where failure to write the _SUCCESS file in the CommitJob phase by JobCommitter did not trigger job rollback.


<span id="1d91418d"></span>
### Download link:

[proton-1.5.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.1-bin.tar.gz)

<span id="21b0edb3"></span>
## Proton 1.5.0

<span id="a0712ea2"></span>
### New features:


* Client now supports automatic failover. When reading data from the data server fails, it can easily fail over to TOS, improving the robustness of data read and write tasks.

* Added support for Fuse, allowing the Proton cache to be mounted to a directory via mount.

* Added Meta server monitoring metrics, including QPS, latency, RocksDB access QPS, and latency, among others.

* Proton CLI now supports displaying block information.

* When Client and data server read data from underlying storage, they now support verifying the file checksum to ensure data read consistency.

* Allows users to set custom schemes for object storage.

* Provides the fs.tos.acl.default option, allowing users to set the ACL for sub\-accounts to write objects.


<span id="b24f9e97"></span>
### Fixed the following issues:


* When batch loading metadata, pressing Ctrl\-C could not stop the load task.

* Fixed the issue where modifying some RPC parameters in MetaServer did not take effect.

* Optimized the issue where the number of tasks generated by Spark was three times the actual number of tasks.

* Fixed the issue where logs were not displayed when using log4j2 with Spark 3.3.x.

* Added retry logic for TOS rate limiting errors to improve task stability.


<span id="e1ac6489"></span>
### Download link:

[proton-1.5.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.0-bin.tar.gz)

<span id="c5959dc2"></span>
## Proton 1.4.3

Optimized the usage of temporary credentials for accessing TOS.

<span id="ef1070ff"></span>
### Download link:

[proton-1.4.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.3-bin.tar.gz)

<span id="b94ca858"></span>
## Proton 1.4.2

Proton 1.4.2 was released on 2023.09.26.

<span id="3c7f3a20"></span>
### New features:


* Implemented Socket Connection Reuse in the DataTransfer pipeline, improving performance by approximately 20%.

* Implemented TransferIO on the DataTransfer side, significantly reducing data copying and improving data transfer performance by approximately 24%.


<span id="b305bcb2"></span>
### Fixed the following issues:


* Fixed the issue where the thread responsible for stopping the SocketListener failed.

* Fixed the issue where ObjectOutputStream had insufficient permissions when writing a Part to the staging dir.


<span id="996411bc"></span>
### Download link:

[proton-1.4.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.2-bin.tar.gz)

<span id="087fcb97"></span>
## Proton 1.4.1

<span id="7d369386"></span>
### New features:


* When performing MPU uploads using object storage, the stage directory is now configurable.

* Optimized cache performance using the ConnectionCache component.

* Added Proton meta server HA mode.

* Replaced ChunkIter with PacketIter to avoid excessive small heap objects.

* Replaced ByteArray with ByteBuffer for performance optimization.


<span id="8957a69f"></span>
### Fixed the following issues:


* Fixed the issue of out\-of\-bounds data reads from RemoteBlockReader.


<span id="6fd63c3f"></span>
### Download link:

[proton-1.4.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.1-bin.tar.gz)

<span id="f3fb388c"></span>
## Proton 1.4.0

Based on 1.3.0, Proton 1.4.0 made the following changes:

<span id="b606644b"></span>
### New features:


* DataServer supports memory\-based BlockCache.

* DataServer adds Block Meta Cache when reading cache blocks.

* Optimized the DataServer transfer thread model.

* DataServer now loads block cache asynchronously by default.

* Optimized PositionRead by using an independent BlockReader.

* Optimized internal configuration conversion logic in proton to avoid excessive copying.

* Proton supports metrics.

* The Proton command line now supports conf, daemon, and loglevel options.

* Added audit log, making it easier to trace requests.


<span id="565fed32"></span>
### Fixed the following issues:


* Fixed an issue where Proton Committer magic path was not properly cleaned up in certain scenarios.

* Fixed the issue with controlling the upper limit of DataServer max transfer thread.

* Fixed the issue with parsing Chinese in MetaServer.


<span id="f743987c"></span>
### Download link:

[proton-1.4.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.0-bin.tar.gz)

<span id="1d426d95"></span>
## Proton 1.3.0

Proton 1.3.0 was released on 2023.08.07, introducing the Proton cache mode, which includes both Meta Server and Data Server. Users can choose to use the Proton SDK mode to connect directly to TOS, or use the Proton Cache mode to cache data accessed from TOS within the EMR cluster. By default, Volcano EMR clusters use the Proton SDK mode. To use the cache mode, Proton service must be installed as an optional component. The following optimizations were also made for version 1.2.2:


* Improved the stability when requesting temporary credentials while accessing TOS during job execution.

* The default value of the hdfs core\-site key `fs.tos.credential.provider.custom.classes` has been updated to: `io.proton.common.object.tos.auth.EmrSidecarCredentialProvider,io.proton.common.object.tos.auth.EnvironmentCredentialsProvider,io.proton.common.object.tos.auth.SimpleCredentialsProvider,io.proton.common.object.tos.auth.IAMInstanceCredentialsProvider`


<span id="f5c2c3bb"></span>
### Download link:

[proton-1.3.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.3.0-bin.tar.gz)
