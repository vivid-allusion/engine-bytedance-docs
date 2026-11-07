---
title: "Migrating data with RDB files by redis-shake"
product: "Cache for Redis"
product_code: "redis"
source: "https://docs.byteplus.com/en/docs/redis/migrate-data-with-rdb-via-redis-shake"
---

Rredis\-shake is an open\-source Redis data migration tool that enables offline data recovery or migration through RDB files in Redis databases. This article explains how to use the redis\-shake tool for data migration between Redis databases.

## Applicable scenarios

In certain cases, the source Redis database does not grant `sync` or `psync` replication permissions, making it impossible to migrate data via [Database Transmission Service(DTS)](https://docs.byteplus.com/en/docs/DTS/about_database_transmission_service). In such scenarios, you can use the redis\-shake tool with RDB files to perform an offline migration of the full dataset from the source Redis database to the target Redis database.

Using RDB files for data migration allows you to migrate data from self\-hosted Redis or third\-party cloud Redis databases to Cache for Redis without relying on `sync` or `psync` permissions. For more details, refer to [redis-shake](https://github.com/tair-opensource/RedisShake).

## Precautions

* In multi\-DB migration scenarios, pay attention to DB mapping between the source and target databases to avoid unintended data overwrites.

* Migration of STREAM type data is not currently supported.

## Preparation

Before using redis\-shake for data migration, you need to complete the following preparations for both the target and source databases.

|Preparation |Database type |Description |
|---|---|---|
|Create Redis database |Target database |Create a Cache for Redis instance as the target database for data migration. For specific procedures, refer to [Creating instance](https://docs.byteplus.com/en/docs/redis/create-instance). |
|Set Redis database allowlist |* Target database<br><br>* Source database |Set up allowlist for the Redis instance and add the client device IP address to the instance's allowlist. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/set-allowlist).<br><br>> **tip**<br><br><br>> If your client device and Redis instance are not in the same VPC, you also need to enable public network access for the Redis instance. For specific procedures, refer to [Applying for public address](https://docs.byteplus.com/en/docs/redis/apply-public-address).<br> |
|Obtain database connection information |* Target database<br><br>* Source database |You can follow these steps to obtain the connection address and port number information for Cache for Redis:<br><br><br>1. Log in to the [Redis console](https://console.byteplus.com/db/redis).<br><br>2. In the top menu bar, select the project and region to which the instance belongs.<br><br>3. On the **Instances** page, click the target instance.<br><br>4. On the instance details page, click the **Connectivity** tab to view the corresponding connection address and port number information in the **Private network access** or **Public network access** section. |
|Obtain RDB file |Source database |Obtain the RDB file and save it to the local server or ECS instance.<br><br>> **tip**<br><br><br><br>* > This example demonstrates migrating from Cache for Redis to Cache for Redis. For specific procedures, refer to [Downloading backup files](https://docs.byteplus.com/en/docs/redis/download-backup-files).<br><br><br>* > If you need to obtain the Redis Database backup file from a self\-built Redis database, connect to the Redis database and execute the `SAVE` command to generate the `dump.rdb` file in the Redis installation directory.<br> |

## Procedure

1. Install the redis\-shake migration tool. The specific procedures are as follows.

   1. Log in to the device where redis\-cli is to be installed, such as an [ECS instance](https://console.byteplus.com/ecs/instance) or a local device.

      > **tip**

      > This guide uses the installation of the redis\-shake migration tool on an ECS server as an example.

   2. Execute the following command to download the redis\-shake migration tool.

      > **tip**

      > The version of the redis\-shake migration tool used in this example is v4.4.1. You can also select the appropriate tool version based on your actual business needs.

      ```Bash
      wget https://github.com/tair-opensource/RedisShake/releases/download/v4.4.1/redis-shake-v4.4.1-linux-amd64.tar.gz
      ```

   3. Execute the following command to extract the Redis source code files.

      ```Bash
      tar xvf redis-shake-v4.4.1-linux-amd64.tar.gz
      ```

      After extraction, you will see the following two files in the current directory:

      * `redis-shake`: Executable file.

      * `shake.toml`: Configuration file.

2. In the current directory, execute the `vim shake.toml` command to modify the configuration file. The parameters that need to be modified and their descriptions are as follows.

   > **tip**

   * > The following table only lists some parameters that need to be modified. You can set other parameters based on your business data migration requirements. For more parameter descriptions, refer to [redis\-shake configuration](https://tair-opensource.github.io/RedisShake/en/guide/config.html).

   * > By default, redis\-shake v4.x restores data from each DB in the source RDB file to the corresponding DB in the target Redis instance (for example, source DB0 is written to target DB0, DB1 to target DB1). You can specify the target DB for data migration using `function` in the `[filter]`section of the `shake.toml` configuration file. For more details, refer to [function](https://tair-opensource.github.io/RedisShake/en/filter/function.html).

   |Parameter category |Parameter name |Required? |Description |Example |
   |---|---|---|---|---|
   |`[rdb_reader]` |`filepath` |Yes |The absolute path of the backup file (RDB file). |Description<br><br>`/root/redis-shake/redis-shake-4.4.1/redisshaketest.rdb` |
   |`[redis_writer]` |`cluster` |No |Specify whether the target Redis database with sharding cluster enabled. Default value: `false`. |`true` |
   ||`address` |Yes |The connection address and port number of the target Redis database.<br><br>> **tip**<br><br><br>> You can refer to the steps in [Preparation](https://docs.byteplus.com/en/docs/redis/migrate-data-with-rdb-via-redis-shake#MtLnTJZZ) to obtain the connection address and port number of the target Redis database.<br> |`redis-cnlft7yolwd5e****.redis.ibytepluses.com:6379` |
   ||`username` |No |The account used for data migration in the target Redis database. If left blank, the default account will be used. |`testuser` |
   ||`password` |Yes |The account password for data migration in the target Redis database.<br><br>> **tip**<br><br><br>> If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).<br> |`Pwd@123` |
   |`[advanced]` |`rdb_restore_command_behavior` |No |Policy for handling cases where the target Redis database contains keys identical to those in the RDB file. Value range:<br><br><br>* `panic` (default): Reports an error and stops recovery if a conflicting key is found.<br><br>* `rewrite`: Overwrite the key in the target Redis database with the key from the RDB file.<br><br>* `skip`: Skips existing conflicting keys. |`rewrite` |
   ||`pipeline_count_limit` |No |Specify the maximum number of commands in each pipeline to improve write throughput. Default value: 1024. |`1024` |

   An example of the `shake.toml` configuration file is shown below.

   ```TOML
   #[sync_reader]
   #cluster = false            # Set to true if the source is a Redis cluster
   #address = "127.0.0.1:6379" # For clusters, specify the address of any cluster node; use the master or slave address in master-slave mode
   #username = ""              # Keep empty if ACL is not in use
   #password = ""              # Keep empty if no authentication is required
   #tls = false                # Set to true to enable TLS if needed
   #sync_rdb = true            # Set to false if RDB synchronization is not required
   #sync_aof = true            # Set to false if AOF synchronization is not required
   #prefer_replica = false     # Set to true to sync from a replica node
   #try_diskless = false       # Set to true for diskless sync if the source has repl-diskless-sync=yes
   
   #[scan_reader]
   #cluster = false            # set to true if source is a redis cluster
   #address = "127.0.0.1:6379" # when cluster is true, set address to one of the cluster node
   #username = ""              # keep empty if not using ACL
   #password = ""              # keep empty if no authentication is required
   #tls = false
   #dbs = []                   # set you want to scan dbs such as [1,5,7], if you don't want to scan all
   #scan = true                # set to false if you don't want to scan keys
   #ksn = false                # set to true to enabled Redis keyspace notifications (KSN) subscription
   #count = 1                  # number of keys to scan per iteration
   ## RedisShake uses the TYPE command to get each key's type.
   ## If the type is in this skip list, the key will be skipped.
   #skip_unknown_type = []  # e.g. ["imset", "mbloom", "string", "hash", "list", "set", "zset"]
   
   [rdb_reader]
   filepath = "/root/redis-shake/redis-shake-4.4.1/redisshaketest.rdb"
   
   # [aof_reader]
   # filepath = "/tmp/.aof"
   # timestamp = 0            # subsecond
   
   [redis_writer]
   cluster = true            # set to true if target is a redis cluster
   address = "redis-cnlft7yolwd5e****.redis.ibytepluses.com:6379" # when cluster is true, set address to one of the cluster node
   username = "testuser"              # keep empty if not using ACL
   password = "Ft_123456"              # keep empty if no authentication is required
   tls = false
   off_reply = false          # turn off the server reply
   
   # [file_writer]
   # filepath = "/tmp/cmd.txt"
   # type = "cmd" #cmd,aof,json (default cmd)
   
   [filter]
   # Allow keys with specific prefixes or suffixes
   # Examples:
   #   allow_keys = ["user:1001", "product:2001"]
   #   allow_key_prefix = ["user:", "product:"]
   #   allow_key_suffix = [":active", ":valid"]
   #   allow A collection of keys containing 11-digit mobile phone numbers
   #   allow_key_regex = [":\\d{11}:"]
   # Leave empty to allow all keys
   allow_keys = []
   allow_key_prefix = []
   allow_key_suffix = []
   allow_key_regex = []
   
   # Block keys with specific prefixes or suffixes
   # Examples:
   #   block_keys = ["temp:1001", "cache:2001"]
   #   block_key_prefix = ["temp:", "cache:"]
   #   block_key_suffix = [":tmp", ":old"]
   #   block test 11-digit mobile phone numbers keys
   #   block_key_regex = [":test:\\d{11}:"]
   # Leave empty to block nothing
   block_keys = []
   block_key_prefix = []
   block_key_suffix = []
   block_key_regex = []
   
   # Specify allowed and blocked database numbers (e.g., allow_db = [0, 1, 2], block_db = [3, 4, 5])
   # Leave empty to allow all databases
   allow_db = []
   block_db = []
   
   # Allow or block specific commands
   # Examples:
   #   allow_command = ["GET", "SET"]  # Only allow GET and SET commands
   #   block_command = ["DEL", "FLUSHDB"]  # Block DEL and FLUSHDB commands
   # Leave empty to allow all commands
   allow_command = []
   block_command = []
   
   # Allow or block specific command groups
   # Available groups:
   #   SERVER, STRING, CLUSTER, CONNECTION, BITMAP, LIST, SORTED_SET,
   #   GENERIC, TRANSACTIONS, SCRIPTING, TAIRHASH, TAIRSTRING, TAIRZSET,
   #   GEO, HASH, HYPERLOGLOG, PUBSUB, SET, SENTINEL, STREAM
   # Examples:
   #   allow_command_group = ["STRING", "HASH"]  # Only allow STRING and HASH commands
   #   block_command_group = ["SCRIPTING", "PUBSUB"]  # Block SCRIPTING and PUBSUB commands
   # Leave empty to allow all command groups
   allow_command_group = []
   block_command_group = []
   
   # Function for custom data processing
   # For best practices and examples, visit:
   # https://tair-opensource.github.io/RedisShake/zh/filter/function.html
   function = ""
   
   [advanced]
   dir = "data"
   ncpu = 0        # runtime.GOMAXPROCS, 0 means use runtime.NumCPU() cpu cores
   pprof_port = 0  # pprof port, 0 means disable
   status_port = 0 # status port, 0 means disable
   
   # log
   log_file = "shake.log"
   log_level = "info"     # debug, info or warn
   log_interval = 5       # in seconds
   log_rotation = true    # enable log rotation
   log_max_size = 512     # MiB, logs max size to rotate, default 512 MiB
   log_max_age = 7        # days, logs are kept, default 7 days
   log_max_backups = 3    # number of log backups, default 3
   log_compress = true    # enable log compression after rotate, default true
   
   # redis-shake gets key and value from rdb file, and uses RESTORE command to
   # create the key in target redis. Redis RESTORE will return a "Target key name
   # is busy" error when key already exists. You can use this configuration item
   # to change the default behavior of restore:
   # panic:   redis-shake will stop when meet "Target key name is busy" error.
   # rewrite: redis-shake will replace the key with new value.
   # skip:  redis-shake will skip restore the key when meet "Target key name is busy" error.
   rdb_restore_command_behavior = "rewrite" # panic, rewrite or skip
   
   # redis-shake uses pipeline to improve sending performance.
   # Adjust this value based on the destination Redis performance:
   # - Higher values may improve performance for capable destinations.
   # - Lower values are recommended for destinations with poor performance.
   # 1024 is a good default value for most cases.
   pipeline_count_limit = 1024
   
   # Use the token bucket rate limiting method to limit the maximum written QPS
   # If the performance of the target end is too poor or you want to protect the target redisyou can reduce this parameter
   # 300,000 is a maximum value. You can consider it as no rate limit
   target_redis_max_qps = 300000
   
   # This setting corresponds to the 'client-query-buffer-limit' in Redis configuration.
   # The default value is typically 1GB.
   # It's recommended not to modify this value unless absolutely necessary.
   target_redis_client_max_querybuf_len = 1073741824  # 1GB in bytes
   
   # This setting corresponds to the 'proto-max-bulk-len' in Redis configuration.
   # It defines the maximum size of a single string element in the Redis protocol.
   # The value must be 1MB or greater. Default is 512MB.
   # It's recommended not to modify this value unless absolutely necessary.
   target_redis_proto_max_bulk_len = 512_000_000
   
   # If the source is Elasticache, you can set this item. AWS ElastiCache has custom
   # psync command, which can be obtained through a ticket.
   aws_psync = "" # example: aws_psync = "10.0.0.1:6379@nmfu2sl5osync,10.0.0.1:6379@xhma21xfkssync"
   
   # destination will delete itself entire database before fetching files
   # from source during full synchronization.
   # This option is similar redis replicas RDB diskless load option:
   #   repl-diskless-load on-empty-db
   empty_db_before_sync = false
   
   [module]
   # The data format for BF.LOADCHUNK is not compatible in different versions. v2.6.3 <=> 20603
   target_mbbloom_version = 20603
   ```

3. After modifying the `shake.toml` configuration file, execute the following command to migrate data in the directory containing the `redis-shake` and `shake.toml `files.

   ```Bash
   ./redis-shake shake.toml
   ```

   After the migration task starts, you will see real\-time log output in the command execution window. When `[rdb_reader] rdb file parse done` and `all done` appear in the log, it indicates that the source RDB file has been successfully parsed and data recovery is complete. You can now manually stop the redis\-shake migration task by pressing `Ctrl+C`.

   ```Bash
   ...
   2025-12-12 11:13:10 INF [rdb_reader] start read
   2025-12-12 11:13:10 INF [rdb_reader] rdb file parse done
   2025-12-12 11:13:10 INF all done
   ...
   ```

After the migration task is completed, you can log in to the target Redis instance and verify if the migrated data is as expected. For specific procedures, refer to [Connecting to instance](https://docs.byteplus.com/en/docs/redis/connect-to-instance).

## FAQs

* **Q: How to handle the ** **`Target key name is busy`** ** error during data migration?**

   **A**: The error `Target key name is busy` occurs when a key with the same name as the key to be restored exists in the target Redis instance, and `rdb_restore_command_behavior = "panic"` is set in the `shake.toml` configuration file. In this case, you can try any of the following methods to resolve it:

   * Adjust the value of the `rdb_restore_command_behavior` parameter in the `shake.toml` configuration file to `rewrite` or `skip`.

   * Clear the data in the target Redis instance before performing data migration. For specific procedures, refer to [Clearing data](https://docs.byteplus.com/en/docs/redis/clear-data).

      > **tip**

      * > After clearing data, existing business data in the instance will be erased and cannot be recovered. Proceed with caution.

      * > We recommend manually backing up Redis instance data before clearing it. For manual backup method, refer to [Manual backup](https://docs.byteplus.com/en/docs/redis/manual-backup).

      * > A single\-node instance does not support persistence and backup features, so data cannot be recovered after being cleared. Proceed with caution. For more details about single\-node instances, refer to [Product architecture](https://docs.byteplus.com/en/docs/redis/product-component-architecture).

* **Q: How to handle the ** **`ERR invalid password`** ** or ** **`ERR NOAUTH Authentication required`** ** error during data migration?**

   **A**: When you incorrectly fill in or omit the `username` or `password` in the `[redis_writer]` section of the `shake.toml` configuration file, you will encounter the aforementioned error. In this case, you need to check if the account name and password of the target Redis instance are correct. If you forget your password, you can reset it. For specific procedures, refer to [Resetting password](https://docs.byteplus.com/en/docs/redis/reset-password).

* **Q: How to handle the ** **`EOF`** ** or ** **`dial failed`** ** error during data migration?**

   **A**: The following table lists potential causes of `EOF` or `dial failed` error and the corresponding solutions for your reference.

   |Potential causes of errors |Solution |
   |---|---|
   |Connect to instance using direct address |Adjust the `address` parameter under `[redis_writer]` in the configuration file to the instance's private or public connection address, and ensure the correct connection address domain and port number are entered.<br><br>> **tip**<br><br><br>> You can refer to the steps in [Preparation](https://docs.byteplus.com/en/docs/redis/migrate-data-with-rdb-via-redis-shake#MtLnTJZZ) to obtain the connection address and port number of the target Redis database.<br> |
   |SSL/TLS configuration mismatch |Confirm that the SSL encryption settings of the target Redis instance match the `tls` settings under `[redis_writer]` in the configuration file. For more information about SSL encryption, refer to [Setting SSL encryption](https://docs.byteplus.com/en/docs/redis/setup-ssl). |
   |Incorrect allowlist settings |Check the allowlist settings of the Redis instance and confirm that the IP address of the client device where redis\-shake is located has been added to the instance's allowlist. For specific procedures, refer to [Setting allowlist](https://docs.byteplus.com/en/docs/redis/set-allowlist). |
