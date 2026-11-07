---
title: "Cluster management"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Cluster_management"
---

This article summarizes the support of Cluster management command family by different engine versions and architecture types of Cache for Redis instances.

<span id="8xjVHN69"></span>
## Precautions


* Regarding the identification in the table, the instructions are as follows:

   * ✔️ : The command is supported in the current scenario.

   * ❌ : The command is not supported in the current scenario.

   * ➖ : This command is not supported in this version of native Redis. For example, in native Redis, the BITFIELD_RO command is only supported in versions 6.0 and above, and the command is marked as ➖ in version 5.0 of the table.

* For more details about the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/command-limit).

* This document's command support is based on the latest database kernel minor version; some commands require upgrading to a specified minor version to be used. For more details about kernel minor versions, refer to [Database minor version upgrade release logs](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log).

* Cache for Redis supports Lua\-related commands. For more details about basic Lua script syntax, usage restrictions, and recommendations, refer to [Lua scripting guide](https://docs.byteplus.com/en/docs/redis/lua-user-guide).

* The commands in the Cluster management command family do not apply to Redis instances with sharding cluster disabled.


<span id="br4mzB8B"></span>
## Command support table


<Tabs>
<Tab zoneid="Hz40uKXFcZ" title="Redis 7.0">
<TabTitle>Redis 7.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|CLUSTER ADDSLOTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER ADDSLOTSRANGE |❌ |❌ |❌ |✔️ |
|CLUSTER BUMPEPOCH |❌ |❌ |❌ |✔️ |
|CLUSTER COUNT\-FAILURE\-REPORTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER COUNTKEYSINSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER DELSLOTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER DELSLOTSRANGE |❌ |❌ |❌ |✔️ |
|CLUSTER FAILOVER |❌ |✔️ |✔️ |✔️ |
|CLUSTER FLUSHSLOTS |❌ |❌ |❌ |✔️ |
|CLUSTER FORGET |❌ |✔️ |✔️ |✔️ |
|CLUSTER GETKEYSINSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER INFO |❌ |✔️ |✔️ |✔️ |
|CLUSTER KEYSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER LINKS |❌ |❌ |❌ |✔️ |
|CLUSTER MEET |❌ |✔️ |✔️ |✔️ |
|CLUSTER MYID |❌ |❌ |❌ |✔️ |
|CLUSTER MYSHARDID |➖ |➖ |➖ |➖ |
|CLUSTER NODES |❌ |✔️ |✔️ |✔️ |
|CLUSTER REPLICAS |❌ |❌ |❌ |✔️ |
|CLUSTER REPLICATE |❌ |✔️ |✔️ |✔️ |
|CLUSTER RESET |❌ |✔️ |✔️ |❌ |
|CLUSTER SAVECONFIG |❌ |✔️ |✔️ |✔️ |
|CLUSTER SET\-CONFIG\-EPOCH |❌ |✔️ |✔️ |✔️ |
|CLUSTER SETSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER SHARDS |❌ |❌ |❌ |✔️ |
|CLUSTER SLAVES |❌ |✔️ |✔️ |✔️ |
|CLUSTER SLOTS |❌ |✔️ |✔️ |✔️ |





</Tab>
<Tab zoneid="cLrHTQoiZy" title="Redis 6.0">
<TabTitle>Redis 6.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|CLUSTER ADDSLOTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER ADDSLOTSRANGE |➖ |➖ |➖ |➖ |
|CLUSTER BUMPEPOCH |❌ |❌ |❌ |✔️ |
|CLUSTER COUNT\-FAILURE\-REPORTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER COUNTKEYSINSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER DELSLOTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER DELSLOTSRANGE |➖ |➖ |➖ |➖ |
|CLUSTER FAILOVER |❌ |✔️ |✔️ |✔️ |
|CLUSTER FLUSHSLOTS |❌ |❌ |❌ |✔️ |
|CLUSTER FORGET |❌ |✔️ |✔️ |✔️ |
|CLUSTER GETKEYSINSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER INFO |❌ |✔️ |✔️ |✔️ |
|CLUSTER KEYSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER LINKS |➖ |➖ |➖ |✔️ |
|CLUSTER MEET |❌ |✔️ |✔️ |✔️ |
|CLUSTER MYID |❌ |❌ |❌ |✔️ |
|CLUSTER MYSHARDID |➖ |➖ |➖ |➖ |
|CLUSTER NODES |❌ |✔️ |✔️ |✔️ |
|CLUSTER REPLICAS |❌ |❌ |❌ |✔️ |
|CLUSTER REPLICATE |❌ |✔️ |✔️ |✔️ |
|CLUSTER RESET |❌ |✔️ |✔️ |✔️ |
|CLUSTER SAVECONFIG |❌ |✔️ |✔️ |✔️ |
|CLUSTER SET\-CONFIG\-EPOCH |❌ |✔️ |✔️ |✔️ |
|CLUSTER SETSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER SHARDS |➖ |➖ |➖ |➖ |
|CLUSTER SLAVES |❌ |✔️ |✔️ |✔️ |
|CLUSTER SLOTS |❌ |✔️ |✔️ |✔️ |





</Tab>
<Tab zoneid="AmbHk1dq0J" title="Redis 5.0">
<TabTitle>Redis 5.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|CLUSTER ADDSLOTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER ADDSLOTSRANGE |➖ |➖ |➖ |➖ |
|CLUSTER BUMPEPOCH |❌ |❌ |❌ |✔️ |
|CLUSTER COUNT\-FAILURE\-REPORTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER COUNTKEYSINSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER DELSLOTS |❌ |✔️ |✔️ |✔️ |
|CLUSTER DELSLOTSRANGE |➖ |➖ |➖ |➖ |
|CLUSTER FAILOVER |❌ |✔️ |✔️ |✔️ |
|CLUSTER FLUSHSLOTS |❌ |❌ |❌ |✔️ |
|CLUSTER FORGET |❌ |✔️ |✔️ |✔️ |
|CLUSTER GETKEYSINSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER INFO |❌ |✔️ |✔️ |✔️ |
|CLUSTER KEYSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER LINKS |➖ |➖ |➖ |✔️ |
|CLUSTER MEET |❌ |✔️ |✔️ |✔️ |
|CLUSTER MYID |❌ |❌ |❌ |✔️ |
|CLUSTER MYSHARDID |➖ |➖ |➖ |➖ |
|CLUSTER NODES |❌ |✔️ |✔️ |✔️ |
|CLUSTER REPLICAS |❌ |❌ |❌ |✔️ |
|CLUSTER REPLICATE |❌ |✔️ |✔️ |✔️ |
|CLUSTER RESET |❌ |✔️ |✔️ |✔️ |
|CLUSTER SAVECONFIG |❌ |✔️ |✔️ |✔️ |
|CLUSTER SET\-CONFIG\-EPOCH |❌ |✔️ |✔️ |✔️ |
|CLUSTER SETSLOT |❌ |✔️ |✔️ |✔️ |
|CLUSTER SHARDS |➖ |➖ |➖ |➖ |
|CLUSTER SLAVES |❌ |✔️ |✔️ |✔️ |
|CLUSTER SLOTS |❌ |✔️ |✔️ |✔️ |





</Tab>
</Tabs>
