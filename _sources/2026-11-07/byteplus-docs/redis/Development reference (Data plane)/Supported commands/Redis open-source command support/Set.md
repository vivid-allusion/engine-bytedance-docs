---
title: "Set"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Set"
---

This article summarizes the support of Set command family by different engine versions and architecture types of Cache for Redis instances.

<span id="ZfjUotRw"></span>
## Precautions


* Regarding the identification in the table, the instructions are as follows:

   * ✔️ : The command is supported in the current scenario.

   * ❌ : The command is not supported in the current scenario.

   * ➖ : This command is not supported in this version of native Redis. For example, in native Redis, the BITFIELD_RO command is only supported in versions 6.0 and above, and the command is marked as ➖ in version 5.0 of the table.

* For more details about the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/command-limit).

* This document's command support is based on the latest database kernel minor version; some commands require upgrading to a specified minor version to be used. For more details about kernel minor versions, refer to [Database minor version upgrade release logs](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log).

* Cache for Redis supports Lua\-related commands. For more details about basic Lua script syntax, usage restrictions, and recommendations, refer to [Lua scripting guide](https://docs.byteplus.com/en/docs/redis/lua-user-guide).


<span id="DYXxMjxv"></span>
## Command support table


<Tabs>
<Tab zoneid="Z6GDrI7d" title="Redis 7.0">
<TabTitle>Redis 7.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|SADD |✔️ |✔️ |✔️ |✔️ |
|SCARD |✔️ |✔️ |✔️ |✔️ |
|SDIFF |✔️ |✔️ |✔️ |✔️ |
|SDIFFSTORE |✔️ |✔️ |✔️ |✔️ |
|SINTER |✔️ |✔️ |✔️ |✔️ |
|SINTERCARD |✔️ |✔️ |✔️ |✔️ |
|SINTERSTORE |✔️ |✔️ |✔️ |✔️ |
|SISMEMBER |✔️ |✔️ |✔️ |✔️ |
|SMEMBERS |✔️ |✔️ |✔️ |✔️ |
|SMISMEMBER |✔️ |✔️ |✔️ |✔️ |
|SMOVE |✔️ |✔️ |✔️ |✔️ |
|SPOP |✔️ |✔️ |✔️ |✔️ |
|SRANDMEMBER |✔️ |✔️ |✔️ |✔️ |
|SREM |✔️ |✔️ |✔️ |✔️ |
|SSCAN |✔️ |✔️ |✔️ |✔️ |
|SUNION |✔️ |✔️ |✔️ |✔️ |
|SUNIONSTORE |✔️ |✔️ |✔️ |✔️ |





</Tab>
<Tab zoneid="rOQVRDqV" title="Redis 6.0">
<TabTitle>Redis 6.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|SADD |✔️ |✔️ |✔️ |✔️ |
|SCARD |✔️ |✔️ |✔️ |✔️ |
|SDIFF |✔️ |✔️ |✔️ |✔️ |
|SDIFFSTORE |✔️ |✔️ |✔️ |✔️ |
|SINTER |✔️ |✔️ |✔️ |✔️ |
|SINTERCARD |➖ |➖ |➖ |➖ |
|SINTERSTORE |✔️ |✔️ |✔️ |✔️ |
|SISMEMBER |✔️ |✔️ |✔️ |✔️ |
|SMEMBERS |✔️ |✔️ |✔️ |✔️ |
|SMISMEMBER |✔️ |✔️ |✔️ |✔️ |
|SMOVE |✔️ |✔️ |✔️ |✔️ |
|SPOP |✔️ |✔️ |✔️ |✔️ |
|SRANDMEMBER |✔️ |✔️ |✔️ |✔️ |
|SREM |✔️ |✔️ |✔️ |✔️ |
|SSCAN |✔️ |✔️ |✔️ |✔️ |
|SUNION |✔️ |✔️ |✔️ |✔️ |
|SUNIONSTORE |✔️ |✔️ |✔️ |✔️ |





</Tab>
<Tab zoneid="EjiX8Qa7" title="Redis 5.0">
<TabTitle>Redis 5.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|SADD |✔️ |✔️ |✔️ |✔️ |
|SCARD |✔️ |✔️ |✔️ |✔️ |
|SDIFF |✔️ |✔️ |✔️ |✔️ |
|SDIFFSTORE |✔️ |✔️ |✔️ |✔️ |
|SINTER |✔️ |✔️ |✔️ |✔️ |
|SINTERCARD |➖ |➖ |➖ |➖ |
|SINTERSTORE |✔️ |✔️ |✔️ |✔️ |
|SISMEMBER |✔️ |✔️ |✔️ |✔️ |
|SMEMBERS |✔️ |✔️ |✔️ |✔️ |
|SMISMEMBER |➖ |➖ |➖ |➖ |
|SMOVE |✔️ |✔️ |✔️ |✔️ |
|SPOP |✔️ |✔️ |✔️ |✔️ |
|SRANDMEMBER |✔️ |✔️ |✔️ |✔️ |
|SREM |✔️ |✔️ |✔️ |✔️ |
|SSCAN |✔️ |✔️ |✔️ |✔️ |
|SUNION |✔️ |✔️ |✔️ |✔️ |
|SUNIONSTORE |✔️ |✔️ |✔️ |✔️ |





</Tab>
</Tabs>
