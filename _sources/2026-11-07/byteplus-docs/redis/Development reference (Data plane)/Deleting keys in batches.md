---
title: "Deleting keys in batches"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/batch-delete-key"
---

Redis provides the DEL command to delete a single key. When multiple keys need to be deleted in batches, you can combine the cat and xargs commands of Linux with the DEL command of Redis for precise matching and batch deletion of keys; or combine Redis's SCAN, RANDOMKEY, KEYS, or FLUSHALL with the DEL command for fuzzy matching and batch deletion of keys.

> **danger**

* > Commands such as DEL and FLUSHALL immediately delete data after execution, the operation is irreversible, and mistakenly deleted data cannot be recovered, so proceed with caution.

* > Before batch deletion, it is recommended to perform a manual backup first, and confirm the range of keys to be deleted (you can first use SCAN or KEYS to preview the matching results). For specific operations, refer to [Manual backup](https://docs.byteplus.com/en/docs/redis/manual-backup).

* > It is recommended to first verify the matching rules in a test environment and then execute them in the production environment, prioritizing operations during off\-peak business hours.

## Precise matching batch deletion of keys

You can refer to the following command syntax to combine the cat and xargs commands of Linux with the DEL command of Redis in a Lua script to perform precise match batch deletion of keys.

```Bash
cat <file> | xargs redis-cli -h <host> -a <password> DEL
```

The description of each parameter in the command syntax is as follows in the table.

|Parameters |Description |
|---|---|
|`cat <file>` |Use the cat command to read each line from a file as a key for Redis, where `<file>` is the file path of the keys to be deleted, for example, `del_key.txt`.<br><br>> **tip**<br><br><br>> Before executing the above command, write the list of keys to be deleted into the specified file.<br> |
|`xargs` |Use the xargs command to pass parameter lists in segments to other commands to avoid issues with overly long parameter lists. The xargs command can be used alone or in combination with other commands through pipe symbols, redirection symbols, etc.<br><br>> **tip**<br><br><br>> When using the xargs command, if there are special characters in the file, escape processing may be required. Otherwise, results different from expectations may occur.<br> |
|`redis-cli -h <host> -a <password>` |Connect to a Redis instance through the redis\-cli tool. Where:<br><br><br>* `host`: The connection address of the Redis instance. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address).<br><br>* `password`: The login password for the default account in the Redis instance. If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |
|`DEL` |Use the DEL command to delete the keys recorded in the specified file. |

The command example is as follows.

```Bash
cat del_key.txt | xargs redis-cli -h redis-cng6qap*****.redis.ivolces.com -a Pwd@123**** DEL
```

## Fuzzy matching batch deletion of keys

You can combine Redis commands such as SCAN, RANDOMKEY, KEYS, or FLUSHALL with the DEL command to perform fuzzy matching and batch deletion of keys.

### (Recommended) Fuzzy batch deletion by SCAN and DEL commands

Combine the SCAN and DEL commands in Python code to iterate and delete keys that match the criteria. The example code is as follows.

```Python
import redis
import sys

def main(argv):
    
    if len(argv) < 5:
        print("Usage: python scan_del.py <host> <port> <password> <match>")
        exit(1)

    host = argv[1]
    port = argv[2]
    password = argv[3]
    match = argv[4]
    print("host: %s, port: %s, password: ********, match: %s\n" % (host, port, match))

    redis_cli = redis.StrictRedis(host=host, port=port, password=password)
    cursor = 0
    rnd = 1

    while rnd == 1 or cursor != 0:
        result = redis_cli.scan(cursor=cursor, match=match, count=1000)
        ret_cursor = result[0]
        ret_keys = result[1]
        num_keys = len(ret_keys)
        print("del %d keys in round %d, cursor: %d" % (num_keys, rnd, ret_cursor))
        if 0 != num_keys:
            ret_del = redis_cli.delete(*ret_keys)
            print("ret_del: %d, ret_keys: %s" % (ret_del, ret_keys))
        cursor = ret_cursor
        rnd += 1
        print("")

if __name__ == '__main__':
    main(sys.argv)
```

Call the above sample code `scan_del.py`. When calling it, you need to specify the connection information of the Redis instance and the matching rule of the key. Then, you can achieve fuzzy matching and batch deletion of keys that meet the conditions.

```Bash
python scan_del.py <host> <port> <password> "match_key"
```

The description of each parameter in the command syntax is as follows in the table.

|Parameters |Description |
|---|---|
|`host` |The connection address of the Redis instance. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address). |
|`port` |Port number of the Redis instance connection address. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address). |
|`password` |The login password for the default account in the Redis instance. If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |
|`match_key` |Key that meets the specified conditions. For example, `"del*"` represents all keys prefixed with `del`, such as `del_a`, `del1`, `delOK`, etc.<br><br>> **tip**<br><br><br>> The following is more details on wildcard matching for your reference:<br><br><br><br>* > `r?dis`: Matches strings that start with `r`, end with `dis`, with a length of 5 characters, such as `redis`, `radis`, and `ridis`.<br><br><br>* > `r*dis`: Matches strings of any length that start with `r` and end with `dis` of any length, such as`rdis` and `reeeeedis`.<br><br><br>* > `r[ae]dis`: Only matches `radis` and `redis`, but not `ridis` or others.<br><br><br>* > `r[^e]dis`: Matches `radis` and `ridis`, but not `redis`.<br><br><br>* > `r[a-z]dis`: Matches strings that start with `r`, end with `dis`, where the second character is any letter from a to z, such as `radis`, `rbdis`, and `rzdis`.<br> |

