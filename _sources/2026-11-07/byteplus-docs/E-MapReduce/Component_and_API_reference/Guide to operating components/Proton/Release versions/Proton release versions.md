---
title: "Proton release versions"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Proton_release_versions"
---

<span id="a97c0819"></span>
## Proton 2.3.19

<span id="e1635d65"></span>
### Optimizations and improvements


* Compatible with the `FsPermission.toOctal()` method of older versions of Hadoop

* Support for the `dfs.user.home.dir.prefix` parameter of HDFS


<span id="268958f7"></span>
### Download link

[proton-2.3.19-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.19-bin.tar.gz)

<span id="c5a66c89"></span>
## Proton 2.3.18

<span id="c7e7d109"></span>
### Optimizations and improvements


* **Important fix**: Upgraded ve\-tos\-java\-sdk to 2.9.16 and fixed an issue where the status of TOS standard bucket rename was misjudged under certain exceptions, affecting correctness.


<span id="401e5f6a"></span>
### Download link

[proton-2.3.18-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.18-bin.tar.gz)

<span id="99085445"></span>
## Proton 2.3.17

<span id="c08a65d5"></span>
### Optimizations and improvements


* Support scheduled flush for the append interface

* Support specifying accelerator access points in bucket configuration


<span id="3756267a"></span>
### Download link

[proton-2.3.17-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.17-bin.tar.gz)

<span id="cd8df819"></span>
## Proton 2.3.13

<span id="23186d1c"></span>
### Optimizations and improvements


* Fixed the issue with error message display


<span id="18ec8d13"></span>
### Download link

[proton-2.3.13-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.13-bin.tar.gz)

<span id="3bdee672"></span>
## Proton 2.3.12

<span id="5a3b2926"></span>
### Optimizations and improvements


* Automatic parsing for tagging URLs


<span id="5caeef2d"></span>
### Download link

[proton-2.3.12-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.11-bin.tar.gz)

<span id="99c165f6"></span>
## Proton 2.3.11

<span id="40aaa778"></span>
### Optimizations and improvements


* Support Flink 2.2


<span id="fca7d2a8"></span>
### Download link

[proton-2.3.11-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.11-bin.tar.gz)

<span id="a20e3d59"></span>
## Proton 2.3.10

<span id="b5228667"></span>
### Optimizations and improvements


* Support ignoring illegal object paths in TOS

* Adapt to semantic changes in TOS SetObjectMeta


<span id="7fcc66f7"></span>
### Download link

[proton-2.3.11-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.11-bin.tar.gz)

<span id="4e5e2a01"></span>
## Proton 2.3.9

<span id="2e82f511"></span>
### Optimizations and improvements


* Fixed the issue where MPU rate limiting was ineffective


<span id="34c692be"></span>
### Download link

[proton-2.3.9-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.9-bin.tar.gz)

<span id="f7e0c82d"></span>
## Proton 2.3.8

<span id="5690537e"></span>
### Optimizations and improvements


* Fixed the issue where data was mistakenly deleted when the recycle bin was not enabled for directory buckets


<span id="4b613de7"></span>
### Download link

[proton-2.3.8-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.8-bin.tar.gz)

<span id="00fb1389"></span>
## Proton 2.3.7

<span id="afd872c9"></span>
### Optimizations and improvements


* Fixed the issue where directory bucket object deletion returned success even if an exception occurred


&nbsp;

<span id="839167c7"></span>
## Proton 2.3.6

<span id="946832ce"></span>
### Optimizations and improvements


* Support Flink 1.11

* Optimized rate limiting scenarios for list operations


&nbsp;

<span id="07606edf"></span>
## Proton 2.3.5

<span id="7d7fd6bb"></span>
### Optimizations and improvements


* Support Flink 1.20

* JobCommitter supports tracking file size in Spark statistics


&nbsp;

<span id="ea99f1bd"></span>
## Proton 2.3.4

<span id="c83329c5"></span>
### Optimizations and improvements


* RawFileSystem and CoreFileSystem use cache pool thread pools, with automatic recycling of idle threads

* Tagging functionality supports automatic parsing of OpenAPI endpoints


&nbsp;

<span id="974436ef"></span>
## Proton 2.3.3

<span id="5ee80a04"></span>
### Optimizations and improvements


* Upgraded TOS SDK to 2.9.2, supports adaptive directory deletion for TOS HNS


&nbsp;

<span id="0c84fa06"></span>
## Proton 2.3.2

<span id="d0b1df5a"></span>
### Optimizations and improvements


* k8s deployment of the Proton 2.3 decentralized architecture cache cluster

* Supports configuration where the multipart staging directory does not exist


<span id="8c61c7c2"></span>
### Download link

[proton-2.3.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.2-bin.tar.gz)

<span id="9b418d73"></span>
## Proton 2.3.1

<span id="138258f9"></span>
### Optimizations and improvements


* Tagging interface supports setting the scheme for request addresses

* FileCredentialsProvider supports adding retries when initially loading files

* Proton configuration supports prefixing keys to resolve key conflicts


<span id="341c83fa"></span>
### Download link

[proton-2.3.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.2-bin.tar.gz)

<span id="7c5e4fe1"></span>
## Proton 2.3.0

<span id="9e81f64e"></span>
### Optimizations and improvements


