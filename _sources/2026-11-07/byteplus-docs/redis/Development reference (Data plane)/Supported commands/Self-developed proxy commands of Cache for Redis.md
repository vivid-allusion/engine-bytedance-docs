---
title: "Self-developed proxy commands of Cache for Redis"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command"
---

In addition to being compatible with open\-source Redis commands, the Cache for Redis also supports several self\-developed proxy commands. You can use these commands in a Redis instance with sharding cluster enabled, which can help you manage the sharding cluster instance more conveniently.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance architecture must be an instance with [sharding cluster enabled](https://docs.byteplus.com/en/docs/redis/product-component-architecture#.5ZCv55So5YiG54mH6ZuG576k), and the instance must be accessed using a public or private network address. When accessing the instance through a direct connection address, self\-developed proxy commands cannot be used. For specific procedures, refer to [Connecting to instance via private address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-private-address) and [Connecting to instance via direct connection address](https://docs.byteplus.com/en/docs/redis/connect-instance-via-public-address).

* The minor version of the instance's proxy must be greater than or equal to 1.504.0.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can view the instance's database version and minor version information of the Proxy under the <strong>Summary</strong> tab. For specific procedures, refer to <a href="https://docs.byteplus.com/en/docs/redis/view-instance">Viewing instance information</a>.   </div>
   

* The instance status is **Running**. For more details, refer to [Instance status](https://docs.byteplus.com/en/docs/redis/instance-status).


<span id=".6Ieq56CU5ZG95Luk6K-t5rOV"></span>
## Self\-developed command syntax

<span id=".5ZG95Luk5YiX6KGo"></span>
### Command list

The self\-developed Proxy commands supported by the Cache for Redis are shown in the following table.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For the command syntax in the following table, the definitions are as follows:</div>



* <div data-tips="true" data-tips-type="tip"><code>UPPERCASE KEYWORD</code>: Command keyword, such as <code>CAS</code>.</div>


* <div data-tips="true" data-tips-type="tip"><code>lowercase keyword</code>: Customizable parameter.</div>


* <div data-tips="true" data-tips-type="tip"><code>[]</code>: The content within <code>[]</code> is an optional parameter, and the content outside <code>[]</code> is a required parameter.</div>




|command |Syntax |Description |
|---|---|---|
|[CAS](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#cas) |`CAS key oldvalue newvalue [EX\|PX time] [NX]` |When the passed `oldvalue` is consistent with the value already set for the specified key, the passed `newvalue` is used to overwrite the original value. |
|[CAD](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#cad) |`CAD key oldvalue` |When the passed `oldvalue` is consistent with the value already set for the specified key, the key is deleted. |
|[IMONITOR](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#imonitor) |`IMONITOR shard_id` |Similar to the open\-source Redis MONITOR command, it is used to execute the MONITOR command on the specified shard of a sharding cluster Redis instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The IMONITOR command needs to be executed via Telnet, and the QUIT command can be used to exit the execution of the IMONITOR command.</div><br> |
|[ISCAN](https://docs.byteplus.com/en/docs/redis/self-developed-proxy-command#iscan) |`ISCAN shard_id cursor [MATCH pattern] [COUNT count]` |Similar to the open\-source Redis SCAN command, it is used to execute the SCAN command on the specified shard of a sharding cluster Redis instance. |


<span id="cas"></span>
### CAS


|Category |Description |
|---|---|
|Command syntax |`CAS key oldvalue newvalue [EX\|PX time] [NX]` |
|Time complexity |O(1). |
|Command description |When the passed `oldvalue` is consistent with the value already set for the specified key, the passed `newvalue` is used to overwrite the original value. |
|Option |* `key`: The name of the key.<br><br>* `oldvalue`: The value already set for the specified key.<br><br>* `newvalue`: When the passed `oldvalue` is consistent with the value already set for the specified key, the passed `newvalue` is used to overwrite the original value.<br><br>* `EX time`: Specify the relative expiration time of the key. Unit: seconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `PX time`: Specify the relative expiration time of the key. Unit: milliseconds. `0` means immediate expiration. Not setting this parameter means the key has no expiration time.<br><br>* `NX`: Write data only if the key does not exist. |
|Response |* `1`: The command was executed successfully, and `newvalue` has overwritten the original value.<br><br>* `0`: The passed `oldvalue` does not match the value already set for the specified key.<br><br>* `-1`: The specified key does not exist.<br><br>* Other cases reply corresponding exception information. |
|Example |* Command example 1<br><br>   Assigns a new value of `5` to key `doctest3` with value `1`, and sets the relative expiration time of this key to 10 seconds. Write only if the key does not exist. The command is as follows.<br><br>   ```Bash```<br>```   CAS doctest3 1 5 EX 10 NX```<br>```   ```<br>   <br><br>   Response example.<br><br>   ```Bash```<br>```   (integer) 1```<br>```   ```<br>   <br><br>* Command example 2<br><br>   Try to change the value of key `doctest3` to `100`. The command is as follows.<br><br>   ```Bash```<br>```   CAS doctest3 1 100```<br>```   ```<br>   <br><br>   Since the value already set for the key `doctest3` is `5` instead of `1`, when the above command is executed, the following information will be returned, indicating that the passed value is inconsistent with the value already set for the key.<br><br>   ```Bash```<br>```   (integer) 0```<br>```   ```<br>    |


<span id="cad"></span>
### CAD


|Category |Description |
|---|---|
|Command syntax |`CAD key oldvalue` |
|Time complexity |O(1). |
|Command description |When the passed `oldvalue` is consistent with the value already set for the specified key, the key is deleted. |
|Option |* `key`: The name of the key.<br><br>* `oldvalue`: The value already set for the specified key. |
|Response |* `1`: The command was executed successfully, and `newvalue` has overwritten the original value.<br><br>* `0`: The passed `oldvalue` does not match the value already set for the specified key.<br><br>* `-1`: The specified key does not exist.<br><br>* Other cases reply corresponding exception information. |
|Example |Delete the key `doctest3` whose value is `5`. The command is as follows.<br><br>```Bash```<br>```CAD doctest3 5```<br><br><br>Response example.<br><br>```Bash```<br>```(integer) 1```<br> |


<span id="imonitor"></span>
### IMONITOR


|Category |Description |
|---|---|
|Command syntax |`IMONITOR shard_id` |
|Time complexity |None. |
|Command description |Similar to the open\-source Redis MONITOR command, it is used to execute the MONITOR command on the specified shard of a sharding cluster Redis instance.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The IMONITOR command needs to be executed via Telnet, and the QUIT command can be used to exit the execution of the IMONITOR command.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Cache for Redis supports returning real client IP addresses through the IMONITOR command. To use it, <a href="https://console.byteplus.com/workorder/create/">submit a ticket</a> to contact technical support to apply for usage.</div><br> |
|Option |`shard_id`: The ID of the shard which used to specify the shard to be viewed. The value range is [0, the total number of shards in the target Redis instance]. |
|Response |* If the execution is successful, it will return OK and display the detailed information of each indicator in the current shard.<br><br>* Other cases reply corresponding exception information. |
|Example |Query the monitoring details of shard 1. The command is as follows.<br><br>```Bash```<br>```IMONITOR 1```<br><br><br>Response example.<br><br>```Bash```<br>```+OK```<br>```+1746503490.811822 [0 11.52.***.***:***] "info" "Server"```<br>```+1746503491.411741 [0 11.52.***.***:***] "info" "Server"```<br>```+1746503491.411832 [0 11.52.***.***:***] "info" "Replication"```<br> |


<span id="iscan"></span>
### ISCAN


|Category |Description |
|---|---|
|Command syntax |`ISCAN shard_id cursor [MATCH pattern] [COUNT count]` |
|Time complexity |The time complexity of each query is O(1).<br><br>The time complexity of a complete query is O(N), where N represents the total number of elements in the set. During a complete query process, multiple command calls will be involved to set the cursor value to 0. |
|Command description |Similar to the open\-source Redis SCAN command, it is used to execute the SCAN command on the specified shard of a sharding cluster Redis instance. |
|Option |* `shard_id`: The ID of the shard which used to specify the shard to be viewed. The value range is [0, the total number of shards in the target Redis instance].<br><br>* The usage and return results of other parameters are similar to those of the open\-source Redis SCAN command. For more details, refer to [SCAN](https://redis.io/commands/scan/). |
|Response |* If the query is successful, it will return a `cursor` value and a list of keys that meet the query criteria.<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The returned cursor value represents the position of this query, and this cursor value can be used to execute the next SCAN command. <code>0</code> indicates that all queries have been completed.   </div><br>   <br><br>* Other cases reply corresponding exception information. |
|Example |Query for keys starting with `doc` in shard 1. The command is as follows.<br><br>```Bash```<br>```ISCAN 1 0 MATCH doc*```<br><br><br>Response example.<br><br>```Bash```<br>```1) "0"```<br>```2) 1) "doctest2"```<br> |


&nbsp;
