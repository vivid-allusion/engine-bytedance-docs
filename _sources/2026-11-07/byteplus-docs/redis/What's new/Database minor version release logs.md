---
title: "Database minor version release logs"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log"
---

Cache for Redis periodically releases minor versions of proxy nodes and server nodes to enrich product features or fix known bugs and improve the user experience. This topic summarizes the updates for proxy and server minor versions for your reference.

## Background information

* **Proxy**

   A proxy node is the proxy server node for instances of Cache for Redis. It is used to achieve high availability in Redis instances. The proxy node can recognize and forward the user's read and write requests. These requests can be sent to the primary node or read\-only secondary node according to parameter settings to achieve [read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting). For more details about proxy, refer to [Core components](https://docs.byteplus.com/en/docs/redis/about-redis#.5Luj55CG6IqC54K5).

* **Server**

   A server node is the smallest unit for building an instance of Cache for Redis. Each instance contains at least one server node. If each shard contains only one node, the instance cannot provide data persistence and high availability. If the number of nodes in each shard exceeds 1, the nodes must have a primary\-secondary relationship.

   Each server node in the instance uses the same Redis version (the Redis version you selected when creating the instance). All server nodes in an instance have the same specifications and memory capacity. Cache for Redis supports various node specifications that provide different memory capacities. For more information on specifications, refer to [Instance specifications](https://docs.byteplus.com/en/docs/redis/product-specification).

* For more information about Cache for Redis major version compatibility, refer to [Redis major version compatibility](https://docs.byteplus.com/en/docs/redis/redis_major_version_compatibility).

* You can upgrade the server or proxy to the latest or a specified version on the Redis console. For specific procedures, refer to [Upgrading minor version](https://vsop-online.bytedance.net/doc/manage/detail/6293/6293/1113727).

## Proxy version release log

**2026**

|Version number |Release date |Type |Description |
|---|---|---|---|
|proxy_version_1.608.0<br><br> |2026\-10\-15 |New features |Added support for the algorithms such as ECDHE and AES\-CBC in SSL encryption. |
|||Feature enhancement |Optimized proxy performance. |
|||Bug fixes |Fixed a rare issue where a small number of messages might be lost when new subscription channels are added to existing pubsub connections. |
| | | | |
||| | |
||| | |
|proxy_version_1.604.0<br><br> <br><br> |2026\-05\-28<br><br> |New features<br><br> |* **Added Support for Valkey JSON Extension Module**: Added support for the Valkey JSON module, enhancing its processing capabilities for JSON data types.<br><br>* **MONITOR Command Supports Displaying Real Client IP**: The MONITOR command now supports displaying the real client IP address of the command executor.<br><br>   > **tip**<br>   <br><br>   > This feature is currently controlled by a toggle. To enable it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br>   <br><br>* **Added support for XSETID command**: Added support for the XSETID command. |
|||Feature enhancement |* **Optimized CLIENT LIST command result display**: Supports displaying connection information for all threads, facilitating more comprehensive client connection status monitoring.<br><br>* **Optimized SCRIPT EXISTS command handling logic**: Supports broadcasting the SCRIPT EXISTS command to all shards, returning "exists" only when the specified script exists on all shards, ensuring script consistency in a clustered environment.<br><br>* **Optimized transaction execution logic**: When a transaction does not include WATCH or SELECT commands, it supports sending requests to backend Redis via shared connections, effectively reducing private connection usage.<br><br>* **Hot key cache supports multi\-DB scenarios**: The hot key cache feature now supports multiple DBs, enhancing access performance in multi\-database environments.<br><br>* **Improved overall performance**: Minor performance optimizations were made to the Proxy, improving the system's overall response speed and stability. |
|||Bug fixes |None. |
|proxy_version_1.602.0<br><br> <br><br> |2026\-04\-13 |New features |The CLIENT LIST command now supports viewing traffic and command count information for each connection. |
|||Feature enhancement |* Improved overall performance.<br><br>* Optimized the primary\-secondary switchover process triggered by O&M, instance specification changes, and manual primary switchovers, preventing abnormal errors during the switchover. |
|||Bug fixes |* Fixed the issue where the proxy might abnormally crash when some commands process a large number of keys.<br><br>* Fixed the issue where Pub/Sub messages might be repeatedly subscribed during primary\-secondary switchover or instance specification changes.<br><br>* Fied the issue with abnormal connection idle time statistics in instance sessions. |
|proxy_version_1.512.0<br><br> <br><br> |2026\-01\-26<br><br> |New features |None. |
|||Feature enhancement |Optimized performance in Pipeline mode. |
|||Bug fixes |None. |

**2025**

|Version number |Release date |Type |Description |
|---|---|---|---|
|proxy_version_1.511.0<br><br> <br><br> |2025\-12\-22<br><br> |New features |None. |
|||Feature enhancement |The default upper limit for the number of key parameters in Lua scripts has been changed from 100 to unlimited. |
|||Bug fixes |None. |
|proxy_version_1.510.0<br><br> |2025\-11\-24<br><br> |New features |Supported setting soft and hard limits for proxy's client buffer. |
|||Feature enhancement |Optimized the return result after executing the INFO command on instances with sharding cluster enabled, where the `redis_mode` field displays as `cluster`. |
|||Bug fixes |None. |
|proxy_version_1.509.0<br><br> |2025\-11\-05<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where proxy memory usage continuously increased in certain scenarios. |
|proxy_version_1.508.1<br><br> |2025\-09\-24<br><br> |New features |None. |
|||Feature enhancement |Optimized proxy's memory usage in certain scenarios. |
|||Bug fixes |None. |
|proxy_version_1.507.0<br><br> |2025\-08\-26<br><br> |New features |* Instances with sharding cluster enabled supported using the SWAPDB command. For more details, refer to [Server management](https://docs.byteplus.com/en/docs/redis/Server_management).<br><br>* Cache for Redis supported Sentinel compatible mode and password\-free command execution in Sentinel compatible mode. For more details, refer to [Configuring password-free command execution in Sentinel mode](https://docs.byteplus.com/en/docs/redis/password-free_execution_in_sentinel_mode). |
|||Feature enhancement |Optimized the transaction command execution logic for instances with sharding cluster enabled, allowing keys operated by transaction commands to be in different slots by default.<br><br>> **tip**<br><br><br>> For more details about transaction command limits for Redis instances with sharding clusters enabled in proxy mode, refer to [Transaction command limits](https://docs.byteplus.com/en/docs/redis/command-limit#.5LqL5Yqh5ZG95Luk6ZmQ5Yi2).<br> |
|||Bug fixes |Fixed the [CVE-2025-21605](https://github.com/redis/redis/security/advisories/GHSA-r67f-p999-2gff) security vulnerability. |
|proxy_version_1.506.0<br><br> <br><br> |2025\-07\-16<br><br> |New features |* Instances with sharding cluster enabled now support the following additional commands:<br><br>   * Supports more commands of [Cluster management](https://docs.byteplus.com/en/docs/redis/Cluster_management):<br><br>      * CLUSTER ADDSLOTS<br><br>      * CLUSTER COUNT\-FAILURE\-REPORTS<br><br>      * CLUSTER DELSLOTS<br><br>      * CLUSTER FAILOVER<br><br>      * CLUSTER FORGET<br><br>      * CLUSTER MEET<br><br>      * CLUSTER REPLICAS<br><br>      * CLUSTER REPLICATE<br><br>      * CLUSTER RESET<br><br>      * CLUSTER SAVECONFIG<br><br>      * CLUSTER SET\-CONFIG\-EPOCH<br><br>      * CLUSTER SETSLOT<br><br>      * CLUSTER SLAVES<br><br>   * Supports more commands of [Server management](https://docs.byteplus.com/en/docs/redis/Server_management):<br><br>      * SLOWLOG GET<br><br>      * SLOWLOG LEN<br><br>      * SLOWLOG HELP<br><br>      * SLOWLOG RESET<br><br>* Both instances with sharding cluster enabled and disabled now support the following additional commands:<br><br>   * Supports the READWRITE command of [Connection management](https://docs.byteplus.com/en/docs/redis/Connection_management).<br><br>   * Supports the FUNCTION HELP command of [Scripting and functions](https://docs.byteplus.com/en/docs/redis/Scripting_and_functions). |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where instances with sharding cluster enabled produced unexpected results when executing SMOVE commands in non\-DB0 scenarios with keys spanning multiple slots. |
|proxy_version_1.505.0 |2025\-06\-24 |New features |None. |
|||Feature enhancement |Optimized proxy memory usage for big key scenarios. |
|||Bug fixes |None. |
|proxy_version_1.504.0 |2025\-05\-27 |New features |Added support for the Proxy self\-developed command IMONITOR. For more details, refer to [IMONITOR](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#imonitor). |
|||Feature enhancement |* Aligned the cursor format in the ISCAN command with that of the open\-source Redis SCAN command. For more details, refer to [ISCAN](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#iscan).<br><br>* Optimized performance when executing single SUBSCRIBE, UNSUBSCRIBE, or PSUBSCRIBE commands with numerous parameters. |
|||Bug fixes |None. |
|proxy_version_1.503.0 |2025\-04\-22 |New features |Supported setting the read/write splitting strategy for the current connection using the `clientsetopt read_priority` command. For more details, refer to [Setting read/write splitting](https://docs.byteplus.com/en/docs/redis/set-read-write-splitting). |
|||Feature enhancement |None. |
|||Bug fixes |* Fixed the issue where the result format was incorrect when the PING command included parameters.<br><br>* Fixed the issue where SCAN commands were incorrectly marked as write commands. |
|proxy_version_1.502.0 |2025\-03\-19 |New features |* Supported negative cache. The proxy can cache queries that return empty results, reducing caching pressure on backend server nodes.<br><br>* Supported RESP 3 protocol.<br><br>   > **tip**<br>   <br><br>   > For specific procedure of switching to the RESP3 protocol, refer to [Switching to RESP3 protocol](https://docs.byteplus.com/en/docs/redis/switch-RESP3-protocol).<br>    |
|||Feature enhancement |* Optimized the proxy's handling of broadcast commands (for example, SCRIPT LOAD); when some server nodes return errors, the error message is directly sent to the client.<br><br>* Optimized the return result of the HELLO command to support displaying the client ID recorded by the proxy. |
|||Bug fixes |Fixed coredump issues caused by clients using illegal protocols. |

**2024**

|Version number |Release date |Type |Description |
|---|---|---|---|
|proxy_version_1.22.0 |2024\-12\-26 |New features |* Proxy supported the CLIENT SETINFO command. For more details, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).<br><br>* Instances with sharding cluster enabled now support operating on cross\-slot keys using UNLINK, EXISTS, and SMOVE commands. For more details, refer to [Limits on multiple key commands](https://docs.byteplus.com/en/docs/redis/command-limit#.5aSaLWtleS3lkb3ku6TpmZDliLY=). |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where messages could not be received when the SSUBSCRIBE command contained multiple channels. |
|proxy_version_1.21.0 |2024\-11\-28 |New features |Added support for PUBSUB SHARDCHANNELS and PUBSUB SHARDNUMSUB commands. For more details, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command). |
|||Feature enhancement |None. |
|||Bug fixes |None. |
|proxy_version_1.20.0 |2024\-10\-24 |New features |* Added support for using `sentinels` and `get-master-addr-by-name` subcommands in Sentinel commands. For more details, refer to [Sentinel](https://docs.byteplus.com/en/docs/redis/Sentinel).<br><br>* Instances with sharding cluster enabled supported operating keys across slots in ZINTERSTORE and ZUNIONSTORE commands. For more details, refer to [Limits on multiple key commands](https://docs.byteplus.com/en/docs/redis/command-limit#.5aSaLWtleS3lkb3ku6TpmZDliLY=). |
|||Feature enhancement |* Optimized the execution results for empty transactions or transactions containing only SELECT commands, which now no longer report errors.<br><br>* Fully disable connection idle timeout when the `proxy-client-idle-timeout` parameter is set to `0`. |
|||Bug fixes |Fixed the issue where proxy failed to intercept some illegal requests, preventing coredumps. |
|proxy_version_1.19.0 |2024\-09\-12 |New features |None. |
|||Feature enhancement |Supported disabling all subcommands under a primary command after passing the primary command in the `disabled-commands` parameter. For more information on disabled commands, refer to [Disabled command](https://docs.byteplus.com/en/docs/redis/command-limit#.56aB55So5ZG95Luk6K-05piO). |
|||Bug fixes |Fixes the issue where the INFO command's return result additionally displayed `cluster section` information. |
|proxy_version_1.18.0 |2024\-08\-08 |New features |None |
|||Feature enhancement |Optimized support for `redis-cli --pipe` mode to prevent connection disconnections. |
|||Bug fixes |Fixed the issue where transaction commands occasionally reported errors. |
|proxy_version_1.16.0 |2024\-05\-09 |New features |Instances with sharding cluster enabled supported setting the `notify-keyspace-events` parameter to specify the type of notifications the server needs to send. For more details, refer to [Supported parameters](https://docs.byteplus.com/en/docs/redis/supported-parameter). |
|||Feature enhancement |None. |
|||Bug fixes |None. |
|proxy_version_1.15.0 |2024\-04\-11 |New features |None. |
|||Feature enhancement |* Optimized the return results of the cluster version's INFO command to ensure that the data returned by the `cluster_enabled` field is consistent with the community edition.<br><br>* Optimized the return results of the CLUSTER INFO command to support displaying the actual number of shards in the `cluster_size` and `cluster_known_nodes` fields. |
|||Bug fixes |* Fixed the issue where SUBSCRIBE or PSUBSCRIBE commands could not receive subsequent PUBLISH messages after horizontal scaling.<br><br>* Fixed the issue of possible data corruption or result timeout when executing SINTER, SINTERSTORE, SUNION, SUNIONSTORE, SDIFF, SDIFFSTORE commands. |
|proxy_version_1.14.0 |2024\-02\-06 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where the SUBSCRIBE command could not receive subsequent PUBLISH messages after a primary\-secondary switchover. |

**2023**

|Version number |Release date |Type |Description |
|---|---|---|---|
|proxy_version_1.12.0 |2023\-11\-28 |New features |None. |
|||Feature enhancement |Instances with sharding cluster disabled supported using BY or GET fields in SORT commands. |
|||Bug fixes |* Fixes the issue where SDIFFSTORE or SUNIONSTORE commands returned an incorrect format in a few scenarios.<br><br>* Fixes the issue where a single command still prompted for insufficient permissions when `+<single command>` was used in ACL rules. |
|proxy_version_1.11.1 |2023\-09\-21 |New features |Supported using the TYPE field in the SCAN command. |
|||Feature enhancement |After enabling read/write splitting mode for Redis instance, the SCAN command is only sent to the primary node for execution. |
|||Bug fixes |None. |
|proxy_version_1.10.0 |2023\-09\-04 |New features |* Supported splitting commands from different slots within a transaction to different shards.<br><br>   > **tip**<br>   <br><br>   * > Transaction atomicity cannot be guaranteed after transactions are split into different shards.<br>   <br><br>   * > To use the above features, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support for parameter settings.<br>   <br><br>* Supported using the following fields in the INFO command:<br><br>   Server、Cluster、Stats、Memory、CPU、Keyspace、Commandstats、Replication。 |
|||Feature enhancement |When executing transaction commands on instances with sharding cluster enabled by connecting via public or private network addresses, the WATCH command is no longer required before the transaction commands. For more details, refer to [Transaction command limits](https://docs.byteplus.com/en/docs/redis/command-limit#.5LqL5Yqh5ZG95Luk6ZmQ5Yi2). |
|||Bug fixes |Fixed the issue where Lua commands (including KEYS, EVAL, EVALSHA) created redundant connections in pipeline scenarios. |

## Server version release log

### Redis 7.0

**2026**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_7.608.0<br><br> <br><br> |2026\-10\-15 |New features |Added support for the atomic slot migrate feature, enabling lossless slot migration. |
|||Feature enhancement |Optimized server performance in some scenarios. |
|||Bug fixes |Fixed security vulnerabilities [CVE-2026-25588](https://www.cve.org/CVERecord?id=CVE-2026-25588) and [CVE-2026-25589](https://www.cve.org/CVERecord?id=CVE-2026-25589). |
|server_version_7.604.0<br><br> <br><br> |2026\-05\-28<br><br> |New features |* **New support for server audit logs**: Added support for Server node\-level audit log functionality, enhancing the system's security auditing capabilities.<br><br>* **Added support for XSETID command**: Added support for the XSETID command.<br><br>* **Added support for JSON extension module**: Added support for the JSON extension module, enhancing the processing capability for semi\-structured data. |
|||Feature enhancement |* **Support lua script persistence and replication**: Supports incorporating Lua scripts into AOF persistence files and synchronous replication links, ensuring script data consistency in persistence and high\-availability scenarios.<br><br>* **Optimize monitoring metric data**: Calibrate and optimize monitoring metrics (total QPS, write QPS, and read QPS) for server nodes. |
|||Bug fixes |None. |
|server_version_7.602.0<br><br> <br><br> |2026\-04\-13<br><br> |New features |* **Added QPS monitoring metrics for server nodes**: Includes total QPS, write QPS, and read QPS monitoring metrics. |
|||Feature enhancement |None. |
|||Bug fixes |None. |
|server_version_7.512.0<br><br> <br><br> |2026\-01\-26<br><br> |New features |None. |
|||Feature enhancement |Support for Lua script persistence and replication. |
|||Bug fixes |Fixed the issue of abnormal CPU usage caused by the ZADD command in certain scenarios. |

**2025**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_7.511.0<br><br> <br><br> |2025\-12\-22<br><br> |New features |Supported the [Valkey-Search](https://docs.byteplus.com/en/docs/redis/valkey-search) extension module.<br><br>> **tip**<br><br><br>> To use the Valkey\-Search feature, [submit a ticket](https://console.byteplus.com/workorder/create/) and contact technical support to apply for usage.<br> |
|||Feature enhancement |None. |
|||Bug fixes |None. |
|server_version_7.508.3<br><br> <br><br> |2025\-11\-18<br><br> |New features |None. |
|||Feature enhancement |Enhanced stability. |
|||Bug fixes |None. |
|server_version_7.508.2<br><br> <br><br> |2025\-10\-17<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed [CVE-2025-49844 (RediShell)](https://github.com/raminfp/redis_exploit#cve-2025-49844-redishell---lab-environment) security vulnerability. |
|server_version_7.507.0<br><br> <br><br> |2025\-08\-26<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the following security vulnerabilities:<br><br><br>* [CVE-2025-32023](https://github.com/redis/redis/security/advisories/GHSA-rp2m-q4j6-gr43)<br><br>* [CVE-2025-21605](https://github.com/redis/redis/security/advisories/GHSA-r67f-p999-2gff) |
|server_version_7.505.0 |2025\-06\-24 |New features |None |
|||Feature enhancement |For non\-String type keys, estimated memory usage values are now displayed in the **Memory usage(Bytes)**  column of big key analysis results; however, this value is for reference only. For more details, refer to [Big key analysis](https://docs.byteplus.com/en/docs/redis/big-key-analysis). |
|||Bug fixes |None. |

**2024**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_7.18.0 |2024\-12\-26 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the following security vulnerabilities:<br><br><br>* [CVE-2023-41056](https://github.com/redis/redis/security/advisories/GHSA-xr47-pcmx-fq2m)<br><br>* [CVE-2023-36824](https://github.com/redis/redis/security/advisories/GHSA-4cfx-h9gq-xpx3)<br><br>* [CVE-2022-24834](https://github.com/redis/redis/security/advisories/GHSA-p8x2-9v9q-c838)<br><br>* [CVE- 2023-25155](https://access.redhat.com/security/cve/cve-2023-25155)<br><br>* [CVE-2023-28425](https://access.redhat.com/security/cve/cve-2023-28425)<br><br>* [CVE-2023-22458](https://access.redhat.com/security/cve/cve-2023-22458)<br><br>* [CVE-2022-36021](https://access.redhat.com/security/cve/cve-2022-36021)<br><br>* [CVE-2022-35977](https://access.redhat.com/security/cve/cve-2022-35977) |
|server_version_7.15.0 |2024\-09\-12 |New features |None. |
|||Feature enhancement |Optimized the `redis_version` return for the INFO command, changing it from an internal version number to the Redis community branch version number. |
|||Bug fixes |None. |
|server_version_7.14.0 |2024\-08\-08 |New features |None |
|||Feature enhancement |Enhanced stability. |
|||Bug fixes |None |
|server_version_7.13.0 |2024\-07\-10 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where the WAIT command might return an error in some scenarios. |
|server_version_7.12.0 |2024\-06\-13 |New features |None. |
|||Feature enhancement |Optimized hot key statistics, which support modifying the hot key sampling frequency to improve the accuracy of hot key judgment.<br><br>> **tip**<br><br><br>> To modify the hot key sampling frequency, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |
|||Bug fixes |None. |
|server_version_7.10.0 |2024\-02\-06 |New features |None. |
|||Feature enhancement |Optimized for inherent Fork issues in native Redis, reducing performance fluctuations. |
|||Bug fixes |None. |

### Redis 6.0

**2026**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_6.608.0<br><br> <br><br> |2026\-10\-15 |New features |Added support for the atomic slot migrate feature, enabling lossless slot migration. |
|||Feature enhancement |Optimized server performance in some scenarios. |
|||Bug fixes |None. |
|server_version_6.512.00<br><br> <br><br> |2026\-01\-26<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Under the RESP3 protocol, the return type of SRANDMEMBER changes from Set to Array to support returning duplicate elements when the COUNT parameter is negative. |

**2025**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_6.508.2<br><br> <br><br> |2025\-10\-17<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed [CVE-2025-49844 (RediShell)](https://github.com/raminfp/redis_exploit#cve-2025-49844-redishell---lab-environment) security vulnerability. |
|server_version_6.506.0<br><br> <br><br> |2025\-07\-16<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the [CVE-2022-24834](https://github.com/redis/redis/security/advisories/GHSA-p8x2-9v9q-c838) security vulnerability. |

**2024**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_6.15.0 |2024\-09\-12 |New features |None. |
|||Feature enhancement |Optimized the `redis_version` return for the INFO command, changing it from an internal version number to the Redis community branch version number. |
|||Bug fixes |None. |
|server_version_6.14.0 |2024\-08\-08 |New features |None |
|||Feature enhancement |Enhanced stability. |
|||Bug fixes |None |
|server_version_6.13.0 |2024\-07\-10 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where the WAIT command might return an error in some scenarios. |
|server_version_6.12.0 |2024\-06\-13 |New features |None. |
|||Feature enhancement |Optimized hot key statistics, which support modifying the hot key sampling frequency to improve the accuracy of hot key judgment.<br><br>> **tip**<br><br><br>> To modify the hot key sampling frequency, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |
|||Bug fixes |None. |
|server_version_6.10.0 |2024\-02\-06 |New features |None. |
|||Feature enhancement |Optimized for inherent Fork issues in native Redis, reducing performance fluctuations. |
|||Bug fixes |None. |

**2023**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_6.9.2 |2023\-11\-28 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where executing commands with Lua scripts in instance with sharding cluster enabled would bypass slot verification, preventing keys not belonging to the current server from being written to the server shard. |
|server_version_6.9.0 |2023\-09\-21 |New features |None. |
|||Feature enhancement |Optimized server fault tolerance in the event of disk failures. |
|||Bug fixes |None. |
|server_version_6.8.0 |2023\-09\-04 |New features |None. |
|||Feature enhancement |Optimized hot key statistics logic for more accurate hot key analysis results. |
|||Bug fixes |None. |

### Redis 5.0

**2026**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_5.608.0<br><br> <br><br> |2026\-10\-15 |New features |Added support for the atomic slot migrate feature, enabling lossless slot migration. |
|||Feature enhancement |Optimized server performance in some scenarios. |
|||Bug fixes |None. |

**2025**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_5.508.2<br><br> <br><br> |2025\-10\-17<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed [CVE-2025-49844 (RediShell)](https://github.com/raminfp/redis_exploit#cve-2025-49844-redishell---lab-environment) security vulnerability. |
|server_version_5.506.0<br><br> <br><br> |2025\-07\-16<br><br> |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the [CVE-2022-24834](https://github.com/redis/redis/security/advisories/GHSA-p8x2-9v9q-c838) security vulnerability. |

**2024**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_5.15.0 |2024\-09\-12 |New features |None. |
|||Feature enhancement |Optimized the `redis_version` return for the INFO command, changing it from an internal version number to the Redis community branch version number. |
|||Bug fixes |None. |
|server_version_5.14.0 |2024\-08\-08 |New features |None |
|||Feature enhancement |Enhanced stability. |
|||Bug fixes |None |
|server_version_5.13.0 |2024\-07\-10 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where the WAIT command might return an error in some scenarios. |
|server_version_5.12.0 |2024\-06\-13 |New features |None. |
|||Feature enhancement |Optimized hot key statistics, which support modifying the hot key sampling frequency to improve the accuracy of hot key judgment.<br><br>> **tip**<br><br><br>> To modify the hot key sampling frequency, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support.<br> |
|||Bug fixes |None. |
|server_version_5.11.0 |2024\-04\-11 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |* Fixed the memory leak issue that occurred when both the `noack` and `block` fields were used simultaneously in the XREADGROUP command.<br><br>* Fixed the issue where Stream type keys, when TTL was set, would cause a server coredump when expired keys were automatically deleted after a consumer group was created and deleted using XGROUP\-related commands. |
|server_version_5.10.0 |2024\-02\-06 |New features |None. |
|||Feature enhancement |Optimized for inherent Fork issues in native Redis, reducing performance fluctuations. |
|||Bug fixes |None. |

**2023**

|Version number |Release date |Type |Description |
|---|---|---|---|
|server_version_5.9.2 |2023\-11\-28 |New features |None. |
|||Feature enhancement |None. |
|||Bug fixes |Fixed the issue where executing commands with Lua scripts in instance with sharding cluster enabled would bypass slot verification, preventing keys not belonging to the current server from being written to the server shard. |
|server_version_5.9.0 |2023\-09\-21 |New features |None. |
|||Feature enhancement |Optimized server fault tolerance in the event of disk failures. |
|||Bug fixes |None. |
|server_version_5.8.0 |2023\-09\-04 |New features |None. |
|||Feature enhancement |Optimized hot key statistics logic for more accurate hot key analysis results. |
|||Bug fixes |None. |