* Support load balancing during DataServer scaling


<span id="31b4744f"></span>
### Download link

[proton-2.3.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.3.0-bin.tar.gz)

<span id="dc489e6b"></span>
## Proton 2.2.9

<span id="b30759ef"></span>
### Optimizations and improvements


* TOS write operations support flow control

* Enhanced UserAgent information included in TOS requests


<span id="0c73a4be"></span>
### Download link

[proton-2.2.9-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.9-bin.tar.gz)

<span id="a167eeaa"></span>
## Proton 2.2.8

<span id="50ba2cf1"></span>
### Optimizations and improvements


* Job committer supports generating manifest files


<span id="a8242e5b"></span>
### Download link

[proton-2.2.8-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.8-bin.tar.gz)

<span id="7d00247b"></span>
## Proton 2.2.7

<span id="9445f009"></span>
### Optimizations and improvements


* Removed redundant warning logs from CredentialProvider

* Adjusted thread pool release method for BucketTagNotifier


<span id="03e0e7ba"></span>
### Download link

[proton-2.2.7-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.7-bin.tar.gz)

<span id="d35cce53"></span>
## Proton 2.2.5

<span id="12e14325"></span>
### Optimizations and improvements


* Fixed the issue where retries of cachedRanges after DataServer failure caused slow reads


<span id="46e22fbb"></span>
### Download link

[proton-2.2.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.5-bin.tar.gz)

<span id="a588b9da"></span>
## Proton 2.2.4

<span id="c62b8e0e"></span>
### Optimizations and improvements


* Fixed secondary index leak caused by rename in strong consistency scenarios

* Support custom bucket domains


<span id="e545fe59"></span>
### Download link

[proton-2.2.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.4-bin.tar.gz)

<span id="01c80125"></span>
## Proton 2.2.3

<span id="076e8f1d"></span>
### Optimizations and improvements


* Disabled setOwner, setTime, and setAcl functions for standard bucket scenarios


<span id="6977f898"></span>
### Download link

[proton-2.2.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.3-bin.tar.gz)

<span id="2aadab15"></span>
## Proton 2.2.2

<span id="9e771d65"></span>
### Optimizations and improvements


* Add more cluster monitoring metrics.

* Optimize the list for strong consistency scenarios.


<span id="886bc7f8"></span>
### Download link

[proton-2.2.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.2-bin.tar.gz)

<span id="c417e286"></span>
## Proton 2.2.1

<span id="eac170a3"></span>
### Optimizations and improvements


* Fix integration issues with logback.


<span id="e335c991"></span>
### Download link

[proton-2.2.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.1-bin.tar.gz)

<span id="974dc69f"></span>
## Proton 2.2.0

<span id="d33cfeab"></span>
### Optimizations and improvements


* Cache mode supports member changes.

* FileSystem compatibility improved.

* Optimize random read scenarios.

* Optimize support for TOS tiered buckets.


<span id="0e142e81"></span>
### Download link

[proton-2.2.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.2.0-bin.tar.gz)

<span id="5a6801f4"></span>
## Proton 2.1.5

<span id="93537844"></span>
### Optimizations and improvements


* When cache is missing, the client reads BackendFS directly.


<span id="93b17dfa"></span>
### Download link

[proton-2.1.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.5-bin.tar.gz)

<span id="d83b4b87"></span>
## Proton 2.1.4

<span id="cefa41b2"></span>
### Optimizations and improvements


* Support for a single application to access TOS across regions.

* In TOS tiered bucket scenarios, support for retrieving directory modification time.


<span id="730665d5"></span>
### Download link

[proton-2.1.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.4-bin.tar.gz)

<span id="9675a04a"></span>
## Proton 2.1.3

<span id="a64b5492"></span>
### Optimizations and improvements


* Optimize flow control issues for HeadBucket under high concurrency.


<span id="95c281f3"></span>
### Download link

[proton-2.1.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.3-bin.tar.gz)

<span id="e45e22cb"></span>
## Proton 2.1.2

<span id="5c1aa71c"></span>
### Optimizations and improvements


* Optimize high latency and UpdateConflict issues when concurrently creating parent directories.


<span id="fe00bf45"></span>
### Download link

[proton-2.1.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.2-bin.tar.gz)

<span id="103550a6"></span>
## Proton 2.1.1

<span id="19bd5a11"></span>
### New features


* Add ProtonAuthorizer interface.


<span id="3c728683"></span>
### Optimizations and improvements


* Add RPC connection timeout configuration.

* RawFS supports fast rename.

* RawFS supports fast delete.

* RawFS supports fast mkdir.

* TOS requests carry more user information.

* Consistency Meta adds allowlist and blocklist.


<span id="d9554511"></span>
### Download link

[proton-2.1.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.1-bin.tar.gz)

<span id="c4951bef"></span>
## Proton 2.1.0

<span id="ce5b19dc"></span>
### New features


* Add strong consistency Meta mode.

* Support for K8S deployment.

* Add showcache command to view the actual cache status of files.

* Add Flink 1.18 plugin.


<span id="c771912e"></span>
### Optimizations and improvements


* Optimize PageCache memory allocation and improve asynchronous caching mechanism.

* Enhance FileSystem interface compatibility.

* Optimize client connection pool.


<span id="0db1196b"></span>
### Download link