The command example is as follows.

```Bash
python scan_del.py redis-cng6qap*****.redis.ivolces.com 6397 Pwd@123**** "del*"
```

### Fuzzy batch deletion by KEYS and DEL commands

> **danger**

* > The KEYS command is a blocking operation. When there are a large number of keys, it may lead to high instance CPU usage and even server blocking. It is not recommended to be used directly in a production environment. If it needs to be used in a production environment, it is strongly recommended to operate when there is less data or during off\-peak business periods.

* > Cache for Redis disables the KEYS command by default. If you need to use this command, you need to remove the corresponding command from the default value of the disabled command parameter. Otherwise, when executing these disabled commands, an error of `no permission to execute the command will occur`. For specific procedures, refer to [Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter).

Use the combination of KEYS and DEL commands to fuzzy match and batch delete qualified keys. First, use wildcards in the KEYS command to fuzzy match all qualified keys, then use the DEL command to delete these keys. The command syntax is as follows.

```Bash
redis-cli -h <host> -a <password> KEYS "<match_key>" | xargs redis-cli -h <host> -a <password> DEL
```

The description of each parameter in the command syntax is as follows in the table.

|Parameters |Description |
|---|---|
|`host` |The connection address of the Redis instance. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address). |
|`password` |The login password for the default account in the Redis instance. If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |
|`match_key` |Key that meets the specified conditions. For example, `"del*"` represents all keys prefixed with `del`, such as `del_a`, `del1`, `delOK`, etc.<br><br>> **tip**<br><br><br>> The following is more details on wildcard matching for your reference:<br><br><br><br>* > `r?dis`: Matches strings that start with `r`, end with `dis`, with a length of 5 characters, such as `redis`, `radis`, and `ridis`.<br><br><br>* > `r*dis`: Matches strings of any length that start with `r` and end with `dis` of any length, such as`rdis` and `reeeeedis`.<br><br><br>* > `r[ae]dis`: Only matches `radis` and `redis`, but not `ridis` or others.<br><br><br>* > `r[^e]dis`: Matches `radis` and `ridis`, but not `redis`.<br><br><br>* > `r[a-z]dis`: Matches strings that start with `r`, end with `dis`, where the second character is any letter from a to z, such as `radis`, `rbdis`, and `rzdis`.<br> |

The command example is as follows.

```Bash
redis-cli -h redis-cng6qap*****.redis.ivolces.com -a Pwd@123**** KEYS "del*" | xargs redis-cli -h redis-cng6qap*****.redis.ivolces.com -a Pwd@123**** DEL
```

### Quickly fuzzy batch deletion by FLUSHALL parameter and DEL command

> **danger**

> Cache for Redis disables the FLUSHALL command by default. If you need to use this command, you need to remove the corresponding command from the default value of the disabled command parameter. Otherwise, when executing these disabled commands, an error of `no permission to execute the command will occur`. For specific procedures, refer to [Setting instance parameters](https://docs.byteplus.com/en/docs/redis/set-parameter).

Combine the FLUSHALL and DEL commands to quickly perform fuzzy matching and batch deletion of keys that meet the conditions. That is, first use the `WITHPATTERN` or `WITHOUTPATTERN` parameter in the FLUSHALL command to perform fuzzy match all qualified keys, and then use the DEL command to delete these keys or other keys other than these keys. The command syntax is as follows:

* Delete all keys that match the rules

   ```Bash
   redis-cli -h <host> -a <password> FLUSHALL WITHPATTERN "<match_key>"
   ```

* Delete all keys except those matching the rules

   ```Bash
   redis-cli -h <host> -a <password> FLUSHALL WITHOUTPATTERN "<match_key>"
   ```

The description of each parameter in the command syntax is as follows in the table.

|Parameters |Description |
|---|---|
|`host` |The connection address of the Redis instance. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address). |
|`password` |The login password for the default account in the Redis instance. If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |
|`match_key` |Key that meets the specified conditions. For example, `"del*"` represents all keys prefixed with `del`, such as `del_a`, `del1`, `delOK`, etc.<br><br>> **tip**<br><br><br>> The following is more details on wildcard matching for your reference:<br><br><br><br>* > `r?dis`: Matches strings that start with `r`, end with `dis`, with a length of 5 characters, such as `redis`, `radis`, and `ridis`.<br><br><br>* > `r*dis`: Matches strings of any length that start with `r` and end with `dis` of any length, such as`rdis` and `reeeeedis`.<br><br><br>* > `r[ae]dis`: Only matches `radis` and `redis`, but not `ridis` or others.<br><br><br>* > `r[^e]dis`: Matches `radis` and `ridis`, but not `redis`.<br><br><br>* > `r[a-z]dis`: Matches strings that start with `r`, end with `dis`, where the second character is any letter from a to z, such as `radis`, `rbdis`, and `rzdis`.<br> |

