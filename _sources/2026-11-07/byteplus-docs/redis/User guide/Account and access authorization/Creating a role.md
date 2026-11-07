---
title: "Creating a role"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/create-role"
---

Cache for Redis supports custom role permissions. You can create new roles and assign different permissions based on business needs, enabling fine\-grained database management and enhancing data security. This topic describes how to create a role.

## Prerequisite

The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).

## Precautions

* Cache for Redis supports setting disabled commands through the `disabled-commands` parameter. By default, the `keys`, `flushdb`, and `flushall` commands are disabled. Therefore, if your account role does not include permissions for these disabled commands, you cannot execute them even if they are removed from the `disabled-commands` parameter. For more information on disabled commands, refer to [Disabled command](https://docs.byteplus.com/en/docs/redis/command-limit#.56aB55So5ZG95Luk6K-05piO).

* Each Redis instance can have up to 100 roles by default. If you need to create more roles, please [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to modify relevant parameters.

## ACL syntax

Cache for Redis groups all supported commands according to certain rules, with each group being a command category. You can use ACL (Access Control Lists) syntax to grant roles permission to call specific commands or command categories.

> **tip**

> For details on the command categories supported by Cache for Redis and the specific commands within each category, refer to the detailed description in the **Create role** dialog box in the [Redis console](https://console.byteplus.com/db/redis).

### Syntax rules

The ACL syntax rules for Cache for Redis are as follows:

* Each ACL rule must start with `+` or `-`. After `+` or `-`, you can add specified commands or command categories, where:

   * `+`: Indicates allowing the invocation of certain commands or command categories. For example, `+@all` indicates allowing the invocation of all commands.

   * `-`: Indicates prohibiting the invocation of certain commands or command categories. For example, `-@dangerous` indicates disallowing all commands in the `dangerous` command category.

* Command categories must be prefixed with `@` to distinguish them from specific commands. For example:

   * Specify command category: For example, `+@read` indicates allowing all commands in the `read` command category.

   * Specify a specific command: For example, `-get` indicates only disallowing the `get` command.

* Commands and command categories can contain lowercase letters, numbers, underscores (_), or periods (.), with a length of 1 to 50 characters.

* Cache for Redis automatically adds `~*` syntax to the ACL rules for all roles by default, indicating that all keys and channels can be accessed.

* Using `~<key>` syntax to access a specific key is not supported.

### ACL rules for default roles

Cache for Redis provides five roles by default: `Administrator`, `NotDangerous`, `ReadWrite`, `ReadOnly`, and `NotWrite`. Each role has different ACL rules and supports different permissions. The following table explains how to set ACL rules for roles using the five default roles as examples.

> **tip**

* > The support for commands by default roles in the following table is based on the**instances with sharding cluster disabled upgraded to the latest kernel minor version**. Some commands can only be used after upgrading to a specified minor version, and some commands are not supported in instances with sharding cluster enabled. For more details, refer to [Database minor version upgrade release logs](https://docs.byteplus.com/en/docs/redis/db-minor-version-release-log) and [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-commands).

* > Native Redis provides two versions of ACL rules: V1 and V2. The native Redis provides two versions of ACL rules, V1 and V2. In Cache for Redis, instances with a proxy version number less than or equal to `proxy_version_1.21.0` adopt the ACL V1 rules by default, while instances with a version number greater than `proxy_version_1.21.0` default to using ACL V2 rules.

* > You can view the minor version information of the database of an instance on the **Summary** tab. For specific procedures, refer to [Viewing instance information](https://docs.byteplus.com/en/docs/redis/view-instance).

* > The following table summarizes the details of the differences in ACL rules between V1 and V2 versions for default roles for reference.

**Administrator**

|Default role name<br><br> |ACL rules |Specific commands included or excluded for the current role ||
|---|---|---|---|
|||**ACL V1** |**ACL V2** |
|Administrator<br><br> |`+@all ~*` |Accounts with the `Administrator` role are allowed to use all commands supported by Cache for Redis for all keys. For more details, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-commands). ||

**NotDangerous**

|Default role name<br><br> |ACL rules |Specific commands included or excluded for the current role ||
|---|---|---|---|
|||**ACL V1** |**ACL V2** |
|NotDangerous<br><br> |`+@all -@dangerous ~*` |Accounts with the `NotDangerous` role selected are allowed to use all commands on all keys **except ** **`dangerous`** ** category** commands.<br><br>The `dangerous` category includes the following specific commands:<br><br><br>* [Cluster management](https://docs.byteplus.com/en/docs/redis/Cluster_management)<br><br>   CLUSTER related commands<br><br>* [Connection management](https://docs.byteplus.com/en/docs/redis/Connection_management)<br><br>   CLIENT related commands<br><br>* [Generic](https://docs.byteplus.com/en/docs/redis/Generic)<br><br>   KEYS, RESTORE, SORT<br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   CONFIG related commands, LATENCY related commands, SLOWLOG related commands, FLUSHALL, FLUSHDB, LASTSAVE, MONITOR, ROLE, SWAPDB |Accounts with the `NotDangerous` role are allowed to use all commands on all keys **except ** **`dangerous`** ** category** commands.<br><br>The `dangerous` category includes the following specific commands:<br><br><br>* [Generic](https://docs.byteplus.com/en/docs/redis/Generic)<br><br>   KEYS, RESTORE, SORT, SORT_RO<br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   FLUSHALL, FLUSHDB, INFO, LASTSAVE, MONITOR, ROLE, SWAPDB<br><br>* [Self-developed Proxy commands](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command)<br><br>   IMONITOR |

**ReadWrite**

|Default role name<br><br> |ACL rules |Specific commands included or excluded for the current role ||
|---|---|---|---|
|||**ACL V1** |**ACL V2** |
|ReadWrite<br><br> |`+@all -@admin ~*` |Accounts with the `ReadWrite` role  are allowed to use all commands on all keys **except ** **`admin`** ** category** commands.<br><br>The `admin` category commands include the following specific commands:<br><br><br>* [Cluster management](https://docs.byteplus.com/en/docs/redis/Cluster_management)<br><br>   CLUSTER related commands<br><br>* [Connection management](https://docs.byteplus.com/en/docs/redis/Connection_management)<br><br>   CLIENT related commands<br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   CONFIG related commands, LATENCY related commands, SLOWLOG related commands, LASTSAVE, MONITOR<br><br><br> |Accounts with the `ReadWrite` role can use all commands on all Keys, **excluding ** **`admin`** ** category commands**.<br><br>The `admin` class commands include the following specific commands:<br><br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   LASTSAVE, MONITOR, ROLE<br><br>* [Self-developed Proxy commands](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command)<br><br>   IMONITOR |

**ReadOnly**

|Default role name<br><br> |ACL rules |Specific commands included or excluded for the current role ||
|---|---|---|---|
|||**ACL V1** |**ACL V2** |
|ReadOnly |`+@read ~*` |Accounts with the `ReadOnly` role are allowed to use all commands in the `read` category for all keys.<br><br>The `read` category includes the following specific commands:<br><br><br>* [Bitmap](https://docs.byteplus.com/en/docs/redis/Bitmap)<br><br>   BITCOUNT, BITFIELD_RO, BITPOS, GETBIT<br><br>* [Connection management](https://docs.byteplus.com/en/docs/redis/Connection_management)<br><br>   ECHO<br><br>* [Generic](https://docs.byteplus.com/en/docs/redis/Generic)<br><br>   OBJECT\-related commands, DUMP, EXISTS, EXPIRETIME, KEYS, PEXPIRETIME, PTTL, RANDOMKEY, SCAN, TOUCH, TTL, TYPE<br><br>* [Geospatial indices](https://docs.byteplus.com/en/docs/redis/Geospatial_indices)<br><br>   GEODIST, GEOHASH, GEOPOS, GEORADIUS_RO, GEORADIUSBYMEMBER_RO, GEOSEARCH<br><br>* [Hash](https://docs.byteplus.com/en/docs/redis/Hash)<br><br>   HEXISTS, HGET, HGETALL, HKEYS, HLEN, HMGET, HRANDFIELD, HSCAN, HSTRLEN, HVALS<br><br>* [HyperLogLog](https://docs.byteplus.com/en/docs/redis/HyperLogLog)<br><br>   PFCOUNT<br><br>* [List](https://docs.byteplus.com/en/docs/redis/List)<br><br>   LINDEX, LLEN, LPOS, LRANGE<br><br>* [Scripting and functions](https://docs.byteplus.com/en/docs/redis/Scripting_and_functions)<br><br>   EVAL_RO, EVALSHA_RO, FCALL_RO<br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   MEMORY commands, DBSIZE, INFO, LASTSAVE, LOLWUT, ROLE, TIME<br><br>* [Set](https://docs.byteplus.com/en/docs/redis/Set)<br><br>   SCARD, SDIFF, SINTER, SINTERCARD, SISMEMBER, SMEMBERS, SMISMEMBER, SRANDMEMBER, SSCAN, SUNION<br><br>* [Sorted set](https://docs.byteplus.com/en/docs/redis/Sorted_set)<br><br>   ZCARD, ZCOUNT, ZDIFF, ZINTER, ZINTERCARD, ZLEXCOUNT, ZMSCORE, ZRANDMEMBER, ZRANGE, ZRANGEBYLEX, ZRANGEBYSCORE, ZRANK, ZREVRANGE, ZREVRANGEBYLEX, ZREVRANGEBYSCORE, ZREVRANK, ZSCAN, ZSCORE, ZUNION<br><br>* [Stream](https://docs.byteplus.com/en/docs/redis/Stream)<br><br>   XINFO, XLEN, XPENDING, XRANGE, XREAD, XREVRANGE<br><br>* [String](https://docs.byteplus.com/en/docs/redis/String)<br><br>   GET, GETRANGE, LCS, MGET, STRALGO, STRLEN |Accounts with the `ReadOnly` role are allowed to use all commands in the `read` category for all keys.<br><br>The `read` category includes the following specific commands:<br><br><br>* [Bitmap](https://docs.byteplus.com/en/docs/redis/Bitmap)<br><br>   BITCOUNT, BITFIELD_RO, BITPOS, GETBIT<br><br>* [Generic](https://docs.byteplus.com/en/docs/redis/Generic)<br><br>   DUMP, EXISTS, EXPIRETIME, KEYS, PEXPIRETIME, PTTL, RANDOMKEY, SCAN, SORT_RO, TOUCH, TTL, TYPE<br><br>* [Geospatial indices](https://docs.byteplus.com/en/docs/redis/Geospatial_indices)<br><br>   GEODIST, GEOHASH, GEOPOS, GEORADIUS_RO, GEORADIUSBYMEMBER_RO, GEOSEARCH, <br><br>* [Hash](https://docs.byteplus.com/en/docs/redis/Hash)<br><br>   HEXISTS, HGET, HGETALL, HKEYS, HLEN, HMGET, HRANDFIELD, HSCAN, HSTRLEN, HVALS<br><br>* [HyperLogLog](https://docs.byteplus.com/en/docs/redis/HyperLogLog)<br><br>   PFCOUNT<br><br>* [List](https://docs.byteplus.com/en/docs/redis/List)<br><br>   LINDEX, LLEN, LPOS, LRANGE<br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   DBSIZE, LOLWUT<br><br>* [Set](https://docs.byteplus.com/en/docs/redis/Set)<br><br>   SCARD, SDIFF, SINTER, SINTERCARD, SISMEMBER, SMEMBERS, SMISMEMBER, SRANDMEMBER, SSCAN, SUNION<br><br>* [Sorted set](https://docs.byteplus.com/en/docs/redis/Sorted_set)<br><br>   ZCARD, ZCOUNT, ZDIFF, ZINTER, ZINTERCARD, ZLEXCOUNT, ZMSCORE, ZRANDMEMBER, ZRANGE, ZRANGEBYLEX, ZRANGEBYSCORE, ZRANK, ZREVRANGE, ZREVRANGEBYLEX, ZREVRANGEBYSCORE, ZREVRANK, ZSCAN, ZSCORE, ZUNION<br><br>* [Stream](https://docs.byteplus.com/en/docs/redis/Stream)<br><br>   XLEN, XPENDING, XRANGE, XREAD, XREVRANGE<br><br>* [String](https://docs.byteplus.com/en/docs/redis/String)<br><br>   GET, GETRANGE, LCS, MGET, STRLEN |

**NotWrite**

|Default role name<br><br> |ACL rules |Specific commands included or excluded for the current role ||
|---|---|---|---|
|||**ACL V1** |**ACL V2** |
|NotWrite |`+@all -@write ~*` |Accounts with the NotWrite role are allowed to use all commands on all keys except **write** category commands.<br><br>The specific commands supported are as follows:<br><br><br>* [Bitmap](https://docs.byteplus.com/en/docs/redis/Bitmap)<br><br>   bitcount, bitfield_ro, bitpos, getbit<br><br>* [Connection management](https://docs.byteplus.com/en/docs/redis/Connection_management)<br><br>   auth, client, client\|caching, client\|getname, client\|getredir, client\|help, client\|id, client\|info, client\|list, client\|reply, client\|setinfo, client\|setname, client\|tracking, client\|trackinginfo, echo, hello, ping, quit, readonly, readwrite, select<br><br>* [Generic](https://docs.byteplus.com/en/docs/redis/Generic)<br><br>   dump, exists, expiretime, keys, object, object\|encoding, object\|freq, object\|help, object\|idletime, object\|refcount, pexpiretime, pttl, randomkey, scan, sort_ro, touch, ttl, type, wait<br><br>* [Geospatial indices](https://docs.byteplus.com/en/docs/redis/Geospatial_indices)<br><br>   geodist, geohash, geopos, georadius_ro, georadiusbymember_ro, geosearch<br><br>* [Hash](https://docs.byteplus.com/en/docs/redis/Hash)<br><br>   hexists, hget, hgetall, hkeys, hlen, hmget, hrandfield, hscan, hstrlen, hvals<br><br>* [HyperLogLog](https://docs.byteplus.com/en/docs/redis/HyperLogLog)<br><br>   pfcount<br><br>* [List](https://docs.byteplus.com/en/docs/redis/List)<br><br>   lindex, llen, lpos, lrange<br><br>* [Pub/Sub](https://docs.byteplus.com/en/docs/redis/Pub-Sub)<br><br>   psubscribe, publish, pubsub, pubsub\|channels, pubsub\|help, pubsub\|numpat, pubsub\|numsub, pubsub\|shardchannels, pubsub\|shardnumsub, punsubscribe, spublish, ssubscribe, subscribe, sunsubscribe, unsubscribe<br><br>* [Scripting and functions](https://docs.byteplus.com/en/docs/redis/Scripting_and_functions)<br><br>   eval_ro, evalsha_ro, fcall, fcall_ro, function, function\|dump, function\|help, function\|kill, function\|list, function\|stats, script, script\|exists, script\|flush, script\|help, script\|kill, script\|load<br><br>* [Server management](https://docs.byteplus.com/en/docs/redis/Server_management)<br><br>   command, command\|count, command\|docs, command\|getkeys, command\|getkeysandflags, command\|help, command\|info, command\|list, config, config\|get, config\|help, config\|resetstat, config\|set, dbsize, info, lastsave, latency, latency\|doctor, latency\|graph, latency\|help, latency\|histogram, latency\|history, latency\|latest, latency\|reset, lolwut, memory, memory\|doctor, memory\|help, memory\|malloc\-stats, memory\|purge, memory\|stats, memory\|usage, monitor, role, slowlog, slowlog\|get, slowlog\|help, slowlog\|len, slowlog\|reset, time<br><br>* [Set](https://docs.byteplus.com/en/docs/redis/Set)<br><br>   scard, sdiff, sinter, sintercard, sismember, smembers, smismember, srandmember, sscan, sunion<br><br>* [Sorted set](https://docs.byteplus.com/en/docs/redis/Sorted_set)<br><br>   zcard, zcount, zdiff, zinter, zintercard, zlexcount, zmscore, zrandmember, zrange, zrangebylex, zrangebyscore, zrank, zrevrange, zrevrangebylex, zrevrangebyscore, zrevrank, zscan, zscore, zunion<br><br>* [Stream](https://docs.byteplus.com/en/docs/redis/Stream)<br><br>   xgroup, xgroup\|help, xinfo, xinfo\|consumers, xinfo\|groups, xinfo\|help, xinfo\|stream, xlen, xpending, xrange, xread, xrevrange, get, getrange, lcs, mget, strlen, substr<br><br>* [Transactions](https://docs.byteplus.com/en/docs/redis/Transactions)<br><br>   discard, exec, multi, unwatch, watch ||

## Procedure

1. Log in to the [Redis console](https://console.byteplus.com/db/redis).

2. In the top menu bar, select the project and region to which the instance belongs.

3. On the **Instances** page, click the target instance name.

4. On the instance details page, click the **Accounts** tab.

5. On the **Accountst** tab, click the **Roles** tab.

6. On the **Roles** tab, click **Create role**, and in the pop\-up dialog box, configure the parameters as follows.

   > **tip**

   > Once a role is created, editing or deleting the role is not supported. By default, users are allowed to access all keys and channels.

   |Parameters |Description |
   |---|---|
   |Role name |The role name must meet the following conditions:<br><br><br>* Consists of lowercase letters, hyphens (\-), and digits.<br><br>* The name must start with a letter and end with a letter or a digit.<br><br>* 2 to 63 characters in length. |
   |ACL rules |Set the ACL rules for the role. After entering the ACL rule, press the space bar or Enter key to generate the rule. Supports entering multiple rules at once.<br><br>For detailed information on ACL rules, refer to [ACL syntax](https://docs.byteplus.com/en/docs/redis/create-role#G8lTkW04). |

7. Click **OK**.

## Subsequent operations

After the role is successfully created, you can select the appropriate role for the account based on business needs when creating an account, enabling fine\-grained management of the database and enhancing data security. For more details, refer to [Creating and managing account](https://docs.byteplus.com/en/docs/redis/manage-account).

## Relevant APIs

|API |Description |
|---|---|
|[CreateDBAccount](https://docs.byteplus.com/en/docs/redis/createdbaccount) |Call the CreateDBAccount API to create an account for target Redis instance. |
|[DescribeDBInstanceAclCommands](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcommands) |Call the DescribeDBInstanceAclCommands API to query the list of commands supported by the specified command category in target Redis instance. |
|[DescribeDBInstanceAclCategories](https://docs.byteplus.com/en/docs/redis/describedbinstanceaclcategories) |Call the DescribeDBInstanceAclCategories API to query the command categories supported by target Redis instance. |