[proton-2.1.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.1.0-bin.tar.gz)

<span id="3aed3667"></span>
## Proton 2.0.2

<span id="1a09474a"></span>
### Optimizations and improvements


* Optimized the handling logic for faulty nodes in cache mode.

* Fixed socket leak issues.

* Improved the stability of FileCredentialsProvider in the VKE environment.


<span id="3f6b8aca"></span>
### Download link

[proton-2.0.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.2-bin.tar.gz)

<span id="8f345678"></span>
## Proton 2.0.1

<span id="4abe9503"></span>
### New features


* The Proton Flink plugin supports entropy injection.

* Supports custom user agents.


<span id="22c74c84"></span>
### Optimizations and improvements


* Performance optimization for fs.listStatus.

* Integrated the TOS getFileStatus API by default to improve fs.getFileStatus performance.


<span id="90701129"></span>
### Download link

[proton-2.0.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.1-bin.tar.gz)

<span id="97bff51f"></span>
## Proton 2.0.0

<span id="4fe8f593"></span>
### New features


* Supports reading and writing TOS tiered buckets.

* Supports Flink 1.14.

* Supports accessing TOS via PyProton.


<span id="2a7fa088"></span>
### Optimizations and improvements


* Cache read performance optimization.

* MetaServer performance optimization.

* DataServer cache policy supports Two Queue.


<span id="5336cdb0"></span>
### Download link

[proton-2.0.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.0-bin.tar.gz)

<span id="07575e62"></span>
## Proton 1.9.0

<span id="47af0a33"></span>
### New features


* Manages cached data in finer\-grained units, improving cache utilization.


<span id="71e77017"></span>
### Optimizations and improvements


* Cache read performance optimization.

* MetaServer RPC performance optimization.

* RawFS listStatus performance optimization.


<span id="824d67d3"></span>
### Download link

[proton-1.9.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.9.0-bin.tar.gz)

<span id="d30c8cf2"></span>
## Proton 1.8.5

<span id="7b118704"></span>
### New features


* Supports configuring authentication information using an additional configuration file.


<span id="30edaaca"></span>
### Optimizations and improvements


* Optimized the issue of excessive uncompleted mpu log printing in JobCommitter.

* Optimized RawFileSystem listStatus performance.


<span id="e5096e8c"></span>
### Download link

[proton-1.8.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.5-bin.tar.gz)

<span id="8ba7d41a"></span>
## Proton 1.8.4

Proton 1.8.4 was released on 2024.04.16, mainly optimizing the performance of the Proton SDK.

<span id="ccb0e9cb"></span>
### Optimizations and improvements:


* Used memory instead of disk files for caching staging data, optimizing small file write performance.

* Optimized Proton Conf copy performance, reducing performance loss caused by configuration copying during read and write operations.

* RawFileSystem supports the Statistics feature, allowing read and write metrics to be obtained through FileSystem Statistics.


<span id="a48e7406"></span>
### Download link:

[proton-1.8.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.4-bin.tar.gz)

<span id="8860257e"></span>
## Proton 1.8.3

Proton 1.8.3 was released on 2024.04.01.

<span id="57730066"></span>
### Optimizations and improvements:


* Optimized Proton SDK Rename performance.


<span id="1b779fc7"></span>
### Download link:

[proton-1.8.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.3-bin.tar.gz)

<span id="b3a1a7d4"></span>
## Proton 1.8.2

Proton 1.8.2 was released on 2024.03.29.

<span id="3339812e"></span>
### Optimizations and improvements:


* Optimized throughput and request handling efficiency of the file writing process.


<span id="e59f603e"></span>
### Download link:

[proton-1.8.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.2-bin.tar.gz)

<span id="c74dcdeb"></span>
## Proton 1.8.1

Proton 1.8.1 was released on 2024.03.23.

<span id="d9f84dc4"></span>
### Bug fixes:


* Optimize the parsing logic for endpoint and URI.


<span id="d8350f98"></span>
### Download link:

[proton-1.8.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.1-bin.tar.gz)

<span id="65b4bc2d"></span>
## Proton 1.8.0

Proton 1.8.0 released on 2024.02.23.

<span id="b00884ef"></span>
### New features:


* Supports setting allowlist and blocklist for different directories, providing more flexible control over whether data needs to be cached locally.


<span id="fea9c9ec"></span>
### Bug fixes:


* Optimized stability during TOS access.


<span id="54ca3856"></span>
### Download link:

[proton-1.8.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.0-bin.tar.gz)

<span id="9947d47e"></span>
## Proton 1.7.0

Proton 1.7.0 released on 2024.01.03.

<span id="7e284aff"></span>
### New features:


* Supports automatic metadata synchronization (Lazy Meta Sync), enabling synchronization of metadata for historical data stored in object storage to Proton MetaServer.

* Reuses network connections used by Proton to improve network access speed.

* Optimizes random read performance in Cache mode.


<span id="2ee54a3a"></span>
### Bug fixes:


* Resolves occasional cache space over\-limit issues under high concurrent writes.


<span id="60ee1f08"></span>
### Download link:

[proton-1.7.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.7.0-bin.tar.gz)

<span id="8afd00d8"></span>
## Proton 1.6.2

Proton 1.6.0 released on 2023.11.20.

<span id="c1584b7f"></span>
### Bug fixes:


