---
title: "Lua scripting guide"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/lua-user-guide"
---

Cache for Redis supports processing CAS (compare\-and\-swap) commands through Lua scripting, thus satisfying the atomic operation requirements of Redis and enhancing its performance. This topic introduces you to basic syntax, usage restrictions, and recommendations for using Lua scripts with Redis.

## Lua script command

The following table lists the Lua script commands and features supported by Cache for Redis.

|Command |Function |
|---|---|
|[EVAL](https://docs.byteplus.com/en/docs/redis/lua-user-guide#eval) |Execute the specified Lua script and return the execution result. |
|[EVALSHA](https://docs.byteplus.com/en/docs/redis/lua-user-guide#evalsha) |Executing longer Lua scripts through the EVAL command entails considerable bandwidth consumption. To avoid this, you can use the EVALSHA command to execute such scripts by its value of `sha1`. |
|[SCRIPT LOAD](https://docs.byteplus.com/en/docs/redis/lua-user-guide#script-load) |Load a Lua script into the Redis instance without immediately executing it and return the value of `sha1` of the script. |
|[SCRIPT EXISTS](https://docs.byteplus.com/en/docs/redis/lua-user-guide#script-exists) |Check if the script corresponding to the specified value of `sha1` is cached in the Redis instance. Supports passing in the `sha1` values of multiple scripts for confirmation simultaneously, separating the values of `sha1` by spaces. |
|[SCRIPT KILL](https://docs.byteplus.com/en/docs/redis/lua-user-guide#script-kill) |Terminate the currently running Lua script.<br><br>This command is primarily used to stop scripts that have been running for too long. For example, scripts stuck in an infinite loop due to an error. |
|[SCRIPT FLUSH](https://docs.byteplus.com/en/docs/redis/lua-user-guide#script-flush) |Clear all Lua script caches from the current Redis instance. |

## Lua script command syntax

### EVAL

* **Function**

   Execute the given script with the specified parameters and return the result.

* **Syntax**

   ```Lua
   EVAL script numkeys [key [key ...]] [arg [arg ...]]
   ```

   The specific parameters are described as follows.

   |Parameter |Description |
   |---|---|
   |`script` |Lua script source code. Redis supports passing data to the script through `KEYS[]` and `ARGV[]` parameters, where:<br><br><br>* `KEYS[]`: Specify Redis Key parameters. Indexing starts from 1, for example, `KEYS [1]`.<br><br>* `ARGV[]`: Specify script parameters. Indexing starts from 1, for example, `ARGV [1]`. |
   |`numkeys` |Specify the number of `KEYS[]` parameters.<br><br>The value of `numkeys` varies depending on the instance architecture. Where:<br><br><br>* Instances with sharding cluster disabled: The value of `numkeys` must be greater than or equal to 0.<br><br>* Instances with sharding cluster enabled: The value of `numkeys` must be greater than or equal to 1. |

   > **tip**

   * > When executing a Lua script using the EVAL command, the system simultaneously caches the script in the Redis instance. For more information on the EVAL command, refer to [EVAL](https://redis.io/commands/eval/).

   * > It is recommended to explicitly pass the keys accessed by the script through the `KEYS[]` parameter instead of encoding them into the script. Excessive similar behavior can lead to an increase in instance memory usage and a reclaiming failure. In extreme cases, it may result in instance primary and secondary memory overflow (Out of Memory), causing data loss.

* **Example**

   * Example 1: Execute the following Lua script using the EVAL command to set the string `Key=department` and `value=Game`. The specific command is as follows.

      ```Lua
      EVAL "return redis.call('SET',KEYS[1],ARGV[1])" 1 department Game
      ```

      An example of the response is as follows:

      ```Bash
      OK
      ```

   * Example 2: Execute the following Lua script using the EVAL command to obtain the string value of `Key=department`. The specific command is as follows.

      ```Lua
      EVAL "return redis.call('GET',KEYS[1])" 1 department
      ```

      An example of the response is as follows:

      ```Bash
      "Game"
      ```

### EVALSHA

* **Function**

   Executing longer Lua scripts through the EVAL command entails considerable bandwidth consumption. To avoid this, you can use the EVALSHA command to execute such scripts by its value of `sha1`.

* **Syntax**

   ```Lua
   EVALSHA sha1 numkeys [key [key ...]] [arg [arg ...]]
   ```

   The specific parameters are described as follows.

   |Parameter |Description |
   |---|---|
   |`sha1` |SHA1 checksum corresponding to the Lua script. |
   |`numkeys` |Specify the number of `KEYS[]` parameters. The value of `numkeys` varies depending on the instance architecture. Where:<br><br><br>* Instances with sharding cluster disabled: The value of `numkeys` must be greater than or equal to 0.<br><br>* Instances with sharding cluster enabled: The value of `numkeys` must be greater than or equal to 1. |

   > **tip**

   > When using the EVALSHA command, Redis generates the `NOSCRIPT No matching script.` error if the script corresponding to the value of `sha1` is not cached in Redis. Please cache the target script in Redis using the EVAL or SCRIPT LOAD command before executing the EVALSHA command. For more information on the EVALSHA command, refer to [EVALSHA](https://redis.io/commands/evalsha/).

* **Example**

   ```Lua
   EVALSHA 620cd258c2c9c88c9d10db67812ccf663d96bdc6 1 department
   ```

   Examples of back results are as follows.

   ```Bash
   "Game"
   ```

### SCRIPT LOAD

* **Function**

   Load a Lua script into the Redis instance without immediately executing it and return the value of `sha1` of the script.

* **Syntax**

   ```Lua
   SCRIPT LOAD script
   ```

   For more information on the SCRIPT LOAD command, refer to [SCRIPT LOAD](https://redis.io/commands/script-load/).

* **Example**

   ```Lua
   SCRIPT LOAD "return redis.call('GET',KEYS[1])"
   ```

   Examples of back results are as follows.

   ```Bash
   "620cd258c2c9c88c9d10db67812ccf663d96bdc6"
   ```

### SCRIPT EXISTS

* **Function**

   Check if the script corresponding to the specified value of `sha1` is cached in the Redis instance.

* **Syntax**

   ```Lua
   SCRIPT EXISTS sha1 [sha1 ...]
   ```

   > **tip**

   * > Supports passing in the `sha1` values of multiple scripts for confirmation simultaneously, separating the values of `sha1` by spaces. The range of returned values is as follows:

      * > `1`The script already exists.

      * > `0`The script does not exist.

   * > For more information on the SCRIPT EXISTS command, refer to [SCRIPT EXISTS](https://redis.io/commands/script-exists/).

* **Example**

   ```Lua
   SCRIPT EXISTS 620cd258c2c9c88c9d10db67812ccf663d96bdc6 620cd258c2c9c88c9d10db67812ccf663d96bdc7
   ```

   Examples of back results are as follows.

   ```Lua
   1) (integer) 1
   2) (integer) 0
   ```

### SCRIPT KILL

* **Function**

   Terminate the currently running Lua script. This command is primarily used to stop scripts that have been running for too long. For example, scripts stuck in an infinite loop due to an error.

* **Syntax**

   ```Lua
   SCRIPT KILL
   ```

   > **tip**

   * > To ensure data atomicity, the SCRIPT KILL command is executed only if the specified script has not performed any write operations.

   * > After executing the SCRIPT KILL command, errors generated from the script command will appear in clients that are executing Lua scripts. For more information on the SCRIPT KILL command, refer to [SCRIPT KILL](https://redis.io/commands/script-kill/).

* **Example**

   ```Lua
   SCRIPT KILL
   ```

   Examples of back results are as follows.

   ```Bash
   OK
   ```

### SCRIPT FLUSH

* **Function**

   Clear all Lua script caches from the current Redis instance.

* **Syntax**

   ```Lua
   SCRIPT FLUSH [ASYNC | SYNC]
   ```

   > **tip**

   * > Redis supports specifying the cache refresh mode after executing the SCRIPT FLUSH command. Valid values:

      * > `SYNC` (Default): Synchronously refresh the cache.

      * > `ASYNC`: Asynchronously refresh the cache.

   * > This command clears all the Lua script caches in the current Redis instance. We recommend that you back up the Lua scripts before clearing them. For more information on the SCRIPT FLUSH command, refer to [SCRIPT FLUSH](https://redis.io/commands/script-flush/).

* **Example**

   ```Lua
   SCRIPT FLUSH
   ```

   Examples of back results are as follows.

   ```Bash
   OK
   ```

## Limits for using Lua scripts

* Different instance types of Cache for Redis have different limitations when using Lua scripts. Among them:

   * **Instances with sharding cluster enabled**

      * All keys should be passed through the `KEYS` array; the Redis commands called in `redis.call/pcall` must have their keys in the `KEYS` array.

      * The value of `numkeys` must be greater than or equal to 1.

      * All keys must be in a single slot.

      * For instances where the proxy minor version is less than 1.511.0, the maximum limit for the number of key parameters in a Lua script is 100 by default. When the number of keys exceeds the limit, an error message `command arguments invalid` will appear. If necessary, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to upgrade the instance's proxy to the latest version to remove this restriction.

   * **Instances with sharding cluster disabled**

      For instances where the proxy minor version is less than 1.511.0, the maximum limit for the number of key parameters in a Lua script is 100 by default. When the number of keys exceeds the limit, an error message `command arguments invalid` will appear. If necessary, [submit a ticket](https://console.byteplus.com/workorder/create/) to contact technical support to upgrade the instance's proxy to the latest version to remove this restriction.

* Cache for Redis restricts the use of certain commands in Lua scripts. For more details about supported commands in Lua scripts, refer to [Supported commands](https://docs.byteplus.com/en/docs/redis/supported-command).

## Suggestions for using Lua scripts

* We recommend explicitly passing the keys accessed by the script through the `KEYS[]` parameter instead of encoding them into the script. Excessive similar behavior can lead to an increase in instance memory usage and a reclaiming failure. In extreme cases, it may result in instance primary and secondary memory overflow (Out of Memory), causing data loss.

* We recommend that you add the `redis.replicate_commands();` parameter in the Lua script to specify the data synchronization mode as an actual command\-based mode to avoid inconsistencies between primary and secondary data.

* Loading Lua scripts entails consumption of considerable computing resources, so Lua scripts should be reused wherever feasible to reduce network overhead and the number of scripts that need to be cached.

* We recommend entering only simple commands in Lua scripts. Use transaction commands for complex operations involving atomicity.

* We recommend not entering too many loops in Lua scripts to prevent script execution timeouts or errors, which can even cause Redis instances to freeze.

* We recommend not using certain unofficial SDKs (such as Redisson) in Lua scripts to prevent unknown problems and even risks.
