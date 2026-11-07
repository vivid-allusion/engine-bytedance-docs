---
title: "Connection management"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Connection_management"
---

This article summarizes the support of Connection management command family by different engine versions and architecture types of Cache for Redis instances.

<span id="2Qfugoh6"></span>
## Precautions


* Regarding the identification in the table, the instructions are as follows:

   * ✔️ : The command is supported in the current scenario.

   * ❌ : The command is not supported in the current scenario.

   * ➖ : This command is not supported in this version of native Redis. For example, in native Redis, the BITFIELD_RO command is only supported in versions 6.0 and above, and the command is marked as ➖ in version 5.0 of the table.

* For more details about the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/command-limit).

* This document's command support is based on the latest database kernel minor version; some commands require upgrading to a specified minor version to be used. For more details about kernel minor versions, refer to [Database minor version upgrade release logs](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log).

* Cache for Redis supports Lua\-related commands. For more details about basic Lua script syntax, usage restrictions, and recommendations, refer to [Lua scripting guide](https://docs.byteplus.com/en/docs/redis/lua-user-guide).

* Instances created before April 28, 2022 only support SELECT 0. You can [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to upgrade the available DB count of the instance to 256, enabling support for SELECT 0 to 255 after the upgrade. For more details about usage limitations of Redis, refer to [Feature limits](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2).


<span id="ZVvI2q8O"></span>
## Command support table


<Tabs>
<Tab zoneid="dFVKsPrC" title="Redis 7.0">
<TabTitle>Redis 7.0</TabTitle>


|**command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|AUTH |✔️ |✔️ |✔️ |❌ |
|CLIENT CACHING |❌ |❌ |❌ |❌ |
|CLIENT GETNAME |✔️ |✔️ |✔️ |❌ |
|CLIENT GETREDIR |❌ |❌ |❌ |❌ |
|CLIENT ID |✔️ |✔️ |✔️ |❌ |
|CLIENT INFO |❌ |❌ |❌ |❌ |
|CLIENT KILL |✔️ |✔️ |✔️ |❌ |
|CLIENT LIST |✔️ |✔️ |✔️ |❌ |
|CLIENT NO\-EVICT |❌ |❌ |❌ |❌ |
|CLIENT NO\-TOUCH |➖ |➖ |➖ |➖ |
|CLIENT PAUSE |❌ |❌ |❌ |❌ |
|CLIENT REPLY |❌ |❌ |❌ |❌ |
|CLIENT SETINFO |✔️ |✔️ |✔️ |❌ |
|CLIENT SETNAME |✔️ |✔️ |✔️ |❌ |
|CLIENT TRACKING |❌ |❌ |❌ |❌ |
|CLIENT TRACKINGINFO |❌ |❌ |❌ |❌ |
|CLIENT UNBLOCK |❌ |❌ |❌ |❌ |
|CLIENT UNPAUSE |❌ |❌ |❌ |❌ |
|ECHO |✔️ |✔️ |✔️ |✔️ |
|HELLO |✔️ |✔️ |✔️ |❌ |
|PING |✔️ |✔️ |✔️ |✔️ |
|QUIT |✔️ |✔️ |✔️ |❌ |
|READONLY |✔️ |✔️ |✔️ |✔️ |
|READWRITE |✔️ |✔️ |✔️ |✔️ |
|RESET |❌ |❌ |❌ |❌ |
|SELECT |✔️ |✔️ |✔️ |✔️ |





</Tab>
<Tab zoneid="VDbXWTn3" title="Redis 6.0">
<TabTitle>Redis 6.0</TabTitle>


|**command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|AUTH |✔️ |✔️ |✔️ |❌ |
|CLIENT CACHING |❌ |❌ |❌ |❌ |
|CLIENT GETNAME |✔️ |✔️ |✔️ |❌ |
|CLIENT GETREDIR |❌ |❌ |❌ |❌ |
|CLIENT ID |✔️ |✔️ |✔️ |❌ |
|CLIENT INFO |➖ |➖ |➖ |➖ |
|CLIENT KILL |✔️ |✔️ |✔️ |❌ |
|CLIENT LIST |✔️ |✔️ |✔️ |❌ |
|CLIENT NO\-EVICT |➖ |➖ |➖ |➖ |
|CLIENT NO\-TOUCH |➖ |➖ |➖ |➖ |
|CLIENT PAUSE |❌ |❌ |❌ |❌ |
|CLIENT REPLY |❌ |❌ |❌ |❌ |
|CLIENT SETINFO |✔️ |✔️ |✔️ |❌ |
|CLIENT SETNAME |✔️ |✔️ |✔️ |❌ |
|CLIENT TRACKING |❌ |❌ |❌ |❌ |
|CLIENT TRACKINGINFO |➖ |➖ |➖ |➖ |
|CLIENT UNBLOCK |❌ |❌ |❌ |❌ |
|CLIENT UNPAUSE |➖ |➖ |➖ |➖ |
|ECHO |✔️ |✔️ |✔️ |✔️ |
|HELLO |✔️ |✔️ |✔️ |❌ |
|PING |✔️ |✔️ |✔️ |✔️ |
|QUIT |✔️ |✔️ |✔️ |❌ |
|READONLY |✔️ |✔️ |✔️ |✔️ |
|READWRITE |✔️ |✔️ |✔️ |✔️ |
|RESET |➖ |➖ |➖ |➖ |
|SELECT |✔️ |✔️ |✔️ |✔️ |





</Tab>
<Tab zoneid="mQgvw356" title="Redis 5.0">
<TabTitle>Redis 5.0</TabTitle>


|**command** |**Sharding cluster disabled** |**Sharding cluster enabled** |**Sharding cluster enabled(direct address)**  |**Use in LUA scripts** |
|---|---|---|---|---|
|AUTH |✔️ |✔️ |✔️ |❌ |
|CLIENT CACHING |➖ |➖ |➖ |❌ |
|CLIENT GETNAME |✔️ |✔️ |✔️ |❌ |
|CLIENT GETREDIR |➖ |➖ |➖ |❌ |
|CLIENT ID |✔️ |✔️ |✔️ |❌ |
|CLIENT INFO |➖ |➖ |➖ |❌ |
|CLIENT KILL |✔️ |✔️ |✔️ |❌ |
|CLIENT LIST |✔️ |✔️ |✔️ |❌ |
|CLIENT NO\-EVICT |➖ |➖ |➖ |➖ |
|CLIENT NO\-TOUCH |➖ |➖ |➖ |➖ |
|CLIENT PAUSE |❌ |❌ |❌ |❌ |
|CLIENT REPLY |❌ |❌ |❌ |❌ |
|CLIENT SETINFO |✔️ |✔️ |✔️ |❌ |
|CLIENT SETNAME |✔️ |✔️ |✔️ |❌ |
|CLIENT TRACKING |➖ |➖ |➖ |➖ |
|CLIENT TRACKINGINFO |➖ |➖ |➖ |➖ |
|CLIENT UNBLOCK |❌ |❌ |❌ |❌ |
|CLIENT UNPAUSE |➖ |➖ |➖ |➖ |
|ECHO |✔️ |✔️ |✔️ |✔️ |
|HELLO |➖ |➖ |➖ |➖ |
|PING |✔️ |✔️ |✔️ |✔️ |
|QUIT |✔️ |✔️ |✔️ |❌ |
|READONLY |✔️ |✔️ |✔️ |✔️ |
|READWRITE |✔️ |✔️ |✔️ |✔️ |
|RESET |➖ |➖ |➖ |➖ |
|SELECT |✔️ |✔️ |✔️ |✔️ |





</Tab>
</Tabs>