* Resolves the issue where the parent directory of the source file does not exist after rename.


<span id="acf1f21d"></span>
### Download link:

[proton-1.6.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.2-bin.tar.gz)

<span id="7885cfe9"></span>
## Proton 1.6.1

<span id="16a42ebe"></span>
### New features:


* Provides proton\-distcp, supports cross\-fs operations, such as checksum verification from hdfs to tos.

* Optimizes rename semantics, reducing the time consumed during rename operations.

* Supports multiple directories for mulistage dir when writing to tos in segments, improving tos fs write performance.

* Adds MetaServer HTTP REST API, allowing access to meta server and viewing service status via WebUI.

* Supports mounting using fuse in Proton\-SDK mode.

* Optimizes the solution for concurrent scenarios where caching IAM Credential information causes local directory creation failure, resulting in an extra network request.


<span id="d081b624"></span>
### Download link:

[proton-1.6.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.1-bin.tar.gz)

<span id="6539c45e"></span>
## Proton 1.6.0

Proton 1.6.0 released on 2023.11.20.

<span id="4080427e"></span>
### New features:


* Retries for TOS#head unexpected of stream issues caused by network exceptions, improving job stability.

* TOS listObjects uses the ListV2 interface to improve performance.

* Proton adds new CLI operation commands (fsck, sync, evict, load data).

* Optimizes MetaServer performance with 10 million files.


<span id="e4774b3d"></span>
### Download link:

[proton-1.6.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.0-bin.tar.gz)

<span id="5069e4e4"></span>
## Proton 1.5.5

<span id="db4f5ea4"></span>
### Bug fixes:


* Fixed the issue where logs were not displayed when using log4j2 with Spark 3.3.x.

* Add retry logic for TOS rate limiting errors to improve task stability.


<span id="41d4f902"></span>
### Download link:

[proton-1.5.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.5-bin.tar.gz)

<span id="8044129d"></span>
## Proton 1.5.4

<span id="3d95acd8"></span>
### Bug fixes:


* Fixes the issue where Put operations occasionally overwrite MPU results during parallel writes.


<span id="8ff1726c"></span>
### Download link:

[proton-1.5.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.4-bin.tar.gz)

<span id="3033ed64"></span>
## Proton 1.5.3

Proton 1.5.3 released on 2023.11.03.

<span id="870fd089"></span>
### New features:


* Provides the fs.tos.acl.default option, allowing users to set the ACL for sub\-accounts writing objects.


<span id="7afda0d2"></span>
### Bug fixes:


* Fixes the issue of imprecise delete semantics in cache mode.


<span id="2aa57906"></span>
### Download link:

[proton-1.5.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.3-bin.tar.gz)

<span id="3d2c03b5"></span>
## Proton 1.5.2

Proton 1.5.2 released on 2023.11.02.

<span id="28d8aa20"></span>
### New features:


* Allow users to configure custom schemes for object storage.


<span id="5251d3dc"></span>
### Download link:

[proton-1.5.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.2-bin.tar.gz)

<span id="57cb73d3"></span>
## Proton 1.5.1

Proton 1.5.1 released on 2023.10.30.

<span id="fa287a05"></span>
### New features:


* Allow users to configure custom schemes for object storage.

* Optimize MetaServer to reduce machine resource usage.


<span id="3bc4cbd5"></span>
### Bug fixes:


* Issue where modifying some RPC parameters in MetaServer did not take effect.

* Fixed the issue where Spark generated three times as many tasks as expected.

* Fixed the thread safety issue with staging during the MPU process.

* Fixed the issue where JobCommitter's failure to write the _SUCCESS file during the CommitJob phase did not trigger a job rollback.


<span id="52af0691"></span>
### Download link:

[proton-1.5.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.1-bin.tar.gz)

<span id="3b25a626"></span>
## Proton 1.5.0

<span id="6c4210f7"></span>
### New features:


* The client supports automatic failover. If an error occurs while reading data from the data server, it can easily failover to TOS, improving the robustness of data read/write tasks.

* Added support for Fuse, allowing Proton cache to be mounted to a directory.

* Added Meta server monitoring metrics, including QPS, latency, RocksDB access QPS, and other metrics.

* Proton CLI supports displaying block information.

* Optimized random read performance in cache mode.

* When the client and data server read data from underlying storage, file checksum verification is supported to ensure data consistency.


<span id="2d2dab22"></span>
### Bug fixes:


* When batch loading metadata, Ctrl\-C cannot stop the load task.

* Fixed the issue where logs were not displayed when using log4j2 with Spark 3.3.x.

* Add retry logic for TOS rate limiting errors to improve task stability.

* Fixed the issue where data could not be read when the file name contained spaces.

* Fixed the permission issue that occurred when switching users during file upload.


<span id="81d3152f"></span>
### Download link:

[proton-1.5.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.0-bin.tar.gz)

<span id="6c2f91f2"></span>
## Proton 1.4.3

<span id="780bef75"></span>
### Bug fixes:


* Optimized the method for using TOS temporary credentials.


<span id="db0d4fe2"></span>
### Download link:

[proton-1.4.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.3-bin.tar.gz)

<span id="14b5c640"></span>
## Proton 1.4.2

Proton 1.4.2 released on 2023.09.26.

