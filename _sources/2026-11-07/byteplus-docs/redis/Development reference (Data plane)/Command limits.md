---
title: "Command limits"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/command-limit"
---

Cache for Redis is compatible with most native Redis commands. Some limits are to be followed when using certain commands. This topic summarizes the command limits in Redis instances.

<span id=".5pSv5oyB55qE5ZG95Luk"></span>
## Supported commands

For more information on the commands supported by Cache for Redis, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).

<span id=".5aSaLWtleS3lkb3ku6TpmZDliLY="></span>
## Limits on multiple key commands

Multiple key commands supported by Redis are listed in the table below.


|Command group |Commands |
|---|---|
|Bitmap |COPY, BITOP |
|Generic |DEL, EXISTS, RENAME, RENAMENX, SORT, TOUCH, UNLINK |
|Geospatial indices |GEOSEARCHSTORE |
|HyperLogLog |PFCOUNT, PFMERGE |
|List |BLMOVE, BLMPOP, BLPOP, BRPOP, RPOPLPUSH, BRPOPLPUSH, LMOVE, LMPOP |
|Scripting and functions |EVAL, EVAL_RO, EVALSHA, EVALSHA_RO, FCALL, FCALL_RO |
|Set |SDIFF, SDIFFSTORE, SINTER, SINTERCARD, SINTERSTORE, SMOVE, SUNION, SUNIONSTORE |
|Sorted set |BZMPOP, BZPOPMIN, BZPOPMAX, ZDIFFSTORE, ZINTER, ZINTERCARD, ZINTERSTORE, ZMPOP, ZMSCORE, ZRANGESTORE, ZUNION, ZUNIONSTORE, ZDIFF |
|Stream |XREAD, XREADGROUP |
|String |MSETNX, MGET, MSET |
|Transactions |WATCH |


The limits when using multiple key commands vary depending on the instance or address type of Redis. Specific limits are as follows.


<Tabs>
<Tab zoneid="AhuIZ3kP3u" title="Instances with sharding cluster enabled">
<TabTitle>Instances with sharding cluster enabled</TabTitle>

* When connecting to instance through public or private addresses

   When using any of the multiple key commands in the table below, ensure that the keys to be operated are distributed within one hash slot.

   
   |Command group |Commands |
   |---|---|
   |Bitmap |COPY, BITOP |
   |Generic |RENAME, RENAMENX, SORT, TOUCH |
   |Geospatial indices |GEOSEARCHSTORE |
   |HyperLogLog |PFCOUNT, PFMERGE |
   |List |BLMOVE, BLMPOP, BLPOP, BRPOP, RPOPLPUSH, BRPOPLPUSH, LMOVE, LMPOP |
   |Scripting and functions |EVAL, EVAL_RO, EVALSHA, EVALSHA_RO, FCALL, FCALL_RO |
   |Set |SINTERCARD |
   |Sorted set |BZMPOP, BZPOPMIN, BZPOPMAX, ZDIFFSTORE, ZINTER, ZINTERCARD, ZMPOP, ZMSCORE, ZRANGESTORE, ZUNION, ZDIFF |
   |Stream |XREAD, XREADGROUP |
   |String |MSETNX |
   |Transactions |WATCH |
   

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">To connect instances through public or private addresses, refer to <a href="https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address">Connecting to instance via public address</a> or <a href="https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address">Connecting to instance via private address</a>.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You can build keys with the same slot through hash tag. For how to use hash tags, refer to <a href="https://redis.io/docs/reference/cluster-spec/#hash-tags">Keys hash tags</a>. You can also use the Key Routing Simulator feature provided in the <a href="https://docs.byteplus.com/en/docs/redis/Slot_distribution_view">Slot distribution view</a> to verify whether data is forcibly routed to the same shard.   </div>
   