The command example is as follows:

* Delete all keys that match the rules

   ```Bash
   redis-cli -h redis-cng6qap*****.redis.ivolces.com -a Pwd@123**** FLUSHALL WITHPATTERN "*yesdel"
   ```

* Delete all keys except those matching the rules

   ```Bash
   redis-cli -h redis-cng6qap*****.redis.ivolces.com -a Pwd@123**** FLUSHALL WITHOUTPATTERN "*nodel"
   ```

### Low\-frequency fuzzy batch deletion by RANDOMKEY and DEL commands

> **danger**

* > Since RANDOMKEY completely randomly obtains keys, it may require multiple retrievals to find keys that meet the matching rules. This method is less efficient and is suitable for business scenarios of low\-frequency fuzz batch deletion of keys.

* > When the number of keys in Redis is very large and the proportion of keys that meet the matching rules is relatively small, the entire command execution process may be time\-consuming.

* > When a Redis instance with sharding clusters enabled executes the RANDOMKEY command, it will access each shard in a round\-robin manner. That is, Redis will send the RANDOMKEY command request to each shard. When the visited shard does not have a key that meets the conditions, it will return `nil`. This return result only means that **there is no key that meets the conditions on the current shard** but **does not mean that there is no key that meets the conditions on other shards**. Therefore, when using the RANDOMKEY command, it is recommended **not to determine whether there are keys** that **meet the conditions based on whether the return result is** **`nil`**.

Combine RANDOMKEY and DEL commands in Python code for low\-frequency fuzzy batch deletion, that is, randomly retrieving keys multiple times and deleting those that match the pattern. The code example is as follows.

```Python
import sys
import time
import redis
import fnmatch


def main(argv):
    if len(argv) < 5:
        print("Usage: python randomkey_del_low_frequency.py host port password match")
        sys.exit(-1)
    host = argv[1]
    port = argv[2]
    password = argv[3]
    match = argv[4]
    print("host: %s, port: %s, password: ********, match: %s\n" % (host, port, match))
    redis_cli = redis.StrictRedis(host=host, port=port, password=password)
    rnd = 1
    total_deleted = 0
    while True:
        random_key = redis_cli.randomkey()
        if not random_key:
            continue
        if fnmatch.fnmatch(random_key.decode('utf-8'), match):
            result = redis_cli.delete(random_key)
            if result == 1:
                total_deleted += 1
                print("del 1 key in round %d" % rnd)
        rnd += 1
        time.sleep(0.1)


if __name__ == '__main__':
    main(sys.argv)
```

Call the above sample code `randomkey_del_low_frequency.py`. When calling, you need to specify the connection information of the Redis instance and the matching rule of the key. Then, fuzzy matching and batch deletion of keys that meet the conditions can be achieved.

```Bash
python randomkey_del_low_frequency.py <host> <port> <password> "<match_key>" 
```

The description of each parameter in the command syntax is as follows in the table.

|Parameters |Description |
|---|---|
|`host` |The connection address of the Redis instance. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address). |
|`port` |Port number of the Redis instance connection address. For more details, refer to [Viewing address](https://docs.byteplus.com/en/docs/redis/view-address). |
|`password` |The login password for the default account in the Redis instance. If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password). |
|`match_key` |Key that meets the specified conditions. For example, `"del*"` represents all keys prefixed with `del`, such as `del_a`, `del1`, `delOK`, etc.<br><br>> **tip**<br><br><br>> The following is more details on wildcard matching for your reference:<br><br><br><br>* > `r?dis`: Matches strings that start with `r`, end with `dis`, with a length of 5 characters, such as `redis`, `radis`, and `ridis`.<br><br><br>* > `r*dis`: Matches strings of any length that start with `r` and end with `dis` of any length, such as`rdis` and `reeeeedis`.<br><br><br>* > `r[ae]dis`: Only matches `radis` and `redis`, but not `ridis` or others.<br><br><br>* > `r[^e]dis`: Matches `radis` and `ridis`, but not `redis`.<br><br><br>* > `r[a-z]dis`: Matches strings that start with `r`, end with `dis`, where the second character is any letter from a to z, such as `radis`, `rbdis`, and `rzdis`.<br> |

The command example is as follows.

```Bash
python randomkey_del_low_frequency.py redis-cng6qap*****.redis.ivolces.com 6397 Pwd@123**** "del*"
```

## Verify whether specified key is successfully deleted

You can check whether the specified key has been successfully deleted by using the following command.

```Bash
redis-cli -h <host> -a <password> KEYS "<key>"
```

The command example is as follows.

```Bash
redis-cli -h redis-cng6qap*****.redis.ivolces.com -a Pwd@123**** KEYS "test_del"
```

If the result returns `empty array`, it means the key does not exist in Redis, indicating the key has been successfully deleted.