<span id="3bbcda3c"></span>
### New features:


* Implemented Socket Connection Reuse in the DataTransfer pipeline, improving performance by approximately 20%.

* Implemented TransferIO on the DataTransfer side, significantly reducing data copying and improving data transfer performance by approximately 24%.


<span id="59bf740f"></span>
### Bug fixes:


* Issue where the SocketListener stop thread failed.

* Issue where ObjectOutputStream lacked sufficient permissions when writing parts to the staging directory.


<span id="34e6f39d"></span>
### Download link:

[proton-1.4.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.2-bin.tar.gz)

<span id="d492c71e"></span>
## Proton 1.4.1

<span id="48754d8b"></span>
### New features:


* When performing MPU uploads using object storage, the stage directory is now configurable.

* Optimize cache performance using the ConnectionCache component.

* Added Proton meta server HA mode.

* Replace ChunkIter with PacketIter to avoid excessive small heap objects.

* Replace ByteArray with ByteBuffer for performance optimization.


<span id="d3ec8d03"></span>
### Bug fixes:


* Fix the issue where reading data from RemoteBlockReader resulted in out\-of\-bounds errors.


<span id="d1e40018"></span>
### Download link:

[proton-1.4.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.1-bin.tar.gz)

<span id="ce6ce97e"></span>
## Proton 1.4.0

Based on Proton 1.3.0, Proton 1.4.0 introduces the following changes:

<span id="c85d6631"></span>
### New features:


* DataServer supports memory\-based BlockCache.

* Added Block Meta Cache when DataServer reads cache blocks.

* Optimized DataServer transfer thread model.

* DataServer now loads block cache asynchronously by default.

* Optimized PositionRead by using an independent BlockReader.

* Optimized Proton internal configuration conversion logic to avoid excessive copying.

* Proton supports metrics.

* The Proton command line now supports conf, daemon, and loglevel options.

* Added audit log for easier request tracing.


<span id="5e85da8b"></span>
### Bug fixes:


* Fixed the issue where Proton Committer magic path was not properly cleaned up in some scenarios.

* Fixed the issue with controlling the upper limit of DataServer max transfer threads.

* Fixed the issue with parsing Chinese in MetaServer.


<span id="979d7727"></span>
### Download link:

[proton-1.4.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.0-bin.tar.gz)

<span id="f2ec82d4"></span>
## Proton 1.3.0

Proton 1.3.0 was released on 2023.08.07, introducing the Proton cache mode, which includes Meta Server and Data Server. Users can choose to use the Proton SDK mode to connect directly to TOS, or use the Proton Cache mode to cache data accessed from TOS within the EMR cluster. By default, Volcano EMR clusters use the Proton SDK mode. To use the cache mode, Proton service must be installed as an optional component. The following optimizations were made for version 1.2.2:


* Improved the stability of temporary credential requests when accessing TOS during job execution.

* The default value of the hdfs core\-site key `fs.tos.credential.provider.custom.classes` has been updated to `io.proton.common.object.tos.auth.EmrSidecarCredentialProvider,io.proton.common.object.tos.auth.EnvironmentCredentialsProvider,io.proton.common.object.tos.auth.SimpleCredentialsProvider,io.proton.common.object.tos.auth.IAMInstanceCredentialsProvider`.


<span id="1322c868"></span>
### Download link:

[proton-1.3.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.3.0-bin.tar.gz)

<span id="36573a24"></span>
## Proton 1.2.2

Proton 1.2.2 includes the following fixes based on version 1.2.1.


* Supports the checksum interface, allowing consistency checks via checksum in distcp.

* Fixed the inconsistency between HDFS and TOS when using mkdir \-p to create parent directories.

* Optimized SDK performance by caching the TOS client according to bucket granularity.


Download link:

eas\-sdk\-1.2.2.tar.gz

<span id="1d165ee7"></span>
## Proton 1.2.1


* Fixed the issue where TOS newThreadpool was not properly closed in the hook, improving stability.


Download link:

eas\-sdk\-1.2.1.tar.gz

<span id="8d2de60d"></span>
## Proton 1.2.0


* Compatible with 1.1\-dev version parameters, allowing normal operation without modifying 1.1\-dev parameters.

* Supports integration with Flink. Flink can write to TOS using the EAS SDK.

* Optimized the stream close issue in the TOS SDK, improving read and write performance.


Download link:

eas\-sdk\-1.2.0.tar.gz

<span id="cc008ebf"></span>
## Proton 1.1\-dev

1.1\-dev is the first production\-ready version of eas and mainly includes the following features:


* Compatible with the HDFS FileSystem interface, enabling various compute engines, such as Hive and Spark, to read and write data in TOS object storage without changing user behavior.

* Provides a Job Committer for MR and Spark, significantly improving the write speed for object storage.

* Improved flow control stability. Since accessing object storage is subject to specific bandwidth limits, requests may experience waiting and timeouts when the bandwidth limit is reached. In eas, retries are handled specially to avoid occurring at the task level, reducing the retry cost caused by bandwidth limitations.


<span id="26835692"></span>
## Proton 2.0.2

<span id="09d54fce"></span>
### Optimizations and improvements


* Optimized the handling logic for faulty nodes in cache mode.

* Fixed socket leak issues.

* Improved the stability of FileCredentialsProvider in the VKE environment.


