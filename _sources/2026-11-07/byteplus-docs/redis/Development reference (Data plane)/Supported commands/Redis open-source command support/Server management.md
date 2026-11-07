---
title: "Server management"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Server_management"
---

This article summarizes the support of Server management command family by different engine versions and architecture types of Cache for Redis instances.

## Precautions

* Regarding the identification in the table, the instructions are as follows:

   * ✔️ : The command is supported in the current scenario.

   * ❌ : The command is not supported in the current scenario.

   * ➖ : This command is not supported in this version of native Redis. For example, in native Redis, the BITFIELD_RO command is only supported in versions 6.0 and above, and the command is marked as ➖ in version 5.0 of the table.

* For more details about the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/command-limit).

* This document's command support is based on the latest database kernel minor version; some commands require upgrading to a specified minor version to be used. For more details about kernel minor versions, refer to [Database minor version upgrade release logs](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log).

* Cache for Redis supports Lua\-related commands. For more details about basic Lua script syntax, usage restrictions, and recommendations, refer to [Lua scripting guide](https://docs.byteplus.com/en/docs/redis/lua-user-guide).

* To be compatible with some client side frameworks, executing the CONFIG SET command only backs OK, but does not actually modify the parameters.

* Supports returning the actual client IP address via the MONITOR command. To use it, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to apply for usage.

## Command support table

**Redis 7.0**

|**command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|ACL CAT |❌ |❌ |❌ |❌ |
|ACL DELUSER |❌ |❌ |❌ |❌ |
|ACL DRYRUN |❌ |❌ |❌ |❌ |
|ACL GENPASS |❌ |❌ |❌ |❌ |
|ACL GETUSER |❌ |❌ |❌ |❌ |
|ACL HELP |❌ |❌ |❌ |✔️ |
|ACL LIST |❌ |❌ |❌ |❌ |
|ACL LOAD |❌ |❌ |❌ |❌ |
|ACL LOG |❌ |❌ |❌ |❌ |
|ACL SAVE |❌ |❌ |❌ |❌ |
|ACL SETUSER |❌ |❌ |❌ |❌ |
|ACL USERS |❌ |❌ |❌ |❌ |
|ACL WHOAMI |❌ |❌ |❌ |❌ |
|BGREWRITEAOF |❌ |❌ |❌ |❌ |
|BGSAVE |❌ |❌ |❌ |❌ |
|COMMAND |✔️ |✔️ |✔️ |✔️ |
|COMMAND COUNT |✔️ |✔️ |✔️ |✔️ |
|COMMAND DOCS |✔️ |✔️ |✔️ |✔️ |
|COMMAND GETKEYS |✔️ |✔️ |✔️ |✔️ |
|COMMAND GETKEYSANDFLAGS |✔️ |✔️ |✔️ |✔️ |
|COMMAND INFO |✔️ |✔️ |✔️ |✔️ |
|COMMAND LIST |✔️ |✔️ |✔️ |✔️ |
|CONFIG GET |✔️ |✔️ |✔️ |❌ |
|CONFIG HELP |✔️ |❌ |✔️ |✔️ |
|CONFIG RESETSTAT |✔️ |✔️ |❌ |❌ |
|CONFIG REWRITE |❌ |❌ |❌ |❌ |
|CONFIG SET |✔️ |✔️ |✔️ |❌ |
|DBSIZE |✔️ |✔️ |✔️ |✔️ |
|DEBUG OBJECT |❌ |❌ |❌ |❌ |
|DEBUG SEGFAULT |❌ |❌ |❌ |❌ |
|FAILOVER |❌ |❌ |❌ |❌ |
|FLUSHALL |✔️ |✔️ |✔️ |✔️ |
|FLUSHDB |✔️ |✔️ |✔️ |✔️ |
|INFO |✔️ |✔️ |✔️ |✔️ |
|LASTSAVE |✔️ |❌ |✔️ |✔️ |
|LATENCY DOCTOR |✔️ |❌ |❌ |❌ |
|LATENCY GRAPH |✔️ |❌ |❌ |❌ |
|LATENCY HELP |✔️ |❌ |❌ |✔️ |
|LATENCY HISTOGRAM |✔️ |❌ |❌ |❌ |
|LATENCY HISTORY |✔️ |❌ |❌ |❌ |
|LATENCY LATEST |✔️ |❌ |❌ |❌ |
|LATENCY RESET |✔️ |❌ |❌ |❌ |
|LOLWUT |✔️ |✔️ |✔️ |✔️ |
|MEMORY DOCTOR |✔️ |✔️ |❌ |✔️ |
|MEMORY HELP |✔️ |✔️ |❌ |✔️ |
|MEMORY MALLOC\-STATS |✔️ |✔️ |❌ |✔️ |
|MEMORY PURGE |✔️ |✔️ |❌ |✔️ |
|MEMORY STATS |✔️ |✔️ |❌ |✔️ |
|MEMORY USAGE |✔️ |✔️ |✔️ |✔️ |
|MODULE LIST |❌ |❌ |❌ |❌ |
|MODULE LOAD |❌ |❌ |❌ |❌ |
|MODULE LOADEX |❌ |❌ |❌ |❌ |
|MODULE UNLOAD |❌ |❌ |❌ |❌ |
|MONITOR |✔️ |✔️ |✔️ |❌ |
|PSYNC |❌ |❌ |❌ |❌ |
|REPLICAOF |❌ |❌ |❌ |❌ |
|ROLE |✔️ |✔️ |✔️ |❌ |
|SAVE |❌ |❌ |❌ |❌ |
|SHUTDOWN |❌ |❌ |❌ |❌ |
|SLAVEOF |❌ |❌ |❌ |❌ |
|SLOWLOG GET |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG LEN |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG HELP |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG RESET |✔️ |✔️ |✔️ |✔️ |
|SWAPDB |✔️ |✔️ |✔️ |✔️ |
|SYNC |❌ |❌ |❌ |❌ |
|TIME |✔️ |✔️ |✔️ |✔️ |

**Redis 6.0**

|**command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|ACL CAT |❌ |❌ |❌ |❌ |
|ACL DELUSER |❌ |❌ |❌ |❌ |
|ACL DRYRUN |➖ |➖ |➖ |➖ |
|ACL GENPASS |❌ |❌ |❌ |❌ |
|ACL GETUSER |❌ |❌ |❌ |❌ |
|ACL HELP |❌ |❌ |❌ |❌ |
|ACL LIST |❌ |❌ |❌ |❌ |
|ACL LOAD |❌ |❌ |❌ |❌ |
|ACL LOG |❌ |❌ |❌ |❌ |
|ACL SAVE |❌ |❌ |❌ |❌ |
|ACL SETUSER |❌ |❌ |❌ |❌ |
|ACL USERS |❌ |❌ |❌ |❌ |
|ACL WHOAMI |❌ |❌ |❌ |❌ |
|BGREWRITEAOF |❌ |❌ |❌ |❌ |
|BGSAVE |❌ |❌ |❌ |❌ |
|COMMAND |✔️ |✔️ |✔️ |✔️ |
|COMMAND COUNT |✔️ |✔️ |✔️ |✔️ |
|COMMAND DOCS |➖ |➖ |➖ |➖ |
|COMMAND GETKEYS |✔️ |✔️ |✔️ |✔️ |
|COMMAND GETKEYSANDFLAGS |➖ |➖ |➖ |➖ |
|COMMAND INFO |✔️ |✔️ |✔️ |✔️ |
|COMMAND LIST |➖ |➖ |➖ |➖ |
|CONFIG GET |✔️ |✔️ |✔️ |❌ |
|CONFIG HELP |✔️ |❌ |✔️ |❌ |
|CONFIG RESETSTAT |✔️ |✔️ |❌ |❌ |
|CONFIG REWRITE |❌ |❌ |❌ |❌ |
|CONFIG SET |✔️ |✔️ |✔️ |❌ |
|DBSIZE |✔️ |✔️ |✔️ |✔️ |
|DEBUG OBJECT |❌ |❌ |❌ |❌ |
|DEBUG SEGFAULT |❌ |❌ |❌ |❌ |
|FAILOVER |➖ |➖ |➖ |➖ |
|FLUSHALL |✔️ |✔️ |✔️ |✔️ |
|FLUSHDB |✔️ |✔️ |✔️ |✔️ |
|INFO |✔️ |✔️ |✔️ |✔️ |
|LASTSAVE |✔️ |❌ |✔️ |✔️ |
|LATENCY DOCTOR |✔️ |❌ |❌ |❌ |
|LATENCY GRAPH |✔️ |❌ |❌ |❌ |
|LATENCY HELP |✔️ |❌ |❌ |❌ |
|LATENCY HISTOGRAM |➖ |➖ |➖ |➖ |
|LATENCY HISTORY |✔️ |❌ |❌ |❌ |
|LATENCY LATEST |✔️ |❌ |❌ |❌ |
|LATENCY RESET |✔️ |❌ |❌ |❌ |
|LOLWUT |✔️ |✔️ |✔️ |✔️ |
|MEMORY DOCTOR |✔️ |✔️ |❌ |✔️ |
|MEMORY HELP |✔️ |✔️ |❌ |✔️ |
|MEMORY MALLOC\-STATS |✔️ |✔️ |❌ |✔️ |
|MEMORY PURGE |✔️ |✔️ |❌ |✔️ |
|MEMORY STATS |✔️ |✔️ |❌ |✔️ |
|MEMORY USAGE |✔️ |✔️ |✔️ |✔️ |
|MODULE LIST |❌ |❌ |❌ |❌ |
|MODULE LOAD |❌ |❌ |❌ |❌ |
|MODULE LOADEX |➖ |➖ |➖ |➖ |
|MODULE UNLOAD |❌ |❌ |❌ |❌ |
|MONITOR |✔️ |✔️ |✔️ |❌ |
|PSYNC |❌ |❌ |❌ |❌ |
|REPLICAOF |❌ |❌ |❌ |❌ |
|ROLE |✔️ |✔️ |✔️ |❌ |
|SAVE |❌ |❌ |❌ |❌ |
|SHUTDOWN |❌ |❌ |❌ |❌ |
|SLAVEOF |❌ |❌ |❌ |❌ |
|SLOWLOG GET |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG LEN |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG HELP |➖ |➖ |➖ |➖ |
|SLOWLOG RESET |✔️ |✔️ |✔️ |✔️ |
|SWAPDB |✔️ |✔️ |✔️ |✔️ |
|SYNC |❌ |❌ |❌ |❌ |
|TIME |✔️ |✔️ |✔️ |✔️ |

**Redis 5.0**

|**command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|ACL CAT |➖ |➖ |➖ |➖ |
|ACL DELUSER |➖ |➖ |➖ |➖ |
|ACL DRYRUN |➖ |➖ |➖ |➖ |
|ACL GENPASS |➖ |➖ |➖ |➖ |
|ACL GETUSER |➖ |➖ |➖ |➖ |
|ACL HELP |➖ |➖ |➖ |➖ |
|ACL LIST |➖ |➖ |➖ |➖ |
|ACL LOAD |➖ |➖ |➖ |➖ |
|ACL LOG |➖ |➖ |➖ |➖ |
|ACL SAVE |➖ |➖ |➖ |➖ |
|ACL SETUSER |➖ |➖ |➖ |➖ |
|ACL USERS |➖ |➖ |➖ |➖ |
|ACL WHOAMI |➖ |➖ |➖ |➖ |
|BGREWRITEAOF |❌ |❌ |❌ |❌ |
|BGSAVE |❌ |❌ |❌ |❌ |
|COMMAND |✔️ |✔️ |✔️ |✔️ |
|COMMAND COUNT |✔️ |✔️ |✔️ |✔️ |
|COMMAND DOCS |➖ |➖ |➖ |➖ |
|COMMAND GETKEYS |✔️ |✔️ |✔️ |✔️ |
|COMMAND GETKEYSANDFLAGS |➖ |➖ |➖ |➖ |
|COMMAND INFO |✔️ |✔️ |✔️ |✔️ |
|COMMAND LIST |➖ |➖ |➖ |➖ |
|CONFIG GET |✔️ |✔️ |✔️ |❌ |
|CONFIG HELP |✔️ |❌ |✔️ |❌ |
|CONFIG RESETSTAT |✔️ |✔️ |❌ |❌ |
|CONFIG REWRITE |❌ |❌ |❌ |❌ |
|CONFIG SET |✔️ |✔️ |✔️ |❌ |
|DBSIZE |✔️ |✔️ |✔️ |✔️ |
|DEBUG OBJECT |❌ |❌ |❌ |❌ |
|DEBUG SEGFAULT |❌ |❌ |❌ |❌ |
|FAILOVER |➖ |➖ |➖ |➖ |
|FLUSHALL |✔️ |✔️ |✔️ |✔️ |
|FLUSHDB |✔️ |✔️ |✔️ |✔️ |
|INFO |✔️ |✔️ |✔️ |✔️ |
|LASTSAVE |✔️ |❌ |✔️ |✔️ |
|LATENCY DOCTOR |✔️ |❌ |❌ |❌ |
|LATENCY GRAPH |✔️ |❌ |❌ |❌ |
|LATENCY HELP |✔️ |❌ |❌ |❌ |
|LATENCY HISTOGRAM |➖ |➖ |➖ |➖ |
|LATENCY HISTORY |✔️ |❌ |❌ |❌ |
|LATENCY LATEST |✔️ |❌ |❌ |❌ |
|LATENCY RESET |✔️ |❌ |❌ |❌ |
|LOLWUT |✔️ |✔️ |✔️ |✔️ |
|MEMORY DOCTOR |✔️ |✔️ |❌ |✔️ |
|MEMORY HELP |✔️ |✔️ |❌ |✔️ |
|MEMORY MALLOC\-STATS |✔️ |✔️ |❌ |✔️ |
|MEMORY PURGE |✔️ |✔️ |❌ |✔️ |
|MEMORY STATS |✔️ |✔️ |❌ |✔️ |
|MEMORY USAGE |✔️ |✔️ |✔️ |✔️ |
|MODULE LIST |❌ |❌ |❌ |❌ |
|MODULE LOAD |❌ |❌ |❌ |❌ |
|MODULE LOADEX |➖ |➖ |➖ |➖ |
|MODULE UNLOAD |❌ |❌ |❌ |❌ |
|MONITOR |✔️ |✔️ |✔️ |❌ |
|PSYNC |❌ |❌ |❌ |❌ |
|REPLICAOF |❌ |❌ |❌ |❌ |
|ROLE |✔️ |✔️ |✔️ |❌ |
|SAVE |❌ |❌ |❌ |❌ |
|SHUTDOWN |❌ |❌ |❌ |❌ |
|SLAVEOF |❌ |❌ |❌ |❌ |
|SLOWLOG GET |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG LEN |✔️ |✔️ |✔️ |✔️ |
|SLOWLOG HELP |➖ |➖ |➖ |➖ |
|SLOWLOG RESET |✔️ |✔️ |✔️ |✔️ |
|SWAPDB |✔️ |✔️ |✔️ |✔️ |
|SYNC |❌ |❌ |❌ |❌ |
|TIME |✔️ |✔️ |✔️ |✔️ |
