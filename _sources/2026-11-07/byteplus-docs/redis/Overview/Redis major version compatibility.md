---
title: "Redis major version compatibility"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/redis_major_version_compatibility"
---

BytePlus Cache for Redis is compatible with open\-source Redis database engines and supports multiple major versions of Redis engines. This topic describes the compatibility changes for each major version of the Redis engine.

<span id="Skjj1Mvf"></span>
### Background information

Cache for Redis supports major versions 5.0, 6.0, and 7.0 of the Redis engine, and supports upgrading or migrating low\-version instances to high\-version instances through [blue-green deployment](https://docs.byteplus.com/en/docs/redis/upgrade_major_version_using_blue_green_deployment) or [DTS data migration](https://docs.byteplus.com/en/docs/DTS/migrating_to_byteplus_cache_for_redis_redis). Before upgrading or migrating to a high\-version instance, it is recommended that you refer to the compatibility change details in this document to fully assess the business impact.

<span id="pNMDBaKI"></span>
### Major version compatibility

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The impact levels in the table below are described as follows:</div>



* <div data-tips="true" data-tips-type="default">High: Directly causes serious issues such as data import failure, application errors, or business interruption, and <strong>requires adjustments and adaptations to business code or usage methods</strong>.</div>


* <div data-tips="true" data-tips-type="default">Medium: May cause partial functional abnormalities, data inconsistency, or potential errors. It is <strong>recommended to adjust relevant business logic (for example, query code) or clear existing data</strong>.</div>


* <div data-tips="true" data-tips-type="default">Low: Primarily manifested in differences in features, performance, or O&M management methods. It generally does not directly affect core business functions, but it is recommended to understand the relevant changes and optimize usage as appropriate.</div>




<Tabs>
<Tab zoneid="a0FQCkuma6" title="Upgrade from 3.0 to 4.0">
<TabTitle>Upgrade from 3.0 to 4.0</TabTitle>


|**Category** |**Compatibility** |**Impact level** |**Business adjustment recommendations** |**Community PR** |
|---|---|---|---|---|
|Geospatial indices command group<br><br> |GEOENCODE and GEODECODE commands are no longer supported. |High<br><br> |Review and remove any business logic that depends on GEOENCODE or GEODECODE commands. |[Commit b96af59](https://github.com/redis/redis/commit/b96af595a5fddbbdcbf78ed3c51acd60976416f4) |
|Lua script<br><br> |Cluster mode prohibits constructing keys that cross local\-node slots within Lua scripts. |High<br><br> |Review and modify Lua scripts used in your business to avoid constructing keys that cross local\-node slots within Lua. |[Commit da95d22](https://github.com/redis/redis/commit/da95d22ad2e8c3232fd34a2c09c30fe74d71532a) |
|Expire and Evict |When the CLIENT PAUSE command is executed, keys will not expire or be evicted.<br><br>After prolonged execution of CLIENT PAUSE, memory overhead on secondary nodes may be slightly higher than that on the primary nodes.<br><br> |Low<br><br> |Be aware of the new behavior.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">BytePlus Cache for Redis does not support the CLIENT PAUSE command. For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/redis-open-source-command-support">Redis open\-source command support</a>.</div><br> |[Commit deeb795](https://github.com/redis/redis/commit/deeb795accaca0f6fb8ee3fcc843eeeb14e360e7) |
|Pub/Sub command group |The LREM command now triggers keyspace event notifications (that is, notifications published with the k`eyspace@<db> `prefix). |Low<br><br> |Check if your business relies on monitoring `__keyspace` channels and assess whether the monitoring results meet expectations. |[Commit 68e779f](https://github.com/redis/redis/commit/68e779f34bd7a06397ebea520f5ce43372fad000) |





</Tab>
<Tab zoneid="BpdAMwAECo" title="Upgrade from 4.0 to 5.0">
<TabTitle>Upgrade from 4.0 to 5.0</TabTitle>


|**Category** |**Compatibility** |**Impact level** |**Business adjustment recommendations** |**Community PR** |
|---|---|---|---|---|
|Expire and Evict |The KEYS command no longer proactively cleans expired keys.<br><br>The SCAN command still deletes expired keys it encounters. |Low<br><br> |Check if your business logic uses KEYS to clean expired keys. If so, replace it with SCAN. |[Commit edc47a3](https://github.com/redis/redis/commit/edc47a3a) |
||With the `volatile-lru` eviction policy enabled, Redis disables the use of shared objects (for example, for small integers like 1, 2, 3) to prevent multiple keys sharing the same object from interfering with each other's LRU metadata updates. This change increases memory overhead slightly.<br><br>However, during full primary\-secondary synchronization, secondary nodes do not apply this restriction while loading the RDB file. This can cause secondary nodes to use shared objects for keys in memory, leading to identical data content but different object encoding between primary and secondary nodes, resulting in lower actual memory usage on secondary nodes. |Low<br><br> |Be aware of the new behavior and monitor memory usage differences between primary and secondary nodes.<br><br> |* [Commit bd92389](https://github.com/redis/redis/commit/bd92389c2dc1afcf53218880fc31ba45e66f4ded)<br><br>* [Commit 0ed0dc3](https://github.com/redis/redis/commit/0ed0dc3c02dfffdf6bfb9e32f1335ddc34f37723)<br><br><br> |
|Lua script<br><br> |Lua scripts now default to effects replication (that is, replicating the commands produced by the script's execution, not the script itself) to prevent data inconsistencies caused by differing execution results on primary and secondary nodes. |Low<br><br> |Be aware of the new behavior.<br><br> |[Commit 3e1fb5f](https://github.com/redis/redis/commit/3e1fb5ff)<br><br> |
||Read\-only scripts are propagated as SCRIPT LOAD commands instead of EVAL commands. |Low |Be aware of the new behavior. |[Commit dfbce91](https://github.com/redis/redis/commit/dfbce91a) |





</Tab>
<Tab zoneid="dIFn9cdsNN" title="Upgrade from 5.0 to 6.0">
<TabTitle>Upgrade from 5.0 to 6.0</TabTitle>


|**Category** |**Compatibility** |**Impact level** |**Business adjustment recommendations** |**Community PR** |
|---|---|---|---|---|
|Propagate<br><br> |During propagation, the INCRBYFLOAT command was incorrectly rewritten as a SET command without a TTL parameter, clearing the expiration time on the target key. Version 6.0 fixes this by rewriting INCRBYFLOAT as a SET command with a TTL parameter, preserving key expiration times correctly during replication and AOF replay. |Low<br><br> |Learn about bug fixes. |[Commit 5855439](https://github.com/redis/redis/commit/58554396d6d49b2c80fcf61ce5c2ccfdc550c7c2)<br><br> |





</Tab>
<Tab zoneid="pUuNrh9N1T" title="Upgrade from 6.0 to 7.0">
<TabTitle>Upgrade from 6.0 to 7.0</TabTitle>


|**Category** |**Compatibility** |**Impact level** |**Business adjustment recommendations** |**Community PR** |
|---|---|---|---|---|
|Lua script<br><br> |Prohibit the use of global variables or global functions in Lua scripts.Global variables and functions are prohibited in Lua scripts. For example, use `redis.log` instead of `print()` in 7.0 version. |High<br><br> |Check if your scripts use global variables or functions and convert them to local ones. |[Pull 0651](https://github.com/redis/redis/pull/10651)<br><br> |
||Scripts themselves are no longer persisted or replicated. Script management commands like SCRIPT LOAD and SCRIPT FLUSH are no longer written to the replication stream or persistence logs. Additionally, the configuration option `lua-replicate-commands` has been removed, and Lua replication is now permanently set to effects replication. |Low<br><br> |BytePlus Cache for Redis supports Lua persistence. It is recommended to upgrade to Redis 7.512.0 or later.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">For more detail, refer to <a href="https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log">Database minor version upgrade release logs</a>.</div><br> |[Pull 9812](https://github.com/redis/redis/pull/9812)<br><br> |
| |Add LCS command to replace deprecated STRALGO command. |High |Check and update your business logic to use LCS instead of STRALGO. |[Pull 9799](https://github.com/redis/redis/pull/9799) |
||Optimized the return behavior of COMMAND GETKEYS for commands that do not strictly require keys. It now returns an empty array instead of an error. |Low<br><br> |Optimize command return results. |[Commit f11a2d4](https://github.com/redis/redis/commit/f11a2d4dd764c996b2d0c0cb5abde13f2445b40c) |
|Set command group |Under the RESP3 protocol, the return type of SRANDMEMBER changes from Set to Array to support returning duplicate elements when the COUNT parameter is negative. |Medium<br><br> |Be aware of the fix. Check if your business logic depends on SRANDMEMBER returning deduplicated elements. If so, adjust accordingly.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">BytePlus Cache for Redis has fixed this in Redis 6.512.0 and later versions. If you are not planning to upgrade to Redis 7.0, it is recommended to upgrade your instance to at least Redis 6.512.0.</div><br> |[Pull 8504](https://github.com/redis/redis/pull/8504)<br><br> |
||Optimized the error message when the parameter for the SPOP command is negative, making it clearer. |Low |Optimize command return results. |[Commit 09b7f6c](https://github.com/redis/redis/commit/09b7f6c2a10d5c50bad64953f9a31e04f81c0444) |
|Sorted set command group<br><br> |Optimized the return behavior of ZPOPMIN and ZPOPMAX for mismatched key types or negative COUNT parameters. These scenarios now return a clear error instead of an empty array. |Medium<br><br> |Be aware of the fix. Check if your business logic handles the return values of ZPOPMIN and ZPOPMAX appropriately. |[Pull 9711](https://github.com/redis/redis/pull/9711) |
|List command group |Optimized the error message when the `pos` parameter in the LPOS command is 0, making it clearer. |Low |Optimize command return results. |[Pull 10645](https://github.com/redis/redis/pull/10645/files) |





</Tab>
</Tabs>