<span id="799057e9"></span>
### Download link

[proton-2.0.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.2-bin.tar.gz)

<span id="d1e6dbe6"></span>
## Proton 2.0.1

<span id="0c1e28bc"></span>
### New features


* The Proton Flink plugin supports entropy injection.

* Supports custom user agents.


<span id="dd441044"></span>
### Optimizations and improvements


* Performance optimization for fs.listStatus.

* Integrated the TOS getFileStatus API by default to improve fs.getFileStatus performance.


<span id="c2f9a656"></span>
### Download link

[proton-2.0.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.1-bin.tar.gz)

<span id="edb41f26"></span>
## Proton 2.0.0

<span id="a20b22e5"></span>
### New features


* Supports reading and writing TOS tiered buckets.

* Supports Flink 1.14.

* Supports accessing TOS via PyProton.


<span id="3877ec50"></span>
### Optimizations and improvements


* Cache read performance optimization.

* MetaServer performance optimization.

* DataServer cache policy supports Two Queue.


<span id="5ed867c9"></span>
### Download link

[proton-2.0.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-2.0.0-bin.tar.gz)

<span id="60fa3152"></span>
## Proton 1.9.0

<span id="423b402d"></span>
### New features


* Manages cached data in finer\-grained units, improving cache utilization.


<span id="9ece6f65"></span>
### Optimizations and improvements


* Cache read performance optimization.

* MetaServer RPC performance optimization.

* RawFS listStatus performance optimization.


<span id="577b9a21"></span>
### Download link

[proton-1.9.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.9.0-bin.tar.gz)

<span id="f3724c2e"></span>
## Proton 1.8.5

<span id="c38a8895"></span>
### New features


* Supports configuring authentication information using an additional configuration file.


<span id="5768f57b"></span>
### Optimizations and improvements


* Optimized the issue of excessive uncompleted mpu log printing in JobCommitter.

* Optimized RawFileSystem listStatus performance.


<span id="fa702a5d"></span>
### Download link

[proton-1.8.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.5-bin.tar.gz)

<span id="8c93de29"></span>
## Proton 1.8.4

Proton 1.8.4 was released on 2024.04.16, mainly optimizing the performance of the Proton SDK.

<span id="62c1b70c"></span>
### Optimizations and improvements:


* Used memory instead of disk files for caching staging data, optimizing small file write performance.

* Optimized Proton Conf copy performance, reducing performance loss caused by configuration copying during read and write operations.

* RawFileSystem supports the Statistics feature, allowing read and write metrics to be obtained through FileSystem Statistics.


<span id="5acee43d"></span>
### Download link:

[proton-1.8.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.4-bin.tar.gz)

<span id="54b54bd3"></span>
## Proton 1.8.3

Proton 1.8.3 was released on 2024.04.01.

<span id="ee4977f5"></span>
### Optimizations and improvements:


* Optimized Proton SDK Rename performance.


<span id="92c62ca4"></span>
### Download link:

[proton-1.8.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.3-bin.tar.gz)

<span id="cd88e510"></span>
## Proton 1.8.2

Proton 1.8.2 was released on 2024.03.29.

<span id="71a062a1"></span>
### Optimizations and improvements:


* Optimized throughput and request handling efficiency of the file writing process.


<span id="363ce7e2"></span>
### Download link:

[proton-1.8.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.2-bin.tar.gz)

<span id="5b074002"></span>
## Proton 1.8.1

Proton 1.8.1 was released on 2024.03.23.

<span id="9e77a4f9"></span>
### Bug fixes:


* Optimize the parsing logic for endpoint and URI.


<span id="89431221"></span>
### Download link:

[proton-1.8.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.1-bin.tar.gz)

<span id="870bf616"></span>
## Proton 1.8.0

Proton 1.8.0 released on 2024.02.23.

<span id="880f58f3"></span>
### New features:


* Supports setting allowlist and blocklist for different directories, providing more flexible control over whether data needs to be cached locally.

* Proton performance optimization

   * DataServer reuses connections for reading TOS data

   * MetaServer RocksDB default parameter optimization


<span id="954e15bb"></span>
### Download link:

[proton-1.8.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.8.0-bin.tar.gz)

<span id="8e477bdb"></span>
## Proton 1.7.0

Proton 1.7.0 released on 2024.01.03.

<span id="b8a24448"></span>
### New features:


* Supports automatic metadata synchronization (Lazy Meta Sync), enabling synchronization of metadata for historical data stored in object storage to Proton MetaServer.

* Reuses network connections used by Proton to improve network access speed.

* Optimizes random read performance in Cache mode.


<span id="72609e3d"></span>
### Bug fixes:


* Resolves occasional cache space over\-limit issues under high concurrent writes.


[proton-1.7.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.7.0-bin.tar.gz)

<span id="35198498"></span>
## Proton 1.6.2

Proton 1.6.2 released on 2023.11.20.

<span id="36108a5d"></span>
### Bug fixes:


* Resolves the issue where the parent directory of the source file does not exist after rename.


<span id="9bf2b598"></span>
### Download link:

[proton-1.6.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.2-bin.tar.gz)

<span id="d24a6a19"></span>
## Proton 1.6.1

<span id="3a709db1"></span>
### New features:


