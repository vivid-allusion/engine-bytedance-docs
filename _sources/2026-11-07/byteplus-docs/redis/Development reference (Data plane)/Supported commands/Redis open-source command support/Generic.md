---
title: "Generic"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Generic"
---

This article summarizes the support of Generic command family by different engine versions and architecture types of Cache for Redis instances.

<span id="hEXrmrb0"></span>
## Precautions


* Regarding the identification in the table, the instructions are as follows:

   * ✔️ : The command is supported in the current scenario.

   * ❌ : The command is not supported in the current scenario.

   * ➖ : This command is not supported in this version of native Redis. For example, in native Redis, the BITFIELD_RO command is only supported in versions 6.0 and above, and the command is marked as ➖ in version 5.0 of the table.

* For more details about the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/command-limit).

* This document's command support is based on the latest database kernel minor version; some commands require upgrading to a specified minor version to be used. For more details about kernel minor versions, refer to [Database minor version upgrade release logs](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log).

* Cache for Redis supports Lua\-related commands. For more details about basic Lua script syntax, usage restrictions, and recommendations, refer to [Lua scripting guide](https://docs.byteplus.com/en/docs/redis/lua-user-guide).


<span id="EyToXT91"></span>
## Command support table


<Tabs>
<Tab zoneid="GNgEtIUY" title="Redis 7.0">
<TabTitle>Redis 7.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|COPY |✔️ |✔️ |✔️ |✔️ |
|DEL |✔️ |✔️ |✔️ |✔️ |
|DUMP |✔️ |✔️ |✔️ |✔️ |
|EXISTS |✔️ |✔️ |✔️ |✔️ |
|EXPIRE |✔️ |✔️ |✔️ |✔️ |
|EXPIREAT |✔️ |✔️ |✔️ |✔️ |
|EXPIRETIME |✔️ |✔️ |✔️ |✔️ |
|KEYS |✔️ |✔️ |✔️ |✔️ |
|MIGRATE |❌ |❌ |❌ |✔️ |
|MOVE |✔️ |✔️ |✔️ |✔️ |
|OBJECT ENCODING |✔️ |✔️ |✔️ |✔️ |
|OBJECT FREQ |✔️ |✔️ |✔️ |✔️ |
|OBJECT HELP |❌ |❌ |❌ |✔️ |
|OBJECT IDLETIME |✔️ |✔️ |✔️ |✔️ |
|OBJECT REFCOUNT |✔️ |✔️ |✔️ |✔️ |
|PERSIST |✔️ |✔️ |✔️ |✔️ |
|PEXPIRE |✔️ |✔️ |✔️ |✔️ |
|PEXPIREAT |✔️ |✔️ |✔️ |✔️ |
|PEXPIRETIME |✔️ |✔️ |✔️ |✔️ |
|PTTL |✔️ |✔️ |✔️ |✔️ |
|RANDOMKEY |✔️ |✔️ |✔️ |✔️ |
|RENAME |✔️ |✔️ |✔️ |✔️ |
|RENAMENX |✔️ |✔️ |✔️ |✔️ |
|RESTORE |✔️ |✔️ |✔️ |✔️ |
|SCAN |✔️ |✔️ |✔️ |✔️ |
|SORT |✔️ |✔️ |✔️ |✔️ |
|SORT_RO |✔️ |✔️ |✔️ |✔️ |
|TOUCH |✔️ |✔️ |✔️ |✔️ |
|TTL |✔️ |✔️ |✔️ |✔️ |
|TYPE |✔️ |✔️ |✔️ |✔️ |
|UNLINK |✔️ |✔️ |✔️ |✔️ |
|WAIT |✔️ |✔️ |❌ |❌ |
|WAITAOF |➖ |➖ |➖ |➖ |





</Tab>
<Tab zoneid="5ycv2lgG" title="Redis 6.0">
<TabTitle>Redis 6.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|COPY |❌ |❌ |❌ |❌ |
|DEL |✔️ |✔️ |✔️ |✔️ |
|DUMP |✔️ |✔️ |✔️ |✔️ |
|EXISTS |✔️ |✔️ |✔️ |✔️ |
|EXPIRE |✔️ |✔️ |✔️ |✔️ |
|EXPIREAT |✔️ |✔️ |✔️ |✔️ |
|EXPIRETIME |❌ |❌ |❌ |❌ |
|KEYS |✔️ |✔️ |✔️ |✔️ |
|MIGRATE |❌ |❌ |❌ |✔️ |
|MOVE |✔️ |✔️ |✔️ |✔️ |
|OBJECT ENCODING |✔️ |✔️ |✔️ |✔️ |
|OBJECT FREQ |✔️ |✔️ |✔️ |✔️ |
|OBJECT HELP |➖ |➖ |➖ |➖ |
|OBJECT IDLETIME |✔️ |✔️ |✔️ |✔️ |
|OBJECT REFCOUNT |✔️ |✔️ |✔️ |✔️ |
|PERSIST |✔️ |✔️ |✔️ |✔️ |
|PEXPIRE |✔️ |✔️ |✔️ |✔️ |
|PEXPIREAT |✔️ |✔️ |✔️ |✔️ |
|PEXPIRETIME |➖ |➖ |➖ |➖ |
|PTTL |✔️ |✔️ |✔️ |✔️ |
|RANDOMKEY |✔️ |✔️ |✔️ |✔️ |
|RENAME |✔️ |✔️ |✔️ |✔️ |
|RENAMENX |✔️ |✔️ |✔️ |✔️ |
|RESTORE |✔️ |✔️ |✔️ |✔️ |
|SCAN |✔️ |✔️ |✔️ |✔️ |
|SORT |✔️ |✔️ |✔️ |✔️ |
|SORT_RO |➖ |➖ |➖ |➖ |
|TOUCH |✔️ |✔️ |✔️ |✔️ |
|TTL |✔️ |✔️ |✔️ |✔️ |
|TYPE |✔️ |✔️ |✔️ |✔️ |
|UNLINK |✔️ |✔️ |✔️ |✔️ |
|WAIT |✔️ |✔️ |❌ |❌ |
|WAITAOF |➖ |➖ |➖ |➖ |





</Tab>
<Tab zoneid="daS7KhGx" title="Redis 5.0">
<TabTitle>Redis 5.0</TabTitle>


|**Command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|COPY |❌ |❌ |❌ |❌ |
|DEL |✔️ |✔️ |✔️ |✔️ |
|DUMP |✔️ |✔️ |✔️ |✔️ |
|EXISTS |✔️ |✔️ |✔️ |✔️ |
|EXPIRE |✔️ |✔️ |✔️ |✔️ |
|EXPIREAT |✔️ |✔️ |✔️ |✔️ |
|EXPIRETIME |❌ |❌ |❌ |❌ |
|KEYS |✔️ |✔️ |✔️ |✔️ |
|MIGRATE |❌ |❌ |❌ |✔️ |
|MOVE |✔️ |✔️ |✔️ |✔️ |
|OBJECT ENCODING |✔️ |✔️ |✔️ |✔️ |
|OBJECT FREQ |✔️ |✔️ |✔️ |✔️ |
|OBJECT HELP |➖ |➖ |➖ |➖ |
|OBJECT IDLETIME |✔️ |✔️ |✔️ |✔️ |
|OBJECT REFCOUNT |✔️ |✔️ |✔️ |✔️ |
|PERSIST |✔️ |✔️ |✔️ |✔️ |
|PEXPIRE |✔️ |✔️ |✔️ |✔️ |
|PEXPIREAT |✔️ |✔️ |✔️ |✔️ |
|PEXPIRETIME |➖ |➖ |➖ |➖ |
|PTTL |✔️ |✔️ |✔️ |✔️ |
|RANDOMKEY |✔️ |✔️ |✔️ |✔️ |
|RENAME |✔️ |✔️ |✔️ |✔️ |
|RENAMENX |✔️ |✔️ |✔️ |✔️ |
|RESTORE |✔️ |✔️ |✔️ |✔️ |
|SCAN |✔️ |✔️ |✔️ |✔️ |
|SORT |✔️ |✔️ |✔️ |✔️ |
|SORT_RO |➖ |➖ |➖ |➖ |
|TOUCH |✔️ |✔️ |✔️ |✔️ |
|TTL |✔️ |✔️ |✔️ |✔️ |
|TYPE |✔️ |✔️ |✔️ |✔️ |
|UNLINK |✔️ |✔️ |✔️ |✔️ |
|WAIT |✔️ |✔️ |❌ |❌ |
|WAITAOF |➖ |➖ |➖ |➖ |





</Tab>
</Tabs>
