---
title: "Switching Memcached to Cache for Redis"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/Switching_Memcached_to_the_Cache_for_Redis"
---

This article explains how to switch Memcached to the Cache for Redis and how to implement atomic updates and distributed locks after switching.

<span id="PCMA1my2"></span>
## Background information

<span id="Z7AE5Run"></span>
### What is Memcached?

Memcached is a distributed memory object caching system mainly used to reduce the load on backend storage systems such as databases. It stores data as string key\-value pairs in memory, allowing retrieval of values through specific keys. Memcached generally does not support data persistence (some third\-party extensions can provide simple persistence to a certain extent, but this is not a native feature of Memcached). This means data in memory will be lost if the server restarts or encounters an unexpected failure.

<span id="nuXc1TUA"></span>
### Comparison of Memcached and Redis features

The following table shows differences in functional features and basic command support between Memcached and Cache for Redis.


|**Comparison items** ||**Cache for Redis** |**Memcached** |
|---|---|---|---|
|**Features**<br><br> |**Application scenarios** |In addition to caching, it can also be used as a message queue, task queue, and session storage. For more details, refer to [Application scenarios](https://docs.byteplus.com/en/docs/redis/application_scenarios). |Mainly used as a simple cache. |
||**Data structures** |Supports multiple data structures. For example, String, List, Set, Zset, Hash, and others. For more details, refer to [Data types](https://docs.byteplus.com/en/docs/redis/quota-and-limit#.5pWw5o2u57G75Z6L6ZmQ5Yi2) and [Extended data structures](https://docs.byteplus.com/en/docs/redis/extended-data-structure). |Only String type key\-value pairs are supported. |
||**Cluster mode** |Supports both sharding cluster enabled and disabled architectures, each supporting single\-node and primary\-secondary instance types. For more details, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture). |Implement cluster mode through third\-party tools. |
||**High availability** |Cache for Redis supports primary\-secondary switching and multi\-availability zone deployment, effectively ensuring high availability. For more details, refer to [High availability](https://docs.byteplus.com/en/docs/redis/high-availability). |High availability is not supported. |
||**Persistence** |The primary and replica instances use RDB snapshot storage for persistence by default, with AOF persistence enabled by default.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Single\-node instances do not have data persistence capabilities and do not support any data persistence policies. For more information on the functional characteristics of primary\-secondary and single\-node instances, refer to <a href="https://docs.byteplus.com/en/docs/redis/feature-faq">Feature differences</a>.</div><br> |Persistence is not supported (usually temporary storage). |
||**Data compression** |Data compression is disabled by default. |Compression can be performed by the client. |
||**Thread support** |Single\-threaded, using an event\-driven model. |Multi\-threaded. |
||**Command complexity** |Supports rich commands and features such as publish/subscribe, transactions, Lua scripting, and more. For more details, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command). |Simple access commands. |
||**Transaction support** |Support transactions through commands such as MULTI/EXEC. For more details, refer to [Transaction command limits](https://docs.byteplus.com/en/docs/redis/command-limit). |Transactions are not supported. |
||**Expiration policy** |Supports setting expiration time (TTL). |Supports setting expiration time (TTL).<br><br> |
||**Eviction policy** |Supports setting the data eviction policy through the `maxmemory-policy` parameter. For more details, refer to [Setting key expiration and eviction policies](https://docs.byteplus.com/en/docs/redis/set-maxmemory-policy). |Memory limits are simple, typically evicting data based on memory size. |
|**Basic commands**<br><br> |**Store data** |Store String type data using [SET](https://redis.io/docs/latest/commands/set/) command.<br><br> |Store data using [SET](https://docs.memcached.org/protocols/basic/#set) command.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The access protocol format of Memcached commands differs from Redis. For more details, see <a href="https://docs.memcached.org/protocols/basic/#storage-commands">Memcached storage commands</a>.</div><br> |
||**Retrieve data** |Retrieve String type data using [GET](https://redis.io/docs/latest/commands/get/) command.<br><br> |Retrieve data using [GET](https://docs.memcached.org/protocols/basic/#get) or [GETS](https://docs.memcached.org/protocols/basic/#gets) command.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default"><a href="https://docs.memcached.org/protocols/basic/#gets">The return result of the GETS</a> command includes a CAS unique identifier, which can be used with <a href="https://docs.memcached.org/protocols/basic/#cas">CAS</a> command to achieve atomic data updates.</div><br> |
||**Atomic data update** |Native Redis does not support atomic data update commands, but the Cache for Redis provides a self\-developed Proxy [CAS](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#cas) command to implement atomic data updates. |Perform atomic data updates using [CAS](https://docs.memcached.org/protocols/basic/#cas) command.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Before using <a href="https://docs.memcached.org/protocols/basic/#cas">CAS</a> command, you need to obtain CAS unique identifier (cas unique) through <a href="https://docs.memcached.org/protocols/basic/#gets">GETS</a> command before you can implement data atomic update.</div><br> |
||**Delete data** |Delete specified key using [DEL](https://redis.io/docs/latest/commands/del/) command. |Delete specified key using [DELETE](https://docs.memcached.org/protocols/basic/#delete) command. |
||**Set expiration time** |Set the expiration time of the key through EX field in [SET](https://redis.io/docs/latest/commands/set/) command. |Set expiration time using the exptime parameter when using [SET](https://docs.memcached.org/protocols/basic/#set) command. Setting it to 0 means it never expires. |
||**Check for existence**<br><br> |Use [EXISTS](https://redis.io/docs/latest/commands/exists/) command to check if one or more specified keys exist; it returns 0. If a key does not exist and returns the number of existing keys.<br><br>For example, check if key1, key2, and key3 exist at the same time:<br><br><br>* If key1, key2, and key3 all do not exist, it returns 0.<br><br>* If only key1 and key2 exist, and key3 does not, it returns 2.<br><br>* If key1, key2, and key3 all exist, it returns 3.<br><br><br> |When querying data with the [GET](https://docs.memcached.org/protocols/basic/#get) or [GETS](https://docs.memcached.org/protocols/basic/#gets) command:<br><br><br>* If the specified key exists, it returns the key name, flags, the number of bytes returned, the corresponding data, and a unique CAS identifier (cas unique, returned only by [GETS](https://docs.memcached.org/protocols/basic/#gets) command).<br><br>* If the specified key does not exist or has expired, END is returned. |
||**Get values of multiple keys** |Retrieve values of multiple keys using [MGET](https://redis.io/docs/latest/commands/mget/) command. |Query multiple keys' values using [GET](https://docs.memcached.org/protocols/basic/#get) or [GETS](https://docs.memcached.org/protocols/basic/#gets) commands. |
||**Batch set data** |Set values for multiple keys separately using [MSET](https://redis.io/docs/latest/commands/mset/) command. |None. |
||**View statistics** |Use [INFO](https://redis.io/docs/latest/commands/info/) command to view Redis server settings and statistics. |View Memcached server settings and statistics with commands related to [statistics](https://docs.memcached.org/protocols/basic/#statistics). |
||**Clear data** |Clear data using [FLUSHDB](https://redis.io/docs/latest/commands/flushdb/) or [FLUSHALL](https://redis.io/docs/latest/commands/flushall/) commands. |Clear data using [FLUSH_ALL](https://docs.memcached.org/protocols/basic/#flush_all) command. |


<span id="wJ8KR6dY"></span>
### Why switch Memcached to Cache for Redis

From the differences in functional features and basic command support mentioned above, it can be seen that:


* Memcached, as a basic cache, does not support common data structure types such as String, List, Set, Zset, and Hash, making it inconvenient to use.

* Memcached lacks high availability capabilities, so it cannot guarantee reliable service during use.

* Memcached's market share has gradually declined over the years, no longer supporting mainstream service frameworks, and older service frameworks lack maintenance.

* Cache for Redis provides entrusted cache database services. It is compatible with the Redis database engine and can help you build Redis databases on the cloud easily and quickly. Cache for Redis provides a high\-performance and secure Redis database solution. The pay\-as\-you\-go and dynamic scalability are combined to significantly help enterprises reduce costs. It also helps eliminate the complexity of database management and operation. For more details, refer to [About Cache for Redis](https://docs.byteplus.com/en/docs/redis/about-redis).


<span id="sUdOOeiK"></span>
## How to switch Memcached to Cache for Redis

Switching Memcached to Cache for Redis requires only the following two steps:


1. Create a Redis 7.0 instance. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance).

2. [Submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to request use of the ExString data structure. You can use the ExString data structure to achieve business dual writes and cache warming. For more information about the [ExString](https://docs.byteplus.com/en/docs/redis/exstring) data structure, refer to [ExString](https://docs.byteplus.com/en/docs/redis/exstring).


<span id="B4GaypYx"></span>
## Best practice 1: Atomic data updates

<span id="uzwnAUUh"></span>
### Atomic data updates using CAS

Assume a key named doctest has been created using the SET command, and you want to update its value to 100 only if the current value is 5. You can implement this using self\-developed [CAS](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#cas) command in Cache for Redis. The command example is as follows.

```Bash
# The input value matches the value set in doctest; update succeeds, and the doctest value is overwritten by the new value
CAS doctest 5 100
# The input value does not match the value set in doctest, and update fails.
CAS doctest 6 100
```


<span id="zV4zywiW"></span>
### Atomic data updates using EXSET

Both Memcached’s CAS command and the [EXSET](https://docs.byteplus.com/en/docs/redis/exstring#exset) command supported by the ExString data structure in the Cache for Redis can be used to implement atomic data updates.

You can migrate CAS commands that rely on Memcached to the EXSET command supported by the ExString data structure in the Cache for Redis to implement atomic data updates. The usage comparison between the two commands is as follows.


<Tabs>
<Tab zoneid="An5S9Tr4IP" title="Examples of commands for Cache for Redis">
<TabTitle>Examples of commands for Cache for Redis</TabTitle>

1. Get the specified version using EXGET command. The command example is as follows.

   ```Bash
   EXGET doctestkey_2
   ```
   


Examples of back results are as follows.


```Bash
1) "doctestvalue_2a"
2) (integer) 2
```


2. Set the value for the specified version using EXSET command. The command example is as follows.

   ```Bash
   EXSET doctestkey_2 doctestvalue_2b ver 2
   ```
   


Examples of back results are as follows.


```Bash
OK
```



Execute EXGET command again to confirm the value and version. The command example is as follows.


```Bash
EXGET doctestkey_2
```



Examples of back results are as follows. The new value has been successfully written, and the version is incremented by 1.


```Bash
1) "doctestvalue_2b"
2) (integer) 3
```


   ####     <span id="ZJJuKuRF"></span>


</Tab>
<Tab zoneid="tWLeOnUHeY" title="Examples of commands for Memcached">
<TabTitle>Examples of commands for Memcached</TabTitle>

1. Get the version of the specified key using GETS command. The command example is as follows.

   ```Bash
   GETS doctestkey_1
   ```
   

   Examples of back results are as follows.

   ```Bash
   VALUE doctestkey_1 0 7 12345
   doctestvalue_1a
   END
   ```
   

2. Set the value for the specified version using CAS command. The command example is as follows.

   ```Bash
   CAS doctestvalue_1b 0 0 7 12345
   ```
   


Examples of back results are as follows.


```Bash
doctestvalue_1b
```





</Tab>
</Tabs>


<span id="vgFJhZwz"></span>
## Best practice 2: Distributed locks

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Due to the asynchronous implementation of data synchronization between primary and secondary nodes, some recently written data on the primary node may be lost. If the lost data involves state information of distributed locks (such as lock holder identifiers, lock validity periods, etc.), it may compromise the mutex characteristics and safety of the locks. This could subsequently lead to severe business anomalies such as resource conflicts or data inconsistencies. For more details on the impact of Redis primary\-secondary switchover, refer to <a href="https://docs.byteplus.com/en/docs/redis/failover">Outcomes of node switch and suggestions</a>.</div>


<span id="Mtkhv1a0"></span>
### Distributed lock based on CAS

Open source Redis supports distributed locks through the NX and EX parameters in the SET command. For example, executing the command `SET unique_lock 1735876863 NX EX 5` means:


* Create a lock object named unique_lock.

* It will only be created if the object does not exist; if creation succeeds, the lock is successfully acquired.

* The lock automatically expires after 5 seconds to prevent deadlocks.


However, the above locking logic has inherent defects. For example, when User 1 wants to unlock but is blocked for some time due to system issues, by the time User 1 tries to unlock, User 2 is successfully locked. At this point, if User 1 tries to lock again, they will successfully acquire the lock, and it is highly likely that a data race will occur between User 1 and User 2.


<Tabs>
<Tab zoneid="XbXHLtWpwh" title="Example of normal locking and unlocking">
<TabTitle>Example of normal locking and unlocking</TabTitle>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_d107b16053da08c3ae28c38933b2e5df.png) </span>


</Tab>
<Tab zoneid="U0jAIsQ7lw" title="Example of lock conflict caused by abnormal unlocking">
<TabTitle>Example of lock conflict caused by abnormal unlocking</TabTitle>

<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c636c67ba32c2416dcc09f60c589e94d.png) </span>


</Tab>
</Tabs>


Since open source Redis **does not support CAS**, businesses often need to introduce complex Lua scripts to implement atomic actions. Nonetheless, unreliable lock events may still occur in extreme cases. To address these issues, the Cache for Redis supports [CAS](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#cas) and [CAD](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#cad) operations in its self\-developed Proxy commands, allowing standard distributed lock usage through atomic operations.

For example, you can create a lock object and set its expiration time using the following command. The command example is as follows.

```Bash
SET unique_lock 10.1.1.1:6379 NX EX 5
```


After successfully locking, you can unlock using the following command. The command example is as follows.

```Bash
CAD unique_lock 10.1.1.1:6379
```


You can also update the lock expiration time regularly with the following command to renew the lock.

```Bash
CAS unique_lock 10.1.1.1:6379 EX 5
```


<span id="322NZ9jy"></span>
### Optimistic lock based on Exstring

Cache for Redis provides ExString, which supports carrying version information in addition to the native Redis String data structure, allowing the version information to be modified. When the Exstring update fails due to version mismatch, it returns `updated version is stale` error message. Based on the above logic, you can implement an optimistic lock model by repeatedly executing the [EXCAS](https://docs.byteplus.com/en/docs/redis/exstring#excas) command.

Example code for optimistic locking is shown below (using Python as an example).

```Python
while(true){
       {ret, value, version} = excas(key, new_value, old_version)    
       # Try to replace Value directly with EXCAS command
       if(ret == OK)
           break; # Exit loop if return value is OK, indicating update success.
       else (if ret.contains("update version is stale")) 
           # If the return value containing update version is stale, it means the update failed due to version mismatch. Update two variables.
           update(value);
           old_version = version;
 }
```


<span id="eHx3G7LE"></span>
### Implementing finer\-grained lock control based on ExString

Cache for Redis supports using the following three version\-related parameters in the [EXSET](https://docs.byteplus.com/en/docs/redis/exstring#exset) command to help implement finer\-grained lock control:


* `VER version`: Specify the version number. When the key exists and the passed version number matches the key's current version number, the version number increases by 1 based on the original version.

* `ABS version`: Absolute version number. After setting, the value will be written directly, and the key's version number will be updated to the version number set by this option.

* `GT version`: Compare version numbers. After setting, if the version number of the specified key is greater than the specified GT version, the value will be written, and the version number will increase by 1 from the original. This parameter relaxes lock granularity while controlling concurrency to some extent.


For example, you can use the `GT version` parameter to implement automatic lock activation of mutex locks when the version number is higher than specified. The code example is as follows (using Python here).

```Python
while(true){
       {ret, value, version} = exset(key, new_value, old_version, GT=true)    
       # Use GT version parameter in EXSET command; if greater than the specified old_version, replace the value
       if(ret == OK)
           break; # Exit loop if return value is OK, indicating update success.
       else (if ret.contains("update version is stale")) 
           # If return value containing update version is stale, it means the update failed due to version mismatch. Update two variables.
           update(value);
           old_version = version;
 }
```