* Provides proton\-distcp, supports cross\-fs operations, such as checksum verification from hdfs to tos.

* Optimizes rename semantics, reducing the time consumed during rename operations.

* Supports multiple directories for mulistage dir when writing to tos in segments, improving tos fs write performance.

* Adds MetaServer HTTP REST API, allowing access to meta server and viewing service status via WebUI.

* Supports mounting using fuse in Proton\-SDK mode.

* Optimizes the solution for concurrent scenarios where caching IAM Credential information causes local directory creation failure, resulting in an extra network request.


<span id="6234b124"></span>
### Download link:

[proton-1.6.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.1-bin.tar.gz)

<span id="9ec41124"></span>
## Proton 1.6.0

Proton 1.6.0 released on 2023.11.20.

<span id="bfec29cc"></span>
### New features:


* Retries for TOS#head unexpected of stream issues caused by network exceptions, improving job stability.

* TOS listObjects uses the ListV2 interface to improve performance.

* Proton adds new CLI operation commands (fsck, sync, evict, load data).

* Optimizes MetaServer performance with 10 million files.


<span id="ac2b5409"></span>
### Download link:

[proton-1.6.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.6.0-bin.tar.gz)

<span id="c08d0a4a"></span>
## Proton 1.5.5

<span id="2a01651f"></span>
### Bug fixes:


* Fixed the issue where logs were not displayed when using log4j2 with Spark 3.3.x.

* Add retry logic for TOS rate limiting errors to improve task stability.


<span id="540fadba"></span>
### Download link:

[proton-1.5.5-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.5-bin.tar.gz)

<span id="9e4729a4"></span>
## Proton 1.5.4

<span id="e82b2107"></span>
### Bug fixes:


* Fixes the issue where Put operations occasionally overwrite MPU results during parallel writes.


<span id="b5cd4b48"></span>
### Download link:

[proton-1.5.4-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.4-bin.tar.gz)

<span id="e0447499"></span>
## Proton 1.5.3

Proton 1.5.3 released on 2023.11.03.

<span id="535fc42b"></span>
### New features:


* Provides the fs.tos.acl.default option, allowing users to set the ACL for sub\-accounts writing objects.


<span id="ba44ae6a"></span>
### Bug fixes:


* Fixes the issue of imprecise delete semantics in cache mode.


<span id="d0681cc6"></span>
### Download link:

[proton-1.5.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.3-bin.tar.gz)

<span id="7d9368ca"></span>
## Proton 1.5.2

Proton 1.5.2 released on 2023.11.02.

<span id="ca67bf0a"></span>
### New features:


* Allow users to configure custom schemes for object storage.


<span id="b997aed9"></span>
### Download link:

[proton-1.5.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.2-bin.tar.gz)

<span id="9307df6e"></span>
## Proton 1.5.1

Proton 1.5.1 released on 2023.10.30.

<span id="bd803268"></span>
### New features:


* Allow users to configure custom schemes for object storage.

* Optimize MetaServer to reduce machine resource usage.


<span id="ffe68829"></span>
### Bug fixes:


* Issue where modifying some RPC parameters in MetaServer did not take effect.

* Fixed the issue where Spark generated three times as many tasks as expected.

* Fixed the thread safety issue with staging during the MPU process.

* Fixed the issue where JobCommitter's failure to write the _SUCCESS file during the CommitJob phase did not trigger a job rollback.


<span id="751ea0b6"></span>
### Download link:

[proton-1.5.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.1-bin.tar.gz)

<span id="478bd952"></span>
## Proton 1.5.0

<span id="371f6e20"></span>
### New features:


* The client supports automatic failover. If an error occurs while reading data from the data server, it can easily failover to TOS, improving the robustness of data read/write tasks.

* Added support for Fuse, allowing Proton cache to be mounted to a directory.

* Added Meta server monitoring metrics, including QPS, latency, RocksDB access QPS, and other metrics.

* Proton CLI supports displaying block information.

* When the client and data server read data from underlying storage, file checksum verification is supported to ensure data consistency.

* Allow users to configure custom schemes for object storage.

* Provides the fs.tos.acl.default option, allowing users to set the ACL for sub\-accounts writing objects.


<span id="018e9f89"></span>
### Bug fixes:


* When batch loading metadata, Ctrl\-C cannot stop the load task.

* Issue where modifying some RPC parameters in MetaServer did not take effect.

* Fixed the issue where Spark generated three times as many tasks as expected.

* Fixed the issue where logs were not displayed when using log4j2 with Spark 3.3.x.

* Add retry logic for TOS rate limiting errors to improve task stability.


<span id="adccf665"></span>
### Download link:

[proton-1.5.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.5.0-bin.tar.gz)

<span id="bb7e68fd"></span>
## Proton 1.4.3

Optimized the method for using TOS temporary credentials.

<span id="9f9591e5"></span>
### Download link:

[proton-1.4.3-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.3-bin.tar.gz)

<span id="3aaf158f"></span>
## Proton 1.4.2

Proton 1.4.2 released on 2023.09.26.

<span id="38991469"></span>
### New features:


* Implemented Socket Connection Reuse in the DataTransfer pipeline, improving performance by approximately 20%.

* Implemented TransferIO on the DataTransfer side, significantly reducing data copying and improving data transfer performance by approximately 24%.


<span id="e121eee6"></span>
### Bug fixes:


* Issue where the SocketListener stop thread failed.

* Issue where ObjectOutputStream lacked sufficient permissions when writing parts to the staging directory.


<span id="0144f55f"></span>
### Download link:

[proton-1.4.2-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.2-bin.tar.gz)

<span id="eea4dbbb"></span>
## Proton 1.4.1

<span id="a5944f4a"></span>
### New features:


* When performing MPU uploads using object storage, the stage directory is now configurable.

* Optimize cache performance using the ConnectionCache component.

* Added Proton meta server HA mode.

* Replace ChunkIter with PacketIter to avoid excessive small heap objects.

* Replace ByteArray with ByteBuffer for performance optimization.


<span id="18042549"></span>
### Bug fixes:


* Fix the issue where reading data from RemoteBlockReader resulted in out\-of\-bounds errors.


<span id="129aaeb4"></span>
### Download link:

[proton-1.4.1-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.1-bin.tar.gz)

<span id="83b46ff4"></span>
## Proton 1.4.0

Based on Proton 1.3.0, Proton 1.4.0 introduces the following changes:

<span id="e662117e"></span>
### New features:


* DataServer supports memory\-based BlockCache.

* Block Meta Cache is added when DataServer reads cache blocks.

* Optimized DataServer transfer thread model.

* DataServer now loads block cache asynchronously by default.

* Optimized PositionRead by using an independent BlockReader.

* Optimized Proton's internal configuration conversion logic to avoid excessive copying.

* Proton supports metrics.

* The Proton command line now supports conf, daemon, and loglevel options.

* Added audit log for easier request tracing.


<span id="504c7e77"></span>
### Bug fixes:


* Fixed the issue where Proton Committer magic path was not properly cleaned up in some scenarios.

* Fixed the issue with controlling the upper limit of DataServer max transfer threads.

* Fixed the issue with parsing Chinese in MetaServer.


<span id="d2900c31"></span>
### Download link:

[proton-1.4.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.4.0-bin.tar.gz)

<span id="6c335976"></span>
## Proton 1.3.0

Proton 1.3.0 was released on 2023.08.07, introducing the Proton cache mode, which includes Meta Server and Data Server. Users can choose to use the Proton SDK mode to connect directly to TOS, or use the Proton Cache mode to cache data accessed from TOS within the EMR cluster. By default, Volcano EMR clusters use the Proton SDK mode. To use the cache mode, Proton service must be installed as an optional component. The following optimizations were made for version 1.2.2:


* Improved the stability of temporary credential requests when accessing TOS during job execution.

* The default value of the hdfs core\-site key `fs.tos.credential.provider.custom.classes` has been updated to `io.proton.common.object.tos.auth.EmrSidecarCredentialProvider,io.proton.common.object.tos.auth.EnvironmentCredentialsProvider,io.proton.common.object.tos.auth.SimpleCredentialsProvider,io.proton.common.object.tos.auth.IAMInstanceCredentialsProvider`.


<span id="00806bf7"></span>
### Download link:

[proton-1.3.0-bin.tar.gz](https://proton-pkgs.tos-cn-beijing.volces.com/public/proton-1.3.0-bin.tar.gz)

<span id="dcff7f16"></span>
## Proton 1.2.2

Based on version 1.2.1, Proton 1.2.2 includes the following fixes:


* Supports the checksum interface, for example, consistency checks using checksum under distcp.

* Fixed the issue where mkdir \-p created parent directories inconsistently between HDFS and TOS.

* Optimized SDK performance by caching TOS Client at the bucket level.


Download link:

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c070447930cdc77a89fe07493323c2d8.gz" name="proton-sdk-1.2.2.tar.gz">proton-sdk-1.2.2.tar.gz</Attachment>


&nbsp;

<span id="c5df0150"></span>
## Proton 1.2.1


* Optimized stability and fixed the ineffective close of TOS newThreadpool in hook.


Download link:

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_593534b8c0cd00fbaa1aba7b0b02c605.gz" name="proton-sdk-1.2.1.tar.gz">proton-sdk-1.2.1.tar.gz</Attachment>


&nbsp;

<span id="73331d6d"></span>
## Proton 1.2.0


* Compatible with 1.1\-dev version parameters, allowing normal operation without modifying 1.1\-dev parameters.

* Supports integration with Flink; Flink can write to TOS via Proton SDK.

* Optimized TOS SDK stream close issue to improve read and write performance.


Download link:

<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_35c78706f47f0f0c7c9eb0f9e92b466a.gz" name="proton-sdk-1.2.0.tar.gz">proton-sdk-1.2.0.tar.gz</Attachment>


&nbsp;

<span id="d79b7cb5"></span>
## Proton 1.1\-dev

1.1\-dev is the first production\-ready version of Proton, mainly including the following features:


* Compatible with the HDFS FileSystem interface, enabling various compute engines such as Hive and Spark to read and write data in object storage TOS without changing user behavior.

* Provides MR and Spark Job Committer, greatly improving the write speed to object storage.

* To improve flow control stability, since accessing object storage is subject to specific bandwidth limitations, requests may experience waiting and timeout issues once the bandwidth limit is reached. Proton implements special handling for retries to prevent them from occurring on the Task side of a job, thereby reducing the cost of retries caused by bandwidth limitations.