* When connecting instance through direct address

   When executing any multiple key command, ensure that the keys to be operated by the command are distributed within one hash slot. To connect instances through direct address, refer to [Connecting to instance through direct connection address](https://docs.byteplus.com/en/docs/redis/connect-instance-through-direct-connection-address).


</Tab>
<Tab zoneid="wcQEq9mEuW" title="Instances with sharding cluster disabled">
<TabTitle>Instances with sharding cluster disabled</TabTitle>

No relevant limits.


</Tab>
</Tabs>


<span id=".5LqL5Yqh5ZG95Luk6ZmQ5Yi2"></span>
## Limits on transaction commands


* For both Redis instances with sharding clusters enabled and sharding cluster enabled, the following commands are not allowed to be used within transactions.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For details about transaction commands supported by Cache for Redis, refer to <a href="https://docs.byteplus.com/en/docs/redis/Transactions">Transactions</a>.   </div>
   

   
   |Command group |Commands |
   |---|---|
   |Connection management |HELLO, AUTH, PING, CLIENT GETNAME, CLIENT SETNAME, CLIENT LIST, CLIENT ID, CLIENT KILL |
   

* Redis instances with sharding cluster enabled supports connecting to the instance through and proxy mode. Different modes have different restrictions on transaction commands.

   
   <Tabs>
   <Tab zoneid="QJMgadFzOQ" title="Direct connection mode">
   <TabTitle>Direct connection mode</TabTitle>
   
   When connecting to an instance in direct connection mode (that is, using direct connection address) to execute transaction commands, it is necessary to ensure that all the keys to be operated on by the commands are distributed in the same hash slot. You can build keys with the same slot through hash tag. For how to use hash tags, refer to [Keys hash tags](https://redis.io/docs/reference/cluster-spec/#hash-tags). You can also use the Key Routing Simulator feature provided in the [Slot distribution view](https://docs.byteplus.com/en/docs/redis/Slot_distribution_view) to verify whether data is forcibly routed to the same shard.
   
   <div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>
   
   
   <div data-tips="true" data-tips-type="default">When executing transaction commands using <strong>direct connection mode</strong> to connect instances, you must <strong>strictly ensure that the keys of the transaction operations are all on the same slot</strong>, otherwise the transaction commands will fail to execute.</div>
   
   
   
   </Tab>
   <Tab zoneid="EuncyLvWKh" title="Proxy mode">
   <TabTitle>Proxy mode</TabTitle>
   
   When connecting to instance to execute transaction commands through proxy mode (that is, using public and private network addresses), the limitations of transaction commands are as shown in the following table.
   
   
   |Key distribution scenarios |Can transaction execute normally |Can transaction atomicity be guaranteed when executing transaction commands |
   |---|---|---|
   |All keys within the transaction are distributed in the same slot. |Yes. |Yes. |
   |Keys within the transaction are in different slots, but keys within each command are in the same slot. |Yes. |* Transaction atomicity can be guaranteed between commands belonging to the same slot.<br><br>* Transaction atomicity cannot be guaranteed between commands belonging to different slots. |
   |Keys within the same command in the transaction are in different slots. |No.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">You can build keys with the same slot through hash tag. For how to use hash tags, refer to <a href="https://redis.io/docs/reference/cluster-spec/#hash-tags">Keys hash tags</a>. You can also use the Key Routing Simulator feature provided in the <a href="https://docs.byteplus.com/en/docs/redis/Slot_distribution_view">Slot distribution view</a> to verify whether data is forcibly routed to the same shard.</div><br> |Not applicable. |
   
   
   
   
   
   </Tab>
   </Tabs>
   


<span id=".bHVhLeiEmuacrOS9v-eUqOmZkOWItg=="></span>
## Limits for using Lua scripting

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more details, refer to <a href="https://docs.byteplus.com/en/docs/redis/lua-user-guide">Lua scripting guide</a>.</div>



* Different instance types of Cache for Redis have different limitations when using Lua scripts. Among them:

   * **Instances with sharding cluster enabled**

      * All keys should be passed through the `KEYS` array; the Redis commands called in `redis.call/pcall` must have their keys in the `KEYS` array.

      * The value of `numkeys` must be greater than or equal to 1.

      * All keys must be in a single slot.

      * For instances where the proxy minor version is less than 1.511.0, the maximum limit for the number of key parameters in a Lua script is 100 by default. When the number of keys exceeds the limit, an error message `command arguments invalid` will appear. If necessary, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to upgrade the instance's proxy to the latest version to remove this restriction.

   * **Instances with sharding cluster disabled**

      For instances where the proxy minor version is less than 1.511.0, the maximum limit for the number of key parameters in a Lua script is 100 by default. When the number of keys exceeds the limit, an error message `command arguments invalid` will appear. If necessary, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to upgrade the instance's proxy to the latest version to remove this restriction.

* Cache for Redis restricts the use of certain commands in Lua scripts. For more details about supported commands in Lua scripts, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).


<span id=".56aB55So5ZG95Luk6K-05piO"></span>
## Description of disabled commands

Cache for Redis instances disable the `flushall`, `flushdb`, and `keys` commands by default.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the above default disabled commands, only commands that are supported by the current instance appear in the default value of the <code>disabled-commands</code> parameter.</div>


* <div data-tips="true" data-tips-type="tip">To use the above commands, you need to remove the corresponding commands from the default value of the disabled\-commands parameter. Otherwise, the error <code>no permission to execute the command</code> will be reported when executing these forbidden commands. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/set-parameter">Setting instance parameters</a>.</div>


* <div data-tips="true" data-tips-type="tip">A single instance can support disabling up to 16 commands at most. Multiple commands are separated by English commas (,). For details on the quantity limit of disabled commands, refer to <a href="https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5Yqf6IO954m55oCn6ZmQ5Yi2">Limit on features</a>.</div>


* <div data-tips="true" data-tips-type="tip">For more information on parameters and commands supported by Redis, refer to <a href="https://docs.byteplus.com/en/docs/redis/supported-parameter">Supported parameters</a> and <a href="https://docs.byteplus.com/en/docs/redis/supported-command">Supported commands</a>.</div>



<span id=".5YW25a6D5ZG95Luk6ZmQ5Yi2"></span>
## Limits on other commands


<Tabs>
<Tab zoneid="yIpUY4Jzvx" title="Instances with sharding cluster enabled">
<TabTitle>Instances with sharding cluster enabled</TabTitle>

* GET or BY parameters are not supported in SORT commands.

* Instances created earlier than May 17, 2022 are only supported SELECT 0.

* When a Redis instance with sharding clusters enabled executes the RANDOMKEY command, it will access each shard in a round\-robin manner. That is, Redis will send the RANDOMKEY command request to each shard. When the visited shard does not have a key that meets the conditions, it will return `nil`. This return result only means that **there is no key that meets the conditions on the current shard** but **does not mean that there is no key that meets the conditions on other shards**. Therefore, when using the RANDOMKEY command, it is recommended **not to determine whether there are keys** **that meet the conditions based on whether the return result is** **`nil`**.


</Tab>
<Tab zoneid="aGRFqfhjNP" title="Instances with sharding cluster disabled">
<TabTitle>Instances with sharding cluster disabled</TabTitle>

GET or BY parameters are not supported in SORT commands.


</Tab>
</Tabs>
